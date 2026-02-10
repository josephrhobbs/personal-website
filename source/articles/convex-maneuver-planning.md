# Maneuver Planning

~

::byline[Joseph Hobbs][Feburary 10, 2026]

Recently, I've taken a great interest in the intersection of probability theory, optimization, and optimal control.  A recent paper by Z. Manchester's lab of MIT (formerly CMU), "Convex Maneuver Planning for Spacecraft Collision Avoidance" by F. Vega et al., found [here](https://roboticexplorationlab.org/projects/cvx_cola.html), caught my attention recently because it unifies optimal control and probability in the wonderfully fascinating (though incredibly harsh) environment of Earth orbit.  Here, I unpack the paper's main point by presenting a _highly_ simplified example of the methodology.

## Collision Avoidance

There are a lot of satellites in low Earth orbit (LEO).  Thousands, in fact.  And the early 21st century is showing nothing less than an explosion in the satellite economy.  Ridesharing, advanced materials, reusable boosters, and a host of other innovations have made LEO orders of magnitude more accessible, relative to even twenty years ago.

Space is a big place, but it's not _that_ big.  With thousands of communications, research, and imaging satellites swarming about, spacecraft __conjunction events__ are becoming commonplace.  Informally, a conjunction event occurs when two spacecraft come into close proximity, and there is a practical probability that they will actually collide, causing millions of dollars of irreversible damage.

Needless to say, we'd like to be able to anticipate conjunction events and correct for possible collisions long before they occur.  Extensive research continues to contribute to anticipating these events using computational methods, but Manchester's lab has achieved something further: they have developed an algorithm for automatically determining minimum-cost thrust profiles to minimize probability of collision.  I highly encourage you to read the paper for the full algorithm, but here, I will present a very simple toy model for two satellites in coplanar, circular orbits.

## Our Setup

Imagine that two fictitious telecommunications companies, Acme Satellite and General Communications (GenCom), have both deployed communications satellites into equatorial orbits in LEO.  However, though Acme has decided to orbit their satellite prograde (counterclockwise, when viewed from the north pole), GenCom had the unusual idea of orbiting retrograde (clockwise).  In our model, we will assume that both satellites orbit at exactly the same altitude \( h \), and the only non-negligible gravitational force is the Earth, which we will model as a perfect sphere with radius \( R \), uniform density, and mass \( M \).

::definition[Conjunction Point]

We take an Earth-centered inertial reference frame.  The equatorial plane, given by \( z = 0 \), contains the orbits of both the Acme and GenCom satellites.  We will call the __conjunction point__ \( P \) the point \( \begin{bmatrix} R + h & 0 \end{bmatrix}^\mathrm{T} \).  At a defined time in the near future, both the Acme and GenCom satellites will pass through \( P \).

::endmath

Suppose that we know both satellites are in the equatorial plane, but we have some _uncertainty_ on their position in that plane.

::definition[Generative Models for Position Measurement]

At the time when both satellites pass through \( P \), the measured position of each satellite will obey the following generative models.  Here, \( \hat{x} \) denotes a measured position and \( x \) denotes a true position.

\[ \hat{x}_\mathrm{Acme} = x_\mathrm{Acme} + \varepsilon_\mathrm{Acme} \]

\[ \hat{x}_\mathrm{GenCom} = x_\mathrm{GenCom} + \varepsilon_\mathrm{GenCom} \]

Here, both \( \varepsilon \) variables are modeled as Gaussian measurement noise with zero mean and covariance according to \( \Sigma_\mathrm{Acme} \) and \( \Sigma_\mathrm{GenCom} \).

::endmath

## Probability of Collision

Now that we've quantified the conjunction point and the measurement uncertainties, we can define spacecraft __probability of collision__.  It turns out, however, that we won't actually care about this probability when we formulate our optimization program.  Rather, we'll care about the __relative position at conjunction__, which is easily determined using orbital dynamics simulation.

::definition[Probability of Collision and Relative Position]

At the conjunction point \( P \), the Acme and GenCom satellites will experience their closest approach, which may involve collision.  At conjunction, we can define as the _b-plane_ the plane perpendicular to the relative velocity between the two satellites.  It is important to observe that, at conjunction, the relative position will lie completely within the b-plane.  In our case, the b-plane is defined by \( y = z = 0 \), because their relative velocity will lie entirely in the \( y \) direction.

The relative position vector \( x_\mathrm{Acme} - x_\mathrm{GenCom} \), in general, has covariance \( \Sigma_\mathrm{Acme} + \Sigma_\mathrm{GenCom} \) assuming the measurement errors are independent.  The covariance of the _projection_ of the relative position vector into the b-plane, then, is

\[ \sigma^2 := \begin{bmatrix} 1 & 0 \end{bmatrix} \left( \Sigma_\mathrm{Acme} + \Sigma_\mathrm{GenCom} \right) \begin{bmatrix} 1 \\ 0 \end{bmatrix} . \]

Suppose collision will occur at conjunction if the two satellites' centers of mass pass within distance \( b \); that is, if the relative position in the b-plane lies between \( \Delta \hat{x} - b \) and \( \Delta \hat{x} + b \), where \( \Delta \hat{x} \) is the difference in measured positions (projected into the b-plane).  We can now work out the probability of collision by integrating the Gaussian PDF over the interval of collision.

\[ \mathbb{P}(\text{collision}) = \int_{x = \Delta \hat{x} - b}^{x = \Delta \hat{x} + b} \frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left( -\frac{x^2}{2\sigma^2} \right) \, \mathrm{d}x \]

Assuming that \( b^2 \) is much smaller than \( \sigma^2 \) (that is, assuming that the measurement error is generally much larger than the size of the satellite itself), then it is safe to take this integral as constant around \( x = \Delta \hat{x} \).

\[ \frac{\mathbb{P}(\text{collision})}{2b} \approx \frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left( -\frac{\Delta \hat{x}^2}{2\sigma^2} \right) \]

Simplifying a bit, we can isolate relative measured position \( \Delta \hat{x} \) in terms of the collision probability.

\[ \ln\left( \frac{\mathbb{P}(\text{collision})}{b} \sqrt\frac{\pi \sigma^2}{2} \right) \approx -\frac{\Delta \hat{x}^2}{2\sigma^2} \]

\[ \therefore \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 \mathbb{P}(\text{collision})^2} \right) \approx \Delta \hat{x}^2 \]

