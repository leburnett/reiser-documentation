---
title: Freely-walking
has_children: true
has_toc: true
nav_order: 3
permalink: /Freely-walking/
---

1. TOC
{:toc}

Here is some general documentation for the freely-walking arena setup that was used to run the "Freely walking course control mechanisms screen" in 2025. This documentation includes information on how to design and run protocols, analyse the data, as well as the specifications of the arena used in experiments. 

For the sake of clarity, this documentation will centre on how to run and analyse the specific protocol that was used in the screen experiments (`protocol_27.mat`). Other protocols that were run on this arena can be found within the `protocols` [folder](https://github.com/leburnett/freely-walking-optomotor/tree/main/protocols) of the repository, but they are not documented here.

## Rig specificiations
These protocols are designed to run on the Reiser Lab's G3 18 x 3 LED panel setup.

[0000 - PNG of setup]

- 18 panel circumeference.
- 3 panel height. 
- Each panel is 8 x 8 pixels, so the arena is 18 x 8 = 144 pixels wide and 3 x 8 = 24 pixels high.
- Each pixel is 1.875 degrees of visual angle per pixel and covers 360 degrees of visual angle along the azimuth and 45 degrees of visual angle along the elevation.
- The LEDS are green LEDs with a peak wavelength of ~570 nm. 

There is a lot of useful, and more detailed documentation on the specifications of the G3 arena and how to design and run protocols [here](https://reiserlab.github.io/Modular-LED-Display/Generation%203/Software/docs/g3_user-guide.html).  

## Designing and running a protocol

Patterns for the G3 arena can be generated using the `G4_pattern_generator_gui`, but for this screen all patterns and function were made from scratch using custom scripts and the protocols themselves are run through custom scripts that present the patterns using the `panel_com` class of functions from the `G4_Display_Tools` repository.

The scripts for making the different patterns can be found within the repository [here](https://github.com/leburnett/freely-walking-optomotor/tree/main/script_to_make_patterns). 

The scripts for the protocols themselves can be found within the repository [here](https://github.com/leburnett/freely-walking-optomotor/tree/main/protocols). This folder contains a [subfolder](https://github.com/leburnett/freely-walking-optomotor/tree/main/protocols/protocol_functions) which contains functions that are required to run the protocols. 

## Analysing the data