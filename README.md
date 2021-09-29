# StudioX ACES configs

An OpenColorIO config based on the [ACES 1.2 Config](https://github.com/colour-science/OpenColorIO-Configs/tree/feature/aces-1.2-config/aces_1.2) and the [OCIOv2 demo config](https://opencolorio.readthedocs.io/en/latest/configurations/ocio_v2_demo.html) with added Look Transforms, gamut compression, and a few other goodies. Created for educational purposes and personal learning.

# <a name="software"></a>Software

Instructions for use of the configs in various software, including those that do not support OCIO:

- [Maya](docs/Maya.md) 
- [Nuke](docs/Nuke.md) 
- [Mari](docs/Mari.md) 
- [Substance Painter](docs/Substance.md) 
- [Houdini](https://www.sidefx.com/docs/houdini/io/ocio.html) 
- [Davinci Resolve](docs/Resolve.md) 
- [Photoshop](docs/Photoshop.md) 

# Overview
Configs are provided for both Animation and VFX pipelines. Each of these has configs in OCIOv1 and OCIOv2. Currently only Maya 2022 can read a v2 OCIO config.

## VFX config
- *OCIOv1_config_VFX.ocio.ocio*
   is designed for a VFX pipeline integtrating CG and VFX into live action film.
 - *OCIOv1_config_VFX.ocio.ocio*
   is the same, but using OCIOv2 for Maya 2022
   
This config has a **Shot** view transform which uses variables to apply the shot specific look LUT provided by the client. For an overview of how the VFX pipeline fits into the whole filmmaking process, see [ACES for Indie Filmmakers](docs/VFXpulls.md)

## ANM config
- *OCIOv1_config_ANM.ocio.ocio*
   is designed for a CG animation pipeline 
 - *OCIOv1_config_ANM.ocio.ocio*
   is the same, but using OCIOv2 for Maya 2022
  
The config adds three Look Transforms to the view transforms included the ACES config included in Maya 2022:

- **Neutral Look**
   is intended as a neutral starting point for color grading and lookdev work. 
- **Filmic Look**
   is intended for shot work and has a similar filmic look to the standard ACES 1.0 RRT, with slightly reduced contrast. 
- **Show** is for the show specific look LUT decided on by the director for the ANM config. This is combined with the Filmic Look.

The *Filmic* and *Neutral* Look Transforms provide differing flavors of [lower contrast tone mapping](docs/tonemap.md) as well as [highlight desaturation](docs/highlight.md) of blackbody color temperatures, and [reduced hue shifts](docs/chroma.md) compared to the default ACES 1.0 Output Transform.
  
The remaining view transforms are the same as the default Maya 2022 config.

- **ACES 1.0 SDR-video**
- **Un-tone-mapped** 
- **Raw** 
- **Log**

Additionally, the above transforms can alternately be viewed with the new [Gamut Compression](docs/gamut.md).



  
