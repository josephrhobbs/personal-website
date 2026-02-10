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

We take an Earth-centered inertial reference frame.  The equatorial plane, given by \( z = 0 \), contains the orbits of both the Acme and GenCom satellites.  We will call the __conjunction point__ \( P \) the point \( \begin{bmatrix} R + h & 0 \end{bmatrix}^\mathrm{T} \end{bmatrix} \).  At a defined time in the near future, both the Acme and GenCom satellites will pass through \( P \).

::endmath

::notice[Under construction!]
