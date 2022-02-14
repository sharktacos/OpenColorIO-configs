# Exporting OpenEXR from camera RAW with Premiere Pro

## Overview

Broadly speaking Premiere is a great software for editing, but is limited in it's ability to debayer camera RAW files. That said, Premiere can debayer camera RW files from:

 - ARRI (.ari)
 - RED (.R3D)
 - Canon (.CRM)
 - MXF (Material Exchange Format is a container for many camera types, for example Sony. By default Premiere reads these in as Rec.709. You can however right-click the media and go to Source Settings where you can select the camera log space)
 
Using the OpenColorIO (OCIO) plugin it is then possible to export these to EXR. That workflow is decribed below.

Premiere can *not* properly debayer files from Black Magic cameras, nor can it properly interpret the following open file formats to log, instead displaying them in display-encoded Rec.709/BT.1886.

- Black Magic (.BRAW)
- CinemaDNG

For these Resolve will need to be used, which can debayer all camera RAW formats.

## Setup

  1. Download the free [OCIO plugin for After Effects](https://fnordware.blogspot.com/2012/05/opencolorio-for-after-effects.html) place it in the common plugin folder, which on Windows is:<br>

| Platform	| Path
|-----------|---------------------------------------------------------------
| Windows	| C:\Program Files\Adobe\Common\Plug-ins\7.0\MediaCore
| Mac	      | /Library/Application Support/Adobe/Common/Plug-ins/7.0/MediaCore/ 

Don't worry about the name, it works in both Premiere and After Effects.

  2. Download the [VFX_mini.ocio](https://github.com/sharktacos/OpenColorIO-configs/blob/main/software/Premiere/VFX_mini.ocio) config, which is configured specifically for converting camera RAW files to OpenEXR in Premiere. 

  3. In Premiere open the Sequence Settings and turn on  **Max Bit Depth**. Otherwise Premiere will clip any image values over 1. 
  4. **Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull.

## Camera log

Next the camera RAW file needs to be set to display in its native log space. This is done in the Effect Controls panel, and differs for each camera. For example for an ARRI camera you simply need to change to color space to LogC:

![img](img/premiereB1.jpg)

For a RED camera you need to first change the image pipeline from legacy to IPP2, and then set the Output Transforms Settings to match the Primary (RedWideGamutRGB color space, Log3G10 gamma)

![img](img/premiereB2.jpg)

This will display your footage in the log color space of your camera

![img](img/premiereB7.jpg)


## OpenColorIO (OCIO)

The OpenColorIO plugin is located in ````Effects > Video Effects > Utility > OpenColorIO````. 

![img](img/premiereB3.jpg)

Drag it onto the Effect Controls panel, under your camera RAW footage. Then click the Configuration drop-down menu, choose "custom" and load the [VFX_mini.ocio](https://github.com/sharktacos/OpenColorIO-configs/blob/main/software/Premiere/VFX_mini.ocio) file.

![img](img/premiereB4.jpg)

Next we need to convert from the log space of your camera into ACES scene-linear color space. in Convert mode, set the **Input Space** to your camera type. Below we have the settings for a RED camera.

![img](img/premiereB5.jpg)


## Exporting OpenEXR

Traditional 10-bit DPX files are not recommended, as they are not sufficient to contain all the information captured by modern digital cameras (For example RED camera RAW files are 16-bit and ARRI are 12-bit). In contrast, OpenEXR is 16-bit float with a dynamic range of 30+ exposure stops. That means it is able to preserve the full dynamic range of the camera RAW file at a reasonable file size. Using PIZ lossless compression an EXR file is actually smaller than a DPX.

Choose the ```File > Export > Media... ``` menu, and in the dialog choose the following options:

 - Format: OpenEXR
 - Compression: PIZ  
 - Bypass linear conversion: ON

![img](img/premiereB6.jpg)


[Back to main](../StdX_ACES)
