# RSVLM

~

In the fall of my junior year of college, I had the privilege of taking MIT's undergraduate aerodynamics course (known to my fellow students simply as 16.100 or "sixteen one hundred") taught by MIT Professor Qiqi Wang.

During the course, we learned about models for aircraft drag, and a significant portion of the course was dedicated to the study of inviscid models of induced drag based on a vortex lattice model.  For this purpose, we made extensive use of AVL (Athena Vortex Lattice), a program developed about 25 years ago by MIT Professor Mark Drela.

Intrigued by this approach, I decided I wanted to write my own program for analyzing the vorticity around an aircraft wing in order to learn more about the internal processes required.  Over the course of two or three days, after investigating the mathematical model required, I developed the bulk of this program in the Rust programming language, and RSVLM was born.

## Inspiration

RSVLM was inspired by Prof. Wang's excellent aerodynamics course, as well as the [AVL](https://web.mit.edu/drela/Public/web/avl/) software developed by MIT Professor Mark Drela.  AVL stands for Athena Vortex Lattice, and it uses a vortex lattice model to calculate the aerodynamic performance of aircraft in the incompressible regime.

## Mathematical Model

The mathematical model used by RSVLM is based on an incompressible, inviscid horseshoe vortex lattice.  It models the wing of an aircraft as a collection of panels and associated vortex filaments dissipating vorticity into the downstream air.  RSVLM calculates the strength and direction of each vortex filament in order to determine the aerodynamic pressure on each wing panel and the overall coefficients of lift and drag.

## What's in a Name?

RSVLM is a simple acronym constructed from both the program's constitution and its purpose.  I derived RS from the name of the Rust programming language in which the program is written, and I derived VLM from Vortex Lattice Model, which descibes the purpose of the program.

## Source Code

The source code for RSVLM is open and available on GitHub, and its source code is licensed under the MIT License.

[https://github.com/josephrhobbs/rsvlm](https://github.com/josephrhobbs/rsvlm)

## Credits

Thanks to MIT Professor Qiqi Wang for teaching vortex lattice models in 16.100.

Thanks to MIT Professor Mark Drela for writing and documenting AVL, which inspired RSVLM.