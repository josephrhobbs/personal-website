# RSA Keychain

~

This semester (Fall 2025), I am taking an undergraduate course at MIT in digital systems and computer hardware design.  The class is known to students in these parts as 6.2050 ("six two oh five oh") or among friends just as "two oh five".  The class focuses on digital systems design in SystemVerilog, a hardware description language used in the industry to design and verify digital circuits.  Throughout the class, we have been using Xilinx ("zy-links") Spartan 7 field-programmable gate arrays (FPGAs) in order to test our designs.  So far in lab, we've designed circuits to process 8-bit audio, generate HDMI video signals, and perform real-time image processing.

For our final project, my friend David proposed to me an RSA cryptographic hardware accelerator.  This device would connect to a personal computer to conduct real-time, asymmetric encryption.  We decided on this because asymmetric encryption in real time is very difficult due to its computationally intensive nature.  By creating specialized computer hardware capable of performing encryption and decryption in real time, we believe our approach has a strong advantage over software-based solutions.  For our encryption algorithm, we selected RSA, a common asymmetric-key cryptosystem that would be relatively easy to implement in hardware.

Because we are creating a piece of hardware that can "lock" and "unlock" secure messages, we have decided to refer to our project as an "RSA keychain".  This page will be updated as the project progresses... we began the project in late October and we expect to be complete by mid-December.

## System Architecture

The below block diagram represents a high-level overview of our project.  We plan to make the key and message sizes parametric, so we can change them throughout the design process without affecting the overall system architecture.  The bulk of the work will be performed by the encryption/decryption block, which will perform the calculations necessary to encrypt and decrypt messages using the RSA algorithm.

::image[RSA Keychain Block Diagram][/media/rsa-block-diagram.png]

An important note is that the RSA secret key is stored on the keychain hardware and is not accessible to the device to which it is connected.  We intentionally designed the keychain in this manner to maximize the security surrounding the secret key and ensure that it cannot be accessed by means of hardware vulnerabilities, such as Meltdown or Spectre.

More information coming soon!

## Credits

Thanks to my project partner and my friend, David Choi, for originally conceiving of this idea and for all of his contributions to the project.  This project could not exist without his hard work and dedication.