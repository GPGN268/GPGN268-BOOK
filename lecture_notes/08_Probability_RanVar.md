# Foundations of Probability & Random Variables
## Learning Objectives
- Understand probability spaces: Define sample spaces, events, and probability measures; apply the three axioms of probability to verify valid probability assignments.
- Understand the definition of a random variable as a deterministic function mapping outcomes to real numbers.
- Work with distribution functions: Compute and interpret cumulative distribution functions (CDFs) and probability density functions (PDFs); classify random variables as discrete, continuous, or mixed.
- Calculate moments: Compute expectation (mean), variance, standard deviation, and higher moments; interpret these as summaries of a distribution's location, spread, and shape.
- Analyze dependence: Calculate covariance and correlation; recognize that zero correlation does not imply independence; apply properties of independent random variables to simplify calculations.
- Apply conditional probability: Compute conditional distributions and expectations.
- Use Bayes' Rule: Interpret prior, likelihood, and posterior; apply Bayes' Rule to update probabilities when new information arrives.

## Motivation
Engineering, physics, and applied mathematics constantly face uncertainty. Probability provides a quantitative language for describing, analyzing, and predicting outcomes in the presence of uncertainty. 

Some physicists believe that the universe itself is fundamentally probabilistic at the quantum level.
Einstein famously protested: "God does not play dice with the universe." But modern physics suggests that, in some situations, nature does roll the dice.
Even if we prepare the same system in the same way, the outcome may vary.
You don’t need to know any quantum mechanics for this course—the point is simply:
Some randomness is believed to be built into the laws of physics.

Other kinds of uncertainty come from systems that are deterministic but too complex to predict exactly.
Example: Rolling a die
A die obeys Newton’s laws.
But tiny changes in position, velocity, friction, or air flow make the outcome unpredictable.
So we treat the result as a random variable.
Geophysics examples:

- Unknown small‑scale Earth heterogeneity
- Irregularities in seismic sources
- Environmental and instrument noise
- Complex Earth processes that amplify tiny variations

Even when the physics is deterministic, we model our lack of knowledge using probability.

In summary, Probability is useful whether nature is truly random or merely too complicated. Either way, we have to “play dice” in our models.

## Probability Spaces and Axioms

This section introduces the mathematical foundation of probability. 

### Sample Space $\Omega$

The **sample space** is the set of all possible outcomes of an experiment.

- Rolling a die:  
  $$\Omega = \{1,2,3,4,5,6\}$$
- Toss two coins:  
  $$\Omega = \{HH, HT, TH, TT\}$$
- Choosing a random day of the week:  
  $$\Omega = \{\text{Mon},\dots,\text{Sun}\}$$

The sample space should include every outcome that could happen, and nothing else.

Also note that $\Omega$ can contain non-numerical values. This is a description of the real world we like to model.

### Events as Subsets of $\Omega$

An **event** is any subset of the sample space.  
Examples (die roll):
$$\Omega = \{1,2,3,4,5,6\}$$

- “Even number”:  
  $$A = \{2,4,6\} \subset \Omega$$
- “Number greater than 4”:  
  $$B = \{5,6\} \subset \Omega$$
- The empty event (impossible):  
  $$\varnothing \subset \Omega$$
- The sure event (always happens):  
  $$\Omega \subset \Omega$$

Operations on events follow set operations:

- Union: $(A \cup B)$  
- Intersection: $(A \cap B)$  
- Complement: $(A^c = \Omega \setminus A)$

In a finite or countable setting, *every* subset is a valid event.

---

### Probability Measure

A **probability measure** $\mathbb{P}$ assigns a number $\mathbb{P}(A)$ to each event $A$, following three axioms (Kolmogorov, simplified).
Note that $\mathbb{P}$ takes a subset of $\Omega$ (an event) as input, not individual elements $\omega \in \Omega$.

- Axiom 1: Non-negativity
$$\mathbb{P}(A) \ge 0 \quad \text{for all events } A.$$

- Axiom 2: Normalization
$$\mathbb{P}(\Omega) = 1.$$

