---
layout: post
read_time: true
show_date: true
title: "New Documentation Series: MAST Pro Tips"
date: 2025-03-20
img: posts/20250320/barnard_astroview_crop.png
tags:
  - tutorials
category: Documentation
author: Richard Shaw
description: Learn some hard-won tips and tricks from the Archivists.
---
A new series of MAST technical articles has been published to our documentation platform. [MAST Pro Tips](https://outerspace.stsci.edu/display/MASTDOCS/MAST+Pro+Tips) features three new articles on advanced topics to help you improve your searches. Technical articles on other topics will appear from time to time. If you wish to learn more about a particular topic, please send your idea to [archive@stsci.edu](mailto:archive@stsci.edu).

## [High Proper Motion Stars in MAST](https://outerspace.stsci.edu/display/MASTDOCS/High+PM+Stars+in+MAST)
Perhaps you knew that coordinates in MAST are assumed to be ICRS at the J2000 epoch, both as input for searches and as output for search results. It may not be a surprise that the Portal AstroView tool shows the selected background survey at the mean epoch of the survey images. This has caused some confusion in the past when users search for observations of sources with high proper motion.

![Barnard's Star as seen in the Portal AstroView tool. The iridescent explosion at top is from PanSTARRS, while the red and blue blobs at bottom are from the Digital Sky Survey. The red circle surrounding the magenta cross (near the center) shows the ICRS J2000 search position.](assets/img/posts/20250320/barnard_astroview.png)
<small>Barnard's Star as seen in the Portal AstroView tool. The iridescent explosion at top is from PanSTARRS, while the red and blue blobs at bottom are from the Digital Sky Survey. The red circle surrounding the magenta cross (near the center) shows the ICRS J2000 search position.</small>

The image above shows a composite of the Digital Sky Survey (DSS, the default, at the bottom) and the Pan-STARRS survey (top) for a field near Barnard's Star. The bright, blue source below the bright red source are both Barnard's star at the mean epoch of the DSS blue and red plates, respectively. The bright star near the top is Barnard's star at the epoch of the Pan-STARRS survey. (The strange PSF is the result of combining individual survey images where the star has moved slightly between the epochs of the contributing images.) Barnard's star has moved considerably in the 25+ years that have elapsed between the DSS and Pan-STARRS surveys. Any HST, JWST, or other mission observation footprints would be shown in J2000 coordinates _at the time of the observation_. The article linked above describes how to search for moving targets and to re-interpret the results at the epoch of interest to you.
## [Finding Solar System Bodies in MAST](https://outerspace.stsci.edu/display/MASTDOCS/Finding+Solar+System+Bodies+in+MAST)
Finding observations of solar system bodies in MAST is challenging because searching for time-dependent coordinates is not well supported. This article descrbes strategies for search by source name, and for using external tools to determine source sky coordinates at a particular epoch to enable MAST searches by position.
## [Searching for Named Sources](https://outerspace.stsci.edu/display/MASTDOCS/Searching+for+Named+Sources)
Searching for sources by name in MAST interfaces (Portal, Mission Search, astroquery) sometimes yields surprising results. Find out what happens behind the scenes to translate a name to sky coordinates, and learn how to avoid pitfalls caused by ambiguous names and poor name syntax.
