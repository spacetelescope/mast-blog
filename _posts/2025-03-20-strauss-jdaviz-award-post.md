---
layout: post
read_time: true
show_date: true
title: "The STRAUSS-Jdaviz integration wins a prize for the 2025 sonification awards"
date: 2025-03-20
img: posts/20241022/jdaviz.svg
tags: [jdaviz, sonification, strauss, award]
category: jdaviz
author: Cami Pacifici
description: "STRAUSS-Jdaviz integration and award"
---

Last year, [STRAUSS](https://strauss.readthedocs.io/en/latest/) and [Jdaviz](https://jdaviz.readthedocs.io/en/stable/)
started a collaboration to sonify astronomical data and open up a whole new way of interacting specifically with 3D cubes.
Today, STRAUSS+Jdaviz [won a prize for the 2025 sonification awards](https://sonification.design/#Jdaviz)!

## What is STRAUSS?
STRAUSS is a Python toolkit for the representation of data into sound with both scientific and outreach applications.
It can be used to enhance visual representations or for accessibility for visually impaired people.
STRAUSS is intended to be straightforward, but also flexible enough to allow for detailed control over
the sonification process. The project is described in more detail in the paper
[Introducing STRAUSS: a flexible sonification Python package](https://arxiv.org/abs/2311.16847).

## How is STRAUSS integrated in Jdaviz?
Jdaviz is a Python package to visualize and analyze imaging and spectroscopic astronomical data.
3D dataset (or cubes) are a combination of imaging and spectroscopy. In practice, for every pixel in an image,
a spectrum spanning a given wavelength range is also available. Exploring cube data can be challenging and
Jdaviz includes a specific configuration for this type of data: [Cubeviz](https://jdaviz.readthedocs.io/en/stable/cubeviz/index.html).

![Cubeviz interface showing...](./assets/img/posts/20250320/cubeviz_sonify.png)
<small>caption</small>

The STRAUSS and Jdaviz teams worked together to build a plugin in Cubeviz to sonify data. In practice,
the user can choose the whole spectrum or a specific wavelength range of interest along with a set of
advanced sound options (e.g., minimum and maximum audio frequency, volume index, flux percentile cut)
to produce a grid of sounds that correspond to features in the data. By moving the cursor on the image,
the user is able to hear differences in the sound, for example in pitch, mapping the position of a specific feature in wavelength,
and in volume, mapping the intensity of a specific feature.
