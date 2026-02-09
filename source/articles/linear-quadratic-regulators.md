# LQR

~

::byline[Joseph Hobbs][February 9, 2026]

The world is full of complicated systems changing over time, interacting with one another, with themselves, and with their environment.  It's difficult to comprehend just how ubiquitous these "systems" are, in the most general sense.  An incredible (and underappreciated) achievement of contemporary engineering is the study of __control__.  Control theorists seek to understand how both natural and engineered systems evolve, and how they can be controlled.

## The Inverted Pendulum

Pendulums do not naturally balance upside-down, but suppose that we want one to anyways.  By sending the right torque commands to a motor at the pendulum's pivot, we can make the pendulum balance upside-down.  Here, we'll derive the dynamics for the pendulum and show how we can make a controller for a motor at the pivot, allowing the inverted pendulum to be stable.

We define \( \theta \) to be the angle of the pendulum counterclockwise from the downward position.  That is, when the pendulum is hanging straight down, \( \theta = 0 \), and \( \theta \) increases as the pendulum rotates to the left (counterclockwise).  The torque acting on a pendulum due to gravity can be written as \( \tau = -m \ell g \sin\theta \), and the angular momentum can be written as \( m \ell^2 \dot{\theta} \).  Because torque is rate of change of angular momentum, i.e.,

\[ \tau = \frac{\partial L}{\partial t} \]

we can show

\[ \ddot{\theta} + \frac{g}{\ell} \sin\theta = 0 . \]

This is the __second-order ordinary differential equation__ (ODE) describing the dynamics of our pendulum.  Much of control theory is based on controlling first-order systems, however.  Fortunately for us, there is a rather easy way to write a second-order ODE as a first-order ODE.  If we define \( x := \begin{bmatrix} \theta & \dot{\theta} \end{bmatrix}^\mathrm{T} \), then we can write

\[ \begin{bmatrix} \dot{\theta} \\ \ddot{\theta} \end{bmatrix} = \begin{bmatrix} \dot{\theta} \\ -\frac{g}{\ell} \sin\theta \end{bmatrix} , \]

or, more succinctly,

\[ \dot{x} = f(x) . \]

If you've never seen this before, I encourage you to take a moment to fully digest it.  This is a __state space__ representation of a second-order ODE in one variable as a first-order ODE in two variables!  First-order ODEs are extraordinarily well-studied, so we should take confidence that we can understand and explain this well.

## Linearization

::notice[Coming soon!]

## Classical Control

More traditional methods of control, often called _classical_ control, focus on describing the dynamics of a __plant__ (the system to be controlled), deciding on the _desired_ dynamics, and then working backwards to determine a good __controller__ (an engineered system capable of changing the plant's dynamics).

## A Paradigm Shift

In recent years, classical control has given way to new ways of thinking about control.  Classical control has one major challenge: how do we determine what dynamics we want in the first place?  The problem becomes rather difficult in the presence of constraints like motor torque limits or minimizing chance of the physical collision of two objects.  For example, consider the case of the pendulum, but we pay a hefty price for every kilojoule of electrical energy expended by the motor.  How do we know what dynamics we "want", apart from anything that's stable and cheap?  Contemporary control theorists have begun reframing the problem of control as an _optimization_.  These methods of _optimal_ control focus on describing a __cost__ (penalty for "bad" outcomes) and then determining controllers that minimize that cost.

::notice[More coming soon!]
