# ADCS

~

::byline[Joseph Hobbs][February 20, 2026]

In the spring of 2026, I began following a course offered at MIT in spacecraft attitude determination and control (known in those parts as 16.S897 or "sixteen S eight nine seven").  The subject covers a variety of topics, including fundamental topics like rigid-body mechanics, applied topics like algorithms for spacecraft attitude control, and more theoretical concepts such as solutions to Wahba's problem (a well-known mathematical problem).  A classic problem covered by the course is __spacecraft tumbling__... many times throughout the history of spaceflight, engineers struggled to keep their spacecraft pointing in the direction they want, and the craft began to tumble uncontrollably.  This has led to loss of mission on several occasions, although fortunately, this particular problem has never led to loss of life.

A fun fact is that, in 1966, N. Armstrong and D. Scott were nearly killed in a violent uncontrolled tumble during the [Gemini VIII](https://www.nasa.gov/mission/gemini-viii/) mission.  Through quick thinking and skilled piloting, Armstrong regained attitude control, though the mission was aborted and both astronauts were returned to Earth immediately after the incident.  The Gemini VIII capsule was in such a violent tumble that Armstrong and Scott had precious seconds to act... any delay would have invariably result in loss of consciousness and potentially even brain hemorrhage.

I've always found throughout my education that I gain a new perspective on a phenomenon when I simulate it numerically.  Because of this, I began writing a very simple software package for simulating rigid-body dynamical systems in Python.  Because I hope to use this package in the near future to simulate the attitude determination and control system (ADCS) of a spacecraft, I fittingly (though admittedly a bit uncreatively) named the software package __ADCS__.

## Features

::notice[Under construction!]

## Source Code

The Rust source code of ADCS is completely open-source and licensed under the MIT License.  Source code is available on GitHub.

[josephrhobbs/adcs](https://github.com/josephrhobbs/adcs)

## Credits

Thanks to MIT Professor Zachary Manchester for teaching 16.S897, an excellent course on attitude determination and control.  Manchester has generously made the lecture videos for the course publicly available on YouTube at [@roboticexplorationlab](https://www.youtube.com/@roboticexplorationlab).  He has also posted lecture notes, homework assignments, and simulation code in Julia on GitHub at [zacmanchester/spacecraft-attitude-course](https://github.com/zacmanchester/spacecraft-attitude-course/).
