# Linear Quadratic Regulator

~

::byline[Joseph Hobbs][July 21, 2026]

The _linear quadratic regulator_ (LQR) is the quintessential optimal controller.  Assuming linear dynamics and a quadratic cost, LQR provides an _almost_ closed-form solution for the optimal control policy.

There is a deep sense in which LQR is to control what the Kalman Filter is to estimation.  Under linear dynamics, both provide optimal outputs; both are easily extended to nonlinear cases by successive linearization; and both are applied to extraordinary breadth across research and industry.

Before we begin, we will define the _system dynamics_

\[ f(x, u) := A x + B u \]

as well as the _instantaneous cost_ \( \ell \).

\[ \ell(x, u) := x^\mathrm{T} Q x + u^\mathrm{T} R u \]

## Dynamic programming

LQR is elegantly derived from the infinite-horizon _Hamilton-Jacobi-Bellman equation_, a partial differential equation describing the optimal policy \( u^\star \) for a continuous-time system with state \( x \) and optimal cost-to-go \( J^\star \).

\[ u^\star = \arg \min_u \left( \ell(x, u) + \frac{\partial J^\star}{\partial x} f(x, u) \right) \]

As a reminder, the _optimal cost-to-go_ \( J^\star \) is defined as the integral

\[ J^\star(t) := \int_t^\infty \ell(x(t), u^\star(t)) \, dt \]

and the state \( x(t) \) evolves according to

\[ \dot{x}(t) = f\left( x(t), u^\star(t) \right) . \]

It is also useful to know beforehand that \( J^\star \) will take the form \( x^\mathrm{T} S x \), for some matrix \( S \succeq 0 \).  We substitute our expressions for \( \ell \) and \( f \) to obtain

\[ u^\star = \arg \min_u \left( x^\mathrm{T} Q x + u^\mathrm{T} R u + 2 x^\mathrm{T} S ( A x + B u ) \right) . \]

The objective here is quadratic in \( u \).  Because \( Q, R \succeq 0 \), the objective is also convex, and a global minimum can be found easily at first-order.

\[ 2 (u^\star)^\mathrm{T} R + 2 x^\mathrm{T} S B = 0 \Rightarrow u^\star = -R^\mathrm{-1} B^\mathrm{T} S x \]

Therefore, with a known \( S \) (which we have yet to determine), \( u^\star \) is easily computed for any given \( x \).

## Towards the continuous-time algebraic Riccati equation

Using dynamic programming, we have successfully determined the optimal policy, \( u^\star \).  Unfortunately, it is dependent on an unknown matrix \( S \) (in our optimal cost-to-go expression).  We can determine \( S \) by substituting the expression for \( u^\star \) _back_ into the Hamilton-Jacobi-Bellman equation (HJB).  The minimum value attained by HJB is always zero.

\[ 0 = \min_u \left( x^\mathrm{T} Q x + x^\mathrm{T} S^\mathrm{T} B R^\mathrm{-1} R R^\mathrm{-1} B^\mathrm{T} S x + 2 x^\mathrm{T} S ( A x - B R^\mathrm{-1} B^\mathrm{T} S x ) \right) \]
