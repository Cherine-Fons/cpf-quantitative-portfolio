# Week 4 Bridge — Covariance Geometry Exercises

## Review Question 1

**Question.** Explain how a covariance matrix summarizes joint risk in a two-asset setting.

**Answer.**

A covariance matrix summarizes the individual risk of each asset and how the two assets move together.

For two assets,

```math
\Sigma=
\begin{pmatrix}
\sigma_1^2 & \sigma_{12}\\
\sigma_{12} & \sigma_2^2
\end{pmatrix}.
```

The diagonal entries are the variances of the individual assets, while the off-diagonal entries are their covariance. This matters because portfolio risk depends not only on how volatile each asset is, but also on whether they tend to move together or in opposite directions.

For portfolio weights $`w`$,

```math
\sigma_p^2=w^\top\Sigma w.
```

So the covariance matrix contains the information needed to describe the joint risk of the two assets.

## Review Question 2

**Question.** Define correlation and explain how it differs from covariance in interpretation.

**Answer.**

Correlation is covariance scaled by the standard deviations of the two assets:

```math
\rho_{12}
=
\frac{\operatorname{Cov}(R_1,R_2)}
{\sigma_1\sigma_2}.
```

Covariance tells me the direction of co-movement, but its numerical size depends on the units and volatility of the assets. Correlation removes that scale dependence and always lies between $`-1`$ and $`1`$.

A correlation near $`1`$ means the assets move strongly together, a correlation near $`-1`$ means they move strongly in opposite directions, and a correlation near $`0`$ means there is little linear relationship.

So covariance measures co-movement in the original units, while correlation gives a standardized measure of the strength and direction of that co-movement.

## Review Question 3

**Question.** Describe how portfolio variance depends on weights, variances, and covariance.

**Answer.**

For two assets with weights $`w_1`$ and $`w_2`$,

```math
\sigma_p^2
=
w_1^2\sigma_1^2
+
w_2^2\sigma_2^2
+
2w_1w_2\sigma_{12}.
```

The first two terms come from the individual asset variances, while the last term captures how the two assets move together.

For a long-only portfolio with positive weights, positive covariance increases the covariance contribution to portfolio variance, while negative covariance reduces it because the assets' deviations tend to offset one another.

If short positions are allowed, the sign of $`w_1w_2`$ also matters. So covariance by itself does not determine whether the cross-term raises or lowers portfolio variance. The effect comes from

```math
2w_1w_2\sigma_{12}.
```

This is why portfolio risk depends not only on the individual asset risks, but also on both their dependence structure and the way the portfolio is weighted.

## Review Question 4

**Question.** Explain the role of eigenvalues and eigenvectors in the geometry of covariance.

**Answer.**

The eigenvectors of a covariance matrix give the principal directions of variation, and the eigenvalues tell me how much variance exists along those directions.

For

```math
\Sigma u_i=\lambda_i u_i,
```

the vector $`u_i`$ is a principal direction and $`\lambda_i`$ is the variance associated with that direction.

The eigenvector corresponding to the largest eigenvalue identifies the direction in which the payoff or return cloud is most spread out. The smaller eigenvalue corresponds to the narrower direction.

Geometrically, the eigenvectors form the principal axes of the covariance ellipse, and the axis lengths are proportional to

```math
\sqrt{\lambda_i}.
```

## Review Question 5

**Question.** Summarize why the minimum-variance portfolio has a geometric interpretation.

**Answer.**

The minimum-variance portfolio has a geometric interpretation because portfolio variance is a quadratic function of the portfolio weights.

Under the budget constraint

```math
w_1+w_2=1,
```

the feasible portfolios form a line in weight space.

If the covariance matrix $`\Sigma`$ is positive definite, the level sets

```math
w^\top\Sigma w=c
```

form elliptical variance contours centered at the origin. Smaller ellipses correspond to smaller values of portfolio variance.

The minimum-variance portfolio is the point where the budget line first touches the smallest variance ellipse that it can reach. Geometrically, this is a tangency condition between the feasible set and a variance contour.

It is important not to confuse this with simply choosing the eigenvector associated with the smallest eigenvalue of $`\Sigma`$. The minimum-eigenvalue eigenvector solves a different optimization problem, namely minimizing

