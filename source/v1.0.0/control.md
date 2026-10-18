# Control

~

The world around us is full of complex systems, both natural and anthropogenic.  Many times, it is desirable to shape the dynamics of these systems to achieve stable operation, robustness to unpredicted disturbances, or other useful performance characteristics.  I speak abstractly here intentionally... these words are equally applied to biological feedback mechanisms, airplanes and spacecraft, industrial systems, and human infrastructure like water or power distribution.  The study of __control__ aims to develop the right mathematical and computational tools for characterizing these systems and shaping their dynamics to achieve a desired behavior.

Here, I summarize many concepts in control.  Those experienced in control will notice that my summary has a distinctly modern flavor, focused on optimal control in high-dimensional systems.  This is not motivated by a disregard for the existing classical techniques (in the frequency domain), but rather by a desire to unify content across _Linotype_ under the _lingua franca_ of nonlinear dynamical systems and optimization.  This common thread is enhanced by frequent nods to ideas, both old and new, which have reshaped our understanding of control, such as the calculus of variations and convex analysis.

## Linear quadratic regulator

The __linear quadratic regulator__ is the quintessential optimal controller.

[Linear Quadratic Regulator](control/linear-quadratic-regulator)

## Numerical optimal control

Increasingly common in the Age of Information are methods for __numerical optimal control__.  A common paradigm for numerical optimal control is _model-predictive control_, in which the controller solves an optimization problem at each step to determine the next control effort.

[Model-Predictive Control](control/model-predictive-control)

Frequently, methods for model-predictive control require writing a continuous-time problem in terms of a countable number of decision variables.  The process of constructing these formulations is frequently known as __transcription__.  Numerous transcription methods exist, with various benefits and limitations.

[Transcription Methods](control/transcription)
