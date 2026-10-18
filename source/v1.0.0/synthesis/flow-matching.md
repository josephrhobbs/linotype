# Flow Matching

~

::byline[Joseph Hobbs][October 18, 2026]

The method of __flow matching__ is a common approach used for sampling (approximately) from a probability distribution \( p_\mathrm{data} \) when only samples from the distribution \( x_i \sim p_\mathrm{data} \) are known.  The method constructs an ordinary differential equation (ODE) which describes the movement of samples from a known distribution \( p_\mathrm{init} \) (often, the standard Gaussian) to samples from the unknown distribution \( p_\mathrm{data} \).  Frequently, the vector field required by the ODE is analytically intractable, but it can be estimated effectively using function approximation techniques (such as deep neural networks).  Here, we derive the sampling and training algorithms for a flow matching model, drawing heavily on the pedagogical resource prepared by (Holderrieth).

## Notation

We write as \( t \) the _time_ variable, which satisfies \( 0 \le t \le 1 \), and we write as \( X_t \in \mathbb{R}^n \) the function that satisfies the ODE.  We write as \( p_t \) the probability distribution over which \( X_t \) is distributed.

Define a _vector field_ \( u_t^\theta : \mathbb{R}^n \rightarrow \mathbb{R}^n \) parameterized by \( \theta \) that defines the ordinary differential equation

\[ \frac{dX_t}{dt} = u_t^\theta(X_t) . \]

Here, the ODE is defined such that \( X_0 \sim p_\mathrm{init} \) and \( X_1 \sim p_\mathrm{data} \).  In English, the ODE _interpolates_ between a selected known distribution \( p_\mathrm{init} \) (for example, a Gaussian distribution) and an unknown "target" distribution \( p_\mathrm{data} \).

## Sampling with an ODE

Given a way to evaluate \( u_t^\theta(X_t) \), sampling from \( p_\mathrm{data} \) is quite simple.  First, sample \( X_0 \sim p_\mathrm{init} \).  Then, select an iteration count \( k \) and a step size \( h \) such that \( kh = 1 \) (for example, select \( k = 20 \) and \( h = 0.05 \)).  Then, let \( t = 0 \) and, for \( k \) iterations, evaluate

\[ X_{t + h} \gets X_t + h \cdot u_t^\theta(X_t) \]

until \( t = 1 \).  By the definition of \( u_t^\theta \), \( X_1 \) will be distributed according to \( p_\mathrm{data} \).  We see that, given a way to evaluate the vector field \( u_t^\theta \), sampling is trivial... the challenge is determining the vector field given only samples from \( p_\mathrm{data} \), which we will refer to from now on as _training examples_.

## Constructing the conditional vector field

_More coming soon!_

## Marginalizing the vector field

_More coming soon!_

## Approximating the marginal vector field

_More coming soon!_

## References

P. Holderrieth and E. Erives. "An Introduction to Flow Matching and Diffusion Models." _Generative AI with Stochastic Differential Equations_, Massachusetts Institute of Technology. (accessed October 18, 2026)
