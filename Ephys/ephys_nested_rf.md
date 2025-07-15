---
title: Nested RF Protocol
parent: Ephys
has_children: true
has_toc: false
nav_order: 1
layout: home
---

1. TOC
{:toc}

The 'Nested RF Protocol' was designed by LE Burnett in 2024 for patch electrophysiology experiments ran by JY Park. 
It is a multi-step protocol that tries to probe the receptive field (RF) structure of the neuron being recorded. 

It was based upon the protocol used in Gruntman et al. 2019(^ref). 

The code for generating and running these protocols is publicly available (here)[https://github.com/leburnett/nested_RF_stimulus]
Running these experiments requires the user to have the 'G4_Display_Tools' (repository)[https://github.com/JaneliaSciComp/G4_Display_Tools] downloaded locally too. 

## Descriptions of current protocols: 

### Protocol 1 (P1)

- Designed to be quick and coarse.
- <b>Aim 1:</b> Find which flash location elicits the greatest response.
- <b>Aim 2:</b> Determine whether the cell shows a preferred contrast to dark or light flashes.
- Use this location and preferred contrast to create and run protocol 2 (P2). 

As of July 2025, there are multiple versions of the first protocol (P1) of the nested RF protocol that exist. 

- Location: The older versions of P1 can be found within the `nested_RF_stimulus` GitHub repository in `protocols/LHS` and `protocols/RHS` folders.
- Intensity values: These protocols have a background pixel intensity value of 6 (out of 15), dark stimuli have a pixel value of 0 and bright stimuli have a pixel value of 15.
- Stimulus parameters: Each protocol consists of both dark and bright flashing squares of 12 x 12 pixel size and then 6 x 6 pixel size that are presented on a non-overlapping grid on one half of the arena screen. One half of the arena relates to an area of 6 x 3 panels (16 x 6 = 96 pixels wide, 16 x 3 = 48 pixels high). In the G4 ephys LED panel setup each pixel is 1.25 degrees of visual anlge per pixel. So, a 12 pixel square is 15 degrees of visual angle, and a 6 pixel square is 7.5 degrees of visual angle.

[ PNG of panel layout and which panels are used for LHS verus RHS verus RHS2 ]

- Protocol design: The protocol starts with 5s of a full field greyscale frame at the background value intensity for 5s, then runs through the larger 12 x 12 pixel flashes first, then the smaller 6 x 6 pixel flashes. The order in which the flashes are presented is not random, but was designed to avoid consecutive flashes appearing close enough to each other that they would activate the same cell's RF. These stimuli (5s static grey + 12 pixel bright and dark flashes + 6 pixel bright and dark flashes) are repeated 4 times.

[ PNG of protocol design ] 

- Flash presentation: The flashes are presented so that dark and light flashes are shown alternately. To try and explain how the flashes are presented: the screen was divided into 4 quadrants, then a dark flash is presented in the lower left corner of the top left quadrant, then a light flash in the lower left corner of the top right quadrant, then a dark flash in the lower left corner of the bottom left quadrant, and finally a light flash in the lower left corner of the bottom right quadrant. This is then repeated for the adjacent flash position in each quadrant, and repeats until both dark and light flashes have been presented in all positions on the screen.

[ PNG of the quadrant layout of the arena screen and how the flashes are presented ]

#### Updates to P1 in July 2025
These protocols were updated in July 2025. The newer versions of P1 can be found within the `protocols/bkg4/LHS` and `protocols/bkg4/RHS2` folders.
Things that were updated in these protocols to the original protocols:

- The background intensity pixel value was decreased from 6 (out of 15) to 4.
- The interval between flashes was increased from 50ms to 150ms. The flash duration was unchanged at 200ms. 


### Protocol 2 (P2)

- Longer, high resolution probing of the cell's receptive field.
- Custom script design. 
- Opens a pop-up at the beginning that asks the user to fill in the `peak_frame` from P1 and the side of the arena used for P1. 
- This `peak_frame` value is then used to generate a protocol with the stimuli centred on the centre of the flash that elicited the greatest response in P1.
- These stimuli are presented within a 30 x 30 pixel area. The rest of the arena is set to the background intensity value.
- Only presents either dark or light stimuli. However, at the end of the protocol the `peak_frame` value that generates the protocol at the same location with the inverse contrast is returned so that the protocol can be run twice, once for each contrast if desired. 

- Location: P2 is made de novo every time the function `generate_protocol2()` is run. A new folder of the format 'yyyy_MM_dd_HH_mm' is made within the the folder 'C:\matlabroot\G4_Protocols\nested_RF_protocol2' that contains both the patterns, functions and experiment file `currentExp.mat` and the data that was recorded in the `Log` file. 
- Intensity values: These protocols have a background pixel intensity value of 6 (out of 15), dark stimuli have a pixel value of 0 and bright stimuli have a pixel value of 15.

#### Updates to P2 in July 2025
These protocols were updated in July 2025. Things that were updated in these protocols to the original protocols:

- The background intensity pixel value was decreased from 6 (out of 15) to 4.
- Instead of showing 4 x 4 pixel flashes at two different speeds (160ms + 340ms and 80ms + 170ms), it was decided to change to two different size flashes at the same speed [4 x 4 pixel flashes (160ms + 440ms) and 6 x 6 pixel flashes (160ms + 440ms)]. Although the flash duration is the same as the slower flash speed before, the interval duration was increased by 100ms from 340ms to 440ms. 
- The 6 x 6 pixel flashes are presented in a 33 x 33 pixel sqaure area - larger than the 30 x 30 pixel square area for the 4 x 4 pixel flashes - to get an even number of flashes on a 50% overlapping grid.
- A 1s interval of a greyscale background was added at the beginning of every bar stimulus (every direction).

















## How to make the protocols from scratch:

P1 protocols are located within the repository within the `protocols` folder. However, a user may wish to make a new modified version of P1, so I will outline the steps to create a version of P1 from scratch below. 

### Making P1 from scratch
#### Brief overview

In order to run P1, there are a few steps that need to be done manually. 
Briefly, the user needs to:
- Run `src.stimulus_generation.generate_protocol1_stimuli`. This creates all of the pattern files and position functions that are needed. 
- Open the `G4_experiment_designer` and compile the experiment. 
- Save the experiment with the folder `protocols/LHS` or `protocols/RHS` etc. 
- Make a copy of the file `protocols/processing_settings.mat` and put it within the experiment folder. 

#### Detailed description

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

        [TODO - update which parameters of the processing_settings.mat file needs to be checked / updated].


### Making P2 from scratch. 

Protocol 2 is made from scratch every time that you run the function `generate_protocol2`. HOWEVER, the cropped bar stimuli that are presented in P2 require premade patterns of full field bar stimuli. These premade patterns are found within the folder `\results\patterns\protocol2\full_field_bars` within the repository. However, the details of how these patterns were made are outlined below. 

#### Pre-making the full field bar stimuli for P2
These patterns were made using the `G4_pattern_generator_gui` using the following parameters:
- 
- 
- 

[ PNG - Add png of whatthe pattern genertor looks like for ]

Describe changing the rotation of the arena to generate the bars moving at different angles. 

#### Modifying the parameters of P2

The parameters that can be modified for P2 are:

        `px_intensity` - The pixel intensity values to be used for the stimuli. This parameter should be a [1 x 3] array corresponding to [bkg_color, off_color, on_color] and should be three integer values between 0 and 15. 0 means the LED is off and 15 is the maximum intensity. 
        `px_crop_flash` - Side length (in pixels) of the area within which to present the flash stimuli. This is currently set to 30 pixels.
        `px_crop_bar` - Side length (in pixels) of the area within which to present the bar stimuli. This is currently set to 30 pixels.

        `flash_dur_slow` - The duration of the slower flash stimuli (seconds).
        `int_dur_slow` - The duration of the interval between flash stimuli during the slow flashes (seconds).
        `px_flash` - The size of the flash stimuli (pixels). 

The range of pixel values of the display are set using the following parameters:
        screen_width_start = 17;
        screen_width_end = 192;
        screen_height_start = 1;
        screen_height_end = 48;

In July 2025, the code that generates P2 was updated to include flashes of two sizes













## How to run the protocols

### Protocol 1 - GUI

`G4_experiment_conductor`

- Load g4p
- Run

### Protocol 2 - script

- `generate_protocol2` into the command line of MATLAB, or run the script. 






































## How to analyse the data from the protocols

### Protocol 1 

- Processing settings file...
- Which boxes need to be ticked in the conductor?


After protocol 1 has finished running - the processing functions should run automatically. This runs code wihtin `G4_Display_Tools` (which functions) - it returns LOG with data inside and it generates 4 plots (grid_ephys). 

From these plots you can see the response of the cell to each flash location on the screen - both 12px and 6px and ON and OFF flashes.
This protocol is mainly for the experimenter to determine where the RF of the cell is located in order to present the second protocol in the correct position. From these plots it is also possible to determine if the RF of the cell is too close to the edge of the screen, in which case it is not worth running protocol 2. You can also see if the quality of the recording is not good enough to run protocol 2.

### Protocol 2

Protocol 2 runs through a single script - not using the G4_experiment_conductor. 
The patterns, functions and experiment data are all created and saved with every call of the script `generate_protocol2()`. 
A pop-up appears that will ask the experimenter to enter the "peak_frame" (this is found above the subplot of the 6 pixel figure that pops up after P1 that haas the largest response). This is the frame that the experimenter will use to set the position of the stimuli in protocol 2.

Protocol 2 runs smaller flashes, 50% overlapping grid - 30 x 30 pixel square area centred on the centre of the flash found in P1 (peak_frame). 
Then it runs 4 pixel width moving bars in the same area, moving in 8 orientations, 16 directions (back and forth for each orientation).
3 reps...

### Processing the data

On the ephys computer, each run of `generate_protocol2()` with create a new folder within `C:\matlabroot\G4_Protocols\nested_RF_protocol2` with the format "YYYY_MM_DD_HH_MM" of the date and time when the protocol was run. Within this folder there will be a `patterns` folder with the patterns that were used in the protocol, a `functions` folder with the position functions that were used, and a `params` folder containing a file with metadata about the protocol run. There will also be a folder `Log Files`, this itself will contain a subfolder with the exact date and time of the run that will contain the raw tdms files of the electrophysiology data and the frame position data. Witin `generate_protocol2()` there is a function `run_protocol2()` that runs the protocol created. At the very end of this function there is a function called `G4_TDMS_folder2struct(log_folder)` - another function from the `G4_Display_Tools` that will convert the tdms files into a combined structure (called `Log`) that can be used for analysis.

`process_protocol2()` - - 
Run the function within the experiment folder - `data/YYYY_MM_DD_HH_MM`. 
It will read in the metadata file that has information about the strain of the fly, peak_frame, side of the arena.

First, runs the bar processing. `process_bars_p2`
- Timeseries plot

Will return the resultant angle of the vector sum of the responses to the bars. 

Then runs, flash analysis. `process_flash_p2`
- Timeseries heatmap plots. 
This takes in the resultant angle and plots the arrow on top of the heatmap plots. 

Two plots generated, one for the 4 pixel flashes and the other for the 6 pixel flashes. 
