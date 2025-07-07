# Overview
This repository contains the code to generate the documentation website (https://leburnett.github.io/reiser-ephys-documentation). This documentation describes how to run electrophysiological experiments on the G4 ephys setup at HHMI's Janelia Research Campus. 

### Hardware:
Generation 4 Modular LED Display designed by Reiser lab members. Detailed documentation can be found at https://reiserlab.github.io/Modular-LED-Display/G4/. 

### Software: 
Presenting stimuli to the G4 arena requires a local copy of the G4_Display_Tools repository (https://github.com/leburnett/G4_Display_Tools).

### Experimental protocols:
Code for running different experimental protocols can be found in different Github repositories. The code found in these repositories contain a mixture of code that works using the G4 software tools (see link above) that run within a GUI, and custom scripts that work through the command line in MATLAB. 

- 1: [Direction selectivity probe protocol]
- 2: [Nested receptive field protocol]

[Direction selectivity probe protocol]: https://github.com/leburnett/DS_probe_protocol
[Nested receptive field protocol]: https://github.com/leburnett/nested_RF_stimulus
