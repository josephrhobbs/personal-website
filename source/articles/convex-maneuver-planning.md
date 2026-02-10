# Maneuver Planning

~

::byline[Joseph Hobbs][Feburary 10, 2026]

Recently, I've taken a great interest in the intersection of probability theory, optimization, and optimal control.  A recent paper by Z. Manchester's lab of MIT (formerly CMU), "Convex Maneuver Planning for Spacecraft Collision Avoidance" by F. Vega et al., found [here](https://roboticexplorationlab.org/projects/cvx_cola.html), caught my attention recently because it unifies optimal control and probability in the wonderfully fascinating (though incredibly harsh) environment of Earth orbit.  Here, I unpack the paper's main point by presenting a _highly_ simplified example of the methodology presented.

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

Now that we've quantified the conjunction point and the measurement uncertainties, we can define spacecraft __probability of collision__.

::definition[Probability of Collision and Relative Position]

At the conjunction point \( P \), the Acme and GenCom satellites will experience their closest approach, which may involve collision.  At conjunction, we can define as the _b-plane_ the plane perpendicular to the relative velocity between the two satellites.  It is important to observe that, at conjunction, the relative position will lie completely within the b-plane.  In our case, the b-plane is defined by \( y = z = 0 \), because their relative velocity will lie entirely in the \( y \) direction.

The relative position vector \( x_\mathrm{Acme} - x_\mathrm{GenCom} \), in general, has covariance \( \Sigma_\mathrm{Acme} + \Sigma_\mathrm{GenCom} \) assuming the measurement errors are independent.  The covariance of the _projection_ of the relative position vector into the b-plane, then, is

\[ \sigma^2 := \begin{bmatrix} 1 & 0 \end{bmatrix} \left( \Sigma_\mathrm{Acme} + \Sigma_\mathrm{GenCom} \right) \begin{bmatrix} 1 \\ 0 \end{bmatrix} . \]

Suppose collision will occur at conjunction if the two satellites' centers of mass pass within distance \( b \); that is, if the relative position in the b-plane lies between \( \Delta \hat{x} - b \) and \( \Delta \hat{x} + b \), where \( \Delta \hat{x} \) is the difference in measured positions (projected into the b-plane).  We can now work out the probability of collision by integrating the Gaussian PDF over the interval of collision.

\[ \mathbb{P}(\text{collision}) = \int_{x = \Delta \hat{x} - b}^{x = \Delta \hat{x} + b} \frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left( -\frac{x^2}{2\sigma^2} \right) \, \mathrm{d}x \]

Assuming that \( b^2 \) is much smaller than \( \sigma^2 \) (that is, assuming that the measurement error is generally much larger than the size of the satellite itself), then it is safe to take this integral as constant around \( x = \Delta \hat{x} \).

\[ \frac{\mathbb{P}(\text{collision})}{2b} \approx \frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left( -\frac{\Delta \hat{x}^2}{2\sigma^2} \right) \]

Simplifying a bit, we can isolate relative measured position \( \Delta \hat{x} \) in terms of the collision probability.

\[ \therefore \ln\left( \frac{\mathbb{P}(\text{collision})}{b} \sqrt\frac{\pi \sigma^2}{2} \right) \approx -\frac{\Delta \hat{x}^2}{2\sigma^2} \]

\[ \therefore \sigma^2 \ln\left( \frac{2 b^2}{\pi \sigma^2 \mathbb{P}(\text{collision})^2} \right) \approx \Delta \hat{x}^2 \]

::endmath

::notice[More coming soon!]
