# Optimization

~

The field of __optimization__ studies formal methods for solving _programs_ of the form

\[ \begin{align*} \min_x & f(x) \\ \text{subject to } & g_i(x) \le 0 \\ & h_j(x) = 0 \end{align*} \]

where \( f : \mathbb{R}^n \rightarrow \mathbb{R} \) is a scalar _objective function_ and \( g_i, h_j : \mathbb{R}^n \rightarrow \mathbb{R} \) are scalar _constraint functions_.  In general, finding the global minimizer \( x^\star \) is NP-hard.  However, there exist efficient (read: polynomial-time) algorithms for two "easier" versions.

Firstly, if \( f \) is a function with a _convex epigraph_, and the constraints defined by \( g_i \) and \( h_j \) define a _convex set_, then the optimization is called a _convex program_ and can be solved to global optimality using efficient (read: polynomial-time) algorithms.

Secondly, if the program is not convex, there exist efficient (read: polynomial-time) algorithms for determining _local minimizers_ of \( f \).  Local minimizers may or may not be globally optimal, yet in many cases a local minimum are acceptable.

## Karush-Kuhn-Tucker Optimality Conditions

The Karush-Kuhn-Tucker conditions (KKT conditions) for optimality are the necessary conditions for global optimality.  In the case of convex programs, they are the necessary _and sufficient_ conditions for global optimality!

[Reference: Karush-Kuhn-Tucker Conditions](optimization/karush-kuhn-tucker)

The KKT conditions suggest an excellent way to solve nonlinear programs.  This is the _Primal-Dual Interior Point Method_ discussed below!

## Primal-Dual Interior Point Method

The primal-dual interior point method (PDIPM) is a highly efficient algorithm for constrained optimization.

[Reference: Primal-Dual Interior Point Method](optimization/primal-dual-interior-point-method)

The open-source solver [IPOPT](https://coin-or.github.io/Ipopt/) (pronounced "eye-pea-opt") performs highly efficient optimization on constrained nonlinear, nonconvex programs.  It is widely considered the academic and industry standard PDIPM solver.
