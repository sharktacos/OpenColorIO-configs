An OpenColorIO config based on the [ACES 1.2 Config](https://github.com/colour-science/OpenColorIO-Configs/tree/feature/aces-1.2-config/aces_1.2) and the [OCIOv2 demo config](https://opencolorio.readthedocs.io/en/latest/configurations/ocio_v2_demo.html) with added Look Transforms.

# Motivation

[ACES Next](https://community.acescentral.com/c/aces-development-acesnext/67) has identified several changes and improvements to the Output Transform that will be available at some furture date. Inspired by that work,  this config is to attempt to implement some of those changes as Look Transforms, to the extent that this is possible, as a stop-gap until ACES 2.0 is released.

# Look Transforms
  
The config adds three Look Transforms to the view transforms included the ACES config included in Maya 2022:

- **Neutral Look**
   is intended as a neutral starting point for color grading and lookdev work. 
- **Filmic Look**
   is intended for shot work and has a similar filmic look to the standard ACES 1.0 RRT, with slightly reduced contrast. 
- **Show** is for the show specific look LUT decided on by the director. This could optionally be combined with the Filmic or Neutral Look if desired.

The *Filmic* and *Neutral* Look Transforms provide the following improvments to the RRT:
  - [Lower Contrast Tone Mapping](../docs/tonemap.md)
  - [Gamut Compression](../docs/gamut.md)
  - [Highlight Desaturation](../docs/highlight.md)
  - [Reduced Hue Shifts](../docs/chroma.md)
  
The remaining view transforms are the same as the default Maya 2022 config.

- **ACES 1.0 SDR-video**
- **Un-tone-mapped** 
- **Raw** 
- **Log**

# Software

Instructions for use of the config's Look Transforms in various software, including those that do not support OCIO:

- [Maya](../docs/Maya.md) (OCIOv2)
- [Premiere Pro](../docs/Premiere.md) (OCIOv2)
- [Nuke](../docs/Nuke.md) (OCIOv1)
- [Mari](../docs/Mari.md) (OCIOv1)
- Houdini 
- [Substance Painter](../docs/Substance.md) 
- [Davinci Resolve](../docs/Resolve.md) 
- [Photoshop](../docs/Photoshop_v2.md) 
  
  



  