- Axiom 3: Additivity (Simplified)
$$\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) \quad \text{if } A \cap B = \varnothing.$$

#### A Note on the Uncountable Case

So far we have focused on **finite or countable** sample spaces, where probabilities are assigned by listing the probability of each individual outcome. However, many real-world quantities in geophysics (and physics in general) take **real-number values**, so the sample space becomes **uncountable**, typically a subset of $\mathbb{R}$ or $\mathbb{R}^n$.

This requires more structure than in the discrete case. If done without care, one can run into contradiction and paradoxes. We will **not** be dealing with the mathematical complexities in this course. Despite skipping the full measure‑theoretic machinery, everything we do in this course is completely rigorous for the kinds of distributions and integrals used in geophysics and engineering. The advanced theory is only needed for pathological cases we will rarely encounter, so the tools we use remain fully sound and mathematically correct.

## Random Variables
Random variables allow us to translate uncertain outcomes into numerical quantities that we can analyze mathematically. They provide the connection between abstract probability spaces and the real-valued measurements used in geophysics and engineering. Although $\omega$ may be abstract, $X(\omega)$ is a **real number** we can compute with.

### Definition
A **random variable** is a function
$$
X:\Omega \to \mathbb{R},
$$
assigning a real number to each outcome $\omega \in \Omega$.

A **random variable** is often misunderstood because of the word *random*. Mathematically, a random variable is **not itself random**—it is a **deterministic function** from the sample space to the real numbers,
$$
X : \Omega \to \mathbb{R}.
$$
The randomness comes entirely from the underlying experiment, which selects an outcome $\omega$ according to the probability measure $\mathbb{P}$. Once $\omega$ is fixed, the value $X(\omega)$ is completely determined. The role of a random variable is simply to assign numerical values to outcomes. All probability statements about a random variable $X$ (such as $\mathbb{P}(X \le x)$) are really probability statements about the underlying set of outcomes
$$
\{\omega \in \Omega : X(\omega) \le x\}.
$$
Thus, a random variable is simply a function—its “randomness” comes entirely from the randomness of the experiment that selects $\omega$, not from the function $X$ itself.


### Connecting Outcomes to Probabilities
Once we have a random variable $X$, statements about real numbers like "$X \le x$" or "$X \in [a,b]$" correspond to **events** in the original probability space:
$$
\mathbb{P}(X \in B) \;\;=\;\; \mathbb{P}\big(\{\omega \in \Omega:\; X(\omega) \in B\}\big)
$$

The probability of these events is inherited from $\mathbb{P}$ on $\Omega$. This is how we build a **distribution** for $X$—the assignment of probability to intervals and sets of real numbers. The formal description of this distribution is the subject of the next section.

## Distribution Functions

The distribution of a random variable describes how probability is assigned to different real values. We formalize this through the **cumulative distribution function (CDF)** and, when it exists, the **probability density function (PDF)**.

### Cumulative Distribution Function (CDF)

For any random variable $X$, the **cumulative distribution function (CDF)** is defined by
$$
F_X(x) = \mathbb{P}(X \le x).
$$

**Universal Properties:**
- $F_X$ is non‑decreasing: if $x_1 < x_2$, then $F_X(x_1) \le F_X(x_2)$.
- Limits: $\lim_{x\to -\infty} F_X(x) = 0$ and $\lim_{x\to +\infty} F_X(x) = 1$.
- Right‑continuity: $F_X(x) = \lim_{\delta \to 0^+} F_X(x+\delta)$.

**Every random variable** — discrete, continuous, or mixed — has a CDF. The CDF fully determines the probability distribution.

### Probability Density Function (PDF)

If the CDF of $X$ is **differentiable**, $X$ can be described by a **probability density function** (PDF) $f_X(x)$ satisfying
$$
F_X(x) = \int_{-\infty}^{x} f_X(t)\, \mathrm{d}t
$$
and 
$$
f_X(x) = \frac{\mathrm{d}}{\mathrm{d}x} F_X(x).
$$

