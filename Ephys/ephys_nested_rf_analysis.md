---
title: Analysis
parent: Nested RF Protocol
has_children: true
has_toc: false
nav_order: 1
layout: home
---

1. TOC
{:toc}


# How to analyse the data from the nested RF protocol.






## Protocol 1 

- Processing settings file...
- Which boxes need to be ticked in the conductor?

After protocol 1 has finished running - the processing functions should run automatically. This runs code wihtin `G4_Display_Tools` (which functions) - it returns LOG with data inside and it generates 4 plots (grid_ephys). 

From these plots you can see the response of the cell to each flash location on the screen - both 12px and 6px and ON and OFF flashes.
This protocol is mainly for the experimenter to determine where the RF of the cell is located in order to present the second protocol in the correct position. From these plots it is also possible to determine if the RF of the cell is too close to the edge of the screen, in which case it is not worth running protocol 2. You can also see if the quality of the recording is not good enough to run protocol 2.











## Protocol 2

### How the data is organised

- Each run of `generate_protocol2()` with create a new folder within `C:\matlabroot\G4_Protocols\nested_RF_protocol2` with the format "YYYY_MM_DD_HH_MM" of the date and time when the protocol was run. 
- Within this folder there will be a `patterns` folder with the patterns that were used in the protocol, a `functions` folder with the position functions that were used, and a `params` folder containing a file with metadata about the protocol run. 
- There will also be a folder `Log Files`, this itself will contain a subfolder with the exact date and time of the run that will contain the raw tdms files of the electrophysiology data and the frame position data. Witin `generate_protocol2()` there is a function `run_protocol2()` that runs the protocol created. At the very end of this function there is a function called `G4_TDMS_folder2struct(log_folder)` - another function from the `G4_Display_Tools` that will convert the tdms files into a combined structure (called `Log`) that can be used for analysis.

[PNG - 0001]

### How to process P2 data

Run the function `src/analysis/process_protocol2()` within the experiment folder (`data/YYYY_MM_DD_HH_MM`). This function reads in the metadata file that has information about the strain of the fly, peak_frame, side of the arena.

The responses to the moving bar stimuli are processed first, since this analysis generates a vector sum of the responses of the cell to bars moving in the 16 different directions. The resultant angle of this vector sum is then fed in to the function that processes the flash responses and overlays an arrow with this direction on top of the receptive field plots. 

#### Breakdown of `process_bars_p2`

This function reads in the frame data:
        `f_data = Log.ADC.Volts(1, :); % frame data`
and then the voltage data:
        `v_data = Log.ADC.Volts(2, :)*10; % voltage data`

This is the data across the entire experiment, the three repetitions of the two flash stimuli and the tw2o bar stimuli. The voltage data is multiplied by 10 because during the data acquisition it is downsampled by a factor of 10. (TODO: ADD WHY). 

[ PNG - General plot of f_data and v_data ]

##### Parsing the bar data

The function `src/analysis/protocol2/pipeline/parse_bar_data` is used to parse the frame data to understand when the moving bar stimuli were presented.

1. Find the range of timepoints during which all of the bar stimuli for each repetition were being presented. This includes both the slow and fast bars. 

