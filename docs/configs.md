# ANM and VFX Configs

The ANM config ````ANM_config.ocio```` is designed for work on CG animation shorts and features. The VFX config ````VFX_config.ocio```` in contrast is designed for integrating CG and VFX with live action film. Consequently each has different Display Transforms geared for its particular pipeline needs.

## ANM Config

![img](img/nuke6.jpg)

The Display Transforms for the above ANM config are all in either sRGB or Gamma 2.2 display for viewing on artist's computer monitors. Additionally, the Apple P3 Display is included for use with a MacBookPro M1 display. Each display type contains two modifications of the standard ACES view transform using Look Transforms that customize them for the animation pipeline and incorporate visual improvements over the standard display, based on the feedback given from artistists for the ACESNext project. 

**Neutral Look** is intended as a neutral starting point for lookdev work. 

**Filmic Look** is intended for lighting shot work and has a similar filmic look to the standard ACES 1.0 RRT, with slightly reduced contrast. 

You can read details about the *Neutral Look* and *Filmic Look* look transoforms on the [tone mapping](tonemap.md) page.  Additionally, both Look Transforms provide [highlight desaturation](docs/highlight.md) of blackbody color temperatures, and [reduced hue shifts](docs/chroma.md) compared to the default ACES 1.0 Output Transform. Finally, the new [Referrence Gamut Compression (RGC)](docs/gamut.md) is baked into all of the display tranforms (including the ACES 1.0 SDR)  to address hue shifts in CG renders with ACES. Note that Reference Gamut Compression (RGC) is not baked into the view for the [VFX config](#VFX-Config) )

**Show Look** is for the show specific look LUT decided on by the director for the ANM config. This Look is combined with the Filmic Look.

The remaining view transforms are the same as the default Maya 2022 config and are used for diagnostic purposes.

- **Un-tone-mapped** 
- **Raw** 
- **Log**


## VFX Config
   
![img](img/nuke5.jpg)

The Display Transforms for the above VFX config contain sRGB, Gamma 2.2, and Apple P3 displays for viewing on the corresponding computer monitors as well as  BT.1886/Rec.709 for viewing in editorial on a Rec.709 reference monitor or on a HDTV display for dailies. In a VFX pipeline [gamut compression](gamut.md) is applied as a node in VFX and thus not included in the Display Transform. The views include the standard **ACES 1.0 RRT**, **Shot Look** (see below) for each display type, as well as several diagnostic views (**un-tone-mapped, Raw, Log**), and finally **Shot Look DPX** for displaying client LUTS from a display-referred non-color managed pipeline. **Un-tone-mapped** is the equivalent to Nuke's native sRGB which is a simple sRGB Gamma function without [tone mapping](tonemap.md).  

**Shot Look** This view transform uses contextual variables to apply the shot-specific look LUT provided by the client to the view. The variables are defined in the config and can be set by the artist.

````
# ---------------- Per Shot Grade Variables ------------------------- #
environment:
#--------------
# example path: ../shots/SM_020_018/01_Client_Original_Footage/5_LUT/
#--------------
  LUT_PATH: path_to/shot_lut/
  LUT_NAME: clientShotLUTname_ACEScct.cube
#--------------
# Camera aliases are: ARRI, RED, CLog2, CLog3, 
# Sony, SonyCine, SonyVenice, SonyVeniceCine, ADX10
#--------------
  CAMERA: ARRI
  SHAPER: ACEScct
# ------------------------------------------------------------------- # 
````
Each artist would have a VFX config file in their local directory for the show they are working on, and set the above variables to correspond to the location (*LUT_PATH*) and name (*LUT_NAME*) of the LUT for the shot they are working on. Additionally if the client is not working in ACES and is instead delivering display-referred DPX footage, the color space of the original camera should be entered into the **CAMERA** variable to set the log space for the **Shot Look DPX** display transform. In the StudioX VFX directory structure, the OCIO config directory is parallel to the shots directory:


- **Show/**
  - <b>Shots/</b>SM_020_018/01_Client_Original_Footage/5_LUT/clientShotLUTname_ACEScct.cube
  - <b>StdX_ACES/</b>OCIOv1_config_VFX.ocio

Therefore to go up a directory simply use ```../``` at the front of the file path. Like so:

````
  LUT_PATH: ../shots/SM_020_018/01_Client_Original_Footage/5_LUT/ 
````

With the variables set, The OCIO config will then display that shot LUT in the program they load the OCIO config into (Maya, Nuke, etc.). The *SHAPER* variable refers to the working color space the LUT was created in (this is referred to as a "shaper" LUT). This will be either ACEScct or (less commonly) ACEScc, based on the Project Settings in DaVinci Resolve. VFX needs to know this in order to properly process the LUT in comp. It is good practice to have the client append the shaper space to the file name for clarity. See [ACES for Indie Filmmakers](VFXpulls.md#require) for details on requirements for VFX pulls.


<iframe src="https://player.vimeo.com/video/670932546?h=ffdbf2d358" width="640" height="360" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