**Computing Probabilities from PDF:**
- Interval probabilities: $\mathbb{P}(a \le X \le b) = \int_a^b f_X(x)\, \mathrm{d}x = F_X(b) - F_X(a)$.
- Individual points: $\mathbb{P}(X = x) = 0$ for all $x$ (continuous distributions have no point masses).

### Discrete, Continuous, and Mixed Random Variables

We classify $X$ by how its probability is distributed over $\mathbb{R}$, as revealed by its CDF.

#### Discrete
$X$ is **discrete** if it places probability on a **finite or countable** set $\{x_1,x_2,\dots\}$:
$$
\mathbb{P}(X \in B) \;=\; \sum_{x_i \in B} \mathbb{P}(X = x_i).
$$
The CDF is a **step function** with jumps at the atoms $\{x_i\}$, where each jump has size
$$
\mathbb{P}(X = x_i) \;=\; F_X(x_i) - \lim_{x \uparrow x_i} F_X(x).
$$

#### Continuous
$X$ is **continuous** if its CDF is differentiable and has a probability density function $f_X(x)$ such that
$$
F_X(x) = \int_{-\infty}^{x} f_X(t)\, dt.
$$
For such a distribution, all **individual points** have zero probability:
$$
\mathbb{P}(X = x) = 0 \quad \text{for all } x \in \mathbb{R}.
$$

#### Mixed
$X$ is **mixed** if it has both **discrete** (jump) and **continuous** parts. The CDF has the form
$$
F_X(x)
\;=\;
\sum_{i} \mathbb{P}(X = x_i)\,\mathbf{1}_{\{x_i \le x\}}
\;+\;
\int_{-\infty}^{x} f_X(t)\, dt,
$$
where:
- **Jumps** represent discrete masses (point probabilities).
- The **integral** represents the continuous part (with density $f_X$).

**Example:** Travel time in seismology may be continuous when a wave arrives, but with some probability the wave **fails** to arrive, contributing a discrete mass at $+\infty$ (or equivalently, a point mass for "no arrival").


## Moments

Moments summarize key numerical properties of a random variable. They describe averages, variability, and dependence, and are central to modeling uncertainty in geophysics and engineering.

### Expectation

The **expectation** (or mean) of a random variable $X$, written $\mathbb{E}[X]$, is the “average value” of $X$ under repeated sampling.

For any random variable,
$$
\mathbb{E}[X] = \int_{-\infty}^{\infty} x \, \mathrm{d}F_X(x),
$$
where $F_X$ is the CDF of $X$.

$\mathrm{d}F_X$ is interpreted as a Riemann–Stieltjes integral. It automatically covers **discrete**, **continuous**, and **mixed** cases. We will expand in these cases below.

#### Discrete case
If $X$ takes values $\{x_i\}_{i\in I}$ (finite or countable) with point probabilities $p_i = \mathbb{P}(X = x_i)$, then
$$
\mathbb{E}[X] \;=\; \sum_{i\in I} x_i \, p_i.
$$

#### Continuous case (with a PDF)
If $X$ has a **probability density function** $f_X$
then
$$
\mathbb{E}[X] \;=\; \int_{-\infty}^{\infty} x\, f_X(x)\, \mathrm{d}x.
$$

#### Mixed case
If $X$ has atoms at $\{x_i\}$ with masses $p_i = \mathbb{P}(X=x_i)$ **and** a continuous part with density $f_X$, then
$$
\mathbb{E}[X]
\;=\;
\sum_i x_i\, p_i \;+\; \int_{-\infty}^{\infty} x\, f_X(x)\, \mathrm{d}x.
$$

### Expectation is linear
That is:
$$
\mathbb{E}[aX + bY] = a\,\mathbb{E}[X] + b\,\mathbb{E}[Y].
$$

### Second Moment

One can easily generalize the expectation to define the **second moment** of $X$
$$
\mathbb{E}[X^2].
$$

For discrete $X$:
$$
\mathbb{E}[X^2] = \sum_i x_i^2 \, p_i.
$$

For continuous $X$ with PDF $f_X$:
$$
\mathbb{E}[X^2] = \int_{-\infty}^{\infty} x^2 \, f_X(x)\, \mathrm{d}x.
$$

