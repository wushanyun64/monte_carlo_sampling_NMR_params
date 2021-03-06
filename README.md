# Posterior distribution of fitted NMR parameters by Markov Chain Monte Carlo (MCMC) 

After the NMR spectrum is fitted, it is often useful to get an estimation of the reliability of the fitted NMR parameters. One of the common methods is through Monte Carlo simulation. Here we present a utility function that makes use of the Markov Chain Monte Carlo (MCMC)[1] method provided by package emcee[2] to sample the posterior distribution of the fitted NMR parameters by Mrsimulator[3].

Here we calculate the log-posterior probability <img src="https://render.githubusercontent.com/render/math?math=\color{gray}\ln p(F_{true} | D)">:

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}\ln p(F_{true} | D) \propto \ln p(D | F_{true}) + \ln p(F_{true})">

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}\F_{true}"> is the NMR parameters, D is the NMR spectrum data.

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}\ln p(D | F_{true})"> is the log-likelihood and $\ln p(F_{true})$ is the log-prior.

The log-likelihood function is defined as:

<img src="https://render.githubusercontent.com/render/math?math=\color{gray}\ln p(D|F_{true}) = -\frac{1}{2}\sum_n \left[\frac{(g_n(F_{true}) - D_n)^2}{s_n^2}+\ln (2\pi s_n^2)\right]">

Where <img src="https://render.githubusercontent.com/render/math?math=\color{gray}\g_n(F_{true})"> is the fitted NMR spectrum data points and  $s_n$ is the standard deviation of the spectrum noise. <img src="https://render.githubusercontent.com/render/math?math=\color{gray}\g_n(F_{true}) - D_n"> can be viewed as the residual of the fitted NMR spectrum. For more details of this implementation, please refer to the emcee package.

After the posterior distribution is correctly sampled, correlation plots as well as histograms for all the parameters can be ploted with Corner[3]. 

![corr_map](./figures/correlation_map.png)

**Reference**
____________________________________________________________________________________________
[1] Hou, F., Goodman, J., Hogg, D. W., Weare, J., & Schwab, C. (2012). An affine-invariant sampler for exoplanet fitting and discovery in radial velocity data. The Astrophysical Journal, 745(2), 198.

[2] Foreman-Mackey, D., Hogg, D. W., Lang, D., & Goodman, J. (2013). emcee: the MCMC hammer. Publications of the Astronomical Society of the Pacific, 125(925), 306.

[3] https://mrsimulator.readthedocs.io/en/stable/

[4] https://corner.readthedocs.io/en/latest/