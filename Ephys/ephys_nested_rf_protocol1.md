---
title: Protocol 1
parent: Nested RF Protocol
has_children: true
has_toc: true
nav_order: 60
layout: home
---

## Protocol 1 (P1)

Designed to be quick - this protocol takes between 6-7.5 minutes depending on the version used.

- <b>Aim 1:</b> Find which flash location elicits the greatest response.
- <b>Aim 2:</b> Determine whether the cell shows a preferred contrast to dark or light flashes.
Use this location and preferred contrast to create and run protocol 2 (P2). 

__________________________________________________________________________________________________

1. TOC
{:toc}
__________________________________________________________________________________________________

<b>Overview:</b><br>
Flickering squares of two different sizes (12 x 12 pixels and 6 x 6 pixels) are presented on one half of the arena screen (either left or right half). Both dark and bright squares are presented in an alternating order. The order of presentation is designed to avoid consecutive flashes appearing close enough to each other that they would activate the same cell's RF. These stimuli are repeated 4 times.

<b>Location:</b> The current most-up-to-date version of P1 can be found within the `nested_RF_stimulus` GitHub repository in `protocols/bkg4/LHS` and `protocols/bkg4/RHS` folders.
<br><b>Intensity values:</b> These protocols have a background pixel intensity value of 4 (out of 15), dark stimuli have a pixel value of 0 and bright stimuli have a pixel value of 15.
<br><b>Stimulus parameters:</b> Each protocol consists of both dark and bright flashing squares of 12 x 12 pixel size and then 6 x 6 pixel size that are presented on a non-overlapping grid on one half of the arena screen. One half of the arena relates to an area of 6 x 3 panels (16 x 6 = 96 pixels wide, 16 x 3 = 48 pixels high). In the G4 ephys LED panel setup each pixel is 1.25 degrees of visual anlge per pixel. So, a 12 pixel square is 15 degrees of visual angle, and a 6 pixel square is 7.5 degrees of visual angle. Each flash is presented for 200ms with an inter-flash interval of 150ms.
<br><b>Protocol design:</b> The protocol starts with 5s of a full field greyscale frame at the background value intensity for 5s, then runs through the larger 12 x 12 pixel flashes first, then the smaller 6 x 6 pixel flashes. The order in which the flashes are presented is not random, but was designed to avoid consecutive flashes appearing close enough to each other that they would activate the same cell's RF. These stimuli (5s static grey + 12 pixel bright and dark flashes + 6 pixel bright and dark flashes) are repeated 4 times.

![Quadrant spatial organisation of flash presentation. Colourscale is the frame number. So flashes are presented from blue to yellow.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0001.png){:standalone .ifr .pop}

<br><b>Flash presentation:</b> The flashes are presented so that dark and light flashes are shown alternately. To try and explain how the flashes are presented: the screen was divided into 4 quadrants, then a dark flash is presented in the lower left corner of the top left quadrant, then a light flash in the lower left corner of the top right quadrant, then a dark flash in the lower left corner of the bottom left quadrant, and finally a light flash in the lower left corner of the bottom right quadrant. This is then repeated for the adjacent flash position in each quadrant, and repeats until both dark and light flashes have been presented in all positions on the screen.
<br>

_____________________________________________________________

### P1 protocol (Dec 2024 - January 2025) - RNAi experiments

- Area of arena presented: Left half of the arena screen (LHS). 17:112 pixels in x (width) and 1:48 pixels in y (height). [96 x 48 pixels area]
- Background intensity: (6/15) - gs_val = 4.
- Number of repetitions: 4
- Flash sizes: 12 x 12 pixels and 6 x 6 pixels
- Flash contrasts: both ON (15/15) and OFF (0/15)
- Flash duration: 200ms
- Flash overlap: 0% (non-overlapping grid)
- Interval between flashes: 50ms
- Location: `protocols/LHS` within the `nested_RF_stimulus` GitHub repository.
- Protocol: "protocol1_10kHz_4reps_12px_6px_LHS_2sbkg_200msfl_50msint_12-13-24_14-33-03"