::endmath

## Avoiding Collision

Let's recap what we've done so far.  We've determined a way to compute probability of collision, and we've figured out how to relate that to relative position at conjunction.  Suppose we input our known measurement covariances, and we get an unacceptably high probability of collision (maybe we want \( 10^{-6} \) or less, but we get \( 10^{-4} \), for example).  Put yourself in the shoes of Acme.  Are you about to lose your expensive, extremely sensitive satellite?

Not necessarily.  Let's assume (for convenience of calculation) that you have one opportunity to save your satellite, by burning tangent to your orbit at exactly one half of an orbit before conjunction (namely, at \( \begin{bmatrix} -(R + h) & 0 \end{bmatrix}^\mathrm{T} \)).  However, you want to burn the minimum amount of fuel possible, because fuel is expensive and you want to maximize the lifespan of your satellite (no fuel means no more corrective maneuvers).  We'll also assume that fuel use is monotonically increasing in magnitude of velocity change; more velocity change, more fuel used.  It turns out we can relate velocity change to changes in the satellite's orbit using an important result from orbital mechanics: the Vis-Viva equation.

::theorem[Vis-Viva Equation]

Assume an object of mass \( m \) is orbiting a central body with mass \( M \gg m \) in an elliptical orbit with semimajor axis \( a \).  Then, when the body is a distance \( r \) from the center of the central body, the orbital velocity of that body is

\[ v = \sqrt{ G M \left( \frac{2}{r} - \frac{1}{a} \right)} \]

where \( G \) is the universal constant of gravitation.

::endmath

From Vis-Viva, we know that initially, the semimajor axis of the spacecraft's orbit is

\[ a = \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-1} . \]

What happens we expend \( \Delta m \) of fuel by burning prograde (in the direction of our orbit)?  We'll pick up an extra velocity \( u \) and our orbit will cease to be a circle; instead, the point of burn will become __perigee__ (closest point to Earth) and the point exactly one half of an orbit later will become __apogee__ (farthest point from Earth).  This is why we are choosing to burn half of an orbit early; determining altitude at apogee is far easier than determining altitude in general for non-circular orbits.  The semimajor axis \( a \) is related to the radius at apogee \( r_a \) and the radius at perigee \( r_p \) like so.

\[ 2a = r_a + r_p \]

From this, we know that the new radius at apogee, after our corrective maneuver to avoid GenCom's satellite, looks like

\[ \begin{align*} r_a &= 2a - r_p \\ &= 2 \left( \frac{2}{R + h} - \frac{(v + u)^2}{GM} \right)^{-1} - (R + h) \end{align*} . \]

For small \( u \), we'll take a first-order Taylor series approximation to this, which will make our calculations later much easier.

\[ r_a \approx (R + h) + \frac{4v}{GM} \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-2} u \]

## Formulating the Optimization

One more time: let's recap.  We know how to compute probability of collision from relative position at conjunction, and vice versa.  We also know how to compute Acme's position at conjunction based on fuel used.  We can now put these results together.  First, we'll set a criterion \( \mathbb{P}(collision) \le p \), for some user-defined \( p \).  The GenCom satellite, at conjunction, will be at altitude \( h \) as usual.  The Acme satellite, however, will perform a maneuever one half of an orbit early, and its new altitude will be

\[ h_\mathrm{Acme} \approx h + \frac{4v}{GM} \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-2} u . \]

This tells us that the relative position at conjunction will be approximately

\[ \Delta \hat{x} \approx \frac{4v}{GM} \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-2} u . \]

Remember our relationship for probability of collision and relative position at conjunction?

\[ \Delta \hat{x}^2 \approx \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 \mathbb{P}(\text{collision})^2} \right) \]

We're actually going to convert this into an inequality, which will make optimization easier.  For a given \( p \), we want \( \Delta \hat{x} \) to be _at least_ the square root of the right-hand side, though of course it's also fine if it's larger than that (being farther away will mean _even lower_ probability of collision).

\[ \Delta \hat{x}^2 \ge \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 p^2} \right) \]

Using our approximation above,

\[ \left( \frac{4v}{GM} \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-2} \right)^2 u^2 \ge \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 p^2} \right) . \]

Woah.  Let's digest this.  We have a relationship between known variables, our decision variable \( u \) (how much velocity we're going to add), and our maximum allowed probability of collision \( p \).  We'll simplify this to

\[ u^2 \ge \frac{G^2 M^2}{16 v^2} \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 p^2} \right) \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-1} . \]

Our objective is rather simple: we just want to minimize the amount of velocity change (positive or negative), which in turn minimizes fuel used.  In all its glory then, here is our optimization program.

\[ \begin{align*} P: \min_u u^2 & \\ \text{subject to } u^2 &\ge \frac{G^2 M^2}{16 v^2} \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 p^2} \right) \left( \frac{2}{R + h} - \frac{v^2}{GM} \right)^{-1} \end{align*} \]
