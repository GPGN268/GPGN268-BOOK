# Common Random Variables & Limit Theorems

## Learning Objectives
- Understand the definitions and basic properties of the most common random variables used in probability, statistics, and geophysics.
- Work with CDFs/PDFs and expectations for:
  - Bernoulli
  - Geometric
  - Uniform
  - Exponential
  - Gaussian (Normal)
- Build intuition for the Law of Large Numbers (LLN) and the Central Limit Theorem (CLT).
- Connect these distributions to modeling choices in geophysical problems.


## Motivation
Many models in geophysics involve simple stochastic components:
- Sensor failures → Bernoulli
- Number of seismic events until the first detection → Geometric
- Modeling unknown phase or angle → Uniform
- Waiting times between nuclear decay events → Exponential
- Measurement noise → Gaussian

These “canonical” distributions form the backbone of probabilistic modeling.  
We introduce each with:
- Definition
- PDF
- Expectation & variance
- Interpretation & use cases

## Discrete Random Variables

### Bernoulli Random Variable
A Bernoulli random variable models a single binary outcome (success/failure).

#### Definition
Let  
```math
X \sim \text{Bernoulli}(p), \quad p \in [0,1].
```
Then  
```math
\mathbb{P}(X=1)=p, \qquad \mathbb{P}(X=0)=1-p.
```

#### Expectation and Variance
```math
\mathbb{E}[X]=p, \qquad 
\mathrm{Var}(X)=p(1-p).
```

#### Interpretation
- Models a “yes/no” event: arrival/no arrival, failure/success, detection/no detection.
- Often used as building blocks for more complex models (e.g., Binomial, Bernoulli processes).


### Geometric Random Variable
The geometric distribution measures the number of independent Bernoulli trials needed until the first success.

#### Definition
Let  
```math
X \sim \text{Geom}(p).
```
Then  
```math
\mathbb{P}(X=k) = (1-p)^{k-1}p.
```

#### Expectation and Variance
```math
\mathbb{E}[X] = \frac{1}{p}, \qquad
\mathrm{Var}(X) = \frac{1-p}{p^2}.
```

#### Interpretation
- Models waiting time (in *counts*) until a success.
- Example: number of seismic traces until the first clear reflection.


## Continuous Random Variables

### Uniform Distribution
The simplest continuous distribution: all values in an interval are equally likely.

#### Definition
Let  
```math
X \sim \text{Uniform}(a,b),\quad a < b.
```
PDF:
```math
f_X(x)=
\begin{cases}
\frac{1}{b-a}, & a \le x \le b, \\
0, & \text{otherwise}.
\end{cases}
```

#### Expectation and Variance
```math
\mathbb{E}[X]=\frac{a+b}{2}, \qquad
\mathrm{Var}(X)=\frac{(b-a)^2}{12}.
```

#### Interpretation
- Unknown phase, unknown time shift, random orientation.
- Often serves as a least-informative prior over bounded ranges.


### Exponential Distribution
The exponential models waiting times between independent events (e.g., Poisson processes).

#### Definition
Let  
```math
X \sim \text{Exponential}(\lambda), \quad \lambda > 0.
```
PDF:
```math
f_X(x)=
\begin{cases}
\lambda e^{-\lambda x}, & x\ge 0, \\
0, & x < 0.
\end{cases}
```

#### Expectation and Variance
```math
\mathbb{E}[X]=\frac{1}{\lambda}, \qquad 
\mathrm{Var}(X)=\frac{1}{\lambda^2}.
```

#### Memoryless Property
```math
\mathbb{P}(X > s+t \mid X > s) = \mathbb{P}(X > t).
```

```{admonition} Proof (click to expand)
:class: dropdown
For $X\sim \mathrm{Exponential}(\lambda)$ and $s,t\ge 0$:
$$\mathbb{P}(X>u)=e^{-\lambda u}, \quad u\ge 0.$$
So,
$$\begin{align}
&\mathbb{P}(X>s+t\mid X>s)\\
=&\frac{\mathbb{P}(X>s+t, X>s)}{\mathbb{P}(X>s)}\\
=&\frac{\mathbb{P}(X>s+t)}{\mathbb{P}(X>s)}\\
=&\frac{e^{-\lambda(s+t)}}{e^{-\lambda s}}\\
=&e^{-\lambda t}\\
=&\mathbb{P}(X>t).
\end{align}$$
Hence the exponential distribution is memoryless.
```

#### Interpretation
- Time between independent seismic events.
- Waiting time until a Poisson-distributed arrival.
- Common in queueing, signal processing, and reliability modeling.

 

### Gaussian (Normal) Distribution
The most important continuous distribution in modeling measurement noise and aggregated effects.

#### Definition
Let  
```math
X \sim \mathcal{N}(\mu, \sigma^2).
```
PDF:
```math
f_X(x)=
\frac{1}{\sqrt{2\pi\sigma^2}}
\exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right).
```

#### Expectation and Variance
```math
\mathbb{E}[X] = \mu, \qquad
\mathrm{Var}(X) = \sigma^2.
```

#### Interpretation
- Models additive noise in seismic recordings.
- Arises from many small independent perturbations.
- Stable under linear transformations and sums.


## Limit Theorems
These theorems bridge between _probability_ and _statistics_. We are now starting to think about how to do things when we have only finite amount of data.

### Law of Large Numbers (LLN)

#### Statement (informal)
Let $X_1, X_2, \dots$ be independent and identically distributed (i.i.d.) random variables with 
$$\mathbb{E}[X_i] = \mu, \qquad \mathrm{Var}(X_i)=\sigma^2<\infty. $$
Define the sample average  
```math
\overline{X}_n = \frac{1}{n}\sum_{i=1}^n X_i.
```

<!-- ```{admonition} Statement (informal) -->
As $n\to\infty$,
$$\overline{X}_n \to \mu \quad \text{with high probability}.$$
and
```math
\mathrm{Var}(\overline{X}_N)
= \mathrm{Var}\!\left(\frac{1}{N}\sum_{i=1}^N X_i\right)
= \frac{1}{N^2}\sum_{i=1}^N \mathrm{Var}(X_i)
= \frac{\sigma^2}{N}.
```
<!-- ``` -->

#### Intuition
- When averaging many independent measurements, random fluctuations “cancel out.”
- The average stabilizes around the true mean.
- The distance from the true mean (the standard deviation) scales as $1/\sqrt{N}$.
- In geophysics: stacking traces reduces noise because signal adds coherently, noise adds incoherently.

 
### Central Limit Theorem (CLT)
Let $X_1,\dots,X_n$ be i.i.d. with mean $\mu$ and variance $\sigma^2$.

#### Statement (informal)
The normalized sum  
```math
Z_n=
\frac{\sum_{i=1}^n X_i - n\mu}{\sigma\sqrt{n}}
```
approaches a standard normal distribution as $n\to\infty$:
```math
Z_n \Rightarrow \mathcal{N}(0,1).
```

#### Intuition
- Many small independent effects aggregate to produce a Gaussian shape.
- Even if the underlying distribution is not Gaussian, the sum behaves Gaussian.
- Explains why normal noise models are widely applicable.

 
## Key Points
- Bernoulli and Geometric model discrete success/failure processes.
- Uniform models complete uncertainty on a bounded interval.
- Exponential models memoryless waiting times.
- Gaussian models aggregated random effects and noise.
- LLN: averages converge to the true mean.
- CLT: sums (properly scaled) converge to a Gaussian regardless of original distribution.
