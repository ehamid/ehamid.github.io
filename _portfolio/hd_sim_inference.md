---
title: "Inference for High-dimensional Single-Index Models"
excerpt: "De-biasing technique for non-linear models + more efficient estimation using Hermite polynomials."
header:
   teaser: /assets/images/hd_sim/histogram.png
gallery:
  - url: /assets/images/hd_sim/link.png
    image_path: assets/images/hd_sim/link.png
    alt: "Using Hermite expansions to estimate link function"
  - url: /assets/images/hd_sim/histogram.png
    image_path: assets/images/hd_sim/histogram.png
    alt: "Histogram comparing efficient and plain de-biased estimates"
---

Preprint on Arxiv: [https://arxiv.org/abs/1909.03540](https://arxiv.org/abs/1909.03540)

In this project we developed methods for constructing confidence intervals and hypothesis tests for the linear component of high-dimensional single-index models.
Single-index models generalize linear models by allowing the reponse $ y $ to depend on a non-linear function of a linear combination of the predictors:
\\[ y = g(\langle x, \beta \rangle ) \\]
This can avoid curse of dimensionality because we are not dealing with a fully non-parametric model $y = g(x)$ which suffers from curse of dimensionality. Even for a high-dimensional $$\beta$$, we still estimate $$\beta$$ if it is sparse and the design is elliptically symmetric.

The code for experiments in the paper is available on github: [https://github.com/ehamid/sim_debiasing](https://github.com/ehamid/sim_debiasing)

{% include gallery caption="More efficient estimation using Hermite polynomials" %}