The second moment captures the "typical squared magnitude" of $X$. It plays a central role in defining variance.


#### Variance and Standard Deviation

The **variance** measures spread around the mean. It is the **second central moment** (i.e., the second moment about the mean):
$$
\mathrm{Var}(X)
= \mathbb{E}\!\left[(X - \mathbb{E}[X])^2\right].
$$

By expanding the square and using linearity of expectation, we obtain a **useful computational formula** in terms of the first and second moments:
$$
\mathrm{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2.
$$

**Interpretation:** Variance quantifies how "spread out" the values of $X$ are around the mean. A small variance means values cluster tightly; a large variance means wider dispersion.

The **standard deviation** is the square root:
$$
\sigma_X = \sqrt{\mathrm{Var}(X)}.
$$

Standard deviation has the same units as $X$, making it easier to interpret physically (e.g., "typical deviation from the mean").

#### Scaling Properties of Variance and Standard Deviation

An important and frequently used property is how variance and standard deviation scale when a random variable is multiplied by a constant.

For any constant $c$ and random variable $X$:
$$
\mathrm{Var}(cX) = c^2 \, \mathrm{Var}(X),
$$
$$
\sigma_{cX} = |c| \, \sigma_X.
$$

**Example:** If a measurement has standard deviation $\sigma = 5$ meters, and you measure the same quantity in centimeters (multiplying by $c = 100$), the new standard deviation is $100 \times 5 = 500$ centimeters, and the variance becomes $100^2 \times \mathrm{Var}(X) = 10000 \times \mathrm{Var}(X)$.

### Higher Moments

More generally, the **$k$‑th moment** of $X$ is
$$
\mathbb{E}[X^k].
$$

The **$k$‑th central moment** (moment about the mean) is
$$
\mathbb{E}\!\left[(X - \mathbb{E}[X])^k\right].
$$

Examples:
- $k=1$: First moment = mean ($\mathbb{E}[X]$)
- $k=2$: Second central moment = variance ($\mathrm{Var}(X)$)
- $k=3$: Third central moment relates to skewness (asymmetry)
- $k=4$: Fourth central moment relates to kurtosis (tailedness)

Higher moments quantify shape features of the distribution beyond location and spread.

### Covariance and Correlation

For random variables $X$ and $Y$ with finite second moments, the **covariance** is
$$
\mathrm{Cov}(X, Y)
= \mathbb{E}\!\left[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])\right].
$$

Equivalent form:
$$
\mathrm{Cov}(X,Y)
= \mathbb{E}[XY] - \mathbb{E}[X]\,\mathbb{E}[Y].
$$

Covariance measures whether $X$ and $Y$ tend to increase together (positive), move oppositely (negative), or behave independently (zero for many but not all cases).

The **correlation coefficient** is the normalized covariance:
$$
\rho_{X,Y}
= \frac{\mathrm{Cov}(X,Y)}{\sigma_X \sigma_Y},
$$
where $\sigma_X$ and $\sigma_Y$ are the standard deviations.

Correlation satisfies:
- $-1 \le \rho_{X,Y} \le 1$
- $\rho_{X,Y} = 1$: perfect linear relationship  
- $\rho_{X,Y} = 0$: uncorrelated (not necessarily independent)




## Random Variables in Multiple Dimensions

Many problems in geophysics and applied mathematics involve **multiple** uncertain quantities at once. For example:
- The horizontal and vertical components of velocity vector.
- Velocity and density in an Earth model.
- Travel time and amplitude of an arrival.

To model such situations, we introduce **random vectors** and their **joint distributions**.

### Random Vectors

A **random vector** is a function
$$
(X_1, X_2, \dots, X_n): \Omega \to \mathbb{R}^n.
$$

Just as a single random variable is a deterministic function of $\,\omega \in \Omega\,$, a random vector assigns an $n$–tuple of real numbers to each outcome. All randomness still comes from the selection of $\omega$.

We will focus mainly on the two‑dimensional case $(X,Y)$, but all definitions extend naturally to higher dimensions.

---

## Joint Distributions

### Joint Cumulative Distribution Function (Joint CDF)

