# Exporting OpenEXR from camera RAW with Premiere Pro

## Overview

For debayering camera RAW files into OpenEXR our recommended workflow is exporting an XML file from Premiere, importing this into Davinci Resolve, and dabayer your footage there. Broadly speaking Premiere is a great software for editing in Rec.709, but was not designed for scene-referred color management or debayering camera RAW footage. If you would like to go this route for a VFX pull, it is [outlined here](VFXpulls.html).

It is possible to debayer camera RAW footage in Premiere for some camera RAW types (ARRI and RED), and export OpenEXR files using OpenColorIO (OCIO). That alternate workflow is decribed below.

Note that traditional 10-bit DPX files are not recommended, as they are not sufficient to contain all the information captured by modern digital cameras (For example RED camera RAW files are 16-bit). In contrast, OpenEXR is 16-bit float with a dynamic range of 30+ exposure stops. 

We work in an [ACES pipeline](VFXpulls.html) for VFX, but are also able to accomidate other workflows. 

## Setup

  1. Download the free [OCIO plugin for After Effects](https://fnordware.blogspot.com/2012/05/opencolorio-for-after-effects.html) place it in the common plugin folder, which on Windows is:<br>

| Platform	| Path
|-----------|---------------------------------------------------------------
| Windows	| C:\Program Files\Adobe\Common\Plug-ins\7.0\MediaCore
| Mac	      | /Library/Application Support/Adobe/Common/Plug-ins/7.0/MediaCore/ 

Don't worry about the name, it works in both Premiere and After Effects.

  2. Download [this OCIO config](https://github.com/sharktacos/OpenColorIO-configs/blob/main/software/Premiere/VFX_mini.ocio) which is configured specifically for converting camera RAW files to OpenEXR in Premiere. 

  3. In Premiere open the Sequence Settings and turn on  **Max Bit Depth**. Otherwise Premiere will clip any image values over 1. 

## Camera log

Next the camera RAW file needs to be set to display in its native log space. This is done in the Effect Controls panel, and differs for each camera. For example for an ARRI camera you simply need to change to color space to LogC:

![img](img/premiereB1.jpg)

For a RED camera you need to first change the image pipeline from legacy to IPP2, and then set the Output Transforms Settings to match the Primary (RedWideGamutRGB color space, Log3G10 gamma)

![img](img/premiereB2.jpg)

## OpenColorIO (OCIO)

The OpenColorIO plugin is located in ````Effects > Video Effects > Utility > OpenColorIO````. 

![img](img/premiereB3.jpg)

Drag it onto the Effect Controls panel, under your camera RAW footage. Then click the Configuration drop-down menu, choose "custom" and load the [VFX_mini.ocio](https://github.com/sharktacos/OpenColorIO-configs/blob/main/software/Premiere/VFX_mini.ocio) file.

![img](img/premiereB4.jpg)

With the Configutation toggled to "convert" Set the Input Space to your camera type, and the Output Space to either **ACES2065-1** if you are working in ACES, or to **scene-linear Rec709-sRGB** if you are not. Below we have the settings for a RED camera going to scene-linear Rec709-sRGB.

![img](img/premiereB5.jpg)




On the RAW file Effect Controls make sure the Output Transform Settings are set to match the Primary settings for Color Space and Gamma, and that the Output Tone Map and Highligh Roll-Off are both set to "none".  

Using the OCIOv2 config, you will make two OCIO FXs (located in ````Effects > Video Effects > Utility > OpenColorIO````), one to read in the files, and another to display them. So your FX layers would be:

   1. **OCIO input** (in: Camera color space, out: ACES2065-1)<br>
   For example for a RED camera the transform is in the ````Input/Camera/RED``` folder
   2.  **OCIO display** (in: ACES2065-1, out: Rec.709 BT1886 HDTV)
   The out transform should be set to match the display you are viewing on, so Rec.709 BT1886 HDTV would be for viewing on a reference broadcast monitor. If viewing on a computer monitor you would instead use Gamma 2.2.
   
To export a file in EXR disable the OCIO display above. This will put the file into ACES2065-1 space. Then export the media with the following settings:
   - Format: OpenEXR
   - Compression: PIZ
   - Bypass linear conversion: ON
   
   ![img](img/Premiere1.jpg)
 


[Back to main](../StdX_ACES)
