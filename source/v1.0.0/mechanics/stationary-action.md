# Principle of Stationary Action

~

::byline[Joseph Hobbs][August 4, 2026]

The **Principle of Stationary Action** (PSA) is the cornerstone of contemporary classical mechanics.  Dissatisfied with the Newtonian formulation, mathematician Joseph-Louis Lagrange set out to develop a more elegant formulation of classical mechanics in the 18th century.  His famous result, described by Euler as the _calculus of variations_, is foundational to analytical mechanics.  Centuries later, the study of **optimal control** has found great utility in Lagrange's work (Liberzon).

Here, I derive the _Euler-Lagrange equation_, the contemporary formulation of Lagrange's work.  Informally, Lagrange proposed a method to optimize _entire functions_ with respect to a _functional objective_ using "ordinary" differential calculus.  Lagrange's discovery is the core of the Principle of Statinonary Action, an elegant reformulation of classical mechanics.  The main theorem is below, and following it is a standard derivation.

## The principle, informally

The PSA informally states that **nature always prefers paths with stationary action**.  The _action_ of a trajectory \( x(t) \) between \( t = a \) and \( t = b \) is written as

\[ S x := \int_a^b \left( T(x) - V(x) \right) \, dt . \]

Note that I use the notation \( S x \) to denote the evaluation of the functional \( S \) on the function \( x(t) \).

Here, \( T \) is the kinetic energy operator, and \( V \) is the potential energy operator.  Notice that nonconservative forces (e.g. friction) are not accounted for here... this formulation only considers movement in a conservative field, though of course nonconservative corrections exist.  Lagrange's work (as well as that by Sir William Hamilton) gives us the brilliant insight that nature always seeks the path with _stationary_ action.  This means that, in all cases, trajectories lie at a local minimum, maximum, or saddle point of the action.

## Deriving the Euler-Lagrange equation

### Theorem statement

::mathblock[Theorem][Euler-Lagrange Theorem]

Let \( f \in C^2 \) be a function \( f: \mathbb{R} \rightarrow \mathbb{R}^n \), \( \mathcal{L} \in C^2 \) be a function \( \mathcal{L} : \mathbb{R}^n \rightarrow \mathbb{R} \), and \( \mathcal{S} \) be a functional over possible functions \( f \) defined by

\[ S f := \int_a^b \mathcal{L} \left( f(t), f^\prime(t) \right) \, dt . \]

For the function \( f \) to be stationary with respect to \( S \), it is both necessary and sufficient that \( f \) satisfy the _Euler-Lagrange equation_.

\[ \frac{d}{dt} \left( \frac{d\mathcal{L}}{df^\prime} \right) - \frac{d\mathcal{L}}{df} = 0 \]

Here, \( t \in \mathbb{R} \) is the argument of \( f \) and \( f^\prime \) is the derivative of \( f \) with respect to its argument \( t \).

::endmath

### Derivation

What follows is a standard derivation of the Euler-Lagrange equation.

::mathblock[Proof][Euler-Lagrange Theorem]

Let \( f \) and \( \mathcal{L} \) be functions as previously described, and let \( S \) be the functional

\[ S f := \int_a^b \mathcal{L} \left( f(t), f^\prime(t) \right) \, dt . \]

We introduce an arbitrary _test function_ \( \eta \in C^1 \) such that \( \eta(a) = \eta(b) = 0 \) and a constant \( \varepsilon \in \mathbb{R} \).  Perturb the function \( f \) by \( \eta(t) \) by defining

\[ f_\varepsilon(t) := f(t) + \varepsilon \eta(t) . \]

Notice that \( f_\varepsilon(a) = f(a) \) and \( f_\varepsilon(b) = f(b) \), because \( \eta(a) = \eta(b) = 0 \).  This fact will become useful later in the proof.  For \( f \) to be stationary with respect to \( S \), it is necessary and sufficient that

\[ \left. \frac{\partial}{\partial \varepsilon} S f_\varepsilon \right\vert_{\varepsilon = 0} = 0 \]

for arbitrary \( \eta \).  In other words, the value of \( S \) is stationary with respect to any possible perturbation to \( f \).  We expand this derivative by writing the definition of the action functional \( S \) and the perturbed function \( f_\varepsilon \).

\[ \frac{\partial}{\partial \varepsilon} \int_a^b \mathcal{L} \left( f(t) + \varepsilon \eta(t), f^\prime(t) + \varepsilon \eta^\prime(t) \right) \, dt = 0 \]

We reverse the order of integration and differentiation, and apply the chain rule.

\[ \int_a^b \left( \frac{\partial \mathcal{L}}{\partial f_\varepsilon} \frac{\partial f_\varepsilon}{\partial \varepsilon} + \frac{\partial \mathcal{L}}{\partial f_\varepsilon^\prime} \frac{\partial f_\varepsilon^\prime}{\partial \varepsilon} \right) \, dt = 0 \]

Substituting known derivatives, we arrive at

\[ \int_a^b \left( \frac{\partial \mathcal{L}}{\partial f_\varepsilon} \eta(t) + \frac{\partial \mathcal{L}}{\partial f_\varepsilon^\prime} \eta^\prime(t) \right) \, dt = 0 . \]

We can integrate the second addend by parts to obtain

\[ \int_a^b \frac{\partial \mathcal{L}}{\partial f_\varepsilon} \eta^\prime(t) \, dt = \left. \frac{\partial \mathcal{L}}{\partial f_\varepsilon} \eta(t) \right\vert_a^b - \int_a^b \frac{d}{dt} \frac{\partial \mathcal{L}}{\partial f_\varepsilon} \eta(t) \, dt . \]

Notice that the first term vanishes because \( \eta(a) = \eta(b) = 0 \).  Our original equality then simplifies to

\[ \int_a^b \left( \frac{\partial \mathcal{L}}{\partial f_\varepsilon} - \frac{d}{dt} \frac{\partial \mathcal{L}}{\partial f_\varepsilon^\prime} \right) \eta(t) \, dt = 0 . \]

This integral must hold for any arbitrary test function \( \eta(t) \).  It is necessary and sufficient that

\[ \frac{\partial \mathcal{L}}{\partial f_\varepsilon} - \frac{d}{dt} \frac{\partial \mathcal{L}}{\partial f_\varepsilon^\prime} = 0 \]

for this integral to equal zero for any test function.  Because \( f_\varepsilon(t) = f(t) \) for \( \varepsilon = 0 \), we have

\[ \frac{\partial \mathcal{L}}{\partial f} - \frac{d}{dt} \frac{\partial \mathcal{L}}{\partial f^\prime} = 0 \]

and, up to the sign of the left-hand side, this proves the theorem.

::qed

::endmath

## References

Liberzon, Daniel.  "Calculus of Variations and Optimal Control Theory: A Concise Introduction".  University of Illinois at Urbana-Champaign.  https://liberzon.csl.illinois.edu/teaching/cvoc/node29.html (accessed August 4, 2026)
