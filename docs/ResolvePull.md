# VFX Pulls in Resolve

For more information about the ACES implementation in Davinci Resolve, please go to the ‘Color Management using ACES’ chapter in the “The Data Levels, Color Management, and ACES” section of the latest DaVinci Resolve Manual.

The following is from the [Netflix Partner Help Center](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360002088888-Color-Managed-Workflow-in-Resolve-ACES-). If you like video instruction, you may also want to check out the following videos made by Netflix in partner ship with Blackmagic:

[ACES Set Up in DaVinci Resolve](https://www.youtube.com/watch?v=u9Rvm5xiuhk&list=PLsJrJgQkAdTnNB5sbmkRLZaZkcd63W8Nb&index=4)
[ACES Deliveries in DaVinci Resolve](https://www.youtube.com/watch?v=2-H3jgXXTiQ&list=PLsJrJgQkAdTnNB5sbmkRLZaZkcd63W8Nb&index=5)

## Project Settings

Once you create a new project, go to the Project Settings > Color Management panel. The first thing you will want to change is the Color Science settings to **ACEScct**. If you don’t have a specific reason to use ACEScc, it is recommended to use ACEScct. 

Generally, we recommend using the latest ACES version.

Set your ACES Output Device Transform to match the calibration and capacities of your video display:

 - For SDR, this will be **Rec. 709**, which corresponds to a monitor calibrated to Rec. 709 / BT.1886 with 100 cd/m2 peak luminance.
    
![img](img/Netflix1.jpg)

 - For HDR, this will be P3-D65 ST.2084 (PQ) with the corresponding nit level your monitor is capable of. Today, most commonly, this will be P3-D65 ST2084 (1000 nits). 

![img](img/Netflix2.jpg)

Notes: 

 - *Make sure the ACES Mid Gray Luminance setting stays at 15.00 throughout the whole grading and finishing process.*

 - *Process Node LUTs will only apply in the event that you are loading LMTs as LUTs to the project. The setting will vary depending on how those LMTs were generated. Note that "Process node luts in: ACEScc:AP1 timeline space" is a bit of a misnomer. With this setting Resolve will process luts in the AP1 timeline space that set in the coresponding "Color Science" section above (set here to ACEScct).*

 - *An important note is that when the ACES Output Device Transform is set to **None**, Resolve will output ACES images a.k.a. ACES 2065-1 or ACES Linear (AP0).*

## Bringing in Clips

By default, for RAW clips, Resolve will automatically debayer images into ACES and you should see a normal looking image. 

For non-RAW formats (such as MXF, DPX, ProRes, XAVC, etc), Resolve may not automatically detect the color space, and read the footage in with the native camera log color space. An indication of this is if your image looks washed out, which is typical of log footage. 

In such cases you will need to manually select your ACES Input Device Transform (IDT). You can do this by right-clicking on a shot or group of shots in the Media Pool, as shown in the screenshot below. 

*Example: you shot XAVC on the Sony F55 using the SLog3-SGamut3.CINE color space, and bring these clips into the Media Pool. Resolve is not able to recognize this based on the metadata, so you must manually select “Sony SLog3 SGamut3CINE” from the ACES Input Device Transform dropdown list.*

![img](img/Netflix3.jpg)

You may also set your Project to *default* to a specific ACES Input Device Transform. This may be handy if the majority of your clips will be in a common color space and cannot be auto-detected. 

*TIP: Sorting your Media Pool by “Format” or “Video Codec” columns can help batch-assign IDTs to groups of clips highlighted at one time. See screenshot below for an example.*

![img](img/Netflix4.jpg)

## Rendering

When you are ready to render your deliverables, open up the Deliver page.
 
**IMF Master, Video Display Master (VDM) or Quicktime references**

When rendering images in display color spaces, such as those required for IMF Master deliverables, a VDM source for IMF creation, or Quicktime references, make sure your ACES Output Transform is enabled and matches the intended display type. For example if sending clips to editorial for offline editing of proxy media viewed on a broadcast reference monitor, the Output Transform would be set to "Rec709" (HDTV). If sending clips to VFX as reference the Output Transform would be set to "sRGB" for display on a computer monitor.
 
**VFX Pulls**

 - **Set color space to ACES2065 (AP0)** This done in Resolve by disabling the ACES Output Transform in order to output ACES AP0/Linear data as shown below. This puts the clip in ACES2065-1 used for interchange if images between facilities or softwares in an ACES pipeline, such as VFX plates. Disabling the Output Transform will display your footage in scene-linear color space, which will appear dark. This is expected. 

![img](img/Netflix5.jpg)

 - **Disable all grades** To disable the grade for your VFX render, the **Enable Flat Pass** option on the **Deliver** page can be used. See screenshot from the DaVinci Resolve Manual below. The basic idea is that VFX returns the ungraded plate to DI, with the VFX added, so that DI gets the full quality film plate back *as if it were filmed that way*. DI can then seamlessly insert it back into the conform and color grade everything together. 

![img](img/Netflix6.jpg)

 - **Disable ACES gamut compression** Frame pulls for VFX should have the ACES Reference Gamut Compression (RGC) *DISABLED* in Resolve. This can be done in the Color Management Settings. The RGC will be added by VFX in the returned plates.

![img](img/Netflix8.jpg)

Ensure you have the following render settings:

 - **Render:** 	Single Clip
 - **File Type:** 	EXR
 - **Codec:** 	RGB half, PIZ lossless compression (note: this is 16-bit half float)
 - **Render Resolution:** 	Equal to the scene’s Working Format
 - **ACES Output Device Transform (in Project Settings):** 	No Output Transform (ACES2065-1)
 - **Apply ACES Referece Gamut Compress (in Project Settings):** OFF
 - **Enable Flat Pass:** 	Always On

![img](img/Netflix7.jpg)

*Tip: The setting ‘Force debayer to highest quality’  will automatically select what Resolve considers to be the highest debayering quality for each RAW file on the timeline. This may differ from your own findings. Please feel free to select your preferred debayering algorithm instead, and untick this option if you prefer.*




[Back to VFX Pulls](VFXpulls.md)
