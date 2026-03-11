# Common Random Variables & Limit Theorems

## Learning Objectives
- Understand the definitions and basic properties of the most common random variables used in probability, statistics, and geophysics.
- Work with CDFs/PDFs and expectations for:
  - Bernoulli
  - Binomial
  - Geometric
  - Uniform
  - Exponential
  - Gaussian (Normal)
- Connect these distributions to modeling choices in geophysical problems.


## Motivation
Many models in geophysics involve simple stochastic components:
- Sensor failures → Bernoulli
- Number of detections in repeated trials → Binomial
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

### Binomial Random Variable
The binomial distribution counts the number of successes in a fixed number of independent Bernoulli trials.

#### Definition
Let  
```math
X \sim \text{Binomial}(n,p), \quad n \in \mathbb{N}, \; p \in [0,1].
```
Then for $k=0,1,\dots,n$,
```math
\mathbb{P}(X=k) = \binom{n}{k} p^k (1-p)^{n-k}.
```

#### Expectation and Variance
```math
\mathbb{E}[X] = np, \qquad
\mathrm{Var}(X) = np(1-p).
```

#### Interpretation
- Models the count of successes in a fixed number of repeated trials.
- Example: number of stations that successfully detect an event out of $n$ stations, assuming each station detects independently with probability $p$.
- Can be viewed as the sum of $n$ independent Bernoulli random variables.



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

 
## Key Points
- Bernoulli models a single success/failure outcome.
- Binomial models the number of successes in a fixed number of trials.
- Geometric models waiting time until the first success.
- Uniform models complete uncertainty on a bounded interval.
- Exponential models memoryless waiting times.
- Gaussian models aggregated random effects and noise.

