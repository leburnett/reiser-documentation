---
title: Freely-walking-analysis
parent: Freely-walking
has_children: true
has_toc: true
nav_order: 5
---

1. TOC
{:toc}

# How to analyse the data from the MIC screen

## `process_freely_walking_data`

### Inputs 

Requires string of the date for which you want to analyse the data. It will process all of the data from experiments conducted with any protocol that are within that day. 

Runs the function `process_data_features` 

### Outputs
- Exports a text file of the number of flies ran per protocol and per strain. [TODO: name of text file]
- Results .mat file
    - Contains: [LOG, feat, trx, comb_data, n_fly_data]
    - per vial
- Figures: 
    - Acclim timeseries
    - Feat_overview timeseries
    - Timeseries per behavioural metric per vial.

### Description of `process_data_features`
Processes the tracked data from FlyTracker. 

Loads: 
    - LOG (metadata about the experiment.)
    - feat (from FlyTracker)
    - trx (from FlyTracker)

- Runs the function `make_overview` which generates a plot of histograms of the general behaviour of the flies over the entire length of the protocol. 
- Runs the function `plot_all_features_filt` which generates a plot of timeseries data for all flies over the entire length of the protocol. fv_data, av_data and dist_data. 
- Runs the function `plot_all_features_acclim` which generates a plot of timeseries data for all flies during the 5 minutes of acclimatisation in the dark. fv_data, av_data and dist_data. 

The data from all flies is combined into an easier to manipulate 'struct' called `DATA` through the function `comb_data_one_cohort_cond`

- Runs the function `plot_allcond_onecohort_tuning` which generates a [(n_conditions/2) x 2] subplot figure of the timeseries data during each condition (mean+SEM of all the flies in the vial) as well as tuning curves per condition. 

### Processing of other protocols

Data from `protocol_30` and `protocol_31` run the functions `plot_errorbar_tuning_curve_diff_contrasts` and `plot_errorbar_tuning_diff_speeds`, respectively. Which plot tuning curve plots in addition to the timeseries plots. 

- Runs the function `generate_movie_from_ufmf` which makes individual movies each rep of each condition per experiment. 

Data from `protocol_25` - individual flies used the script `single_lady_analysis.m`. 




## `process_screen_data`

This function works by using the .mat results files that were generated after running `process_freely_walking_data`. It heavily relies upon the structured format of the data into the same 'DATA' struct created by `comb_data_one_cohort_cond` but instead uses `comb_data_across_cohorts_cond` to generate the structure across all flies from multiple cohorts.

- Runs the function `comb_data_across_cohorts_cond` to generate the struct `DATA`.
- Runs the funciton `plot_allcond_acrossgroups_tuning` to create [(n_conditions/2) x 2] subplot figures for each strain versus the empty split control flies. It creates 5 of these subplot figures per strain, one for each data type ['fv_data', 'av_data', 'curv_data', 'dist_data', 'dist_data_delta']. 


### Inputs 
- String of the protocol e.g. 'protocol_27' 
- '.mat' results files from `process_data_features`.

### Outputs
- 5 x figures per strain (timeseries per condition)
- Text file and 2 plots of the number of vials per strain and the number of flies per strain. 

## Making p-value heatmap using `make_summary_heat_maps_p27`

This [function](https://github.com/leburnett/freely-walking-optomotor/blob/processing_computer/plotting_functions/summary_plot/make_summary_heat_maps_p27.m) generates a red-blue heatmap of the p-value for different behavioural metrics across each condition compared to the empty-split control flies.  

- It combines all of the data for `protocol_27` in the same way as before using the function `comb_data_across_cohorts_cond`.
- It then uses the function `make_pvalue_heatmap_across_strains` to generate arrays of all of the p-values.
- A False-Detection Rate adjustment is performed using `fdr_bh`. 
- The data is plotted altogether using the function `plot_pval_heatmap_strains`. 
