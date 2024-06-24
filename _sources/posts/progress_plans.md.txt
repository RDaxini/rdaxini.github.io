# pvlib v0.11.0 release and GSoC update
```{post} 2024-06-24
:author: Rajiv Daxini
:tags: pvlib, solar, open science, gsoc, v0.11.0
```
## pvlib v0.11.0 release

A new version of pvlib-python was released on 23 June 2024, featuring multiple updates including: 

* Two new spectral correction factor models
* A water albedo model for floating PV applications
* Functions to calculate shaded fraction and electrical loss due to row-to-row shading
* A simple transformer efficiency model

More details on this release and previous versions can be [found here](https://pvlib-python.readthedocs.io/en/stable/whatsnew.html).

This month's release features two contributions from myself through my GSoC project, which are my first ever contributions to pvlib python. I am grateful to my mentors, Adam Jensen and Kevin Anderson, for supporting me through my first contribution, as well as Cliff Hansen and fellow GSoC students Echedey and Ioannis for helping with reviews. At the time of this month's release and the conclusion of my first pvlib contribution, I'd like to summarise the progress of my GSoC project so far and highlight the ongoing work as well as next stages for the project.

## Progress to date
There are two categories to the progress so far: new knowledge and hard output.

As for new knowledge, these involve both workflow and coding; I've developed (and still developing...) a new work environment and learnt (and still learning) how to use GitHub for collaborative coding. As for coding, I've learnt new skills in terms of testing, as well as writing documentation (as a general skill, as well as specifically in markdown), and creating and reviewing pull requests (PRs).

For hard outputs, I've created three PRs, two of which have been merged while the third remains open. Summary:

* [PVSPEC spectral factor model](https://pvlib-python.readthedocs.io/en/stable/reference/generated/pvlib.spectrum.spectral_factor_pvspec.html#pvlib.spectrum.spectral_factor_pvspec)
* [JRC spectral factor model](https://pvlib-python.readthedocs.io/en/stable/reference/generated/pvlib.spectrum.spectral_factor_jrc.html#pvlib.spectrum.spectral_factor_jrc)
* Update First Solar spectral factor model ([open PR](https://github.com/pvlib/pvlib-python/pull/2100))

## Onward plans
For the remainder of the GSoC project, there are three key tasks:
* Close the ([open PR](https://github.com/pvlib/pvlib-python/pull/2100)) to update the First Solar spectral factor model
* Create a new addition to the example gallery that will demonstrate the application of spectral factor models to calculate the spectral mismatch factor and compare their outputs ([Open issue](https://github.com/pvlib/pvlib-python/issues/2107))
* Stretch goal: add a new spectral factor model that takes spectral irradiance data as an input (stretch goal in [this related issue](https://github.com/pvlib/pvlib-python/issues/2065))
* Contribute more reviews

The final point links to a skill I will continue developing over the course of this project. As I build up my knowledge of pvlib, I will contribute more to reviewing open PRs and providing feedback on issues. 

------------------
-Dax

24 June 2024
