# Reading key A/V metadata

The following information is related to the _NDSR 2016 Immersion Week - Automating Procedures for Digital Asset Management_ presentation also found in this GitHub repository. 

## Overview

The activities and discussion points below provide an overview of the scenarios where adding, deleting, or modifying metadata in audiovisual files might take place. 


## Getting started

The first question we need to address is: *why are you trying to modify metadata?*

For this workshop, we will be working with writing metada to individual test files. This is not necessarily the scenario you'll be faced with during your residencies. Hopefully, any writing of metadata would be done by batch (preferably scripted or using an existing tool) as part of a workflow dictated by policy.


### DISCUSSION: Sharing metadata modification scenarios

1. Individually, brainstorm scenarios where you might need to *intervene and modify technical, descriptive, or administrative metadata*.

2. Document these scenarios as use cases, using this format:

   _As a_ [ROLE], _I need_ [REQUIREMENT] _so that_ [BENEFIT].

 For example, a use case for modifying metadata might be:

   _As an archivist, I need to embed my institution's copyright notice into all access derivatives of our Video Collection so that when these access derivatives are released to the public, users will see the rights information for each file they are interested in using._

3. Let's discuss.


### ACTIVITY: Add descriptive metadata to A/V files

1. Open Terminal. `cd` to the Desktop copy of _av-metadata-samples_ folder.

2. We are going to use FFmpeg to write metadata in a key,value pair into an A/V file. Tools that write metadata only or default options frequently create a temporary file or create a new output file with updated metadata values. This is useful for testing commands because it does not overwrite your original file. We want to add a dummy *title* to the file _test1.mkv_. We can do that using the FFmpeg command:

        ffmpeg -loglevel quiet -i test1.mkv -codec copy -metadata title="My title" test1-out.mkv

*ffmpeg* | starts the command

*-loglevel quiet* | show nothing at all from the library's set log level 

*-i input_file* | path, name and extension of the input file

*-codec copy* | a complex filtergraph using the fps filter to set frame rate, the scale filter to resize. The scale value of -1 preserves the aspect ratio

*-metadata title=""* | sets metadata option for tag "title" with text between the double quotes

*output_file* | path, name and extension of the output file (make sure it's different than the source filename so there are no conflicts!)

3. Using the format in Step #2, try to update other metadata in other provided sample files. NB: assigning an empty value ("") will delete metadata from the field. Review the [`-metadata` docs](http://ffmpeg.org/ffmpeg.html#Main-options) for more information and check out the resources in the next section for metadata tag IDs and more command examples. 

## Recommended resources 

- [FFmpeg Metadata Wiki](https://wiki.multimedia.cx/index.php?title=FFmpeg_Metadata)
- [How To: Create/Write ID3 tags using ffmpeg](http://jonhall.info/how_to/create_id3_tags_using_ffmpeg) by John Hall (2016?)
- [Supplying FFmpeg With Metadata](http://multimedia.cx/eggs/supplying-ffmpeg-with-metadata/) by "Multimedia Mike"
 (2010)