For two random variables $(X, Y)$, the **joint CDF** is
$$
F_{X,Y}(x,y)
= \mathbb{P}(X \le x,\; Y \le y).
$$

This fully characterizes the joint distribution of $(X,Y)$.

Properties:
- Non‑decreasing in each argument.
- $\lim_{x,y \to -\infty} F_{X,Y}(x,y) = 0$.
- $\lim_{x,y \to +\infty} F_{X,Y}(x,y) = 1$.
- Right‑continuous in each variable.

---

### Joint Probability Density Function (Joint PDF)

If the joint CDF is differentiable, we can define the **joint PDF**
$$
f_{X,Y}(x,y)
= \frac{\partial^2}{\partial x\, \partial y} F_{X,Y}(x,y).
$$

The joint PDF satisfies:
$$
\mathbb{P}\big((X,Y) \in A\big)
= \iint_A f_{X,Y}(x,y)\, \mathrm{d}x\, \mathrm{d}y
\quad \text{for any region } A \subset \mathbb{R}^2,
$$

and the normalization condition:
$$
\iint_{\mathbb{R}^2} f_{X,Y}(x,y)\, \mathrm{d}x\, \mathrm{d}y = 1.
$$

---

## Marginal Distributions

The individual (1D) distributions of $X$ and $Y$ are obtained by **integrating out** the other variable from the joint PDF.

### Marginal PDFs

If $(X,Y)$ has joint PDF $f_{X,Y}$, then:

- **Marginal PDF of $X$:**
  $$
  f_X(x) 
  = \int_{-\infty}^{+\infty} f_{X,Y}(x,y)\, \mathrm{d}y.
  $$

- **Marginal PDF of $Y$:**
  $$
  f_Y(y)
  = \int_{-\infty}^{+\infty} f_{X,Y}(x,y)\, \mathrm{d}x.
  $$

Interpretation:
> The joint PDF describes the full 2D distribution, while a marginal PDF gives the distribution of one variable considered on its own.

---

## Independence

### Definition via Joint CDF

Random variables $X$ and $Y$ are **independent** if and only if
$$
F_{X,Y}(x,y)
= F_X(x)\, F_Y(y)
\quad \text{for all } x,y.
$$

### Equivalent Definition via Joint PDF

If densities exist, independence is equivalent to:
$$
f_{X,Y}(x,y)
= f_X(x)\, f_Y(y).
$$

Independence means: *knowing one variable tells you nothing about the other*.

### Important Example of Dependence Without Correlation

It is possible for $X$ and $Y$ to be dependent even if $\mathrm{Cov}(X,Y)=0$.
Thus:
> Zero covariance does **not** imply independence.

---

### Consequences of Independence

Independence dramatically simplifies many computations.

#### Expectation of Sums

Using linearity of expectation:
$$
\mathbb{E}[X+Y]
= \mathbb{E}[X] + \mathbb{E}[Y]
\quad \text{(always true, no independence needed).}
$$

#### Expectation of Products (requires independence)

If $X$ and $Y$ are independent:
$$
\mathbb{E}[XY]
= \mathbb{E}[X]\, \mathbb{E}[Y].
$$

This is *not* generally true without independence.

#### Variance of sum of random variables (requires independence)

If random variables $X_1, X_2, \dots, X_n$ are **independent**, then the variance of their sum is the sum of their variances:
$$
\mathrm{Var}\!\left(\sum_{i=1}^n X_i\right)
= \sum_{i=1}^n \mathrm{Var}(X_i).
$$

This is *not* generally true without independence.

---

## Conditional Probability

Conditional probability allows us to update or refine probability assessments when new information becomes available. It is fundamental in statistics, inversion theory, and Bayesian inference used throughout geophysics.

### Conditional Probability of Events

For events $A$ and $B$ with $\mathbb{P}(B) > 0$, the **conditional probability** of $A$ given $B$ is
$$
\mathbb{P}(A \mid B)
= \frac{\mathbb{P}(A \cap B)}{\mathbb{P}(B)}.
$$

Interpretation: We restrict our sample space to $B$ (the information we now know has occurred), then renormalize the probability of $A$ within this reduced space.