```math
w^\top\Sigma w
```

subject to a unit-length constraint such as

```math
\|w\|_2=1.
```

The portfolio problem instead imposes the budget constraint

```math
\mathbf 1^\top w=1.
```

So the covariance eigenvectors describe the principal geometry of risk, but the minimum-variance portfolio is determined by how that geometry interacts with the portfolio constraint.

# Exercises

## Exercise 1

**Question.** Given two assets with variances $`\sigma_1^2`$ and $`\sigma_2^2`$ and correlation $`\rho`$, write the covariance matrix and compute the portfolio variance for weights $`w`$ and $`1-w`$.

**Answer.**

For two assets with variances

```math
\sigma_1^2
\qquad\text{and}\qquad
\sigma_2^2
```

and correlation $`\rho`$,

```math
\operatorname{Cov}(R_1,R_2)
=
\rho\sigma_1\sigma_2.
```

Therefore, the covariance matrix is

```math
\Sigma
=
\begin{pmatrix}
\sigma_1^2 & \rho\sigma_1\sigma_2\\
\rho\sigma_1\sigma_2 & \sigma_2^2
\end{pmatrix}.
```

If Asset 1 has weight $`w`$, then Asset 2 has weight

```math
1-w.
```

The portfolio variance is

```math
\sigma_p^2
=
\begin{pmatrix}
w & 1-w
\end{pmatrix}
\Sigma
\begin{pmatrix}
w\\
1-w
\end{pmatrix}.
```

Expanding,

```math
\boxed{
\sigma_p^2
=
w^2\sigma_1^2
+
(1-w)^2\sigma_2^2
+
2w(1-w)\rho\sigma_1\sigma_2
}.
```

The first two terms are the weighted variance contributions of the two assets. The third term is the covariance contribution.

For fixed volatilities and fixed positive portfolio weights, reducing $`\rho`$ reduces

```math
2w(1-w)\rho\sigma_1\sigma_2,
```

so it lowers the covariance contribution to portfolio variance.

Therefore, lower correlation gives a greater diversification benefit, provided the portfolio weights remain positive.

## Exercise 2

**Question.** Choose two return series of length ten and compute their sample covariance and correlation. Compare the sign and magnitude of both measures.

**Answer.**

I will use these ten returns:

```math
R_1=
(0.02,-0.01,0.03,0.01,-0.02,0.04,0,0.02,-0.01,0.03)
```

and

```math
R_2=
(0.01,-0.005,0.02,0,-0.015,0.03,0.005,0.015,-0.01,0.025).
```

The sample means are

```math
\bar R_1=0.011,
\qquad
\bar R_2=0.0075.
```

Sample covariance is

```math
s_{12}
=
\frac{1}{n-1}
\sum_{i=1}^{n}
(R_{1i}-\bar R_1)(R_{2i}-\bar R_2).
```

For these data,

```math
\boxed{s_{12}\approx0.0002972}.
```

The sample variances are approximately

```math
s_1^2=0.000410,
\qquad
s_2^2=0.0002292,
```

so

```math
s_1\approx0.02025,
\qquad
s_2\approx0.01514.
```

The correlation is therefore

```math
r
=
\frac{0.0002972}
{(0.02025)(0.01514)}
\approx0.9696.
```

Thus,

```math
\boxed{r\approx0.970}.
```

Both covariance and correlation are positive, so the assets tend to move in the same direction. The correlation is close to $`1`$, which shows that the linear relationship is very strong.

The covariance itself looks numerically small because the returns are written as decimals. Correlation is easier to interpret because it is standardized.

A Python check would be

    import numpy as np

    r1 = np.array([
        0.02, -0.01, 0.03, 0.01, -0.02,
        0.04, 0.00, 0.02, -0.01, 0.03
    ])

    r2 = np.array([
        0.01, -0.005, 0.02, 0.00, -0.015,
        0.03, 0.005, 0.015, -0.01, 0.025
    ])

    covariance = np.cov(r1, r2, ddof=1)[0, 1]
    correlation = np.corrcoef(r1, r2)[0, 1]

    print(covariance)
    print(correlation)

