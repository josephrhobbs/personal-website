# Convex Optimization

~

::byline[Joseph Hobbs][February 17, 2026]

In recent years, I've taken up a great interest in the theory of __optimization__.  The formal study of optimization covers a vast body of problems ubiquitous in pure mathematics, computer science, and engineering.  Whenever we are faced with one or more __decision variables__, an __objective__, and zero or more __constraints__, we are dealing with an optimization problem.  Scientists use results from optimization to determine reliable estimators for dependent variables in their experiments.  Engineers of computer hardware use algorithms born from optimization to arrange transistors elegantly on their silicon die.  Roboticists use similar algorithms to determine optimal path plans for their robots.

## Optimization, in General

The field of optimization formalizes "problems" as __optimization programs__.  In general, an optimization program looks like the following.

\[ \begin{align*} \min_x & f(x) \\ \text{subject to } & g_i(x) \le 0 \\ & h_j(x) = 0 \end{align*} \]

The __objective__ function \( f(x) \) accepts a vector of decision variables \( x \) and returns a scalar value.  The value of \( x \) which globally minimizes \( f \) is considered the __minimizer__ of this objective function.

This is the _most general form_ of an optimization program because we make no assumptions about the objective function \( f \) or the constraint functions \( g_i \) and \( h_j \).  Notice that, to write a maximization problem, we can simply minimize the _negative_ of the corresponding objective function.  If we make no assumptions about these functions, finding the global minimizer \( x \) is NP-hard in the number of decision variables.  I've written a proof of this rather unfortunate fact in a different article [here](/articles/hardness-of-nonlinear-programming) for those interested.

## Convex Optimization

There is hope for us yet.  Though optimization is NP-hard in general, there are special cases which are much easier to solve.  Fortunately, these special cases are far more common that they might initially appear, particularly due to clever reparameterizations.

One extraordinary special case is __convex optimization__.  An optimization program is _convex_ if it has a convex objective function and a convex feasible region.  What does this mean?

### Convex Sets

### Convex Functions

### Feasible Regions

## Complexity of Convex Optimization

TODO
