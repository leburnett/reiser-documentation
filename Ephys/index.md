---
title: Ephys
has_children: true
has_toc: false
nav_order: 2
layout: home
---

1. TOC
{:toc}

Here is some general documentation for the Ephys setup. This includes information on how to design and run protocols, as well as the specifications of the arena used in experiments.

## Rig specificiations
These protocols are designed to run on the Reiser Lab's G4 ephys LED panel setup.

[PNG of setup]

- 18 panel circumference area. However, there is only space for 12 panels on the arena circuit board and in our setup the leftmost panel is not used, so there are 11 panels in total. 
- Since this is a G4 (4th generation)setup, each panel is 16 x 16 pixels, so the arena is 12 x 16 = 192 pixels wide and 3 x 16 = 48 pixels high.
- Each pixel is 1.25 degrees of visual angle per pixel, so the arena is 240 degrees wide and 60 degrees high.
- The arena can be tilted in elevation depending on how the fly is positioned in the rig.
- The LEDS are green LEDs with a peak wavelength of (XX nm). 

___________________________________________________________________________________________________________________________________________________________________________________________

There are different protocols that can be run on the Ephys setup. This website contains documentation on the following protocols:
- nested_RF_stimulus protocol
- DS_Probe_protocol

## Designing and running a protocol

Protocols to be run on the G4 ephys arena can be designed in two ways. Through the in-built G4 GUIs or through custom scripts.

The G4 GUIs are designed to be user-friendly and allow for the generation of patterns, position functions, and experiment designs without needing to write code.
The full documentation can be found at https://reiserlab.github.io/Modular-LED-Display/G4/. 
The code for the GUI can be found here: https://github.com/JaneliaSciComp/G4_Display_Tools. 
- Generate patterns in the `G4_pattern_generator_gui`.
- Generate position functions in the `G4_function_generator_gui`.
- Design the experiment in the `G4_experiment_designer`. 
- Run the experiment in the `G4_experiment_conductor`.

A detailed description of the patterns, functions and the experiment design for each protocol can be found within the protocol's section of this documentation.

## Analysing the data

After running a protocol, either through the GUI or through the custom scripts, a 'Log' file is generated that contains the electrophysiology data and the frame position data. The rate at which both of these types of data are acquired is set in the `G4_experiment_designer` GUI or in the custom scripts. For these ephys protocols, both the electrophysiology data and the frame position is acquired at 10 kHz. How this data is processed and analysed depends on the protocol that was run and will be described within the relevant sections of this documentation for each protocol. 