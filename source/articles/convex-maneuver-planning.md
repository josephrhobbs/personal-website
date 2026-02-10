# Maneuver Planning

~

::byline[Joseph Hobbs][February 10, 2026]

Recently, I've taken a great interest in the intersection of probability theory, optimization, and optimal control.  The last three decades or so has witnessed a tremendous amount of research in the field of __convex optimization__, which focuses on an extremely important subset of optimization problems.

A recent paper by Z. Manchester's lab of MIT (formerly CMU), "Convex Maneuver Planning for Spacecraft Collision Avoidance" by F. Vega et al. (found [here](https://roboticexplorationlab.org/projects/cvx_cola.html)), caught my attention recently because it unifies optimal control and probability in the wonderfully fascinating (though incredibly harsh) environment of Earth orbit.  Here, I unpack the paper's main point by presenting a (highly) simplified example of the methodology presented.

## Review of Optimization

For those unacquainted, the study of optimization formalizes "optimization problems" as __optimization programs__.  The field makes formal distinctions between various programs and provides rigorous, certifiable methods for solving them.  The most general optimization program is the __Nonlinear Program__ (NLP).

\[ P : \begin{align*} \min_x & f(x) \\ \text{subject to } & g_i(x) \le 0 \\ & h_i(x) = 0 \end{align*} \]

Here, the optimization program \( P \) is an NLP.