## Exercise 3

**Question.** For a two-asset portfolio, derive the weight that minimizes variance and state how it changes when correlation increases.

**Answer.**

Let Asset 1 have weight $`w`$ and Asset 2 have weight

```math
1-w.
```

The portfolio variance is

```math
\sigma_p^2(w)
=
w^2\sigma_1^2
+
(1-w)^2\sigma_2^2
+
2w(1-w)\sigma_{12}.
```

Differentiate with respect to $`w`$:

```math
\frac{d\sigma_p^2}{dw}
=
2w\sigma_1^2
-
2(1-w)\sigma_2^2
+
2(1-2w)\sigma_{12}.
```

Set the derivative equal to zero:

```math
2w\sigma_1^2
-
2(1-w)\sigma_2^2
+
2(1-2w)\sigma_{12}
=
0.
```

Dividing by $`2`$,

```math
w\sigma_1^2
-
(1-w)\sigma_2^2
+
(1-2w)\sigma_{12}
=
0.
```

Expanding,

```math
w\sigma_1^2
-\sigma_2^2
+w\sigma_2^2
+\sigma_{12}
-2w\sigma_{12}
=
0.
```

Collecting the terms containing $`w`$,

```math
w\left(
\sigma_1^2+\sigma_2^2-2\sigma_{12}
\right)
=
\sigma_2^2-\sigma_{12}.
```

Therefore,

```math
\boxed{
w^*
=
\frac{\sigma_2^2-\sigma_{12}}
{\sigma_1^2+\sigma_2^2-2\sigma_{12}}
}.
```

Since

```math
\sigma_{12}
=
\rho\sigma_1\sigma_2,
```

we can also write

```math
\boxed{
w^*
=
\frac{
\sigma_2^2-\rho\sigma_1\sigma_2
}{
\sigma_1^2+\sigma_2^2-2\rho\sigma_1\sigma_2
}
}.
```

To determine precisely how the optimal weight changes with correlation, differentiate $`w^*`$ with respect to $`\rho`$:

```math
\boxed{
\frac{\partial w^*}{\partial\rho}
=
\frac{
\sigma_1\sigma_2
\left(
\sigma_2^2-\sigma_1^2
\right)
}{
\left(
\sigma_1^2+\sigma_2^2
-2\rho\sigma_1\sigma_2
\right)^2
}
}.
```

The denominator is squared, so away from degenerate cases it is positive. Therefore, the sign of the derivative is determined by

```math
\sigma_2^2-\sigma_1^2.
```

If

```math
\sigma_1>\sigma_2,
```

then

```math
\frac{\partial w^*}{\partial\rho}<0.
```

So as correlation increases, the optimal weight $`w^*`$ in Asset 1 decreases. The minimum-variance allocation shifts toward Asset 2, which is the lower-volatility asset.

If instead

```math
\sigma_1<\sigma_2,
```

then

```math
\frac{\partial w^*}{\partial\rho}>0,
```

so increasing correlation shifts the allocation toward Asset 1.

The intuition is that when correlation is low, combining the two assets creates diversification benefits even if one asset is more volatile. As correlation rises, that diversification benefit weakens, so the minimum-variance portfolio places relatively more weight on the asset with lower standalone volatility.

This formula gives the **unconstrained** minimum-variance solution. If the portfolio is required to be long-only,

```math
0\le w\le1,
```

then the unconstrained optimum applies only while $`w^*`$ remains inside that interval. If increasing correlation pushes the theoretical optimum outside the interval, the long-only solution stops at the appropriate boundary, either

```math
w=0
```

or

```math
w=1.
```

That last qualification is important because the unconstrained formula can imply short positions even when the actual portfolio problem forbids them.

## Exercise 4

**Question.** Using a covariance matrix with entries you choose, compute the eigenvalues and interpret which direction represents the dominant risk factor.

**Answer.**

I will use

```math
\Sigma
=
\begin{pmatrix}
0.04 & 0.018\\
0.018 & 0.0225
\end{pmatrix}.
```

The eigenvalues satisfy

```math
\det(\Sigma-\lambda I)=0.
```

For a $`2\times2`$ symmetric matrix,

