# pvlib: toolbox vs application
```{post} 2024-06-12
:author: Rajiv Daxini
:tags: pvlib, solar, open science, gsoc
```
I wanted to write a short post sharing an interesting discussion that arose in the last pvlib GSoC meeting. What started as a conversation about input data screening in a new spectral correction function turned into a discussion on the role of pvlib for the user. It helped me understand the meaning of "toolbox" in the [official introduction](https://pvlib-python.readthedocs.io/en/stable/index.html) to pvlib:

>pvlib python is a community developed toolbox that provides a set of functions and classes for simulating the performance of photovoltaic energy systems and accomplishing related tasks. 

In short, the question raised (not for the first time) was to what extent should pvlib guide and educate the user in the general field of PV performance modelling, compared with serving as a neutral tool for PV performance modelling as and however the user wishes.

Imagine a user inputs _unusual_* data to a pvlib function, such as negative irradiance or exceptionally high double-digit air mass values, should the function raise an error and fail to proceed? Warn the user? Change the input? Just continue with what it has been given?

I don't intend to conclude the discussion on this subject, which has already been going on for longer than I have even been using pvlib, but just share a summary of some thoughts on the matter through this new blog channel.

*I prefer _unusual_ here as I want to encompass non-physical data as well as inputs that are mathematically correct in the purest sense but may be highly unlikely scenarios that some developers may wish to classify as effectively non-physical and invalidate the user's operation

## Toolbox vs application<a name="summary"></a>
pvlib is officially a toolbox, no denying that. So, what is a toolbox and how does it differ from an application? Whereas an **application** is typically built on predetermined workflows, a **toolbox** contains the building blocks for the user to construct their own workflows. The models, functions, resources (tools...) within the pvlib toolbox can each be used separately for specific applications, or combined with any range of pvlib models as well as custom models from the user [1]. This flexibility is a paramount, particularly in research applications where developers seek to experiment with new modelling models and methods.

Besides this fundamental difference in principles between the two, another difference is that a toolbox typically has a minimal user interface, if one at all. Meanwhile, an application may be run through a graphical user interface. In turn, this leads to a toolbox requiring a greater level of user proficiency since the user retains greater autonomy over the modelling process.

In summary, compared with an application, a toolbox...

- Enables custom workflows
- Provides increased flexibility
- Assumes a higher level of user proficiency

## Implications
Returning to our data screening scenario. In the case of an application, the user interface may only accept inputs of values that meet certain conditions in order to satisfy the requirements of the preset modelling conditions. Currently in pvlib, there is no standard way to approach this.

Some functions contain data screens to warn users of _unusual_ inputs, and change their values to `nan` or some other pre-determined default. For example, the [`pvlib.spectrum.spectral_factor_firstsolar()`](https://pvlib-python.readthedocs.io/en/v0.10.5/reference/generated/pvlib.spectrum.spectral_factor_firstsolar.html) takes airmass and precipitable water as two of its inputs. The function allows the user to set a maximum value for precipitable water. Any data greater than this value will be replaced by `nan` and the user will be warned. If the user does not define a maximum, the maximum defaults to 8. The model also contains a restriction on airmass values, over which the user has no control. No matter the circumstances, air mass values greater than 10 will default to 10 without warning. On the other hand, a function such as [`pvlib.pvsystem.Array_get_irradiance()`](https://pvlib-python.readthedocs.io/en/stable/reference/generated/pvlib.pvsystem.Array.get_irradiance.html) would allow you to input airmass values of 100 if you so wish.

pvlib may be characterised quite clearly as a toolbox, which has a fairly straightforward (albeit somewhat subjective) definition. In practice, as functions have been implemented over time, the content of the toolbox appears to cross boundaries between applications and tools. Is that a bad thing? No, not necessarily. I'd like to float a few ideas on what I think might be important to consider in future though.

## What next?
Referring back to the three key characteristics of a toolbox in [the summary here](#summary), I think emphasing flexibility is key. Pvlib is a toolbox; that's what makes it unique and that is its strength. Does that mean we should go through all existing pvlib functions with pitchforks to purge out every last data input screen that ever dare glance upon our data? No, certainly not. There is good reason to screen data in some cases where a particular model that is implemented stipulates such data limits as part of its implementation. While I am hesitant to encourage _changing_ any user's input data in any scenario, and even more so in the absence of any user control, I do see some value in educating the user through the use of data screens for basic "sense checks". Preventing a user from running certain modelling scenarios diminishes flexibility, but at the same time some sense checks accompanied by warnings could help enhance the usability of pvlib while retaining the flexibility of its application.

Another way to think about this is that each user will have their own intended use for pvlib and as a toolbox it is the role of pvlib to serve the user however they wish. I think it is reasonable to advise a user on what may constitute extreme input conditions, but I maintain the user should retain control of how they use any function in pvlib. I can imagine a scenario in which a user may wish to see how or why a particular modelling scenario does not work under certain extreme conditions, or even see for themselves why certain conditions are in fact extreme, and needs to input _unusual_ data. On the other hand, using the airmass example again, if a user enters a negative air mass value then although I would let them run their scenario it could be argued that the most likely reason for this is a typo and as such it may be useful to prompt the user with a brief warning.

I lean more towards maintaining the core principles of a toolbox within pvlib and minimising interference with the user's actions. However, I do feel there is room for supporting users. This could take the form of data screens for basic sense checks, but without preventing users from running their desired scenarios. It could also take the form of enhancing the documentation, for example to explicitly state the bounds within which models have been designed for use, and perhaps including references to external resources that can educate the user on the associated modelling theory.

## Closing remarks
Pvlib is a toolbox containing tools. Paraphrasing the wise words of one pvlib maintainer:

> A hammer is a tool from a toolbox. It is used to knock in nails. If you try using it to knock in a screw, does it throw an error at you? No. Neither should pvlib.

Personally, I almost wholly on board with team hammer.

Would I be annoyed if my hammer tried to switch out my screw for a nail? Yes.

Would I be bothered if my hammer warned me that hitting screws is not the function for which it is designed? No, as long as it still allowed me to hit my screw.
If I'd never used a hammer before, I'd probably even appreciate the warning.

_But_ let's say I bought my hammer to knock in tent stakes and the developer didn't consider that application... well, then I might get a little, just a little, irritated by the warning every time I tried to pitch my tent.

Okay, we (I) might getting carried away with the hammers now but I think my point is clear and I hope this post gets us thinking about what we want from pvlib.

------------------
-Dax

Published: 12 June 2024
Revised: 24 June 2024 following GH discussions

## References
[1] [Anderson, Kevin S., et al. "pvlib python: 2023 project update." _Journal of Open Source Software 8_(92) (2023): 5994.](https://joss.theoj.org/papers/10.21105/joss.05994)

