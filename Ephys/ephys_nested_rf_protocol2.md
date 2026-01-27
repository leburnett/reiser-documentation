---
title: Protocol 2
parent: Nested RF Protocol
has_children: true
has_toc: true
nav_order: 70
layout: home
---


## Protocol 2 (P2)

- <b>Aim 1:</b> Determine higher resolution features of the cell's receptive field by using smaler flashes.
- <b>Aim 2:</b> Determine whether the cell displays directionally selective responses to bar sweeps in 16 directions. 

__________________________________________________________________________________________________


1. TOC
{:toc}

__________________________________________________________________________________________________


- <b>Overview:</b>
- Longer, high resolution probing of the cell's receptive field.
- Custom script design. 
- Opens a pop-up at the beginning that asks the user to fill in the `peak_frame` from P1 and the side of the arena used for P1. 
- This `peak_frame` value is then used to generate a protocol with the stimuli centred on the centre of the flash that elicited the greatest response in P1.
- These stimuli are presented within a 30 x 30 pixel area. The rest of the arena is set to the background intensity value.
- Only presents either dark or light stimuli. However, at the end of the protocol the `peak_frame` value that generates the protocol at the same location with the inverse contrast is returned so that the protocol can be run twice, once for each contrast if desired. 

- Location: P2 is made de novo every time the function `generate_protocol2()` is run. A new folder of the format 'yyyy_MM_dd_HH_mm' is made within the the folder 'C:\matlabroot\G4_Protocols\nested_RF_protocol2' that contains both the patterns, functions and experiment file `currentExp.mat` and the data that was recorded in the `Log` file. 

_______________________________

### P2 protocol (Dec 2024 - Jan 2025) - RNAi experiments

- Area of arena presented: [30 x 30 pixel area]
- Background intensity: (6/15) - gs_val = 4.
- Number of repetitions: 3
- Only ONE contrast - either ON (15/15) or OFF (0/15)
- Square flashes presented on 50% overlapping grid.

Sequence of stimuli in the protocol:
- 4 pixel square flashes - 160ms duration - 340ms interval
- 4 pixel square flashes - 80ms duration - 170ms interval
- 4 pixel wide bar sweeps - 28 dps
- 4 pixel wide bar sweeps - 56 dps

[<b>Note for LEB.</b> Results file: "Spring2025_RNAi_Protocol2_Analysis". Data: 2024_12_12 to 2025_01_23. See the file "RNAi_exp_log".]

![Example polar plot of bar sweep responses in a control RNAi fly to P2 in Dec 2024.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0005.png){:standalone .ifr_center}
![Example receptive field analysis to 4 pixel square flashes in the same fly as the polar plot above.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0006.png){:standalone .ifr_center}

_______________________________

### P2 protocol (April 2025 - May 2025) - TmY3, TmY18, TmY5a, Tm5Y

- Area of arena presented: [30 x 30 pixel area]
- Background intensity: (6/15) - gs_val = 4.
- Number of repetitions: 3
- Only ONE contrast - either ON (15/15) or OFF (0/15)
- Square flashes presented on 50% overlapping grid.

Sequence of stimuli in the protocol:
- 10s background at the start and between repetitions (added 2025_05_06 onwards)
- 4 pixel square flashes - 160ms duration - 340ms interval
- 4 pixel square flashes - 80ms duration - 170ms interval
- 4 pixel wide bar sweeps - 28 dps
- 4 pixel wide bar sweeps - 56 dps

[<b>Note for LEB.</b> Results file: "Exp_Log_NestedRF_v2". Data: 2025_04_08 to 2025_05_09]

_______________________________

### P2 protocol (July 2025 - Sep 2025) - T4/T5 experiments - SUMMER

- Area of arena presented: [30 x 30 pixel area]
The 6 x 6 pixel flashes are presented in a 33 x 33 pixel square area - larger than the 30 x 30 pixel square area for the 4 x 4 pixel flashes - to get an even number of flashes on a 50% overlapping grid.
- Background intensity: (4/15) - gs_val = 4.
- Number of repetitions: 3
- Only ONE contrast - either ON (15/15) or OFF (0/15)
- Square flashes presented on 50% overlapping grid.
- 1s interval between each bar sweep

