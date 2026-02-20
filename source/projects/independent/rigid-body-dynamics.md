# ADCS

~

::byline[Joseph Hobbs][February 20, 2026]

In the spring of 2026, I began following a course offered at MIT in spacecraft attitude determination and control (known in those parts as 16.S897 or "sixteen S eight nine seven").  The subject covers a variety of topics, including fundamental topics like rigid-body mechanics, applied topics like algorithms for spacecraft attitude control, and more theoretical concepts such as solutions to Wahba's problem (a well-known mathematical problem).  A classic problem covered by the course is __spacecraft tumbling__... many times throughout the history of spaceflight, engineers struggled to keep their spacecraft pointing in the direction they want, and the craft began to tumble uncontrollably.  This has led to loss of mission on several occasions, although fortunately, this particular problem has never led to loss of life.

A (not so fun) rather interesting fact is that, in 1966, N. Armstrong and D. Scott were nearly killed in a violent uncontrolled tumble during the [Gemini VIII](https://www.nasa.gov/mission/gemini-viii/) mission.  Through quick thinking and skilled piloting, Armstrong regained attitude control, though the mission was aborted and both astronauts were returned to Earth immediately after the incident.  The Gemini VIII capsule was in such a violent tumble that Armstrong and Scott had precious seconds to act... any delay would have invariably resulted in loss of consciousness and potentially even brain hemorrhage.

I've always found throughout my education that I gain a new perspective on a phenomenon when I simulate it numerically.  Because of this, I began writing a very simple software package for simulating rigid-body dynamical systems in Python.  Because I hope to use this package in the near future to simulate the attitude determination and control system (ADCS) of a spacecraft, I fittingly (though admittedly a bit uncreatively) named the software package __ADCS__.

## Features

Currently, the ADCS software package has the ability to simulate rigid-body rotation (using the Euler equation) with and without external torque.  I have also recently added _Kane damping_, which is a simple model for energy dissipation through fluid slosh, excitation of structural modes, or flexible structures like antennas.

## Simulation Example

Using ADCS, I plan to simulate a few missions notable to the study of attitude determination and control.

### Explorer 1

In 1958, NASA launched the first successful U.S. satellite, named __Explorer 1__.  The spacecraft was designed to spin about its long axis for stability.  However, soon after deployment, the Explorer 1 spacecraft entered an uncontrolled "flat spin", spinning about its major axis and flipping end-over-end.  This unexpected turn of events demonstrated weaknesses in our understanding of classical physics, and later revealed the effects of _energy dissipation_ on the movement of rigid bodies.  Using the ADCS package, I plan to simulate the Explorer 1 capsule's initial rotation and loss of stability due to energy dissipation.

::notice[Coming soon!]

### Gemini VIII

In 1966, N. Armstrong and D. Scott embarked on the Gemini VIII mission to low Earth orbit (LEO).  Armstrong and Scott managed to achieve the first successful docking of two spacecraft in orbit.  However, shortly after, the two docked spacecraft entered an uncontrolled and violent spin, nearly killing the astronauts aboard.  Fortunately, the astronauts regained control of the capsule and performed a controlled reentry shortly after.  Using the ADCS package, I plan to simulate the tumble of Gemini VIII and its quick recovery.

::notice[Coming soon!]

## Source Code

The Rust source code of ADCS is completely open-source and licensed under the MIT License.  Source code is available on GitHub.

[josephrhobbs/adcs](https://github.com/josephrhobbs/adcs)

## Credits

Thanks to MIT Professor Zachary Manchester for teaching 16.S897, an excellent course on attitude determination and control.  Manchester has generously made the lecture videos for the course publicly available on YouTube at [@roboticexplorationlab](https://www.youtube.com/@roboticexplorationlab).  He has also posted lecture notes, homework assignments, and simulation code in Julia on GitHub at [zacmanchester/spacecraft-attitude-course](https://github.com/zacmanchester/spacecraft-attitude-course/).
