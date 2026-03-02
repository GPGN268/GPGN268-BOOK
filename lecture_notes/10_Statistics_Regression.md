# Statistics & Linear Regression
## Learning Objectives: 
- 

## 



## Key Points
- 



Lecture 3 — Statistics & Linear Regression


Statistical Estimation

Samples X1,…,XnX_1,\ldots,X_nX1​,…,Xn​
Empirical mean/variance
Law of Large Numbers (engineering intuition, no proof)
CLT



Covariance & Correlation Matrices

Vector-valued data
Interpretation for engineering signals


histogram and PDF



Linear Regression (basic but rigorous)

Model: y=a+bx+εy = a + bx + \varepsilony=a+bx+ε
Least-squares derivation:
b^=∑(xi−xˉ)(yi−yˉ)∑(xi−xˉ)2,a^=yˉ−b^ xˉ\hat{b} = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}, 
\qquad 
\hat{a} = \bar{y} - \hat{b}\,\bar{x}b^=∑(xi​−xˉ)2∑(xi​−xˉ)(yi​−yˉ​)​,a^=yˉ​−b^xˉ

Interpretation in terms of covariance:
b^=Cov⁡(X,Y)Var⁡(X)\hat{b} = \frac{\operatorname{Cov}(X,Y)}{\operatorname{Var}(X)}b^=Var(X)Cov(X,Y)​

(Optional: multivariate linear regression in matrix form)



Connection to Probability

Regression viewed as conditional expectation
Gaussian noise model → maximum likelihood = least squares