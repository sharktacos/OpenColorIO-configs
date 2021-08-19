# Motivation

[ACES Next](https://community.acescentral.com/c/aces-development-acesnext/67) has identified several changes and improvements to the Output Transform that will be available at some furture date. Inspired by that work,  this config is to attempt to implement some of those changes as Look Transforms, to the extent that this is possible, as a stop-gap until ACES 2.0 is released.

# Look Transforms
  
The config adds three Look Transforms to the view transforms included the ACES config included in Maya 2022:

- **Neutral Look**
   is intended as a neutral starting point for color grading and lookdev work. It reduces contrast (by a factor of 0.85 in log space) pulling the shadows and highlights slightly out of the toe and shoulder curves, to make more of the shot range visible. 
- **Filmic Look**
   is intended for shot work and has a similar filmic look to the standard ACES 1.0 RRT, with a little less contrast, resulting of less crushing of shadows. 
- **Show** is for the show specific look LUT decided on by the director. This could optionally be combined with the Filmic or Neutral Look if desired.

The *Filmic* and *Neutral* Look Transforms provide following improvments to the RRT:
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

Instructions for use of the config's Look Transforms is various software, including those that do not support OCIO:

- [Maya](../docs/Maya.md)
- [Nuke](../docs/Nuke.md)
- [Substance Painter](../docs/Substance.md)
- [Premiere Pro](../docs/Premiere.md)
- [Davinci Resolve](../docs/Resolve.md)
  
  
## Color Spaces
**Pick - sRGBlin desat**
  
Defined as color picking role to pick colors in sRGB/Rec.709 primaries with slight desaturation (0.85 based on rec709 luma) resulting in colors having around 0.95 max saturation. Standard computer color pickers lead artists to pick extremely saturated neon colors. With the Rec2020 gamut of ACEScg this is exaserbated. The motivation is to have a color picker which encourages artists to pick painterly colors, meaning one has to lower the luminance to achieve deeply saturated colors.<p>



  