Firstly, using the value of the parameter `on_off`, which refers to whether bright ('on') or dark (off') stimuli were used during the protocol, the parameter `drop_at_end` is set to either '-200' for `on_off` == 'on' or '-100' for `on_off` == 'off'. 

Then `idx` is set to the timepoints for which the difference in the frame position is equal to `drop_at_end`. This happens both once during the 4 pixel flashes and for the last timepoint of the last 6 pixel flash. The 1st, 3rd and 5th values are removed to remove the timepoints during the 4 pixel flashes and so only the timepoints corresponding to the end of the 6 pixel flashes remain. This is useful because this is the stimulus before the bar stimuli start.

` idx = find(diff_f_data == drop_at_end);`
` idx([1,3,5]) = [];`

[ PNG - 0002]
^ This shows the values of `idx`. 

[ PNG - 0003]
^ Zoom in on just the second value of `idx` - end of first rep of 6 pixel flashes. 

Since each flash stimulus is followed by a 440ms gap, and each bar stimulus is preceded by a 1000ms gap, there is a ~1440ms period before the first bar stimulus being presented and the last of the 6 pixel flashes being shown. Ultimately, the data will be broken up into chunks of the same length with 1000ms before the bar stimulus and until 900ms after the end of the bar stimulus, but first we want to find the range of timepoints during which ALL bar stimuli (both slow and fast) are presented for each repetition.

[ PNG - 0004 ] 
^ Zoom in on frame position data. 
Red line = Last frame of the last flash of the 6 pixel flashes.
Cyan line = after 440ms gap after flash and before 1000ms gap before bar stimulus starts. 
Magenta line = first frame of the first bar stimulus.

[ PNG - 0005 ]
^ Zoom out of frame position data showing the end of the first rep of 6 pixel flashes, all bar stimuli and the beginning of the second rep of 4 pixel flashes.
The vertical bars are the timepoints that are found in the code. The two timepoints that represent the start and end of the first repetition of bar stimuli are defined as `rep1_rng` and are represented graphically by the magenta vertical bar and the green vertical bar. This range excludes the interval periods before the stimuli start and after the stimuli stop.

This is the code that was used to plot the cyan, magenta and green lines:
`plot([idx(1)+gap_between_flash_and_bars idx(1)+gap_between_flash_and_bars], [0 100], 'c')`
`plot([start_f1 start_f1], [0 100], 'm')`
`plot([end_f1 end_f1], [0 100], 'g')`

[ PNG - 0006 ]
^ This shows the range of timepoints for the bar stimuli in rep1 (magenta lines), rep2 (red lines) and rep3 (green lines). The third rep uses the last frame of the experiment as the end of it's range. It doesn't matter that this includes the interval time at the end because the actual start and stop times of the bar stimuli are found within these ranges in the next step. 

2. Find the timepoints for when each individual bar stimulus starts and stops. 

Now that we have extracted the range of timepoints during which all of the bar stimuli of one repetition are presented, we now want to extract the timepoints for each individual bar stimulus (one sweep of the bar) within each repetition. To do this, the difference between frame positions are used again. This time we are looking for the timepoints when the frame position changes from 0 (the background interval frame) and 

[ PNG - 0007]
^ Red vertical lines for the start and end of each bar stimulus. From `idxs_all{1,1}`. These are the indices only for the first repetition of bar stimuli. 

3. Create the cell array `data` which combines the voltage data for each bar stimulus including 9000ms before and after each sweep of the bar.

The indices found above and stored in `idxs_all` are then used to extract the relevant voltage data for each bar sweep. Since there is a 1000ms gap between each bar sweep (added in July 2025), 900ms is added before and after the bar sweep timepoints to see the baseline voltage between each sweep.

[ PNG - 0008]
^ Frame position (blue) and the magenta vertical lines show the range of data that is included for the first bar and the cyan vertical lines show the range of data to include for the second bar. These ranges include 900ms before and after the bar stimulus itself.

This data is combined into the [32 x 4] cell array `data`. The voltage data for the slow bar stimuli are in rows 1:16 and the voltage data for the fast bar stimuli are in rows 17:32. Each cell contains a linear array of the voltage over the 900ms before the bar stimulus, the bar stimulus presentation and 900ms after the bar stimulus. This means that the slow bar stimuli have voltage data arrays of roughly [1 x 41100] timepoints (10kHz acquisition - 0.9s pre, 2.3s stim, 0.9s post = ~4.1s total) and the fast stimuli of [1 x 29100] timepoints (10kHz acquisition - 0.9s pre, 1.1s stim, 0.9s post = ~2.9s total). The first three columns contain the data for each repetition to each condition adn the fourth column is the mean across the three repetitions. The size of the linear arrays are trimmed to the length of the shortest repetition, concatenated and then averaged using `mean()`.

[ PNG - 0009]
^ Example `data` cell array. 

The cell array `data` is returned by the function `parse_bar_data` and is used for plotting and analysing the responses to the bar stimuli.

##### Plotting the bar data

1. Circular timeseries plot with central polar plot for both speeds.

`data` is first fed into the function `src/analysis/plotting/plot_timeseries_polar_bars`. 

Will return the resultant angle of the vector sum of the responses to the bars. 













#### Breakdown of `process_flash_p2`

##### Parsing the flash data

The function `src/analysis/protocol2/pipeline/parse_flash_data` is used to parse the frame data to understand when the flash stimuli were presented.

##### Plotting the flash data

- Timeseries heatmap plots. 
This takes in the resultant angle and plots the arrow on top of the heatmap plots. 

Two plots generated, one for the 4 pixel flashes and the other for the 6 pixel flashes. 
