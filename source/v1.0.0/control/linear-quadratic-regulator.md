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