[<b>Note for LEB.</b> Results file: "Spring2025_RNAi_Protocol2_Analysis". Data: 2024_12_12 to 2025_01_23. See the file "RNAi_exp_log".]

_______________________________________________________________

### P1 protocol (April 2025 - May 2025) - TmY3, TmY18, TmY5a, Tm5Y

- Area of arena presented: Right half of the arena screen (LHS). 97:196 pixels in x (width) and 1:48 pixels in y (height). [96 x 48 pixels area]
- Background intensity: (6/15) - gs_val = 4.
- Number of repetitions: 4
- Flash sizes: 12 x 12 pixels and 6 x 6 pixels
- Flash contrasts: both ON (15/15) and OFF (0/15)
- Flash duration: 200ms
- Flash overlap: 0% (non-overlapping grid)
- Interval between flashes: 50ms
- Location: `protocols/RHS` within the `nested_RF_stimulus` GitHub repository.
- Protocol: "protocol1_10kHz_4reps_12px_6px_RHS_2sbkg_200msfl_50msint_04-08-25_08-08-42" and "protocol1_10kHz_4reps_12px_6px_RHS2_2sbkg_200msfl_50msint_81_180_05-05-25_16-18-66"

[<b>Note for LEB.</b> Results file: "Exp_Log_NestedRF_v2". Data: 2025_04_08 to 2025_05_09]

_______________________________________________________________

### P1 protocol (July 2025 - Nov 2025) - T4/T5 experiments

- Area of arena presented: Left half of the arena screen (LHS). 17:112 pixels in x (width) and 1:48 pixels in y (height). [96 x 48 pixels area]
- Background intensity: (4/15) - gs_val = 4.
- Number of repetitions: 4
- Flash sizes: 12 x 12 pixels and 6 x 6 pixels
- Flash contrasts: both ON (15/15) and OFF (0/15)
- Flash duration: 200ms
- Flash overlap: 0% (non-overlapping grid)
- Interval between flashes: 150ms
- Location: `protocols/bkg4/LHS` within the `nested_RF_stimulus` GitHub repository.
- Protocol: "protocol1_10kHz_4reps_12px_6px_LHS_2sbkg_200msfl_150msint_07-10-25_15-45-60"

[<b>Note for LEB.</b> Results file: "Summer2025_MARCM_p2_analysis" and "Autumn2025_MARCM_p2_analysis". Data: 2025_07_12 to 2025_11_13]

__________________________________________________________________

### P1 protocol (Sep 2025 - Dec 2025) - pharmacology experiments

- Area of arena presented: Left half of the arena screen (LHS). 17:112 pixels in x (width) and 1:48 pixels in y (height). [96 x 48 pixels area]
- Background intensity: (4/15) - gs_val = 4.
- Number of repetitions: 4
- Flash sizes: 6 x 6 pixels
- Flash contrasts: both ON (15/15) and OFF (0/15)
- Flash duration: 200ms
- Flash overlap: 0% (non-overlapping grid)
- Interval between flashes: 150ms
- Location: `protocols/bkg4/LHS` within the `nested_RF_stimulus` GitHub repository.
- Protocol: "protocol1_10kHz_4reps_6pxONLY_LHS_2sbkg_200msfl_150msint_11-14-25_13-47-30"

[<b>Note for LEB.</b> Results file: "Autumn2025_T4T5_Pharma". Data: 2025_11_18 to 2025_12_22]

__________________________________________________________________

![Example plots that are generated after running protocol 1.They show the responses of the cell to 6 pixel square flashes being presented at different locations on the screen. The location of each subplot corresponds to the actual location of the flash on the arena from the fly's perspective. Thinner lines show the responses to each repetition and the thicker line shows the mean across repetitions. The plots show the responses to light and dark flashes separately. The number above each subplot is the frame number within the pattern that contains the flash in that location. The number above the subplot with the largest response should be entered when running `generate_protocol2()`.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0002.png){:standalone .ifr_center}
