# Estimation

~

Both the natural world and the plethora of devices created by humankind trouble us with two issues when we try to build systems to control them.  The first issue is that our measurements of physical quantities (distances, temperatures, times, etc.) are not always correct, nor are they always completely repeatable to perfect precision.  The second issue is that we can not always _fully_ observe every variable... we may be forced by constraints fundamental or practical to measure proxies.  We refer to these troubles as __noise__ and __partial observability__, respectively.

The study and theory of __estimation__ provides rigorous tools for making inferences from measurements under uncertainty (noise) and partial observability.  The field has a long history rooted in the theory of probability, but the rise of the Age of Information has caused a massive explosion in estimation theory and practice.

Here, I attempt to summarize the field of estimation as it may be useful to a contemporary theoretician or practitioner.  Those already familiar will notice that, like many other materials on _Linotype_, my coverage of the theory of estimation has a characteristic "modern" flair, with a focus on the intersection between Bayesian statistics and convex optimization whenever possible.

## Luenberger observer

The __Luenberger observer__ is the quintessential multiple-state observer under known linear dynamics.  Given a dynamics model and a measurement model, the Luenberger observer constructs estimates of a system's underlying state.

[Luenberger Observer](estimation/luenberger-observer)
