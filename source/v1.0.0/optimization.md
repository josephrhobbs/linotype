# Optimization

~

An extraordinarily general paradigm for design and inference under uncertainty is __optimization__.  Given some function \( f(x) \) and some constraints \( g(x) = 0 \) and \( h(x) \le 0 \), what is the value of \( x \) that minimizes \( f \) and satisfies all constraints?  This is the central question in optimization, and rich bodies of literature have evolved over recent decades, approximately classified by the structure of each of the functions \( f \), \( g \), and \( h \).

Here, I summarize several _algorithms for multivariable optimization_.  I have made the intentional choice to focus _Linotype_'s summary and application on a specific subfield of optimization referred to as __convex optimization__, so named because it focuses on the optimization of convex functions over convex feasible sets.

Convex optimization algorithms have two particularly nice properties.  Firstly, they always return _global_ optimizers (and never "get stuck" in local, non-global optimizers).  Secondly, they require no special "tricks" for initialization.

Readers of _Linotype_ will notice that many other topics covered here draw on convex optimization.  In a way, it is the _lingua franca_ of _Linotype_.  I have chosen to make _convex_ optimization the _lingua franca_ of "modern" schools of control, estimation, and design.  A wealth of critical results in these fields can be demonstrated using a single convex optimization program.  We aim to embrace convexity wherever we find it, and to encourage it when at first we perceive a problem to be nonconvex.

_More coming soon!_
