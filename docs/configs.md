# ANM and VFX Configs

The ANM config ````ANM_config.ocio```` is designed for work on CG animation shorts and features. The VFX config ````VFX_config.ocio```` in contrast is designed for integrating CG and VFX with live action film. Consequently each has different Display Transforms geared for its particular pipeline needs.

## ANM Config

![img](img/Nuke_view_anm.png)

### View Transforms

- **ACES 1.0 SDR - RGC** <br> The standard ACES RRT with added RGC (see below).
- **Low Contrast Look - RGC** <br> Look transform that lowers contrast of the ACES Output Transform a wee bit intendewd to provide a neutral starting point for lookdev work. This is done using an ASC CDL transform which mirrors lowering contrast in Resolve to 0.85 in log space (ACEScct).
- **Film Print Look - RGC** <br> Look transform for film print emulation. Based on [Alex Fry's Nuke implementation](https://github.com/alexfry/NukeAnalyticLMTs) of the [Academy Analytic LMT 3](https://community.acescentral.com/t/lmts-part-4-how-do-they-work-and-how-are-they-made-continued/1217) with some added tweaks: restoring saturation (chroma raised from 0.7 to 0.85), lifting the shadows (gamma lowered from 1.5 to 0.95), and introducing a color balance (warmth 0.1, tint 0.03) to lessen the "yellow dinge" a bit, and bringing back green (reducing the hue rotation of green to yellow from -15 to -10). I like it, YMMV.
- **Show Look** <br> Look transform for the show specific look LUT decided on by the director for the ANM config. See "Shot LUTs" below for setup.
- **Un-tone-mapped** <br> The default Nuke transform without tone mapping. Intended for diagnostic purposes only. See the [tone mapping](tonemap.md) page for details on the importance of ACES tone-mapping for CG work and integration with film.

- **RGC - Referrence Gamut Compression** <br> Note above where the view transforms have "RGC" in their name they contain added [Referrence Gamut Compression (RGC)](gamut.md). For CG renders this has the happy accident of [highlight desaturation](highlight.md) of blackbody color temperatures, and [reduced hue shifts](chroma.md). Note that this is not the case for the VFX config below, where the RGC is applied as a comp node in Nuke.

### Display Transforms
A View Transform is paired with a Display Transform corresponding to the display it is being viewed on.

- **Gamma 2.0** <br> For viewing on artist's computer monitors. This uses the pure gamma 2.2, rather than the piece-wise sRGB EOTF. If an image is encoded for a 2.2 display, but shown on a piece-wise sRGB display in can appear a bit low contrast. Conversely if an image is encoded for a piece-wsie sRGB display, but shown on a pure gamma 2.2 display the shadows will appear crushed. Since there is no way to control the calibration of a viewers computer monitor, best practice is for artists  to work in pure gamma 2.2.
- **Apple Display P3** <br> Display transform for the MacBookPro M1 XDR display in the wider P3 gamut used for film with a pure 2.2 gamma. This display transform also contains options for HDR display.

The remaining view transforms are the same as the default Maya 2022 config and are used for diagnostic purposes.

- **Raw** 
- **Log**


## VFX Config
   
![img](img/Nuke_view_vfx.png)

As noted above, in a VFX pipeline [gamut compression](Nuke.md#gamut-compression-and-nuke) is applied as a node in VFX and thus not included in the Display Transform. 

The VFX config has the following views:

- **ACES 1.0 SDR - (RGC)** The standard ACES RRT
- **Shot Look** This view transform uses contextual variables to apply the shot-specific look LUT provided by the client to the view. The variables are defined in the config and can be set by the artist. See below.
- **Un-tone-mapped** is the equivalent to Nuke's native sRGB which is a simple sRGB Gamma function without [tone mapping](tonemap.md). 

Each of these above views is paired with an output display:

- **sRGB** For viewing on artist's computer monitors calibrated to sRGB Peicewise EOTF
- **Gamma 2.0** For viewing on artist's computer monitors calibrated to pure gamma 2.2
- **Rec.709 - BT.1886 HDTV** For viewing in editorial on a Rec.709 (Gamma 2.4) reference monitor or on a HDTV display for dailies. 

There are again transoforms for diagnostic purposes.
- **Raw** For checking renders
- **Log** For checking comps

And finally there is 
- **DPX Shot Look** for displaying client LUTS from a display-referred non-color managed pipeline. See below.

# Shot & Show LUTs 

Both the **Show Look** from the ANM config and the **Shot Look** and **DPX Shot Look** view transforms from the VFX config use contextual variables to apply the shot-specific look LUT provided by the client to the view. The variables are defined in the config and can be set by the artist. **Shot Look** is intended for LUTs in an ACES pipline (the client is delivering EXR files in ACES2065-1 color space) and **DPX Shot Look** is for LUTs in a non-color managed display-referred pipeline (ther client is delivering DPX in the log space of the oroiginal camera raw).

The config has the following section at the top.

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
Because the config file uses OCIOv2 it is self-contained and does not require external LUTs, instead using built-in mathematical transforms. Therefore each artist can simply copy the ```VFX_config.ocio``` file into their local directory for the show they are working on, and edit the file setting the above variables to correspond to the location (*LUT_PATH*) and name (*LUT_NAME*) of the LUT for the shot they are working on. Additionally if the client is delivering a LUT for display-referred DPX footage, the color space of the original camera should be entered into the **CAMERA** variable to set the log space for the **Shot Look DPX** display transform. 

In the StudioX VFX directory structure, the OCIO config directory is parallel to the shots directory:

- **Show/**
  - <b>shots/</b>SM_020_018/01_Client_Original_Footage/5_LUT/clientShotLUTname_ACEScct.cube
  - <b>ocio/</b>VFX_config.ocio

Therefore to go up a directory simply use ```../``` at the front of the file path. Like so:

````
  LUT_PATH: ../shots/SM_020_018/01_Client_Original_Footage/5_LUT/ 
````
The *SHAPER* variable refers to the working color space the LUT was created in (this is referred to as a "shaper" LUT). This will be either ACEScct or (less commonly) ACEScc, based on the Project Settings in DaVinci Resolve. VFX needs to know this in order to properly process the LUT in comp. It is good practice to have the client append the shaper space to the file name for clarity. See the [VFX Pulls](VFXpulls.md) guide for details on requirements for VFX pulls. 

Below is the first part of a two part video series covering how to use the VFX config both for when the client is working in ACES and also when then are still using the display-referred workflow, and how to integrate that into a color managed ACES pipeline for VFX.

<iframe src="https://player.vimeo.com/video/670932268?h=22be11d525" width="640" height="360" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
