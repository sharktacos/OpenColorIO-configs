# Contents

## OCIO configs for Animation & VFX Pipelines 
OCIO Configs are provided for an ACES workflow for both [CG Animation and VFX pipelines](docs/configs.md). Each of these configs (ANM and VFX) has versions v1 and v2 of OCIO. Currently OCIO v2.0 is compatable with Maya Arnold (2022+), Nuke (v13.1+), Substance Painter (v7.4+), Mari (v5+), Houdini (v19). 

## VFX Pulls

Check out the [VFX Pulls](docs/VFXpulls.md), page for requirements, as well as an overview of ACES color management for the indie filmmaker! Included are detailed instructions of how to do a VFX Pull in DaVinci Resolve.


## AcesNext
The ACES Next Project has identified several changes and improvements to the Output Transform that will be available at some future date. Inspired by that work,  this config is to attempt to implement some of those changes as Look Transforms, to the extent that this is possible, as a stop-gap until ACES 2.0 is released. For details check out the pages on [tone mapping](docs/tonemap.md), [highlight desaturation](docs/highlight.md), [reduced hue shifts](docs/chroma.md), and the new [Reference Gamut Compression](docs/gamut.md). 

## <a name="software"></a>Software
Instructions for use of the configs in various software, including those that do not support OCIO:

- [Maya](docs/Maya.md) 
- [Nuke](docs/Nuke.md) 
- [Mari](docs/Mari.md) 
- [Substance Painter](docs/Substance.md) 
- [Houdini](https://www.sidefx.com/docs/houdini/io/ocio.html) 
- [Davinci Resolve](docs/Resolve.md) 
- [Premiere Pro](docs/PremierePull.md)
- [Photoshop](docs/Photoshop.md) 



