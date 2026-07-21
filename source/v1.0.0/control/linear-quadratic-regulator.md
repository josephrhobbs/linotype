# Linear Quadratic Regulator

~

::byline[Joseph Hobbs][July 21, 2026]

The __linear quadratic regulator__ (LQR) is the quintessential optimal controller.  Assuming linear dynamics and a quadratic cost, LQR provides an _almost_ closed-form solution for the optimal control policy.

There is a deep sense in which LQR is to control what the Kalman Filter is to estimation.  Under linear dynamics, both provide optimal outputs; both are easily extended to nonlinear cases by successive linearization; and both are applied to extraordinary breadth across research and industry.

Before we begin, we will define the _system dynamics_

\[ f(x, u) := A x + B u \]

as well as the _instantaneous cost_ \( \ell \).

\[ \ell(x, u) := x^\mathrm{T} Q x + u^\mathrm{T} R u \]

## Dynamic programming

LQR is elegantly derived from the infinite-horizon __Hamilton-Jacobi-Bellman equation__, a partial differential equation describing the optimal policy \( u^\star \) for a continuous-time system with state \( x \) and optimal cost-to-go \( J^\star \).

\[ u^\star = \arg \min_u \left( \ell(x, u) + \frac{\partial J^\star}{\partial x} f(x, u) \right) \]

As a reminder, the _optimal cost-to-go_ \( J^\star \) is defined as the integral

\[ J^\star(t) := \int_t^\infty \ell(x(t), u^\star(t)) \, dt \]

and the state \( x(t) \) evolves according to

\[ \dot{x}(t) = f\left( x(t), u^\star(t) \right) . \]

It is also useful to know beforehand that \( J^\star \) will take the form \( x^\mathrm{T} S x \), for some matrix \( S \succeq 0 \).  We substitute our expressions for \( \ell \) and \( f \) to obtain

\[ u^\star = \arg \min_u \left( x^\mathrm{T} Q x + u^\mathrm{T} R u + 2 x^\mathrm{T} S ( A x + B u ) \right) . \]

The objective here is quadratic in \( u \).  Because \( Q, R \succeq 0 \), the objective is also convex, and a global minimum can be found easily at first-order.

\[ 2 (u^\star)^\mathrm{T} R + 2 x^\mathrm{T} S B = 0 \Rightarrow u^\star = -R^{-1} B^\mathrm{T} S x \]

Therefore, with a known \( S \) (which we have yet to determine), \( u^\star \) is easily computed for any given \( x \).

## Towards the continuous-time algebraic Riccati equation

Using dynamic programming, we have successfully determined the optimal policy, \( u^\star \).  Unfortunately, it is dependent on an unknown matrix \( S \) (in our optimal cost-to-go expression).  We can determine \( S \) by substituting the expression for \( u^\star \) _back_ into the Hamilton-Jacobi-Bellman equation (HJB).  The minimum value attained by HJB is always zero, and with grouping of like terms, we get

\[ 0 = x^\mathrm{T} Q x + x^\mathrm{T} S B R^{-1} B^\mathrm{T} S x + 2 x^\mathrm{T} S ( A - B R^{-1} B^\mathrm{T} S ) x . \]

This can be written as an expression quadratic in \( x \) like so.

\[ x^\mathrm{T} \left( Q - S B R^{-1} B^\mathrm{T} S + 2 S A \right) x = 0 \]

This expression can only be identically zero when the _symmetric component_ of the matrix expression is zero.  This is because all square matrices can be written as the sum of a symmetric matrix \( A \) and an anti-symmetric matrix \( B \).  The quadratic form

\[ x^\mathrm{T} B x \]

is identically zero for any anti-symmetric matrix \( B \).  Therefore, it is sufficient to take the symmetric component of the above matrix.  The terms

\[ Q - S B R^{-1} B^\mathrm{T} S \]

are symmetric by construction (because \( S \) and \( R \) are symmetric), but \( 2 S A \) may not be symmetric if \( A \) is not symmetric.  Taking the symmetric component of this term,

\[ \frac12 (2 S A + 2 A^\mathrm{T} S) = S A + A^\mathrm{T} S \]

we can write the __continuous-time algebraic Riccati equation__ (CARE).

\[ Q - S B R^{-1} B^\mathrm{T} S + S A + A^\mathrm{T} S = 0 \]

This is typically solved numerically for \( S \); the optimal policy is then easily computed from the expression above.
