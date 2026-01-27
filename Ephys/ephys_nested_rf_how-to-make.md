---
title: How to make the protocols
parent: Nested RF Protocol
has_children: true
has_toc: true
nav_order: 80
layout: home
---

## How to make the protocols

__________________________________________________________________________________________________


1. TOC
{:toc}

__________________________________________________________________________________________________


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

- Load the patterns and position functions into the experiment designer
        File-Import-Folder - navigate to the folder where you saved the patterns and position functions that you just made. All patterns and position functions that are saved in this folder will be imported into the GUI. 
        You will have to do this twice, once for the patterns and once for the position functions.

- Set the "pre" stimulus with pattern 0001 and the static position function (0003).
- Set condition 1 as pattern 0001 and position function 0001.
- Set condition 2 as pattern 0002 and position function 0002.
- Set the number of repetitions to 4.
- Set the acquisition rate for the first two channels (voltage and frame position) as 10,000 Hz. 

![Screenshot of the G4_Experiment_Designer used to make a version of protocol 1 with 6 and 12 pixel square flashes].({{ site.baseurl }}/assets/imgs/ephys/nested_RF_stimulus/protocol_generation/0000.png){:standalone .ifr_center}
        
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

__________________________________________________________________________________________________


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