Equivalently,
$$
\mathbb{P}(A \cap B) = \mathbb{P}(A \mid B)\,\mathbb{P}(B).
$$

This identity is often used as the starting point for defining conditional densities.

---

### Conditional PDFs

Let $(X,Y)$ be jointly continuous with joint PDF $f_{X,Y}(x,y)$ and marginal PDF $f_Y(y) > 0$.  
The **conditional PDF** of $X$ given $Y=y$ is defined by
$$
f_{X \mid Y}(x \mid y)
= \frac{f_{X,Y}(x,y)}{f_Y(y)}.
$$

This parallels the discrete formula  
$\mathbb{P}(A \mid B) = \mathbb{P}(A \cap B)/\mathbb{P}(B)$  
but in density form.

It has the properties
1. Normalization
   $$
   \int_{-\infty}^{+\infty} f_{X \mid Y}(x \mid y)\, \mathrm{d}x = 1.
   $$

2. Relation to joint and marginal PDFs
   $$
   f_{X,Y}(x,y)
   = f_{X \mid Y}(x \mid y)\, f_Y(y)
   = f_{Y \mid X}(y \mid x)\, f_X(x).
   $$

3. Independence
   If $X$ and $Y$ are independent, then
   $$
   f_{X \mid Y}(x \mid y) = f_X(x),
   $$
   so conditioning on $Y$ has no effect on the PDF of $X$.

---

### Conditional Expectation

The **conditional expectation** of $X$ given $Y=y$ is the expectation taken with respect to the conditional PDF:
$$
\mathbb{E}[X \mid Y=y]
= \int_{-\infty}^{+\infty} x\, f_{X \mid Y}(x \mid y)\, \mathrm{d}x.
$$

This defines a **function of the variable $y$**.  
In many statistical applications (including inversion and filtering), this function acts as the “best predictor” of $X$ given knowledge of $Y$.

We note the key identities

- Law of total expectation
  $$
  \mathbb{E}[X]
  = \mathbb{E}\big[\mathbb{E}[X \mid Y]\big].
  $$

- Independence
  If $X$ and $Y$ are independent,
  $$
  \mathbb{E}[X \mid Y] = \mathbb{E}[X]
  $$
  (conditioning on $Y$ provides no information about $X$).

---

## Bayes' Rule

Conditional probability allows us to update beliefs when new information becomes available.  
**Bayes' Rule** formalizes how to reverse the conditioning: it expresses $\mathbb{P}(A \mid B)$ in terms of $\mathbb{P}(B \mid A)$.

### Bayes' Rule

For events $A$ and $B$ with $\mathbb{P}(B) > 0$,
$$
\mathbb{P}(A \mid B)
= \frac{\mathbb{P}(B \mid A)\,\mathbb{P}(A)}{\mathbb{P}(B)}.
$$

This follows directly from the definition:
$$
\mathbb{P}(A \cap B)
= \mathbb{P}(A \mid B)\mathbb{P}(B)
= \mathbb{P}(B \mid A)\mathbb{P}(A).
$$

---

### Likelihood, Prior, and Posterior

Bayes' Rule is often interpreted in terms of three components:

- **Prior**  
  $\mathbb{P}(A)$  
  Your initial belief about event \(A\) before seeing new evidence.

- **Likelihood**  
  $\mathbb{P}(B \mid A)$  
  How probable the evidence \(B\) is if \(A\) were true.

- **Posterior**  
  $\mathbb{P}(A \mid B)$  
  Your updated belief about \(A\) after observing \(B\).

Bayes' Rule becomes:
$$
\text{Posterior}
= \frac{\text{Likelihood} \times \text{Prior}}{\text{Evidence}}.
$$

The denominator
$$
\mathbb{P}(B) 
= \mathbb{P}(B\mid A)\mathbb{P}(A)
 + \mathbb{P}(B\mid A^c)\mathbb{P}(A^c)
$$
acts as a normalization constant.

---

### Example: Medical Testing and Base Rates

Medical tests illustrate Bayes’ Rule clearly—especially how **rare events** can dramatically affect posterior probabilities.

