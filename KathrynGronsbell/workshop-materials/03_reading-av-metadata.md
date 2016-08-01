
# Reading key A/V metadata

The following information is related to the _NDSR 2016 Immersion Week - Automating Procedures for Digital Asset Management_ presentation also found in this GitHub repository. 

## Overview

This page focuses on getting comfortable using two common tools - [MediaInfo](http://mediaarea.net/en/MediaInfo) and [ffprobe](http://ffmpeg.org/ffprobe.html) - for basic metadata tasks related to audiovisual archiving and preservation. 


## Getting started

1. Open Terminal (Applications > Utilities > Terminal). 

2. Download the sample materials for this exercise [av-metadata-samples.zip](./workshop-samples/av-metadata-samples.zip). Use `mv` to move the zip file to your Desktop. Then use `unzip` to unpackage it into a directory (see [cli-basics](./01_cli-basics.md) for a refresher on how to do this). 

3. You should already have MediaInfo and ffprobe installed. Check this by trying to look at the documentation for MediaInfo:

            mediainfo

 - And for ffprobe:

            man ffprobe

If you do not have either of these tools installed, follow directions to [install FFmpeg/ffprobe](https://trac.ffmpeg.org/wiki/CompilationGuide/MacOSX) and [install MediaInfo](http://mediaarea.net/en/MediaInfo/Download). If you are using Homebrew (which is great, simple to use package installer for Mac), you can simply type for FFmpeg (ffprobe included):

            brew install ffmpeg

 - And for MediaInfo:

            brew install media-info


### Read metadata using MediaInfo

MediaInfo is ["a convenient unified display of the most relevant technical and tag data for video and audio files."](https://mediaarea.net/en/MediaInfo). It also is one of the most common and referenced metadata tools for a/v material in use by those working in the archiving and preservation fields. The tool has a GUI but these instructions will explore MediaInfo on the CLI. The CLI has more flexibility and opportunities for customization of commands. It also makes it possible to integrate MediaInfo commands into programs or scripts, if you choose to in the future. 

1. Let's start by looking at MediaInfo's output when it is run on a sample file with no options. `cd` to the _av-metadata-samples_ folder on your Desktop. Run this command and look at the output:

            mediainfo fred_ott_sneeze_512kb.mp4


 The data presented as part of this full output may be divided into:
 - General
 - Video
 - Audio
 - Text
 - Chapters
 - Other

 You may also wonder what [KiB, MiB, GiB](https://mediaarea.net/us/MediaInfo/Support/FAQ#BinaryPrefix) is in the File Size value?

2. You can also review the output formatted as XML by adding an option and then opening the XML. This command redirects MediaInfo's output to a new XML document you are creating in your working folder:

            mediainfo --Output=XML fred_ott_sneeze_512kb.mp4 > fred-mediainfo.xml

3. Now, open that XML file and review. Type this command to open the XML file in your default XML viewing application:

            open fred-mediainfo.xml

4. Run MediaInfo on the other sample files provided in _av-metadata-samples_. 
 - Review the output with a partner - how does this output align with what was discussed as part of your _Introduction to managing digital audiovisual media_ and _Introduction to audiovisual metadata_ sessions during NDSR Immersion week? 
 - Where is the technical metadata? The descriptive metadata? Where are administrative values present?

 - Run MediaInfo with the Full option (`-f`) - what additional information is available in the output? 

5. There may be workflows where you do not want the general output from a metadata extraction tool. For example, you may just want to audit the wrapper formats or durations for a target set of files. You can specify which tags you want to output from MediaInfo. Try out these commands for any of the sample files:

            mediainfo --Inform="General;%FileName%" [file]


            mediainfo --Inform="Video;%Format%" [file]


            mediainfo --Inform="Audio;%SamplingRate%" [file] 

6. Now try to output only the values for: *duration, video bit depth, and audio compression mode* for a few different files. (HINT: Run `mediainfo --Language=raw [file]` to see the tag names as they need to be called as an option.) You can also throw the `--Inform` options together on the same line - so the combined command for Step #5 would look like:
            
            mediainfo --Inform="General;%FileName%" --Inform="Video;%Format%" --Inform="Audio;%SamplingRate%" [file]

  Want to dig down to a specific string within the full output? Find out from this [stackexchange answer](http://stackoverflow.com/a/26508567) from the MediaInfo creator/main developer. 

7. FROM 7/28/2016 in-person NDSR session. How to create formatted PBCore record outputs using MediaInfo:

            mediainfo --Output=PBCore fred_ott_sneeze_512kb.mp4 > fred-pbcore.xml
            
            mediainfo --Output=PBCore2 fred_ott_sneeze_512kb.mp4 > fred-pbcore2.xml

### Read metadata using ffprobe

ffprobe ["gathers information from multimedia streams and prints it in human- and machine-readable fashion"](http://ffmpeg.org/ffprobe.html). It, like MediaInfo, is a common metadata extaction and analysis tool that can be incorporated into workflows or used on its own. We will explore ffprobe as a standalone utility to understand its strengths, specifically in terms of surfacing information from specific streams within a given file. 

1. Like we did with MediaInfo, let's see what ffprobe's output is without any options. Enter the command below and read through the output - how does it differ (format and content) from the MediaInfo output for the same file?:

            ffprobe fred_ott_sneeze_512kb.mp4

2. Ok that's alot to parse, right? Let's cut it down by adding the `-hide_banner` option, which tells it to not print copyright, build, or library version info. Run:

            ffprobe fred_ott_sneeze_512kb.mp4 -hide_banner

3. Fun fact - you don't actually need ffprobe to find out this basic info! FFmpeg also allows you to find the same information about a file's contents' - run:

            ffmpeg -i fred_ott_sneeze_512kb.mp4 -hide_banner

 NB: FFmpeg will yell at you that atleast one output file is required. We can ignore that warning for now since we are just poking around the extracted metadata.

4. Back to ffprobe. Try all these commands (you can change the input file if you'd like to try another sample file) - what gets printed to the Terminal? Can you think of some use cases for isolating this information:

            ffprobe IMG_7770.mov -select_streams v:0 -show_entries stream=width,height -hide_banner

            ffprobe IMG_7770.mov -select_streams v:0 -show_entries stream=codec_type -hide_banner

            ffprobe IMG_7770.mov -select_streams v:1 -show_entries stream=codec_name -hide_banner

            ffprobe IMG_7770.mov -select_streams v:0 -show_entries stream=duration -hide_banner


## Recommended resources

- [ffprobe Tips from FFmpeg Wiki](https://trac.ffmpeg.org/wiki/FFprobeTips)

- If you're looking for the ability to read/write metadata in still image files, recommend checking out [ExifTool](http://owl.phy.queensu.ca/~phil/exiftool/). It has the ability to do metadata wrangling for a/v files, but MediaInfo and ffprobe are designed to support a/v while the focus of ExifTool has always been on still image (also has a great overview of IPTC metadata). 
