# Hardness of NLP

~

::byline[Joseph Hobbs][February 10, 2026]


## Review of Optimization

For those unacquainted, the study of optimization formalizes "optimization problems" as __optimization programs__.  The field makes formal distinctions between various programs and provides rigorous, certifiable methods for solving them.  The most general optimization program is the __Nonlinear Program__ (NLP).

\[ \begin{align*} P: \min_x f(x) & \\ \text{subject to } g_i(x) &\le 0 \\ h_j(x) &= 0 \end{align*} \]

Here, the optimization program \( P \) is general because we make _no assumptions_ about the behavior of \( f \), \( g \), or \( h \).  These functions could be extraordinarily "nice" (linear functions, maybe!) or terribly behaved functions.  We call the vector \( x \) the __decision variable__, the scalar function \( f \) the __objective__, and the inequalities and equalities below the __constraints__.

Optimization programs, in general, can have three possible results: __infeasibility__, __unboundedness__, and __optimality__.  As you might imagine, we like that last one the best!  A program is _infeasible_ if there exists no \( x \) that can satisfy the constraints.  For example, consider \( P_1 \).

\[ \begin{align*} P_1: \min_x x^2 & \\ \text{subject to } x &\ge 1 \\ x &\le -1 . \end{align*} \]

Clearly, because there is no such \( x \) such that \( x \ge 1 \) and \( x \le -1 \), this program is _infeasible_.  A problem is _unbounded_ if there is a feasible region, but there is no optimal solution within it.  This is easily visualized by \( P_2 \).

\[ \begin{align*} P_2: \min_x \frac{1}{x} & \\ \text{subject to } x &\ge 1 . \end{align*} \]

By increasing \( x \), we continually decrease the objective function, but we can never reach a minimum value, because we can just keep increasing \( x \) forever.  The program is feasible, but it is _unbounded_.  Finally, programs like \( P_3 \) can be solved to optimality.

\[ \begin{align*} P_3: \min_x x^2 & \\ \text{subject to } x &\le 1 . \end{align*} \]

Here, it's clear to see that \( x = 0 \) is the _minimizer_ of \( P_3 \), and the program is solved to optimality.  Generally, the problem of solving NLPs is __NP-hard__.  I've presented a proof below, if you're interested.  Otherwise, you may safely skip ahead!

Hardness of NLP.  __Theorem 1__.  Let \( P \) be an NLP.  Then, solving \( P \) is NP-hard.

Hardness.  __Definition 1__.  A problem \( Q \) is _NP-hard_ if, for every problem \( R \) in NP, there exists a polynomial-time reduction \( L \) such that \( L(R) \) rewrites \( R \) as \( Q \).

Hardness of SAT.  __Lemma 1__.  The problem of Boolean satisfiability (SAT) is NP-hard in the number of decision variables.  The problem of Boolean satisfiability is parameterized by decision variables \( x_i \) for \( i = 1, \cdots, N \) and an expression in conjunctive normal form (CNF), involving a finite number of terms joined by AND, where each term is a finite number of terms joined by OR.  For example, the following is CNF. 

\[ ( x_1 \lor x_3 \lor x_7 ) \land ( x_2 \lor \neg x_1 ) \land \cdots \]

Polynomial-time reduction of SAT.  __Lemma 2 and Proof__.  SAT can be reduced to an NLP by introducing constraint

\[ x_i (1 - x_i) = 0 \]

for each \( x_i \) and introducing constraint

\[ \sum_{i = 1}^n x_i \ge 1 \]

for each CNF clause.  The first constraint enforces \( x_i \in \{ 0, 1 \} \), where \( 0 \) is falsy and \( 1 \) is truthy.  The second constraint ensures that each CNF clause is truthy; if at least one \( x_i \) in a clause is equal to one (truthy), the sum of \( x_i \) will be at least one and the entire clause will be truthy.  For clauses containing negatives like \( \neg x_1 \), we can replace \( x_i \) with \( 1 - x_i \) in the summation.  If all clauses are truthy, the entire CNF is truthy.  Here, we are only looking for feasible solutions, so we do not require any particular objective function.  The final NLP is

\[ \begin{align*} P_\mathrm{SAT}: \min_x 0 & \\ \text{subject to } x_i (1 - x_i) &= 0 \\ \sum_{i = 1}^n x_i &\ge 1 \end{align*} . \]

Note that we have abused notation to omit cases of negatives like \( \neg x_1 \).  In these cases, we modify the corresponding constraint as previously described.  With \( N \) decision variables, \( k \) CNF clauses, and a maximum of \( n \) decision variables per CNF clause, it is clear that _SAT can be reduced to NLP_ in \( O(N + kn) \) time.

Hardness of NLP.  __Proof of Theorem 1__.  By Lemma 2, any SAT problem can be reduced to an NLP in \( O(N + kn) \) time.  Therefore, a polynomial-time reduction \( L_1 \) exists from SAT to NLP.  By Lemma 1, SAT is NP-hard, which means there exists a polynomial-time reduction \( L_2 \) exists from any problem in NP to SAT.  Therefore, the reduction \( L_3 := L_1(L_2(\cdot)) \) is polynomial-time.  This means that \( L_3 \) is a polynomial-time reduction from any problem in NP to NLP.  By Definition 1, the existence of \( L_3 \) implies NLP is NP-hard.  \( \blacksquare \)

::notice[Under construction!]
