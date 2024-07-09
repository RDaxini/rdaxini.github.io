# How to account for the spectral effect on PV devices using pvlib-python?
```{post} 2024-07-09
:author: Rajiv Daxini
:tags: pvlib, solar, example, mismatch, gsoc, spectral
```
This post introduces a new addition to the pvlib-python example gallery that demonstrates the application of pvlib-python to model the shift in PV performance as a result of spectral variation. An update on the GSoC project so far is also presented.

### Importance of the solar spectrum for PV performance modelling

While the effects of variables such as broadband irradiance, temperature, angle of incidence, and so on are bread and butter fundamentals for PV performance modelling, the spectral distribution of the available irradiance is a more subtle yet still important factor to consider. Even for crystalline silicon PV, which is the most stable PV type under variable spectral irradiance conditions, can exhibit weekly changes in performance of up to 14% with respect to standard test condition (STC) performance [1].

The spectral mismatch factor, _M_, characterises the shift in PV performance from STC performance as a result of deviation in the solar spectrum from the STC spectrum (AM1.5). _M_ less (greater) than unity implies lower (higher) performance under the prevailing spectrum compared to performance under the reference spectrum. An _M_value equal to 1 implies no change in performance compared with performance under the reference spectrum.

pvlib-python contains several methods to estimate the spectral mismatch factor based on either PV spectral response and spectral irradiance data, or proxy characterisation indices of the spectrum such as air mass, precipitable water, and clearsky index. If [the stetch goal](https://github.com/pvlib/pvlib-python/issues/2065) of my GSoC project is achieved, a new estimation method using only spectral irradiance data (no spectral response curves) will also be implemented. A full review of different spectral and PV performance shift characterisation indices, as well as methods to estimate _M_ using these indices, is presented in [2].

### Updates in pvlib-python
I have built a new example demonstrating the application of several methods to estimate _M_ found in pvlib-python. The example can be found in the example gallery of the latest (development) version of pvlib-python [here](https://pvlib-python.readthedocs.io/en/latest/gallery/spectrum/spectral_factor.html#sphx-glr-gallery-spectrum-spectral-factor-py), which has not yet been released. This link will be updated to the stable version of the docs once available.

The example takes you through how to import some TMY3 data, select a time period for analysis, calculate the required input variables for three spectral mismatch factor functions, estimate _M_ over the desired timeframe, and plot the results.

### Future work and closing remarks
It is hoped that improvements to the documentation of pvlib-python, in particular for modelling the spectral effect on PV performance, will make it easier for users to account for these effects on their PV systems using pvlib-python. The addition of this example to the example gallery marks the completion of the main GSoC project goals. Future work in this area will include working on the GSoC stretch goal, which is to implement a new function in pvlib-python to estimate the spectral mismatch factor using spectral irradiance data. In addition, enhancements to the user guide documentation for the spectrum unit of pvlib-python are being planned.

### References
[1] Kinsey, G., et al. "Impact of measured spectrum variation on solar photovoltaic efficiencies worldwide." Renewable Energy 196 (2022): 995-1016.

[2] Daxini, R., and Wu, Y. "Review of methods to account for the solar spectral influence on photovoltaic device performance." Energy (2023): 129461.
