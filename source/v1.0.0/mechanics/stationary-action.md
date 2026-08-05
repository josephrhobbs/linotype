# Principle of Stationary Action

~

::byline[Joseph Hobbs][August 4, 2026]

The **Principle of Stationary Action** (PSA) is the cornerstone of contemporary classical mechanics.  Dissatisfied with the Newtonian formulation, mathematicians Joseph-Louis Lagrange set out to develop a more elegant formulation of classical mechanics in the 18th century.  His famous result, described by Euler as the _calculus of variations_, is foundational to analytical mechanics.  Centuries later, the study of **optimal control** has found great utility in Lagrange's work (Liberzon).

Here, I derive the _Euler-Lagrange equation_, the contemporary formulation of Lagrange's work.  Informally, Lagrange proposed a method to optimize _entire functions_ with respect to a _functional objective_ using "ordinary" differential calculus.  Lagrange's discovery is the core of the Principle of Statinonary Action, an elegant reformulation of classical mechanics.  The main theorem is below, and following it is a standard derivation.

## The principle, informally

The PSA informally states that **nature always prefers paths with stationary action**.  The _action_ of a trajectory \( x(t) \) between \( t = a \) and \( t = b \) is written as

\[ S x := \int_a^b \left( T(x) - V(x) \right) \, dt . \]

Note that I use the notation \( S x \) to denote the evaluation of the functional \( S \) on the function \( x(t) \).

Here, \( T \) is the kinetic energy operator, and \( V \) is the potential energy operator.  Notice that nonconservative forces (e.g. friction) are not accounted for here... this formulation only considers movement in a conservative field, though of course nonconservative corrections exist.  Lagrange's work (as well as that by Sir William Hamilton) gives us the brilliant insight that nature always seeks the path with _stationary_ action.  This means that, in all cases, trajectories lie at a local minimum, maximum, or saddle point of the action.

## Deriving the Euler-Lagrange equation

### Theorem statement

::mathblock[Theorem][Euler-Lagrange Theorem]

Let \( f \in C^2 \) be a function \( f: \mathbb{R} \rightarrow \mathbb{R} \), and let \( \mathcal{S} \) be a functional over possible functions \( f \) defined by

\[ S f := \int_a^b \mathcal{L} \left( f(x), f^\prime(x) \right) \, dt . \]

For the function \( f \) to be stationary with respect to \( \mathcal{L} \), it is both necessary and sufficient that \( f \) satisfy the _Euler-Lagrange equation_.

\[ \frac{d}{dx} \left( \frac{d\mathcal{L}}{df^\prime} \right) - \frac{d\mathcal{L}}{df} = 0 \]

Here, \( x \in \mathbb{R} \) is the argument of \( f \) and \( f^\prime \) is the derivative of \( f \) with respect to its argument \( x \).

::endmath

### Derivation

_More coming soon!_

## References

Liberzon, Daniel.  "Calculus of Variations and Optimal Control Theory: A Concise Introduction".  University of Illinois at Urbana-Champaign.  https://liberzon.csl.illinois.edu/teaching/cvoc/node29.html (accessed August 4, 2026)
