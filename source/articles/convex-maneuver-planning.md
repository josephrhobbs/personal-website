# Maneuver Planning

~

::byline[Joseph Hobbs][February 10, 2026]

Recently, I've taken a great interest in the intersection of probability theory, optimization, and optimal control.  A recent paper by Z. Manchester's lab of MIT (formerly CMU), "Convex Maneuver Planning for Spacecraft Collision Avoidance" by F. Vega et al. (found [here](https://roboticexplorationlab.org/projects/cvx_cola.html)), caught my attention recently because it unifies optimal control and probability in the wonderfully fascinating (though incredibly harsh) environment of Earth orbit.  Here, I unpack the paper's main point by presenting a (highly) simplified example of the methodology presented.

## Review of Optimization

For those unacquainted, the study of optimization formalizes "optimization problems" as __optimization programs__.  The field makes formal distinctions between various programs and provides rigorous, certifiable methods for solving them.  The most general optimization program is the __Nonlinear Program__ (NLP).

\[ \begin{align*} P: \min_x f(x) & \\ \text{subject to } g_i(x) &\le 0 \\ h_j(x) &= 0 \end{align*} \]

Here, the optimization program \( P \) is an NLP because we make _no assumptions_ about the behavior of \( f \), \( g \), or \( h \).  These functions could be extraordinarily "nice" (linear functions, maybe!) or terribly behaved functions.  We call the vector \( x \) the __decision variable__, the scalar function \( f \) the __objective__, and the inequalities and equalities below the __constraints__.

Generally, NLPs are __NP-hard__.

__Proof__.

::notice[Under construction!]
