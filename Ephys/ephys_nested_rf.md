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

The <b>Nested RF Protocol</b> was designed by LE Burnett in 2024 for patch electrophysiology experiments ran by JY Park. 
It is a multi-step protocol that tries to probe the receptive field (RF) structure of the neuron being recorded. 

It was based upon the protocol used in <i>Gruntman et al. 2019(^ref)</i>. 

The code for generating and running these protocols is publicly available [here](https://github.com/leburnett/nested_RF_stimulus).
Running these experiments requires the user to have the 'G4_Display_Tools' [repository](https://github.com/JaneliaSciComp/G4_Display_Tools) downloaded locally too. 

____________________________________________________________________________________________________________________

The premise of the nested receptive field protocol was to make a multi-step protocol consisting of a short <b>first protocol</b> that determines the rough receptive field location and preferred contrast of the cell, and a longer <b>second protocol</b> that is only presented at the location of the RF determined in protocol 1. This follow-up protocol probes the direction selectivity of the cell using moving bar stimuli, as well as measuring the ON and OFF receptive field structure at higher spatial resolution using small flashing squares.

