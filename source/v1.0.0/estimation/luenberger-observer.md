# Luenberger Observer

~

::byline[Joseph Hobbs][October 18, 2026]

The __Luenberger observer__ is the quintessential observer under known linear dynamics and measurement models.  Here, we derive the observer and its stability conditions.  The _Kalman filter_, a technique ubiquitous in industry and research for state estimation, is in fact a special case of the Luenberger observer and is considered optimal (minimum variance) under certain assumptions of process and measurement noise.  We derive the observer's continuous-time formulation, but of course a discrete-time formulation exists and may be derived according to a similar method.

## Dynamics and measurement models

We assume the following, _known_ linear dynamics model.

\[ \dot{x} = A x + B u \]

Here, \( x \in \mathbb{R}^n \) is the state variable, \( u \in \mathbb{R}^k \) is control input, and \( A \in \mathbb{R}^{n \times n}, B \in \mathbb{R}^{n \times k} \) are matrices with known entries.  We also assume the following _known_ linear measurement model.

\[ y = C x \]

We write as \( y \in \mathbb{R}^d \) the measurement output and \( C \in \mathbb{R}^{d \times n} \) a matrix with known entries.

## Defining the observer

The __Luenberger observer__ \( \hat{x} \) is an _unbiased_ and _asymptotically stable_ estimator of \( x \).  The observer solves the ordinary differential equation

\[ \dot{\hat{x}} = A \hat{x} + B u + L e \]

where \( e \in \mathbb{R}^d \) is a _measurement error_ term, and \( L \in \mathbb{R}^{n \times d} \) is an __observer gain__ selected by the user.  The observer gain _must_ satisfy the _observer stability condition_, or the observer will become unstable.

### Computing measurement error

The measurement error \( e \) is defined according to

\[ e := y - \hat{y} \]

where \( \hat{y} \) is the system output _as estimated by the observer_, and \( y \) is the true system output.

\[ \hat{y} := C \hat{x} \]

### Expanding the ODE

Substituting expressions for \( y, \hat{y} \) we find the following.

\[ \dot{\hat{x}} = A \hat{x} + B u + LC x - LC \hat{x} \]

\[ \therefore \dot{\hat{x}} = (A - LC) \hat{x} + Bu + LCx \]

This expression is not useful during estimation because we do not know the value of \( x \) directly.  However, we can use this to derive the conditions under which the observer is stable.

### Constructing the stability condition

The Luenberger observer is a __stable observer__ when the _state error_ \( x - \hat{x} \) is known to converge as \( t \rightarrow \infty \).  This can be ensured by correctly selecting the gain matrix \( L \).  We write the time derivative of the state error as

\[ \frac{d}{dt} \left( x - \hat{x} \right) = \dot{x} - \dot{\hat{x}} \]

\[ \therefore \frac{d}{dt} \left( x - \hat{x} \right) = A x + B u - (A - LC) \hat{x} - B u - LC x \]

\[ \therefore \frac{d}{dt} \left( x - \hat{x} \right) = (A - LC)(x - \hat{x}) \]

We define \( A_\mathrm{obs} := A - LC \) to be the _observer dynamics_ matrix.  For observer stability, we want the time derivative of \( x - \hat{x} \) to go to zero.  This occurs if and only if \( A - LC \) is strictly _negative definite_... that is, the eigenvalues of \( A - LC \) must all be strictly less than zero.  We write this condition as \( A - LC \prec 0 \).

### Analyzing stability of the observer

_More coming soon!_

### A connection to Lyapunov analysis

Let us write the state error as \( q(t) \in \mathbb{R}^n \).  Defining the matrix \( R \in \mathbb{R}^{n \times n} \) such that \( R \succ 0 \), we define a Lyapunov candidate for the observer as

\[ V(q) := q^\top R q. \]

It is easy to see that, as \( q \rightarrow 0 \), the Lyapunov function decreases towards zero.  For this Lyapunov candidate to certify asymptotic stability of our Luenberger observer, we must have \( \dot{V} < 0 \).  In other words,

\[ \dot{V}(q) = q^\top R \dot{q} + \dot{q}^\top R q < 0 \]

\[ \therefore \dot{V}(q) = q^\top R (A - LC) q + q^\top (A - LC)^\top R q < 0 \]

For this expression to be always negative, there must exist a matrix \( P \succeq 0 \) such that

\[ R (A - LC) + (A - LC)^\top R = -P . \]

Expanding, we have

\[ R A - R L C + A^\top R - C^\top L^\top R + P = 0 . \]

This equation is linear in \( L \) and, after user selection of \( P \), is easily solved by various software toolboxes for multivariate control design.

## References
