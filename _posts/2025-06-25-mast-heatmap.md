---
layout: post
read_time: true
show_date: true
title: "MAST's View of the Sky: Your Next Wallpaper"
date: 2025-06-24
img: posts/20250625/mast_wallpaper_blue.png
tags:
  - fun
  - outreach
category: fun
author: MAST Staff
description: Cool MAST wallpapers
---

TL;DR - Here are the cool desktop backgrounds. Enjoy! Scroll down for the full story.
### "Standard" Celestial Coordinates
![mast background in "standard", surface of the Earth, coordinates](assets/img/posts/20250625/mast_wallpaper_blue.png)

### Reprojection 1: Ecliptic Coordinates
![the MAST heatmap, reprojected to the plane of the ecliptic](assets/img/posts/20250625/mast_wallpaper_ecl_blue.png)
### Reprojection 2: Galactic Coordinates
![the mast heatmap, projected to galactic coordinates](assets/img/posts/20250625/mast_wallpaper_gal_blue.png)

## So, What am I looking at?
You're looking at MAST's view of the sky! Specifically, each pixel in these images is colored according to the number of observations archived at those coordinates. Dark pixels have fewer observations, while brighter pixels have many.

## How did you make this?
First, consider a "typical" use of the archive: astronomers query for and access data from space telescopes. This is a two stage process: you might start by querying for HST observations of M101 in the ultraviolet range, then download all calibrated files produced by those observations. The first step is a metadata search, where you filter on telescope, wavelength, and [other fields we make searchable in our CAOM metadata database](https://mast.stsci.edu/api/v0/_c_a_o_mfields.html).

MAST is not *merely* a data archive; we spend lots of time and effort making sure that our metadata are accurate, too. Given that we have over 250 million observations in our archive, this is no small feat. Using the coordinates of all observations in our database, we can create this density plot on the sky!
## Yeah, but like, HOW specifically did you make this?

### First Version: Intelligent Requests
Our initial goal was for pixels half a degree wide, so there were `720x360=259200` regions for which we needed to know the total number of observations. Spamming our own servers with one request for each of the 2.6 million regions either requires immense patience (I'm not waiting 30 days for an answer!) or performing a [denial-of-service attack](https://en.wikipedia.org/wiki/Denial-of-service_attack) on our own servers. The other extreme would be to do a single query, loading the entire database into memory. Clearly absurd<sup>1</sup>.

<small><sup>1</sup> Unless....?</small>

Instead, the first successful image was produced with data from 720 [ADQL](https://en.wikipedia.org/wiki/Astronomical_Data_Query_Language) queries, avoiding a DoS attack while also working with reasonable RAM limitations. Here's roughly how the code works:
1. Perform an ADQL query to get vertical slices of the sky. For the first slice, as an example, it would be: 
```
SELECT trgposRA,trgposDec FROM [REDACTED].[CaomObservation] WHERE (trgposRA < 0.5 AND targposRA >= 0)
``` 
Or, "Dear CAOM, please send me the coordinates of every observation with an RA between 0" and 0.5".
2. The resulting vertical slice is`1/720` of the entire database. In our actual code, it is a pandas dataframe; we can use a mask to filter on the declination values and get a count. Here's how we accomplished this in practice:
```
for dec in dec_sample: 
	mask = (data['trgPosDEC']>=(dec-(degree_res/2)))&(data['trgPosDEC']<(dec+(degree_res/2))) 
	num_obs = sum(mask) 
	obs_array.append(num_obs)
```

3. We now have the first vertical slice broken up into 360 pieces, with a count for each. We can repeat steps 1&2 until we have data for the entire sky.

Following this recipe produces an image like the one below:
![the first, lower resolution version of the wallpaper](assets/img/posts/20250625/mast_wallpaper_blue_og.png)
<small>The first version of the MAST background, with pixels half a degree wide. The intrinsic resolution of our data is therefore 720x360, which results in some noticeable pixellation. </small>

Looks phenomenal! Many archive scientists were super excited to see this.
### Revised Version: RAM go brrrr
Now, producing this image is very cool. But 360 pixels?? Surely we can get something at a higher resolution than that. However, it took us 2 hours of queries to get the above image, and unfortunately doubling the resolution means the queries will take four times as long.

Unless....

We said it would be unreasonable to load the entire archive into RAM. But what if we just try it? Drop the filters on the query and just send me everything!
```
SELECT trgposRA,trgposDec FROM [REDACTED].[CaomObservation]
```

Much to our surprise, it worked! With the entire database in memory, we could now create images of arbitrary resolution. With `matplotlib.plt.hist2d`, it's trivially easy to specify the desired resolution of the image and let matplotlib handle the details. Just, uh... don't have too many other applications open.
![a screenshot showing that Python is currently consuming 51.86GB of RAM](assets/img/posts/20250625/brrrrr.png)
At the end of this shockingly quick — roughly 2 minute— process, you'll have the first image from the intro:
![mast background in "standard", surface of the Earth, coordinates](assets/img/posts/20250625/mast_wallpaper_blue.png)
<small>A deliciously crispy 15000x7500 image of MAST's view of the sky. Ah, the smell of roasting RAM in the office.</small>
### Revised Version addendum: Reprojection
Now this is neat, but we have another trick up our sleeves: [astropy.coordinates](https://docs.astropy.org/en/stable/coordinates/index.html). Thankfully, our friends at astropy love to optimize code, and it was pretty painless to reproject all of CAOM into another frame. Of the [available coordinate systems](https://docs.astropy.org/en/stable/coordinates/index.html#module-astropy.coordinates.builtin_frames), we went with `geocentricmeanecliptic` and `galactic`. 

#### Projection 1: Ecliptic
As a quick refresher, CAOM uses coordinates aligned to the celestial pole, which is aligned to our rotating Earth. A declination of +90 is directly overhead the north pole, while -90 is directly overhead the south pole. Our first transformation is to the ecliptic plane, aligned instead to Earth's orbit around the sun:
![a diagram showing how the ecliptic plane is defined](assets/img/posts/20250625/Earths_orbit_and_ecliptic.svg)
<small>By <a href="//commons.wikimedia.org/wiki/User:CielProfond" title="User:CielProfond">CielProfond</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=156276169">Source</a></small>

Ecliptic coordinates are useful for space-based telescopes, since the sun is — by definition —always at a declination of 0º. In fact, the [survey design of the TESS spacecraft](https://youtu.be/Q4KjvPIbgMI&t=115) takes advantage of this by always keeping one camera on the ecliptic pole, with the others facing opposite the sun.

![the MAST heatmap, reprojected to the plane of the ecliptic](assets/img/posts/20250625/mast_wallpaper_ecl_blue.png)
<small>Ohhhh, so that's why those observations make a straight line around the plane of the ecliptic! They're from TESS.</small>
#### Projection 2: Galactic
Galactic coordinates are, somewhat counter-intuitively, still centered on our Sun. In this case, 0º longitude is defined to be the line between the sun and the center of the galaxy. Latitude measures the angle of an object relative to the flat disk of the galaxy, as seen from Earth.

![](assets/img/posts/20250625/mw.jpg)
<small>By NASA/JPL-Caltech/ESO/R. Hurt - <a rel="nofollow" class="external free" href="http://www.eso.org/public/images/eso1339e/">http://www.eso.org/public/images/eso1339e/</a>, Public Domain, <a href="https://commons.wikimedia.org/w/index.php?curid=28274906">Source</a></small>

The nice thing about using the galactic coordinate system is that most stars are near the plane of the galaxy, so it shows up quite nicely on our plot!
![the mast heatmap, projected to galactic coordinates](assets/img/posts/20250625/mast_wallpaper_gal_blue.png)
<small>The Milky Way, as seen by MAST. Come on, TESS! Observe that last little part in the middle so we can see the whole galaxy.</small>
## Conclusions and Other Thoughts
It's pretty dang cool that through metadata alone, we can reconstruct the shape and even texture of the milky way. These images, which are gorgeous, are also a powerful reminder that MAST has a lot of data. And this is a reminder that those data are free for anyone to access, so check them out through our [search forms](https://mast.stsci.edu/search/ui) or our [astroquery API](https://spacetelescope.github.io/mast_notebooks/intro.html)!

If you've read this far, thanks. Here are a few extra tidbits that you might be thinking about right now:
### Hey, what is that thing I see?
Great question. Take a look at our annotated map, which highlights a few points of interest.
![an annotated version of the heatmap](assets/img/posts/20250625/annotated.png)

### I want to make my own map!
You probably should not do this! It's a pretty large database query, and will degrade the performance of our server if a bunch of people attempt it.

If you absolutely MUST make your own version, please use this [TAR file containing all CAOM observations](https://stsci.box.com/s/ok36t5mmczw6jjj4d6kcmsiiur6vmh1m). Pandas will know how to read it, with a quick `pd.read_pickle()`.

### What does this look like for individual missions?
If you also `SELECT obs_collection` from CAOM, you can build up this map for a particular mission. You'll see that the coverage of the sky depends highly on which mission you select! The largest collection, by far, is our [High-Level Science Products](https://mast.stsci.edu/hlsp/#/). This is due, in part, due to intense community interest in reprocessing TESS observations.
![16 images, showing this map for various MAST missions](assets/img/posts/20250625/mast_missions.png)

### What does this look like over time?
You can also `SELECT t_min` to get the observation start time, which allows you to build up a picture of the archive over time:
![animated GIF, showing the evolution on the sky of MAST observations over time](assets/img/posts/20250625/mast_movie.gif)

Want more visualizations? Stay tuned to the blog! We'll post anything new here.