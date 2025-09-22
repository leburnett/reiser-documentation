---
title: Analysing a new protocol
parent: Analysis (freely-walking)
has_children: true
has_toc: true
nav_order: 100
layout: home
---

1. TOC
{:toc}

If you create a new protocol for the freely-walking arena, you should be able to make simple overview plots using the same "cohort level" analysis code described [here](https://leburnett.github.io/reiser-documentation/Freely-walking/freely_walking_analysis.html#level-1---analyse-per-cohort-process_freely_walking_data) since this analysis doesn't need any knowledge of the conditions and stimuli used in the protocol. However, the second level of analysis might not work automatically and might not do what you want anyway.


[pink /blue rects in overview plots - how this needs to be updated.]


You probably want to return the 'DATA' sturcture with the behavioural data parsed by condition. `comb_data_across_cohorts_cond` should be able to do this automatically if the protocol saves the condition number to the LOG file. From this structure many things can be looked at and plotted.
