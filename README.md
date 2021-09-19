# StudioX ACES config

An OpenColorIO config based on the [ACES 1.2 Config](https://github.com/colour-science/OpenColorIO-Configs/tree/feature/aces-1.2-config/aces_1.2) and the [OCIOv2 demo config](https://opencolorio.readthedocs.io/en/latest/configurations/ocio_v2_demo.html) with added Look Transforms, gamut compression, and a few other goodies. Created for educational purposes and personal learning.

## Motivation

[ACES Next](https://community.acescentral.com/c/aces-development-acesnext/67) has identified several changes and improvements to the Output Transform that will be available at some furture date. Inspired by that work,  this config is to attempt to implement some of those changes as Look Transforms, to the extent that this is possible, as a stop-gap until ACES 2.0 is released.

## Configs

Three configs are provided

- **ANM_config.ocio**
   is designed for a CG animation pipeline 
- **ANM_config_Maya22.ocio**
   is the same, but using OCIOv2 for Maya 2022
- **VFX_config.ocio**
   is designed for a VFX pipeline integtrating CG and VFX into live action film.

For an overview of how the VFX pipeline fits into the whole filmmaking process, see [ACES for Indie Filmmakers](docs/VFXpulls.md)

## Look Transforms
  
The config adds three Look Transforms to the view transforms included the ACES config included in Maya 2022:

- **Neutral Look**
   is intended as a neutral starting point for color grading and lookdev work. 
- **Filmic Look**
   is intended for shot work and has a similar filmic look to the standard ACES 1.0 RRT, with slightly reduced contrast. 
- **Show** is for the show specific look LUT decided on by the director for the ANM config. This is combined with the Filmic Look.
- **Shot** is for the shot specific look LUT provided by the client for the VFX config. This is set with contextual variables in [Nuke](docs/Nuke.md).

The *Filmic* and *Neutral* Look Transforms provide differing flavors of [lower contrast tone mapping](docs/tonemap.md) as well as [highlight desaturation](docs/highlight.md) of blackbody color temperatures, and [reduced hue shifts](docs/chroma.md) compared to the default ACES 1.0 Output Transform.
  
The remaining view transforms are the same as the default Maya 2022 config.

- **ACES 1.0 SDR-video**
- **Un-tone-mapped** 
- **Raw** 
- **Log**

Additionally, the above transforms can alternately be viewed with the new [Gamut Compression](../docs/gamut.md).

## Software

Instructions for use of the config's Look Transforms in various software, including those that do not support OCIO:

- [Maya](docs/Maya.md) 
- [Nuke](docs/Nuke.md) 
- [Mari](docs/Mari.md) 
- [Substance Painter](docs/Substance.md) 
- [Houdini](https://www.sidefx.com/docs/houdini/io/ocio.html) 
- [Davinci Resolve](docs/Resolve.md) 
- [Photoshop](docs/Photoshop.md) 

  
