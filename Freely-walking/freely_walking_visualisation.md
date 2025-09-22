---
title: Freely-walking-visualisation
parent: Freely-walking
has_children: true
has_toc: true
nav_order: 30
layout: home
---

1. TOC
{:toc}

# `generate_circ_stim_ufmf`

This function can be used to generate .mp4 videos of each individual condition within an experiment. These videos contain the behavioural video of the flies, recorded in IR, with the visual stimulus displayed around the outside of this circular image. 2s trajectories of the flies are superimposed on to the image and only every other frame from the behavioural video is used so the videos are 2x the speed of real time.

It should be run within each experiment's directory - for instance: "/Users/burnettl/Documents/Projects/oaky_cokey/data/2025_04_18/protocol_27/2575_LPC1_shibire_kir/F/15_58_42". In order to work, inside this directory there should be:
- the .ufmf video of the entire experiment.
- the .mat LOG file. 
- a directory containing the 'trx.mat' file containing the output from FlyTracker.

It also requires the JAABA repository to be downloaded and saved locally on the computer.
A folder containing the patterns used within the experiments should also be available since these videos used the metadata from the experiment to open the exact pattern used and use that to generate the stimulus pattern within the video. 

If no inputs are used when running the function, then the function defaults to generating the stimulus videos for all conditions within the experiment. Otherwise, if an array is inputted then only videos for those conditions will be made.

[Fig. X] - Screenshot of a single frame of this stim-cond video. 


## Detailed description of how this script runs:

Requires LOG, ufmf video, trx 

Logged during the experiment - the frame numbers at the beginning and end of each condition, the pattern used for each condition. 
These are then used to open the appropriate pattern from within the "pattern_optomotor" folder. 
At the moment, the speed is not linked to the actual speed of the experiment.
These videos are 2x real time. Only every other frame of the original video is used. 

This function then calls `create_stim_video_loop.m` ["plotting_functions/videos"]. 

Things that need to be updated if run on a different computer:
- Path to the patterns. 
- Path to the JAABA repository.
- Output directory.

