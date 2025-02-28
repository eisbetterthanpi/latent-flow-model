# latent-flow-model
conditional latent flow matching from scratch

Flow Matching for Generative Modeling (feb 2023)
https://arxiv.org/pdf/2210.02747.pdf

High-Resolution Image Synthesis with Latent Diffusion Models (apr 2022)
https://arxiv.org/pdf/2112.10752
Stable Diffusion; Latent Diffusion Models(LDM)

Photorealistic Text-to-Image Diffusion Models with Deep Language Understanding (may 2022)
https://arxiv.org/pdf/2205.11487
Imagen

## an exploration into timestep stepsize during sampling 
---
while adaptive solvers are able to produce high quality generations with little hyperparameter tuning
at the expense of speed and simplicity

explore various timestep schedules for image generation with euler's method
simple flow matching model

https://en.wikipedia.org/wiki/Logit-normal_distribution

1) Linear
1) S-shaped
2) Invere Exponential
3) Inverted S shape

horizontal axis: time step
vertical axis: t value for sampling


1) Linear
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/linear.png" width="200"/>
  <div align="center">Linear</div>
</div>
constant stepsize of 1/num_steps
<br/><br/>

2) S-shaped
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/Cosine.png" width="200"/>
  <img src="resources/Polynomial.png" width="200"/>
  <div align="center">Cosine | Polynomial</div>
</div>
small steps at the start and end and larger steps in the middle

3) Inverse Exponential
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/InvertCubic.png" width="200"/>
  <img src="resources/InvertExp.png" width="200"/>
<!--   <div align="center">Inverted Cubic | Invert Exponential</div> -->
</div>
start with large stepsizes and quickly slow down when converging to the final limage
<br/><br/>

4) Inverted S shape
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/LogitNormalCDF_mu0std3.png" width="200"/>
<!--   <div align="center">Logit-Normal CDF with mu=0, std=3</div> -->
</div>
large steps at the start and end and smaller steps in the middle

Scaling Rectified Flow Transformers for High-Resolution Image Synthesis mar 2024
https://arxiv.org/pdf/2403.03206
rf/lognorm(0.00, 1.00)

<br/><br/>

### Results
---
1) Linear
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/lin.png" width="200"/>
<!--   <div align="center">JEPA architecture | Hierarchial JEPA </div> -->
</div>
good baseline results
<br/><br/>

2) S-shaped
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/cos.png" width="200"/>
  <img src="resources/poly.png" width="200"/>
<!--   <div align="center">JEPA architecture | Hierarchial JEPA </div> -->
</div>
quality is worse than linear
<br/><br/>

3) Invere Exponential
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/invcubic.png" width="200"/>
  <img src="resources/invexp.png" width="200"/>
<!--   <div align="center">JEPA architecture | Hierarchial JEPA </div> -->
</div>
quality also worse than linear
<br/><br/>

4) Inverted S shape
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/logitnormcdf_mu0std3.png" width="200"/>
  <div align="center">Logit-Normal CDF with mu=0, std=3</div>
</div>
gives the best results
<br/><br/>

## position of slowdown
---
next we explore how the position of the slowed position influences generation quality

<div align="center">
  <div>&nbsp;</div>
  <img src="resources/LogitNormalCDF_mu-1std3.png" width="200"/>
  <img src="resources/LogitNormalCDF_mu0std3.png" width="200"/>
  <img src="resources/LogitNormalCDF_mu1std3.png" width="200"/>
  <div align="center">Logit-Normal CDF with std=3 and mu=-1(left), mu=0(mid), mu=1(right)</div>
</div>
<div align="center">
  <div>&nbsp;</div>
  <img src="resources/logitnormcdf_mu-1std3.png" width="200"/>
  <img src="resources/logitnormcdf_mu0std3.png" width="200"/>
  <img src="resources/logitnormcdf_mu1std3.png" width="200"/>
<!--   <div align="center">JEPA architecture | Hierarchial JEPA </div> -->
</div>
seem to get bestter results when position of slowdown is towards the end.



