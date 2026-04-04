# Primal-Dual Interior Point Method

~

::byline[Joseph R. Hobbs][April 3, 2026]

The [Karush-Kuhn-Tucker conditions](karush-kuhn-tucker) (KKT conditions) for global optimality are

\[ \begin{align*} \nabla f(x^\star) + \sum_i \lambda_i^\star \nabla g_i(x^\star) + \sum_j \nu_j^\star \nabla h_j(x^\star) &= 0, \\ g_i(x^\star) &\le 0, \\ h_j(x^\star) &= 0, \\ \lambda_i^\star &\ge 0, \\ \lambda_i^\star g_i(x^\star) &= 0. \end{align*} \]

These suggest a very natural approach to solving a complex, potentially nonlinear, potentially nonconvex optimization.  Instead of solving the _primal_ (original) problem, or the _dual_ (Lagrangian) problem, what if we solve both at once?

A very powerful tool in optimization for solving constrained second-order problems is __Newton's method__.  Newton's method is an iterative method for finding a local optimizer by sucessively computing second-order approximations of the objective function.  However, Newton's method only works with _equality_ constraints, not _inequality_ constraints.  Furthermore, the final constraint ("complementary slackness") is rather difficult to handle in practice, as it can induce numerical instability in KKT solvers.  We will need to develop clever workarounds for these two challenges before we can apply Newton's method.

## Slack variables

There is an extremely simple way to convert an inequality into an equality.  Simply introduce a __slack variable__ \( s_i \) for every inequality.  Then, require

\[ g_i(x) + s_i = 0, \]

and also constrain the slack variable to be nonnegative, ensuring that \( g_i(x) \le 0 \).

\[ s_i \ge 0 \]

If we replace every inequality in our original program with an equality, notice that the gradient of the Lagrangian doesn't change, because \( s_i \) is not a function of \( x \) and is therefore eliminated by the differentiation.  However, we _do_ need to update the KKT conditions to include our new feasibility constraints.

\[ \begin{align*} \nabla f(x^\star) + \sum_i \lambda_i^\star \nabla g_i(x^\star) + \sum_j \nu_j^\star \nabla h_j(x^\star) &= 0, \\ g_i(x^\star) + s_i^\star &= 0, \\ h_j(x^\star) &= 0, \\ s_i^\star &\ge 0, \\ \lambda_i^\star &\ge 0, \\ \lambda_i^\star g_i(x^\star) &= 0. \end{align*} \]

Notice how we have added replaced the inequality constraint on \( g_i(x) \) with an equality constraint and a much simpler \( s_i \ge 0 \) constraint.  Now, all we need is a way to relax the complementary slackness constraint (\( \lambda_i g_i = 0 \)) to allow for numerical stability during solving.

## Central path

The complementary slackness constraint (\( \lambda_i g_i = 0 \)) can often lead to numerical instability in Newton's method.  This is easily relaxed by replacing \( 0 \) with \( \mu \), a small positive constant.  This constant, called the __barrier coefficient__, represents the strength of "action at a distance" that the inequality constraints are allowed.  As a candidate solution approaches the inequality "barrier", the inequality barrier can "push" back on the solution.  As \( \mu \rightarrow 0 \), the barrier is allowed less and less "action at a distance" until it allows the candidate to rest right up against it.

We call the series of candidate solutions, parameterized by \( \mu \rightarrow 0 \), the __central path__ of the optimization program.  PDIPM solvers are guided by the central path, reducing \( \mu \) until the candidate solution may lie anywhere in the feasible set, including _right at the boundary_ if it wishes.

## One Newton step

We are now finally ready to apply Newton's method to the KKT conditions.  Newton's method, as aforementioned, solves an optimization by computing second-order approximations.  These second-order approximations can be computed using _symbolic differentiation_ or _automatic differentiation_.  The use of _numerical differentiation_ (via the method of secants) is not recommended for Newton's method, as functions with high local curvature will not differentiate correctly.  We will assume that local first and second derivatives are available to use, perhaps by an automatic differentiation engine.

We begin by assuming that the optimal solution \( (x^\star, \lambda^\star, \nu^\star) \) is separated from our initial point \( (x, \lambda, \nu ) \) by some \( ( \Delta x, \Delta \lambda, \Delta \nu) \).  We can then solve for these values and update our guess.  We can then reduce \( \mu \) and repeat the process until we achieve all four KKT conditions within machine precision.  At this point, we declare \( (x, \lambda, \nu) \) a local optimizer!  And if we know that the KKT conditions are _sufficient_ as well as _necessary_ for our problem, then we have a global optimizer!

## Stationarity

We first take second-order approximations for the _stationarity_ condition (gradient of the Lagrangian vanishes).

\[ \begin{multline*} \nabla f(x) + \nabla^2 f(x) \Delta x + \sum_i \lambda_i \nabla g_i(x) + \sum_i \lambda_i \nabla^2 g_i(x) \Delta x + \sum_i \Delta \lambda_i \nabla g_i(x) \\ + \sum_j \nu_j \nabla h_j(x) + \sum_j \nu_j \nabla^2 h_j(x) \Delta x + \sum_j \Delta \nu_j \nabla h_j(x) &= 0 \end{multline*} \tag{1} \]

Notice that we have dropped terms including the products of two updates.  At the sacrifice of some accuracy, this allows us to solve a linear system for \( ( \Delta x, \Delta \lambda, \Delta \nu) \).

_TODO_

## References

