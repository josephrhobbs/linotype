# Karush-Kuhn-Tucker Conditions

~

::byline[Joseph R. Hobbs][April 3, 2026]

In general, a possibly nonlinear, possibly nonconvex optimization program has the form

\[ \begin{align*} \min_x & f(x) , \\ \text{subject to } & g_i(x) \le 0 , \\ & h_j(x) = 0 . \end{align*} \tag{1} \]

where \( f : \mathbb{R}^n \rightarrow \mathbb{R} \) is a scalar _objective function_ and \( g_i, h_j : \mathbb{R}^n \rightarrow \mathbb{R} \) are scalar _constraint functions_.  Assuming all functions are differentiable (formally, in \( C^1 \), meaning their gradients are continuous), the __Karush-Kuhn-Tucker__ (KKT) conditions serve as necessary conditions for the global optimality of a candidate solution \( x^\star \).

## Motivation: Lagrangian Duality

Every optimization program has a corresponding _dual program_.  The dual formulation is constructed using the _Lagrangian_.  Formally, we introduce the __Lagrange multipliers__ \( \lambda_i, \nu_j \) as real numbers, and we write the Lagrangian function as follows.

\[ L(x, \lambda, \nu) = f(x) + \sum_i \lambda_i g_i(x) + \sum_j \nu_j h_j(x) \tag{2} \]

Using the Lagrangian, we can reformulate our original _constrained_ optimization problem as an _unconstrained_ problem like so.

\[ \min_x \max_{\lambda \ge 0, \nu} L(x, \lambda, \nu) \tag{3} \]

Why does this work?  For a fixed \( x \), consider the values of \( g_i(x) \) and \( h_j(x) \).  If \( h_j(x) \neq 0 \), then the Lagrangian can be driven to infinity by the selection of an arbitrarily large corresponding Lagrange multiplier (\( \nu_j \rightarrow \infty \))... but if \( h_j(x) = 0 \), then the Lagrangian remains bounded from above in terms of \( \nu_j \).  Similarly, if \( g_i(x) > 0 \), then the Lagrangian can be driven to infinity by \( \lambda_i \rightarrow \infty \).  Notice, however, that we have constrained \( \lambda_i \ge 0 \).  This means that if \( g_i(x) \le 0 \) (the inequality condition is satisfied) then the Lagrangian is again bounded from above in terms of \( \lambda_i \).

Using this Lagrangian, we can derive the KKT conditions which are necessary (and sometimes even sufficient!) for global optimality.

## Deriving the KKT Conditions

### Differentiating the Lagrangian

We can find the optimizer of the Lagrangian by solving for where its gradient vanishes.

\[ \nabla L(x, \lambda, \nu) = 0 \tag{4} \]

\[ \therefore \nabla f(x) + \sum_i \lambda_i \nabla g_i(x) + \sum_j \nu_j \nabla h_j(x) = 0 \tag{5} \]

### Primal Feasibility

Of course, a candidate solution \( x^\star \) must satisfy the feasibility conditions of the _primal_ (original) problem.

\[ g_i(x) \le 0 \tag{6} \]

\[ h_j(x) = 0 \tag{7} \]

### Dual Feasibility

As we mentioned before, it is necessary to constrain \( \lambda_i \ge 0 \).  Otherwise, if \( g_i(x) < 0 \), the Lagrangian could be driven to infinity by \( \lambda_i \rightarrow -\infty \).

\[ \lambda_i \ge 0 \tag{8} \]

### Complementary Slackness

There is one final constraint in the KKT conditions.  It is very important that \( \lambda_i \) is nonzero _only when the constraint is active_ and \( g_i(x) = 0 \) (note the equality).  If \( \lambda_i \) can be strictly positive while \( g_i(x) < 0 \), then the Lagrangian is not optimal because \( \lambda_i \) can be decreased more!  We encode this requirement as

\[ \lambda_i g_i(x) = 0 \tag{9} \]

## Final KKT Conditions

Combining (5), (6), (7), (8), and (9), we have the KKT conditions in their full glory.

\[ \begin{align*} \nabla f(x^\star) + \sum_i \lambda_i^\star \nabla g_i(x^\star) + \sum_j \nu_j^\star \nabla h_j(x^\star) &= 0 \\ g_i(x^\star) &\le 0 \\ h_j(x^\star) &= 0 \\ \lambda_i^\star &\ge 0 \\ \lambda_i^\star g_i(x^\star) &= 0 \end{align*} \]

These conditions are always __necessary conditions for global optimality__... that is, if the KKT conditions _aren't_ met for a given \( (x^\star, \lambda^\star, \nu^\star) \), then that point is definitely not the global optimizer.  However, the KKT conditions are not always _sufficient_ conditions.  In convex programs, they are always necessary and sufficient, but in generalized, nonlinear, nonconvex optimization, they are only necessary, because nonconvex programs can have local optimizer that are not globally optimal.

That said, the KKT conditions suggest a very natural approach to general nonlinear, nonconvex optimization.  A solver using the Primal-Dual Interior Point Method (PDIPM) iteratively solves a series of relaxations on the KKT conditions, successively "tightening" the conditions as it progresses, until it converges on a local optimizer in _polynomial time_.  If the original problem was known to be convex, then _a PDIPM solver will find the global optimizer for the original program_.

## References

S. Boyd and L. Vandenberghe. _Convex Optimization_. Cambridge University Press, Cambridge, UK, 2004.