```math
\lambda_{1,2}
=
\frac{
a+d\pm
\sqrt{(a-d)^2+4c^2}
}{2}.
```

Here,

```math
a=0.04,
\qquad
d=0.0225,
\qquad
c=0.018.
```

Thus,

```math
a+d=0.0625
```

and

```math
\sqrt{(0.04-0.0225)^2+4(0.018)^2}
\approx0.040028.
```

Therefore,

```math
\lambda_1
=
\frac{0.0625+0.040028}{2}
\approx0.051264,
```

and

```math
\lambda_2
=
\frac{0.0625-0.040028}{2}
\approx0.011236.
```

So

```math
\boxed{\lambda_1\approx0.0513}
```

and

```math
\boxed{\lambda_2\approx0.0112}.
```

Corresponding normalized eigenvectors are approximately

```math
u_1=
\begin{pmatrix}
0.848\\
0.530
\end{pmatrix},
\qquad
u_2=
\begin{pmatrix}
-0.530\\
0.848
\end{pmatrix}.
```

Because

```math
\lambda_1>\lambda_2,
```

the direction $`u_1`$ is the dominant risk direction.

In geometric terms, most of the variation lies along a direction in which the two assets move together. The perpendicular $`u_2`$ direction has much less variance.

## Exercise 5

**Question.** Sketch the variance ellipse implied by a covariance matrix and label the axes with the eigenvectors and eigenvalues.

**Answer.**

Using the same covariance matrix,

```math
\Sigma
=
\begin{pmatrix}
0.04 & 0.018\\
0.018 & 0.0225
\end{pmatrix},
```

we found

```math
\lambda_1\approx0.051264,
\qquad
\lambda_2\approx0.011236.
```

The corresponding eigenvectors are

```math
u_1\approx
\begin{pmatrix}
0.848\\
0.530
\end{pmatrix},
```

and

```math
u_2\approx
\begin{pmatrix}
-0.530\\
0.848
\end{pmatrix}.
```

For a one-standard-deviation covariance ellipse, the principal semi-axis lengths are

```math
\sqrt{\lambda_1}
\approx0.226,
```

and

```math
\sqrt{\lambda_2}
\approx0.106.
```

So the ellipse would look roughly like this:

                       u2
                      /
                  ____/____
              ___/         \___
          ___/                 \___
    -----/---------- center --------\----- u1
        /                           /
       \___                     ___/
           \___________________/

The long axis lies along $`u_1`$, because $`\lambda_1`$ is the larger eigenvalue.

The narrow axis lies along $`u_2`$, because $`\lambda_2`$ is smaller.

So I would label the ellipse as

```math
u_1
\longleftrightarrow
\lambda_1\approx0.0513
```

for the dominant direction, and

```math
u_2
\longleftrightarrow
\lambda_2\approx0.0112
```

for the narrow direction.

A simple Python plot is

    import numpy as np
    import matplotlib.pyplot as plt

    Sigma = np.array([
        [0.04, 0.018],
        [0.018, 0.0225]
    ])

    eigvals, eigvecs = np.linalg.eigh(Sigma)

    order = np.argsort(eigvals)[::-1]
    eigvals = eigvals[order]
    eigvecs = eigvecs[:, order]

    theta = np.linspace(0, 2 * np.pi, 400)

    circle = np.vstack([
        np.cos(theta),
        np.sin(theta)
    ])

    ellipse = (
        eigvecs
        @ np.diag(np.sqrt(eigvals))
        @ circle
    )

    plt.plot(ellipse[0], ellipse[1])

    for i in range(2):
        axis = np.sqrt(eigvals[i]) * eigvecs[:, i]

        plt.plot(
            [-axis[0], axis[0]],
            [-axis[1], axis[1]],
            label=f"u{i+1}, lambda={eigvals[i]:.4f}"
        )

    plt.axhline(0)
    plt.axvline(0)
    plt.axis("equal")
    plt.legend()
    plt.show()

The main thing I would take from the picture is that the covariance matrix is not just a table of numbers. Its eigenvectors tell me the directions of joint risk, and its eigenvalues tell me how much risk lies along each of those directions.
