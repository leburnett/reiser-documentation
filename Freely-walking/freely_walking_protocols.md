---
title: Freely-walking-protocols
parent: Freely-walking
has_children: true
has_toc: true
nav_order: 10
layout: home
---

1. TOC
{:toc}

# Description of the protocol used for the Motion-Induced Centring (MIC) screen

The protocol used was protocol 27. 

## How to generate the stimuli

## Breakdown of the protcol structure.

## How to run the protocol

- Arena on and controller on. 
- BIAS open
- PControl open in MATLAB
- Camera open to view flies live in the arena (visible light).
- Run MATLAB protocol script. 

# Description of the other protocols that were used. 

1. p10
2. p24
3. p25
4. p30
5. p31
6. p32

## Automatic logging of experiments using a google form. 
As well as recording which experiments were run in a physical lab book, the running of any "protocol_X" script will automatically log the experiment using an in-built [google form](https://docs.google.com/spreadsheets/d/1IsT3YndxAy3yN8o38r5RGK4dZsEdPXe0In4-OTEcXNw/edit?resourcekey=&gid=35583985#gid=35583985). This process works by feeding the parameter "params" into a pre-made google form which then exports the results to a google sheet. 

When any protocol is started by clicking on the "Run" button within the MATLAB editor, the function `get_input_parameters()` is run which opens a pop up window where the user can fill in details about the current experiment using a series of dropdown boxes (See figure). These values are assigned to fields within the struct `params` which is returned by the function.

![`get_input_parameters` GUI that pops up when you run any protocol.]({{ site.baseurl }}/assets/imgs/freely/protocols/0001.png){:standalone .ifr}

Within the function `initialize_video_and_folder`, `params` is added to with the current date, the experiment time and the protocol which is being run. The in-built MATLAB function `input` is used within this function enable the user to type a string describing initial notes before the experiment has started. This string is also added to `params`. Within the protocol script itself, there is another call to `input` which can be used to enter notes at the end of experiment. These notes could relate to the general behaviour of the group of flies or some experimental abnormality. After this final `input` call, the function `export_to_google_sheets` is run which takes in the URL of the pre-made google form that will be filled by the values of `params`. 

## How to make google form logging system
<b>1</b> - Generate a pop up to take in data from the user. See`get_input_parameters` or `get_video_observations` in this repository for inspiration.<br>
<b>2</b> - Use the MATLAB function `input` if you want to include a long form string in your documentation.<br>
<b>3</b> - Make a google form with "questions" relating to the fields of data that you would like to record. The "questions" do not need to match exactly the naming of the struct that is returned from GUI.<br> 
<b>4</b> - Set the "type" of each question to "short answer" question. Don't use "date" or "time" even if you have those fields.<br> 

![Select 'short answer' when creating the google form.]({{ site.baseurl }}/assets/imgs/freely/protocols/0002.png){:standalone .ifr_center}

<b>5</b> - Click on the three-dot menu (⋮) in the top right and select "Pre-fill form".

![Select 'Pre-fill form']({{ site.baseurl }}/assets/imgs/freely/protocols/0003.png){:standalone .ifr_center}

<b>6</b> - Fill in sample responses and click "Get link" to generate a URL.

![Fill in the form with example entries then press 'Get link'.]({{ site.baseurl }}/assets/imgs/freely/protocols/0004.png){:standalone .ifr_center}

<b>7</b> - Copy the generated link (it will look something like this):

```
"https://docs.google.com/forms/d/e/1FAIpQLScgK2F-PiaHaW9AiqUjHNZ9D1WYpF1-W19sEwlob2orr2wyfg/viewform?usp=pp_url&entry.104586054=10_23_25&entry.1144953751=10_04_27&entry.1017789798=empty_split&entry.462337747=10&entry.635492352=4Hz_gratings&entry.1832623891=1&entry.932164432=None&entry.324082057=None&entry.1509506971=None&entry.350553119=Sparse&entry.1178542927=None&entry.1494282419=10&entry.183573490=Test+case"
```

<b>8</b> - From this link extract the "googleFormURL" and the entry IDs.<br> 
To find the "googleFormURL", get the first part of this URL up to "/viewform?....". Copy this initial part of the URL and after the last "/" add "formResponse". So, the final URL will be:

```
googleFormURL = "https://docs.google.com/forms/d/e/1FAIpQLScgK2F-PiaHaW9AiqUjHNZ9D1WYpF1-W19sEwlob2orr2wyfg/formResponse"
```

<b>9</b> - Link the MATLAB data with the questions in the google form.<br>
Each number after `entry.` is the entry ID that corresponds to each field in your form, these need to be added within the `webwrite` call. This is what the code in MATLAB will look like:

```
    % Google Form Response URL (Make sure it ends with /formResponse)
    googleFormURL = 'https://docs.google.com/forms/d/e/1FAIpQLScgK2F-PiaHaW9AiqUjHNZ9D1WYpF1-W19sEwlob2orr2wyfg/formResponse';
    
    % Use weboptions to set character encoding
    options = weboptions('MediaType', 'application/x-www-form-urlencoded', 'Timeout', 30);
    
    % Submit data using name-value pairs instead of struct
    webwrite(googleFormURL, ...
        'entry.104586054', metadata.date, ...
        'entry.1144953751', metadata.time, ...
        'entry.1017789798', metadata.strain, ...
        'entry.462337747', metadata.condition_n, ...
        'entry.635492352', metadata.condition_str, ...
        'entry.1832623891', metadata.rep, ...
        'entry.932164432', observations.centring, ...
        'entry.324082057', observations.turning, ...
        'entry.1509506971', observations.rebound, ...
        'entry.350553119', observations.distribution, ...
        'entry.1178542927', observations.locomotion, ...
        'entry.1494282419', observations.diversity, ...
        'entry.183573490', notes, ...
        options); % Include options for correct encoding
```
<b>10</b> - Publish the form. 

![Publish the form to make it accessible.]({{ site.baseurl }}/assets/imgs/freely/protocols/0005.png){:standalone .ifr_center}

<b>11</b> - Try running the script and see if a response is recorded within the form!

![View the responses in the 'response' tab within the form.]({{ site.baseurl }}/assets/imgs/freely/protocols/0006.png){:standalone .ifr_center}

Once you get responses you can open a google sheet and look at the combined responses there. 

![View the responses in the linked google sheet.]({{ site.baseurl }}/assets/imgs/freely/protocols/0007.png){:standalone .ifr_center}