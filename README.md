# Modified assets to capture IIDX title and intro sequences without HUD elements
This repository provides modified assets that remove any kind of text and HUD elements
from intro and title sequences of IIDX games. This allows video capturing the rendered
sequences which look better for use in SGL.

## Steps
A few notes/steps how I have done this for the existing assets.

* Figure out which images need to be removed. For example: "Network Off", "Free Play"
* Find the appropriate system.idx files
* Open in a hex editor and check where clip data and names start
* Modify offsets in gcz2tga.c, recompile
* Dump the system.idx file using the compiled gcz2tga
* Look for the labels, e.g. FREEPLAY, EAMU_OFF, etc
* Take the clip data offset and go there using a hex editor
* Skip x and y data and modify width and height, set width to 1 and height to 0 -> makes the graphic invisible
* Don't use width 0 and height 0. The engine doesn't like that and starts to mess up other graphics as well
* Some stuff is rendered text and must be modified in the executable (e.g. GAME LEVEL, VER: JXX)

## Post Processing
Some notes for post processing the captured videos for mastering.

avidemux:
video output: mpeg4 avc (x264), configure -> quality 0 (highest)
audio: copy
output format: MP4 Muxer
