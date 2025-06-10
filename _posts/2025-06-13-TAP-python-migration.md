---
layout: post
read_time: true
show_date: true
title: "June 26: all TAP access to Python"
date: 2025-06-13
tags: [tools-techniques]
category: IVOA
author: Theresa Dower
description: "Migration of MAST TAP services, sunsetting vao.stsci.edu"
---

MAST has been busy building support for Table Access Protocol (TAP) services on a modern Python platform, to support our catalogs large and small. Updates to improve metadata, usability, and documentation have culminated in a series of catalogs available via [TAP standard API interfaces](https://mast.stsci.edu/vo-tap); this includes all data we've made available via TAP on older platforms. It is now time to sunset the TAP services on the previous system. We will be closing down the vao.stsci.edu TAP services on _Thursday, June 26, 2025_.

In order to support these improvements — especially TAP's powerful but complex asynchronous job management infrastructure — queries to the old TAP services based on https://vao.stsci.edu _will not be automatically forwarded_. Links to vao.stsci.edu TAP services will not work after this date; scripts with hardcoded links to a MAST TAP service on vao.stsci.edu must be updated. The [service listing](https://mast.stsci.edu/vo-tap) provides the new URL to reach every TAP-accessible catalog at MAST.

 The new Python TAP service on mast.stsci.edu includes every catalog previously available on the older vao platform, as well as new catalogs and High Level Science Products (HLSPs). Current catalogs include CAOM, GAIA DR3, Hubble Source Catalog, PanSTARRS1 DR1 and 2, the MAST searchable IVOA registry, TIC, and HLSPs including CLASSY, ULLYSES, GOODS, 3D-HST, and CANDELS. We have already updated IVOA registry resources to point to the new services. This update will be invisible to most of our users, including those using smart client access with pyvo, [MAST tutorial notebooks](https://spacetelescope.github.io/mast_notebooks/intro.html), and links within research software like TOPCAT. The move comes with updated status pages, examples, improved metadata, and try-it-yourself Swagger-based OpenAPI documentation on the new site. If you encounter any issues, please contact the [MAST helpdesk](https://stsci.service-now.com/mast).
