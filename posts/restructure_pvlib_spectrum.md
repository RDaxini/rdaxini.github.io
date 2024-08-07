# Restructuring and renaming: pvlib/spectrum
```{post} 2024-08-07
:author: Rajiv Daxini
:tags: pvlib, solar, spectrum, testing, gsoc, spectral
```
This post discusses and summarises some recent work to restructure the [`pvlib/spectrum`](https://github.com/pvlib/pvlib-python/tree/main/pvlib/spectrum) package and [associated tests](https://github.com/pvlib/pvlib-python/tree/main/pvlib/tests/spectrum).

### The issue

Following the implementation of multiple new functions in what was originally a single `mismatch.py` file through not only my GSoC project but that of a fellow GSoC'er too, the size and scope of the contents was being stretched far beyond spectral mismatch. It felt like the right time to break the file down into more easily maintainable chunks that followed a clearer categorisation according to function contents. Splitting `mismatch.py` would not be a user-facing change, since the functions would still be called from `pvlib.spectrum`, but would impact future maintenance of the `spectrum` package.

### The solution

Proposing to break up a file is one thing, deciding how is another. The first question is naming and categorisation. The original proposal from myself in [GH issue #2125](https://github.com/pvlib/pvlib-python/issues/2125) was to define three categories in three files as follows:

1. `pvlib/spectrum/mismatch.py` 
--> covers the effect on PV performance; calculations of spectral mismatch (atmospheric, field, indoor)

2. `pvlib/spectrum/spectral_irr.py`
--> covers the outdoor meteorological side of things; all spectral irradiance calcs, e.g. `get_reference_spectra`, possibly move `spectrl2` into here as well

4. `pvlib/spectrum/spectral_resp.py` 
--> covers the PV characteristics side of things, e.g. sr_to_qe / qe_to_sr calculations, `get_example_spectral_response`

While the suggestion of categories stuck, an interesting discussion ensued over the naming. First, using full names "irradiance" and "response" was suggested. The question of whether to include the `spectral_` prefix then arose. On the one hand, the prefix could be argued as redundant since the files are already location in a folder entitled "spectrum". On the other hand, having an `irradiance.py` file with no prefix could cause issues in a specific scenario where a user tries the following:

```
from pvlib import irradiance
from pvlib.spectrum import irradiance
```

since the name "irradiance" alone is being used by the `pvlib/irradiance` package. Ultimately, it was decided that the prefix should be banished to a land far far away where it may wallow in its redundancy.

For the PRs associated with this task, see [#2136](https://github.com/pvlib/pvlib-python/pull/2136) (restructuring `pvlib/spectrum` functions) and [#2151](https://github.com/pvlib/pvlib-python/pull/2151) (restructuring the associated tests from `test_spectrum.py`).

### Concluding remarks

Working on the structure of folders in pvlib has been an interesting experience and involved different discussions and coding skills compared with my previous tasks, which have primarily been to implement new spectral mismatch estimation models. One of these new discussions for me has been naming in pvlib, which is an ongoing process and challenge. I have also raised [an issue](https://github.com/pvlib/pvlib-python/issues/2150) about how we refer to spectral irradiance in pvlib, and I have noticed that we refer to the spectral mismatch as both "mismatch" and "spectral factor", which may need standardising at some point. Having consistent and understandable naming for both maintainers and users, as well as a clear structure and organisation makes both maintenance and use easier.
