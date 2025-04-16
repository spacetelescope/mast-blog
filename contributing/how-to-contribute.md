## Template
See the [template post](1900-01-01-template-post.md) to understand the structure of a typical post. You can also look at some previous posts, like the ["MAST Pro Tips" article](../_posts/2025-03-20-mast-pro-tips.md).

## Where do posts go?
Once you've written a markdown post following the template above, you can add it to `_posts/`. Please follow the naming convention `YYYY-MM-DD-article-name-here.md`. Any images should be added to a folder corresponding to the article date, i.e. `assets/img/posts/YYYYMMDD/`.

## How do I preview a post?
Generally, most editors are capable of parsing markdown files. If you want to make sure images will show up [obsidian](https://obsidian.md/) is a great tool; it also does some fancy syntax formatting of the article metadata

## Article Metadata
Most of the metadata are straightforward for contributors. Potential points of confusion are clarified below.

### "Don't Change" Categories
Please do not change any of the following values:
- `layout: post` keeps your contribution as a blog post
- `read_time: true` includes a reading time estimate for users
- `show_date: true` shows the published date

### Img
The `img` in the metadata is the preview image for that article. For example, in the ["STRAUSS Award" article](https://spacetelescope.github.io/mast-blog/strauss-jdaviz-award-post.html), it is the STRAUSS logo at the top of the page. It will also be used as the "preview" image for the post in searches and on the blog homepage. An image with a landscape aspect ratio will work best.

Images within articles are included separately, by specifying a path to them using markdown link syntax.

### Tags
Tags are used to sort posts. You should use at least one tag from the table below. When appropriate you may use multiple tags, including those not listed in the table (for example, tagging a post with "software-release" and "jdaviz").

|Tag|Usage|
|---|-----|
|data-release|New data are available in MAST. HLSPs are the most common example of this.|
|fun|Quirky updates from everyone's favorite space telescope archive. MAST RPG character sheets and the mast-match card game are good examples of "fun" updates.|
|pi-corner|Big updates from MAST's principal investigator, or leadership staff.|
|outreach|Annoucements about AAS, or similar opportunities for the community to interact directly with us.|
|software-release|An STScI-maintained package has been updated with an exciting new feature or performance improvement.|
|tech-stack|Deep-dives into the technology that enables MAST or STScI-produced software. This can be forward-looking, but we should have a robust plan to build something before sharing with the community.|
|tools-techniques|Novel tools and techniques to analyze MAST data; more about interesting science than the tool itself. A paper that uses 30 years of multi-mission observations to establish a long baseline is a great example of this.
|tutorials|New or updated jupyter notebooks, videos, and documentation. Anything else that can reasonably be considered a tutorial is ok, too.|
