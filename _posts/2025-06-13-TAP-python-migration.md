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

MAST has been quietly building support for Table Access Protocol services on a modern Python platform for catalogs large and small. Updates to improve metadata, usability, and documentation have culminated in a series of catalogs available via TAP standard API interfaces at [https://mast.stsci.edu/vo-tap](https://mast.stsci.edu/vo-tap). It is time to sunset the TAP services on the previous system. We will be closing down the vao.stsci.edu TAP services on _Thursday, June 26, 2025_. 

In order to support improvements to TAP's complex asynchronous job management infrastructure, queries to the old TAP services based on https://vao.stsci.edu _will not be automatically forwarded_.

We have updated IVOA registry resources for smart client access, tutorial notebooks, and links within research software including TOPCAT to point to the new services, and expect this move to be invisible to most of our users. The new TAP service includes every catalog we had previously made available on the older vao.stsci.edu platform, as well as new catalogs and High Level Science Products (HLSPs). Current catalogs include CAOM, GAIA DR3, Hubble Source Catalog, PanSTARRS1 DR1 and 2, the MAST searchable IVOA registry, TIC, and HLSPs including CLASSY, ULLYSES, GOODS, 3D-HST, and CANDELS. The move comes with updated status pages, examples, improved metadata, and try-it-yourself Swagger-based OpenAPI documentation on the new site. 
