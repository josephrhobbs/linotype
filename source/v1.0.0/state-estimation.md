# State Estimation

~

Tightly coupled with the study of control is the study of __state estimation__.  The world is a chaotic, messy place, and the field of state estimation provides _powerful, efficient algorithms_ for estimating the state of a dynamical system, such as a robot or aerospace vehicle, given potentially sparse, potentially noisy, potentially inaccurate measurements.

## Kalman filter

The __Kalman filter__ is the classical "holy grail" of time-domain state estimation.

[Reference: Kalman Filter](state-estimation/kalman-filter)

## Wahba's problem

An interesting, and highly impactful, problem in state estimation is __Wahba's problem__.  First proposed by statistician Grace Wahba in the 1960s, Wahba's problem involves solving the nonconvex program

\[ \min_{R \in \mathrm{SO(3)}} \sum_i w_i \left\Vert y_i - R x_i \right\Vert_2^2 \]

where \( x_i, y_i \) are corresponding unit vectors in \( \mathbb{R}^3 \) and \( w_i \) are positive scalar weights.

[Reference: Wahba's Problem](state-estimation/wahba's-problem)

Since the 1960s, a variety of solution methods for Wahba's problem have emerged.  Three of the most notable are, in no particular order, the _Davenport q-method_, _singular value decomposition_, and _convex optimization_.

[Reference: Davenport q-Method for Wahba's Problem](state-estimation/davenport-q)

[Reference: Singular Value Decomposition for Wahba's Problem](state-estimation/singular-value-decomposition)

[Reference: Convex Optimization for Wahba's Problem](state-estimation/convex-optimization)

## Factor graphs

_TODO_

## References

More coming soon!
