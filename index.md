# Contents

## ACES OCIOv2 config for CG Animation and VFX studio pipelines
OCIO Config for an ACES workflow for both [CG Animation and VFX pipelines](docs/configs.md), based on the [Academy Software Foundation's CG and Studio configs](https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES) optimized for our university's studio pipeline.

The config is for OCIO v2 with older versions in the "legacy" folder. Currently OCIO v2.0 is compatable with Maya Arnold (2022+), Nuke (v13.1+), Substance Painter (v7.4+), Mari (v5+), Houdini (v19). 

## VFX Pulls

Check out the [VFX Pulls](docs/VFXpulls.md), page for requirements, as well as an overview of ACES color management for the indie filmmaker! Included are detailed instructions of how to do a VFX Pull in DaVinci Resolve.

## ACES 1.3
ACES introduced [Reference Gamut Compression](docs/gamut.md) which requires OCIO 2.1 and is thus currently not compatible with most DCC apps. While waiting for this, the config contains both a 3D LUT for viewing with the gamut compression (applied to the [ANM - Studio Look](docs/configs.md)) as well as an analytic Nuke node.

## <a name="software"></a>Software
Instructions for use of the config in various software, including those that do not support OCIO:

- [Maya](docs/Maya.md) 
- [Nuke](docs/Nuke.md) 
- [Mari](docs/Mari.md) 
- [Substance Painter](docs/Substance.md) 
- [Houdini](https://www.sidefx.com/docs/houdini/io/ocio.html) 
- [Davinci Resolve](docs/Resolve.md) 
- [Premiere Pro](docs/PremierePull.md)
- [Photoshop](docs/Photoshop.md) 



