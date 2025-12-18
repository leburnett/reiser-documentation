---
title: Nested RF Protocol
parent: Ephys
has_children: true
has_toc: true
nav_order: 10
layout: home
---

1. TOC
{:toc}

The 'Nested RF Protocol' was designed by LE Burnett in 2024 for patch electrophysiology experiments ran by JY Park. 
It is a multi-step protocol that tries to probe the receptive field (RF) structure of the neuron being recorded. 

It was based upon the protocol used in Gruntman et al. 2019(^ref). 

The code for generating and running these protocols is publicly available [here](https://github.com/leburnett/nested_RF_stimulus)
Running these experiments requires the user to have the 'G4_Display_Tools' [repository](https://github.com/JaneliaSciComp/G4_Display_Tools) downloaded locally too. 

## Protocol 1 (P1)

- Designed to be quick and coarse.
- <b>Aim 1:</b> Find which flash location elicits the greatest response.
- <b>Aim 2:</b> Determine whether the cell shows a preferred contrast to dark or light flashes.
- Use this location and preferred contrast to create and run protocol 2 (P2). 

- <b>Overview:</b>
Flickering squares of two different sizes (12 x 12 pixels and 6 x 6 pixels) are presented on one half of the arena screen (either left or right half). Both dark and bright squares are presented in an alternating order. The order of presentation is designed to avoid consecutive flashes appearing close enough to each other that they would activate the same cell's RF. These stimuli are repeated 4 times.

- Location: The current most-up-to-date version of P1 can be found within the `nested_RF_stimulus` GitHub repository in `protocols/bkg4/LHS` and `protocols/bkg4/RHS` folders.
- Intensity values: These protocols have a background pixel intensity value of 4 (out of 15), dark stimuli have a pixel value of 0 and bright stimuli have a pixel value of 15.
- Stimulus parameters: Each protocol consists of both dark and bright flashing squares of 12 x 12 pixel size and then 6 x 6 pixel size that are presented on a non-overlapping grid on one half of the arena screen. One half of the arena relates to an area of 6 x 3 panels (16 x 6 = 96 pixels wide, 16 x 3 = 48 pixels high). In the G4 ephys LED panel setup each pixel is 1.25 degrees of visual anlge per pixel. So, a 12 pixel square is 15 degrees of visual angle, and a 6 pixel square is 7.5 degrees of visual angle. Each flash is presented for 200ms with an inter-flash interval of 150ms.
- Protocol design: The protocol starts with 5s of a full field greyscale frame at the background value intensity for 5s, then runs through the larger 12 x 12 pixel flashes first, then the smaller 6 x 6 pixel flashes. The order in which the flashes are presented is not random, but was designed to avoid consecutive flashes appearing close enough to each other that they would activate the same cell's RF. These stimuli (5s static grey + 12 pixel bright and dark flashes + 6 pixel bright and dark flashes) are repeated 4 times.
- Flash presentation: The flashes are presented so that dark and light flashes are shown alternately. To try and explain how the flashes are presented: the screen was divided into 4 quadrants, then a dark flash is presented in the lower left corner of the top left quadrant, then a light flash in the lower left corner of the top right quadrant, then a dark flash in the lower left corner of the bottom left quadrant, and finally a light flash in the lower left corner of the bottom right quadrant. This is then repeated for the adjacent flash position in each quadrant, and repeats until both dark and light flashes have been presented in all positions on the screen.

![Quadrant spatial organisation of flash presentation. Colourscale is the frame number. So flashes are presented from blue to yellow.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0001.png){:standalone .ifr .pop}

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

### P1 protocol (Sep-Dec 2025) - pharmacology experiments

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


## Protocol 2 (P2)

- <b>Overview:</b>
- Longer, high resolution probing of the cell's receptive field.
- Custom script design. 
- Opens a pop-up at the beginning that asks the user to fill in the `peak_frame` from P1 and the side of the arena used for P1. 
- This `peak_frame` value is then used to generate a protocol with the stimuli centred on the centre of the flash that elicited the greatest response in P1.
- These stimuli are presented within a 30 x 30 pixel area. The rest of the arena is set to the background intensity value.
- Only presents either dark or light stimuli. However, at the end of the protocol the `peak_frame` value that generates the protocol at the same location with the inverse contrast is returned so that the protocol can be run twice, once for each contrast if desired. 

- Location: P2 is made de novo every time the function `generate_protocol2()` is run. A new folder of the format 'yyyy_MM_dd_HH_mm' is made within the the folder 'C:\matlabroot\G4_Protocols\nested_RF_protocol2' that contains both the patterns, functions and experiment file `currentExp.mat` and the data that was recorded in the `Log` file. 

![The plots of the spatial position of the 6 pixel flashes used to generate protocol 2.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0002.png){:standalone .ifr .pop}

### P2 protocol (Dec 2024 - January 2025) - RNAi experiments

- Area of arena presented: [30 x 30 pixels area]
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

### P2 protocol (April 2025 - May 2025) - TmY3, TmY18, TmY5a, Tm5Y

- Area of arena presented: [30 x 30 pixels area]
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

### P2 protocol (July 2025 - Sep 2025) - T4/T5 experiments - SUMMER

- Area of arena presented: [30 x 30 pixels area]
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

### P2 protocol (Oct 2025 - Nov 2025) - T4/T5 experiments - AUTUMN

- Area of arena presented: [30 x 30 pixels area]
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

![Bar flash stimuli examples showing the 11 different positions for the 8 different orientations.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0003.png){:standalone .ifr .pop}

The bar flashes are presented in different random orders for each repetition.
The bar flash stimuli contains 11 different positions. 
From 2025_10_15 - 2025_10_23, the "central" bar flash is positioned in the middle of the 30 x 30 pixel area, then the 5 positions either side are this bar moved by 1 pixel increments and decrements from this position in the 8 different orientations.

![Example bar flash stimuli analysis. Timeseries are plotted for the responses to each flash. The coloured squares in the top row correspond to the colours of the bars in the images in the furthest left column. Left column contains an image of all 11 bars of that orientation overlaid. This example was made for the bar flashes that were shifted by 1 pixel steps.]({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/overview/0004.png){:standalone .ifr .pop}

From 2024_10_23 onwards, these 5 other positions are the central bar moved by 2 pixel increments and decrements. 

[<b>Note for LEB.</b> Results file: "Autumn2025_MARCM_p2_analysis". Data: 2025_10_15 to 2025_11_17]

### P2 protocol (Nov-Dec 2025) - T4/T5 pharmacology experiments

- Area of arena presented: [30 x 30 pixels area]
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






## How to make the protocols

P1 protocols are located within the repository within the `protocols` folder. However, a user may wish to make a new modified version of P1, so I will outline the steps to create a version of P1 from scratch below. 

### Making P1 from scratch - overview

In order to run P1, there are a few steps that need to be done manually. 
Briefly, the user needs to:
- Run `src.stimulus_generation.generate_protocol1_stimuli`. This creates all of the pattern files and position functions that are needed. 
- Open the `G4_experiment_designer` and compile the experiment. 
- Save the experiment with the folder `protocols/LHS` or `protocols/RHS` etc. 
- Make a copy of the file `protocols/processing_settings.mat` and put it within the experiment folder. 

### Making P1 from scratch - detailed

First, you need to make the patterns and functions that will be used in the protocol. This is done by running the function `src/stimulus_generation/generate_protocol1_stimuli.m`. 
Within this function you can modify different parameters to suit your needs. 

- Display settings: The range of pixels within which to present the stimuli is defined within this function by `disp_x1`, `disp_x2`, `disp_y1` and `disp_y2`. For the LHS version of the protocol, the pixel limits start with `disp_x1` = 17. This is because we skip the leftmost column (from the fly's perspective, right most column when looking at the panels from the front). The LED arena is also 3 rows high, so the y range is from 1 to 48, since there are 16 pixels per panel. 

- Stimulus parameters: 

A number of metrics are assigned to a structure called `params` which is the input to the function `generate_stimulus` to create the patterns and position functions. 
        `params.px_intensity` - The pixel intensity values to be used for the stimuli. This parameter should be a [1 x 3] array corresponding to [bkg_color, off_color, on_color] and should be three integer values between 0 and 15. 0 means the LED is off and 15 is the maximum intensity.  
        `params.flash_sz` - The size of the flash (`flash_sz` x `flash_sz`) in pixels.
        `params.root_dir` - Directory to create the `patterns` and `functions` folders for saving the files.
        `params.px_rng = [disp_y1, disp_y2, disp_x1, disp_x2]` - Pixel range of screen within which to present the flashes - [row_start, row_end, col_start, col_end]
        `params.overlap` - Percentage of overlap of the grid within which the flashes are presented. If `overlap` = 0, then there is no overlap between flash positions.
        `params.bkg_frame` - The background frame = frame 1 in the pattern.
        `params.interval_dur` - The duration of interval background screen between flashes (seconds).
        `params.flash_dur` - The duration of each flash stimulus (seconds).
        `params.on_off` - Whether to present bright 'on', dark 'off' or both 'both' flashes. For P1 this should be set to 'both'. 

This `params` structure is then fed into the function `generate_stimulus` which then creates the patterns and postion functions required for P1. 

The static position function is also made within `src/stimulus_generation/generate_protocol1_stimuli.m`. There is an additional parameter that can be modified: `t_bkg_s`, which is the duration for which the background frame is shown at the beginning of each repetition. This duration is in seconds. 
This position function will be saved within the same 'Functions' folder as the other position functions that are generated within `generate_stimulus`. 

- Creating the protocol in the `G4_experiment_designer`

After running `src/stimulus_generation/generate_protocol1_stimuli.m` you should now have two pattern files within `protocols/LHS/patterns` etc. and three position functions within `protocols/LHS/functions` etc. You are now ready to assemble these components into a protocol. To do this: 
        - Run the code: `G4_experiment_designer` in the MATLAB Command Window and the GUI window will appear. 

[ PNG of empty experiment designer GUI ]

- Load the patterns and position functions into the experiment designer
        File-Import-Folder - navigate to the folder where you saved the patterns and position functions that you just made. All patterns and position functions that are saved in this folder will be imported into the GUI. 
        You will have to do this twice, once for the patterns and once for the position functions.

[ PNG - importing folder]

- Set the "pre" stimulus with pattern 0001 and the static position function (0003).
- Set condition 1 as pattern 0001 and position function 0001.
- Set condition 2 as pattern 0002 and position function 0002.
- Set the number of repetitions to 4.
- Set the acquisition rate for the first two channels (voltage and frame position) as 10,000 Hz. 

[ PNG - how the experiment designer should look]
        
- Set the name of the protocol to something logical. For instance, one of the protocols within the repository is named: `protocol1_4reps_12px_6px_LHS_2sbkg_200msfl_50msint`.
- Save the protocol. 

You should then see that a folder has been made within the `protocols/LHS` folder with the name of the protocol and within that folder there should be a `.g4p` file with the same name as the folder. 

- Make a copy of the file `protocols/processing_settings.mat` and paste it within the newly created experiment folder `protocols/LHS/protocol1_...`. 

Within the `processing_settings.mat` file, whenever a new project is created the `settings.path_to_protocol` variable must be updated to the path of the `.g4p` file within the new experiment folder. For P1 protocols, it is impoprtant to make sure that the correct 'ephys processing' variables are set too. 

`settings.path_to_protocol` - must be set to  the path to the protocol, including the full name of the `.g4p` file (with the extension).

The following variables should be set for a P1 protocol:
`settings.is_ephys_grid = 1;`
`settings.neutral_frame = 1;`
`settings.grid_columns = [8, 16];`
`settings.grid_rows = [4, 8];`

If a variation of P1 is made that only uses one pixel size, then the values for `settings.grid_columns` and `settings.grid_rows` will be integers and not tuples.

### Making P2 from scratch. 

Protocol 2 is made from scratch every time that you run the function `generate_protocol2`. HOWEVER, the cropped bar stimuli that are presented in P2 require premade patterns of full field bar stimuli. These premade patterns are found within the folder `\results\patterns\protocol2\full_field_bars` within the repository. However, the details of how these patterns were made are outlined below. 

#### Pre-making the full field bar stimuli for P2
These patterns were made using the `G4_pattern_generator_gui` using the following parameters:
- 
- 
- 

[ PNG - Add png of what the pattern generator looks like]

To make the patterns of the bars in different orientations, the "arena parameters" were updated to rotate the 'arena' to get the desired rotation of the bar. 

#### Modifying the parameters of P2

The parameters that can be modified for P2 are:

        `px_intensity` - The pixel intensity values to be used for the stimuli. This parameter should be a [1 x 3] array corresponding to [bkg_color, off_color, on_color] and should be three integer values between 0 and 15. 0 means the LED is off and 15 is the maximum intensity. 
        `px_crop_flash` - Side length (in pixels) of the area within which to present the flash stimuli. This is currently set to 30 pixels.
        `px_crop_bar` - Side length (in pixels) of the area within which to present the bar stimuli. This is currently set to 30 pixels.

        `flash_dur_slow` - The duration of the slower flash stimuli (seconds).
        `int_dur_slow` - The duration of the interval between flash stimuli during the slow flashes (seconds).
        `px_flash` - The size of the flash stimuli (pixels). 

The range of pixel values of the display are set using the following parameters:
        `screen_width_start = 17;`
        `screen_width_end = 192;`
        `screen_height_start = 1;`
        `screen_height_end = 48;`

In July 2025, the code that generates P2 was updated to include flashes of two sizes













## How to run the protocols

### Protocol 1 - GUI

`G4_experiment_conductor`

- Load g4p
- Run

### Protocol 2 - script

- `generate_protocol2` into the command line of MATLAB, or run the script. 

Protocol 2 runs through a single script - not using the G4_experiment_conductor. 
The patterns, functions and experiment data are all created and saved with every call of the script `generate_protocol2()`. 
A pop-up appears that will ask the experimenter to enter the "peak_frame" (this is found above the subplot of the 6 pixel figure that pops up after P1 that haas the largest response). This is the frame that the experimenter will use to set the position of the stimuli in protocol 2.

Protocol 2 runs smaller flashes, 50% overlapping grid - 30 x 30 pixel square area centred on the centre of the flash found in P1 (peak_frame). 
Then it runs 4 pixel width moving bars in the same area, moving in 8 orientations, 16 directions (back and forth for each orientation).
3 reps...

