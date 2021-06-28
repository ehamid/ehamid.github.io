---
title: "Empirical Bayes for Binomial Probabilities"
header:
  tags: 
  - Empirical Bayes
  - Hierarchical Bayes
---

In a recent project I encountered a problem that after some pre-processing reduces to estimation of probabilities for many independent Binomial experiments each having a different success probability. Also, in each experiment the number of trials is not large, so some way of pooling the data seemed appropriate. I thought empirical Bayes may be useful here and this post describes some of the approaches inspired by this methodology. Next I describe the mathematical formulation of the problem.

Suppose that $$X_i \sim \operatorname{Bin}(m,p_i), i = 1,2,\dots,n $$ are iid binomial random variables with known $$m$$ and unknown $$p_i$$. Our goal is to estimate $$p_i$$ given the observations $$(X_i)_1^n$$. 

The most natural estimate for $$p_i$$ is perhaps $$X_i / m$$, the proportion of successes among the $$m$$ trials. This is an unbiased, uniformly minimum variance estimate of $$p_i$$ and by the strong/weak law of large numbers it is also consistent as $$m \rightarrow \infty$$. But can we do better when $$m$$ is not large?

Specifically, we are interested in cases where $$m \ll n$$ (say, $$m = 5$$). Clearly, in this case we have almost as many parameters as observations, and the problem is therefore called a high-dimensional estimation problem. In such cases it is usually beneficial to dispense with the unbiasedness requirement and instead use some sort of shrinkage to trade variance for bias, hoping that at the end this tradeoff results in a better estimator.

Empirical Bayes is one such methodology that allows borrowing strength when faced with many estimation problems together. In this problem, we can relate all these $$n$$ seemingly disparate problems by assuming that the parameters $$p_i$$ are themselves iid random variables generated according to a prior $$\pi(p)$$. In contrast to a genuine Bayesian method, we do not speficy the prior $$\pi(p)$$ beforehand. 

Let us follow this line of thinking for our problem. The posterior mean seems like a reasonable estimator of $$p_i$$ if we can compute it without needing to specify the prior. We have

\\[
E[p_i \mid X_i] = \frac{ \int p_i {m \choose X_i} p_i^{X_i} (1 - p_i)^{m - X_i} d\pi(p_i)}{\int {m \choose X_i} p_i^{X_i} (1 - p_i)^{m - X_i} d\pi(p_i)} = \frac{ \int p_i {m \choose X_i} p_i^{X_i} (1 - p_i)^{m - X_i} d\pi(p_i)}{f_m(X_i)},
\\]
where $$f_m(X_i)$$ denotes the marginal mass/density function of data at $$X_i$$ given Bernoulli $m$ trials.
It seems we are out of luck unless we choose a prior and compute the integral (analytically or via stochastic methods) in the numerator. But that's where the genius of Robbins's Empirical Bayes comes in. 

The numerator already looks kind of like the denominator. Let's see if we can write it in terms of a quantity that can be estimated based on data alone (like the marginal in the denominator). We can rewrite the numerator as

\\[ 
\int p_i {m \choose X_i} p_i^{X_i} (1 - p_i)^{m - X_i} d\pi(p_i) = \frac{{m \choose X_i}}{{m+1 \choose X_i+1}} \int {m+1 \choose X_i+1} p_i^{X_i+1} (1 - p_i)^{(m+1) - (X_i+1)} d\pi(p_i) \\
= \frac{X_i + 1}{(m+1)} f_{m+1}(X_i + 1),
\\]
where $$f_{m+1}$$ is the p.m.f. of data but now given $$m+1$$ trials. Plugging this back into the equation for the posterior mean, we find

\\[
E[p_i \mid X_i] = \frac{(X_i + 1)}{ m+1 } \cdot \frac{f_{m+1}(X_i+1)}{f_{m}(X_i)}.
\\]

This looks promising. It is fairly obvious how to estimate $$f_m$$ given the data we have: for $$ 0 \leq k \leq m $$ we can estimate $$f_m(k)$$ by the proportion of $$X_i$$ that are equal to $$k$$:

\\[
\hat{f}_m(k) = \frac{|\{ i \leq n : X_i = k  \} |}{n}.
\\]

It is less clear how to estimate $$\hat{f}_{m+1}(k)$$ since it requires data from $$\operatorname{Bin}(m+1, p_i)$$ distribution which we don't have. We can not make up the extra $$(m+1)$$th observation, but what we can do, is to first pretend we only observed $$m-1$$ observations (and replace $$m$$ by $$m-1$$ in the above formula), and then bring in the $$m$$th trial as the extra observation. This is exactly what [Robbins (1955)](https://projecteuclid.org/ebooks/berkeley-symposium-on-mathematical-statistics-and-probability/Proceedings%20of%20the%20Third%20Berkeley%20Symposium%20on%20Mathematical%20Statistics%20and%20Probability,%20Volume%201:%20Contributions%20to%20the%20Theory%20of%20Statistics/chapter/An%20Empirical%20Bayes%20Approach%20to%20Statistics/bsmsp/1200501653) suggested: if we let $$X_i'$$ be the number of successes among the first $$m-1$$ trials in stage $$i$$, then we can compute an estimate

\\[
\hat{p}_i = \frac{ X_i' + 1 }{m} \cdot \frac{\hat{f}_{m}(X_i' + 1)}{\hat{f}_{m-1}.(X_i')}.
\\]

This doesn't look too bad. In a future post I'll show that estimating odds $$p_i / (1 - p_i)$$ or log-odds $$\log(p_i / (1 - p_i) )$$ may be more straightforward, and then we can compare several of these estimators in our particular problem.

In addition to [Robbins (1955)](https://projecteuclid.org/ebooks/berkeley-symposium-on-mathematical-statistics-and-probability/Proceedings%20of%20the%20Third%20Berkeley%20Symposium%20on%20Mathematical%20Statistics%20and%20Probability,%20Volume%201:%20Contributions%20to%20the%20Theory%20of%20Statistics/chapter/An%20Empirical%20Bayes%20Approach%20to%20Statistics/bsmsp/1200501653), a good source to learn more about empirical Bayes is Efron's [Large-Scale Inference: Empirical Bayes Methods for Estimation, Testing and Prediction](https://statweb.stanford.edu/~ckirby/brad/LSI/monograph_CUP.pdf).