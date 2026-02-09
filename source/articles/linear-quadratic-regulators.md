# LQR

~

::byline[Joseph Hobbs][February 9, 2026]

The world is full of complicated systems changing over time, interacting with one another, with themselves, and with their environment.  It's difficult to comprehend just how ubiquitous these "systems" are, in the most general sense.  An incredible (and underappreciated) achievement of contemporary engineering is the study of __control__.  Control theorists seek to understand how both natural and engineered systems evolve, and how they can be controlled.

More traditional methods of control, often called _classical_ control, focus on describing the dynamics of a __plant__ (the system to be controlled), deciding on the _desired_ dynamics, and then working backwards to determine a good __controller__ (an engineered system capable of changing the plant's dynamics).  For example, a classic toy example is the inverted pendulum.  Pendulums do not naturally balance upside-down (existing dynamics), but we want them to (desired dynamics).  So by sending the right torque commands to a motor at the pendulum's pivot, we can make the pendulum balance upside-down.

In recent years, classical control has given way to new ways of thinking about control.  Classical control has one major challenge: how do we determine what dynamics we want in the first place?  The problem becomes rather difficult in the presence of constraints like motor torque limits or minimizing chance of the physical collision of two objects.  For example, consider the case of the pendulum, but we pay a hefty price for every kilojoule of electrical energy expended by the motor.  How do we know what dynamics we "want", apart from anything that's stable and cheap?  Contemporary control theorists have begun reframing the problem of control as an _optimization_.  These methods of _optimal_ control focus on describing a __cost__ (penalty for "bad" outcomes) and then determining controllers that minimize that cost.

## Linear Systems

For this article, I'm restricting myself to __linear systems__, obeying

\[ \dot{x} = A x + B u \]

for system state \( x \in \mathbb{R}^d \), control input \( u \in \mathbb{R}^k \), and constant matrices \( A \in \mathbb{R}^{d \times d}, B \in \mathbb{R}^{d \times k} \).  Very few systems in our world are truly linear (rotation immediately introduces trigonometric functions, which are obviously not linear functions), but many systems can be considered "close" to linear in certain cases, so this is after all a useful representation.

## Cost

Notice that, for this linear system, \( x = 0, u = 0 \) is a _fixed point_.  That means that, when \( x = 0 \) and \( u = 0 \), then \( \dot{x} = 0 \) and the system doesn't change.  This doesn't mean that the system is _stable_ around \( x = 0 \)... if you _perfectly_ balance a pendulum upside-down, it will stay, but as soon as you bump it at all then it will fall.  Suppose we want to make the system stable around the fixed point \( x = 0 \), and we'd like to know what control input \( u \) to use.  One very simple to define cost is to use a __quadratic cost__.  At a given time, the cost function

\[ g(x, u) = x^\mathrm{T} Q x + u^\mathrm{T} R u \]

quantifies how "bad" we are doing.  For \( Q \succeq 0, R \succeq 0 \), notice that \( g(0, 0) = 0 \) is the global minimum of \( g \).  This means that, when \( x \neq 0 \) or \( u \neq 0 \), the cost is strictly positive, meaning the system is a state less than ideal.  Because \( g \) only tells us about _instantaneous_ cost, we can integrate it to determine the total cost accrued over time.

\[ J(x, u) = \int_0^\infty \left( x^\mathrm{T} Q x + u^\mathrm{T} R u \right) \, \mathrm{d}t \]

Without proof, I will assert that, when \( u = -K x \) for some constant matrix \( K \), this reduces to

\[ J(x, u) = x^\mathrm{T} S x \]

for some matrix \( S \succeq 0 \).

::notice[More coming soon!]
