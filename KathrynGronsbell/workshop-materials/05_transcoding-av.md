
# Transcoding A/V for preservation and access

The following information is related to the _NDSR 2016 Immersion Week - Automating Procedures for Digital Asset Management_ presentation also found in this GitHub repository. 

## Overview

This page will not tell you how, when, or why to transcode audiovisual material for preservation and access. Requirements and decisions around transcoding should be informed by assessment, prioritization, and the resulting policies. The following information should be used to gain comfort using the command line to transcode or otherwise modify audiovisual files and metadata - the activities and tasks below do not represent best practices, but they do represent a cross-section of realistic practices. 

Below are recommendations to explore [FFmpeg](http://ffmpeg.org/ffmpeg.html) through the CLI with significant support from [ffmprovisr](http://amiaopensource.github.io/ffmprovisr/), an open source web app that provides common ffmpeg commands and information so that even a novice user can understand what the command syntax means and what it does. 


## Getting started

### Running a FFmpeg command

1. Open Terminal and `cd` into the _av-metadata-samples_ folder on your Desktop (used in the previous section).

2. I'll be honest - the first FFmpeg command I ever ran was an attempt to make a GIF. There's a steep learning curve with FFmpeg, which is why I think it's good to start off with a task (like making a GIF!) that's as fun as it is useful. That's also why we are kicking it off with ffmprovisr as a guide. Start by [checking out the ffmprovisr app](http://amiaopensource.github.io/ffmprovisr/) and notice the sections of tasks:

- Change formats
- Make derivative variations
- Preservation
- Test videos
- Other

3. Ok, now to gif-ifying! I want to create a GIF from the _feeding_doves.ogv_ file. We are going to use the *Simpler GIF creation* [create GIF](http://amiaopensource.github.io/ffmprovisr/#create_gif) command from ffmprovisr, copied below with info from the site. The syntax is:

            ffmpeg -ss HH:MM:SS -i input_file -vf "fps=10,scale=500:-1" -t 3 -loop 6 output_file

*ffmpeg* | starts the command
*-ss HH:MM:SS* | starting point of the gif. If a plain numerical value is used it will be interpreted as seconds
*-i input_file* | path, name and extension of the input file
*"fps=frame rate,scale=width:height,palettegen"* | a complex filtergraph using the fps filter to set frame rate, the scale filter to resize. The scale value of -1 preserves the aspect ratio
*-t 3* | duration in seconds (here 3; can be specified also with a full timestamp, i.e. here 00:00:03)
*-loop 6* | number of times to loop the gif. A value of -1 will disable looping. Omitting -loop will use the default which will loop infinitely
*output_file* | path, name and extension of the output file (in our case, make sure to end it with .gif!)

So the command to run in Terminal would be:

            ffmpeg -ss 00:00:02 -i feeding_doves.ogv -vf "fps=10,scale=500:-1" -t 3 -loop 6 feeding_doves.gif

4. Check out your GIF! How does it look? Now read through the [Create high quality GIF](http://amiaopensource.github.io/ffmprovisr/#create_gif) command on ffmprovisr. What is the difference in outcome between this command and the one we used in Step #3?

5. Try the [Create high quality GIF](http://amiaopensource.github.io/ffmprovisr/#create_gif) command using the sample file _IMG_7770.mov_. Modify the starting point (HH:MM:SS) so you have a more aesthetically pleasing GIF result with the fancy filter. :) Name the output file _monkeys.gif_

### BYO ffmprovisr command

1. Pick a partner.

2. Choose a command from the ones provided on ffmprovisr. Now choose an input file from the samples provided. Try to run the command.

3. Write down the answers to these questions:
- What ffmprovisr command did you choose? 
- What was your actual command that you entered into Terminal? Can you walk us through the options you chose?
- What was the outcome? Is it what you expected? Did it work the first time?
- What is a use case that could be satisfied by using the command you chose (real or educated imagining)?

4. We'll have a group discussion and trying to replicate your command as a group. Did we all get the same results? 


* Reminder that ffmprovisr relies on the community for support, new ideas, and maintenance! If you have a great FFmpeg command you'd like to see, find a typo or a bug, or just want to help out - contribute by [submitting an issue](https://github.com/amiaopensource/ffmprovisr/issues) on ffmprovisr's GitHub page.


