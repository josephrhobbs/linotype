# Robotics & Control

~

Contemporary research in robotics, particularly in bipedal or legged robotics, places an incredible emphasis on formal algorithms for __control__.  Fundamentally, the study of control, when applied to robotics, asks one of three questions.

Firstly, how can a controller stabilize a system _about a provided fixed point_?

Secondly, how can a controller stabilize a system _about a predetermined trajectory_?

And finally, how can a controller stabilize a system _about a cycle_?

Notice that the first question is rather a degenerate case of the other two, because a fixed point is a trajectory that goes nowhere, and a fixed point is also a cycle that does nothing interesting.  That said, these three questions call for rather different methods, which we explore here.

Furthermore, what we know can dramatically shape the decisions we make about controller design.  If our dynamics are linear, the __Linear Quadratic Regulator__ (LQR) is proven to be the optimal controller for a quadratic cost-to-go, and it demonstrates global asymptotic stability.  When dynamics are polynomial, __Lyapnov analysis__ can provide globally asymptotically stable controllers, but they make no guarantees of optimality.  In the very worst case, when dynamics are extremely nonlinear or difficult to characterize, __trajectory optimization__ can provide _locally_ optimal trajectories, but they must often be stabilized by LQR or other controllers, as they make no guarantee of stability on their own.

## Dynamic Programming

This is the ideal case in every control problem.  The mathematician Richard Bellman devised algorithms for determining optimal solutions to decision and control problems through the lens of __dynamic programming__ (Padoan).

[Reference: Dynamic Programming](robotics-and-control/dynamic-programming)

In the case of linear dynamics, there exists a computationally tractable solution to the __Hamilton-Jacobi-Bellman equation__, the governing relation of dynamic programming.  This solution is called the __Linear Quadratic Regulator__ (LQR).

[Reference: Linear Quadratic Regulators](robotics-and-control/linear-quadratic-regulators)

## Lyapunov Analysis

LQR is a wonderful special case of dynamic programming, but often, dynamic programming algorithms are intractable for complex, polynomial dynamics.  In this case, __Lyapunov analysis__ allows a new perspective on control.  Instead of focusing on _optimality_, Lyapunov analysis focuses only on determining the _stability_ of a controlled system.

[Reference: Lyapunov Analysis](robotics-and-control/lyapunov-analysis)

## SOS Relaxations

The last few decades have yielded a number of wonderful algorithms that have drastically accelerated the field of control.  Notable among these are the methods introduced by P. Parrilo for __sum-of-squares programming__ (SOS).  Parrilo's algorithms for SOS can find, _in polynomial time_, polynomials that are always nonnegative and satisfy given constraints (Parrilo).  This reduces Lyapunov analysis to an SOS program.  If SOS programming finds a solution, the Lyapnov criteria are satisfied, and if SOS programming fails to find a solution, then the Lyapunov criteria _might not_ be satisfied.

[Reference: SOS Relaxations](robotics-and-control/sum-of-squares-relaxations)

It's important to recognize that SOS leaves a "gap".  There are some functions which are always nonnegative and satisfy the given constraints, but SOS programming cannot find them.  This is why, if SOS fails to find a solution, we cannot conclude if the Lyapunov criteria are satisfied or not.  Characterizing the SOS "gap" is still an open problem in the research of both semialgebraic geometry and controls engineering for robotics.  However, _empirically_, it's important to remember that the "gap" is "small" enough not to make a significant impact on the field's ability to use SOS programming, at least in a practical sense.

## Trajectory Optimization

Unfortunately, despite how powerful dynamic programming can be, and despite the elegance of Lyapunov analysis and SOS, some problems simply refuse to admit these methods.  The most general, albeit least "powerful", method of control available to use is __trajectory optimization__.  Trajectory optimization determines locally optimal trajectories from a given starting point to a goal point (frequently a fixed point), or alternatively can be used to determine limit cycle trajectories ("oscillations").

Trajectory optimization has three basic _transcriptions_ (problem formulations).  These are rather unfortunately named _direct transcription_, _direct shooting_, and _direct collocation_.  The overloading of the adjective "_direct_" tends to cause confusion, so I have created separate articles for each one.

[Reference: Direct Transcription](robotics-and-control/direct-transcription)

[Reference: Direct Shooting](robotics-and-control/direct-shooting)

[Reference: Direct Collocation](robotics-and-control/direct-collocation)

Trajectory optimization can be used for a variety of difficult problems and is found all over robotics engineering in the 21st century.  Nonlinear control problems, highly underactuated control problems, and control through contact can all be solved using trajectory optimization.

_TODO_

## References

A. Padoan. "Richard Bellman: The Father of Dynamic Programming." _inControl_, January 17, 2025. https://www.incontrolpodcast.com/1632769/episodes/16452722-ep29-richard-bellman-the-father-of-dynamic-programming (accessed April 3, 2026)

P. Parrilo. "Structured Semidefinite Programs and Semialgebraic Geometry Manifolds in Robustness and Optimization." Ph.D. thesis, California Institute of Technology, Pasadena, CA, United States.
