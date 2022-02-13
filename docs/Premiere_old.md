# Premiere Pro

## Overview

There are many possible ways to work in Premiere Pro. The most common is to work in Rec.709 with proxy video clips. These would later be swapped out with the high res footage in the [conform](VFXpulls.md) stage of production with an EDL. 

A second option is to work with high quality Prores 4444 files in log space (ACEScct). This maintains the full quality of the debayered footage. The difficulty is that when these are viewed in log this can lead to many inadvertent errors, such as writing out the files with two log spaces applied. Therefore it's important to view this color managed. It's also a lot nicer for everyone to edit a movie that doesn't look washed out! 

## Reading Apple Prores clips (color space: ACEScct)

The free [OCIO plugin for After Effects](https://fnordware.blogspot.com/2012/05/opencolorio-for-after-effects.html) also works in Premiere Pro. You just need to place it in the common plugin folder, which on Windows is:<br>

C:\Program Files\Adobe\Common\Plug-ins\7.0\MediaCore

You then simply read in the OCIOv2 config, and use a Display Transform: *in: ACEScct, Display: Filmic (Rec709).* Just like in Nuke this lets you work on the log image, but view it as it will look in the final film.

To export the clip you simply disable the OCIO display, and export in your desired format. This will export the clip "raw" i.e. in the same color space it was it was originally.

## Reading EXR Sequences (color space: AP0 ACES-2065-1)

This last option is generally not recommended because of the slow down in interactive speed in Premiere. If you really want to edit EXR files. Consider using AVID instead.

In the Sequence Settings turn  **Max Bit Depth** on if reading EXR files. Otherwise Premiere will clip any image values over 1. Using the OCIOv2 config, you will make two OCIO FXs, one to read in the files, and another to display them, with any image adjustments in between. So your FX layers would be:

   1. **OCIO input** (in: Premiere color space, out: ACEScct)<br>
   The Premiere input spaces are located in ````Input/Adobe````
   3. Grade in Luminare (in ACEScct log space)
   4.  **OCIO display** (in: ACEScct, out: Filmic Look)
   
   ![img](img/Premiere1.jpg)
 
Note that because Premiere adds a gamma adjustment to EXR files to bring it into its BT.1886/Rec.709 working space the config has a color space made for reading EXR files into Premiere: *Input - Premiere Pro - AP0 2.4 gamma* and *Input - Premiere Pro - AP0 2.4 gamma* which would be used as the input color space above.


[Back to main](../StdX_ACES)
