# Blotch

~

::author[Joseph R. Hobbs]
::date[February 7, 2026]

At MIT, in between the fall and spring semesters, students may optionally choose to participate in a one-month long "Independent Activities Period" (IAP) during which students can take classes or practical trainings.  During the IAP of my freshman year of college, I had the pleasure of enrolling in the Mobile Autonomous Systems Laboratory (MASLAB).  This occurred during January of 2022, so we referred to this course as MASLAB 2022.

MASLAB is an MIT tradition in which students take one month to build an autonomous robot to play a specific game, typically involving the manipulation of small wooden blocks or balls.  MASLAB 2022 involved the collection of small wooden balls about 2 inches in diameter.

My team and I was given the four weeks of January to design, build, integrate, and test a fully autonomous robot that could identify and collect wooden balls on a playing field.

After the month was complete, our team was very excited and honored to tie for first prize in the MASLAB competition.

## Our Team

Inspired by the innovative robotics company Boston Dynamics, we humorously selected the team name "Boston Statics".

My team members were MIT undergraduates Brian Minnick, Diego Rivero, and Ethan Yang.  Brian took the lead on hardware design and Ethan developed the vast majority of the autonomy stack.

## Our Robot

In line with our humorous selection of team name, we chose the name Blotch for our robot.  We felt it communicated well the hastiness of the engineering that it required as well as the large amount of hot glue that held our robot together.

See below for an image of the final CAD.

::image[Blotch][/media/blotch-example.png]

## Hardware

Our robot's hardware primarily consisted of a front-mounted ball collection mechanism as well as two 3D printed spiral towers in order to store the balls collected.

## Software

Our robot's autonomy stack ran on an Intel NUC, a very small PC that sells for about $200 to $400.  The Intel NUC ran Ubuntu 22.04 LTS, which supported the Robot Operating System 2 (ROS2).

### Computer Vision

While ROS2 provided the overhead for the robot's operations, computer vision was performed by the Open Computer Vision library (OpenCV) running on Python 3 and a simple Logitech webcam.

### Sensor & Actuator Control

Because the Intel NUC does not have input/output (I/O) pins for direct control of peripherals, robotic sensors and actuators (including the drive motors and encoders) were controlled using a Teensy 3.5 microcontroller, which is very similar to an Arduino Nano.

The Teensy 3.5 was connected to the Intel NUC over USB and controlled using a proxy software named TAMProxy (or "Totally A Microcontroller Proxy").  TAMProxy is an open-source program which has been under development specifically by MASLAB instructors for MASLAB students since January of 2016.

The TAMProxy source code is available freely on GitHub at the following link.

[https://github.com/MASLAB/TAMProxy-Firmware](https://github.com/MASLAB/TAMProxy-Firmware)

## MASLAB Website

More information about Blotch can be found on the MIT MASLAB Competitor's Wiki at the link below.

[https://maslab.mit.edu/2022/wiki/team03](https://maslab.mit.edu/2022/wiki/team03)

## Credits

Thanks to MIT students Adi Mehrotra, Fischer Moseley, and John Zhang, among others, for teaching MASLAB 2022 and encouraging our team along the way.

Thanks to MIT undergraduate Adrienne Lai (class of 2025) for organizing the MASLAB team.  Adrienne was unfortunately unable to join the team over January as she had another commitment, but we are still most grateful for her initiative in bringing the team together.

Thanks to my teammates, Brian, Diego, and Ethan, for their constant enthusiasm, energy, and collaboration during the many long days in the machine shop.  Let alone their skill, creativity, perseverance, it was a pleasure to share their mere company on cold mornings and late nights that January. 