Sequence of stimuli in the protocol:
- 10s background at the start and between repetitions 
- 4 pixel square flashes - 160ms duration - 440ms interval
- 6 pixel square flashes - 160ms duration - 440ms interval
- 4 pixel wide bar sweeps - 28 dps
- 4 pixel wide bar sweeps - 56 dps

[<b>Note for LEB.</b> Results file: "Summer2025_MARCM_p2_analysis". Data: 2025_07_12 to 2025_09_12]

_______________________________

### P2 protocol (Oct 2025 - Nov 2025) - T4/T5 experiments - AUTUMN

- Area of arena presented: [30 x 30 pixel area]
The 6 x 6 pixel flashes are presented in a 33 x 33 pixel square area - larger than the 30 x 30 pixel square area for the 4 x 4 pixel flashes - to get an even number of flashes on a 50% overlapping grid.
- Background intensity: (4/15) - gs_val = 4.
- Number of repetitions: 3
- Only ONE contrast - either ON (15/15) or OFF (0/15)
- Square flashes presented on 50% overlapping grid.
- 1s interval between each bar sweep

Sequence of stimuli in the protocol:
- 10s background at the start and between repetitions 
- 3s background interval between square flashes and sweeps, between sweep speeds and between bar flash speeds. (Added 2025_10_21).
- 4 pixel square flashes - 160ms duration - 440ms interval
- 6 pixel square flashes - 160ms duration - 440ms interval
- 4 pixel wide bar sweeps - 28 dps
- 4 pixel wide bar sweeps - 56 dps
- <b>4 pixel wide bar sweeps - 168 dps</b>
- <b>4 pixel wide bar flashes - 80ms duration - 920ms interval</b>
- <b>4 pixel wide bar flashes - 14ms duration - 486ms interval</b>

The bar flashes are presented in different random orders for each repetition.
The bar flash stimuli contains 11 different positions. 
From 2025_10_15 - 2025_10_23, the "central" bar flash is positioned in the middle of the 30 x 30 pixel area, then the 5 positions either side are this bar moved by 1 pixel increments and decrements from this position in the 8 different orientations.
From 2024_10_23 onwards, these 5 other positions are the central bar moved by 2 pixel increments and decrements. 

[<b>Note for LEB.</b> Results file: "Autumn2025_MARCM_p2_analysis". Data: 2025_10_15 to 2025_11_17]

![Bar flash stimuli examples showing the 11 different positions for the 8 different orientations.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0003.png){:standalone .ifr_center}

![Example bar flash stimuli analysis. Timeseries are plotted for the responses to each flash. The coloured squares in the top row correspond to the colours of the bars in the images in the furthest left column. Left column contains an image of all 11 bars of that orientation overlaid. This example was made for the bar flashes that were shifted by 1 pixel steps.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0004.png){:standalone .ifr_center}

_______________________________

### P2 protocol (Nov 2025 - Dec 2025) - T4/T5 pharmacology experiments

- Area of arena presented: [30 x 30 pixel area]
- Background intensity: (4/15) - gs_val = 4.
- Number of repetitions: 3
- Only ONE contrast - either ON (15/15) or OFF (0/15)
- 1s interval between each bar sweep
- NO SQUARE PIXEL FLASHES PRESENTED IN P2.

Sequence of stimuli in the protocol:
- 10s background at the start and between repetitions 
- 3s background interval between sweep speeds and between bar flash speeds. 
- 4 pixel wide bar sweeps - 28 dps
- 4 pixel wide bar sweeps - 56 dps
- 4 pixel wide bar sweeps - 168 dps
- <b>4 pixel wide bar sweeps - 250 dps</b>
- <b>4 pixel wide bar sweeps - 500 dps</b>
- 4 pixel wide bar flashes - 80ms duration - 920ms interval
- 4 pixel wide bar flashes - 14ms duration - 486ms interval

There are 88 bar flash stimuli. 8 different orientations. Bar centred on the 30 x 30 pixel square and then moved by 2 pixel steps in either direction along this axis.

[<b>Note for LEB.</b> Results file: "Autumn2025_T4T5_Pharma". Data: 2025_11_18 to 2025_12_22]

_______________________________

![Example polar plot of a T4 cell after Octopamine application showing the responses to the 5 different bar sweep speeds in the P2 version used in Dec 2025.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0007.png){:standalone .ifr_center}