Suppose:
-  **Prior**: the prevalence of this disease in the general population (1% of people have it)
  $$
  \mathbb{P}(D) = 0.01
  $$  
  
- **Likelihood**: test sensitivity (probability of a positive result if the patient has the disease):  
  $$
  \mathbb{P}(+\mid D) = 0.95
  $$

- Test false positive rate (probability of positive if patient does NOT have the disease):  
  $$
  \mathbb{P}(+\mid D^c) = 0.05
  $$

**Posterior**: We want the probability the patient actually has the disease given a positive test:
$$
\mathbb{P}(D \mid +)
= \frac{\mathbb{P}(+\mid D)\mathbb{P}(D)}
       {\mathbb{P}(+\mid D)\mathbb{P}(D)
        + \mathbb{P}(+\mid D^c)\mathbb{P}(D^c)}.
$$

Plug in the numbers:

- Prior: $\mathbb{P}(D) = 0.01$
- Complement: $\mathbb{P}(D^c) = 0.99$
- Likelihoods: $0.95$ and $0.05$

Compute:
$$
\mathbb{P}(D \mid +)
= \frac{0.95 \cdot 0.01}
       {0.95 \cdot 0.01 + 0.05 \cdot 0.99}= \frac{0.0095}{0.059}
\approx 0.161.
$$

#### Interpretation

Even though the test is quite accurate, a **positive** result gives only a **16% chance** of actually having the disease.  
This is because the disease is **rare**, and most positives come from false positives among the 99% of healthy patients.

This phenomenon—counterintuitive but ubiquitous—is the **base-rate effect**.

---

## Key Points

Foundations
- Probability is a quantitative framework for reasoning about uncertainty—whether from fundamental randomness, measurement noise, or complexity too large to predict.
- A sample space $\Omega$ contains all possible outcomes of an experiment; events are subsets of $\Omega$; a probability measure $\mathbb{P}$ assigns probabilities to events following three axioms (non-negativity, normalization, additivity).

Random Variables and Distributions
- A random variable is a deterministic function $X: \Omega \to \mathbb{R}$ mapping outcomes to real numbers. All randomness comes from selecting $\omega$, not from $X$ itself.
- The cumulative distribution function (CDF) $F_X(x) = \mathbb{P}(X \le x)$ fully determines a distribution; every random variable has one.
- If the CDF is differentiable, the probability density function (PDF) $f_X(x) = \mathrm{d}F_X/\mathrm{d}x$ describes how probability is distributed over $\mathbb{R}$.
- Discrete random variables concentrate probability on a countable set; continuous ones have a PDF; mixed variables have both.

Moments and Dependence
- Expectation $\mathbb{E}[X]$ is the mean; variance $\mathrm{Var}(X) = \mathbb{E}[(X-\mathbb{E}[X])^2]$ measures spread; standard deviation $\sigma = \sqrt{\mathrm{Var}(X)}$ has the same units as $X$.
- Covariance measures whether two variables increase/decrease together; correlation normalizes covariance to $[-1,1]$—but zero correlation does not imply independence.
- Independence means $F_{X,Y}(x,y) = F_X(x)F_Y(y)$ or equivalently $f_{X,Y}(x,y) = f_X(x)f_Y(y)$. Independence allows product rules: $\mathbb{E}[XY] = \mathbb{E}[X]\mathbb{E}[Y]$ and $\mathrm{Var}(\sum X_i) = \sum \mathrm{Var}(X_i)$.

Conditioning and Bayes' Rule
- Conditional probability and conditional distributions represent updated beliefs when information becomes available.
- Bayes' Rule $\mathbb{P}(A|B) = \mathbb{P}(B|A)\mathbb{P}(A)/\mathbb{P}(B)$ reverses conditioning: prior (initial belief) $\times$ likelihood (data under hypothesis) $\div$ evidence (marginal probability of data) $=$ posterior (updated belief).
- Base-rate effect: Even accurate tests produce misleading posteriors if the prior probability is very low, because false positives among the large population of unaffected individuals outnumber true positives.
