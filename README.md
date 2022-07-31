# bayesian-optimization-tutorial

## What is Bayesian Optimization?

Objective: get the maximun value of the function.
Exploration: sample the part with high variance
Exploitation: sample the part with high mean

### Component1: using GP to represent the objective function
* Need to tune the hyperparameters of the kernel and mean

### Component2: using Bayesian Optimization to explore the space (to sample point)
The choice of acquisition function matters. 
#### Expected Improvement (EI)

**Details**
choose the exploration point with highest **sample point** value improvement (assume we only choose from the explored point)

$$
\mathrm{EI}_{n}(x):=E_{n}\left[\left[f(x)-f_{n}^{*}\right]^{+}\right] = \left[\Delta_{n}(x)\right]^{+}+\sigma_{n}(x) \varphi\left(\frac{\Delta_{n}(x)}{\sigma_{n}(x)}\right)-\left|\Delta_{n}(x)\right| \Phi\left(\frac{\Delta_{n}(x)}{\sigma_{n}(x)}\right) \\
x_{n+1}=\operatorname{argmax} \mathrm{EI}_{n}(x)
$$

**Pros** 
inexpensive to evaluate

**Cons**
Prone to noise
Highly risk averse

#### Knowledge Gradient (KG)

**Details**
choosing exploration point can lead to highest **mean** value gain. 
considers the posterior over f’s full domain.

$$
\mathrm{KG}_{n}(x):=E_{n}\left[\mu_{n+1}^{*}-\mu_{n}^{*} \mid x_{n+1}=x\right]
$$

> How to calculate $\mu_{n+1}^{*}$? 
> A: monte carlo simulation 

> How to calculate $argmax\mathrm{KG}_{n}(x)$? 
> A: SGD $\nabla \mathrm{KG}_{n}(x)=\nabla E_{n}\left[\mu_{n+1}^{*}-\mu_{n}^{*} \mid x_{n+1}=x\right] .=E_{n}\left[\nabla \mu_{n+1}^{*} \mid x_{n+1}=x\right] =\nabla \mu_{n+1}\left(\widehat{x^{*}} ; x, \mu_{n}(x)+\sigma_{n}(x) Z\right)$

**Pros**
substantial performance improvements in problems with noise, multi-fidelity observations,

**Cons**
Little gain in noise-free evaluation


#### Entropy Search and Predictive Entropy Search (ES/PES)

**Details**
seek the point to evaluate that causes the largest decrease in differential entropy in maximum value point.

$$
\mathrm{ES}_{n}(x)=H\left(P_{n}\left(x^{*}\right)\right)-E_{f(x)}\left[H\left(P_{n}\left(x^{*} \mid f(x)\right)\right)\right] \\
\mathrm{PES}_{n}(x)=\mathrm{ES}_{n}(x)=H\left(P_{n}(f(x))\right)-E_{x^{*}}\left[H\left(P_{n}\left(f(x) \mid x^{*}\right)\right)\right]
$$

$P_n$ is the distribution of optimal $x^{*}$



**Pros**
useful in exotic problems

**Cons**
the entropy of the maximizer no closed form
hard to estimate and optimize

## Plan

 - [ ] 2D object reconstruction
 - [ ] 2D object reorientation
 - [ ] 3D object reconstruction
 - [ ] 3D object reorientation


## Q&A

> What is mutli-fidelity?
> A: many information source with different fidelity

> How to deal with noisy x?

> How to deal with continous x?

> How to integrate our task into acquisition function?

