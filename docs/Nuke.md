# Nuke

Nuke currently supports OCIOv1. To load the config Press “S” to access **Project Settings → Color**. Set *color managment* to "OCIO," select "custom" from the *OpenColorIO Config* dropdown and then enter the file path to the  ````StdX_ACES_OCIOv1.config```` file . 

![nk](img/nuke1.png)

[Back to main](../StdX_ACES)

## Gamut Compression

First of all it's important to differentiate between two concepts:
 1. gamut correction applied to the *view transform* which does not alter the image in any way.
 1. Gamut correction baked into an image

For phases of production such as on set monitoring, dailies, editorial, etc. it can be beneficial to *see* footage with gamut compression in order to get an idea of the final look, just as it can be good to see footage through a LUT. For this purpose the config contains View Transforms with gamut compression. 

![nk](img/nuke2.png)

However, for VFX pulls a compositor will want to have unaltered footage. When that footage contains negative pixel values it can be really hard to do common compositing tasks like pull a key, denoise, or blur an image. This is where gamut compression comes in. Because the gamut compression algorithm only affects the pixels that are out of gamut, gamut compression in Nuke and VFX work can be thought of as "pixel healing" rather than color correction. 

Gamut compression needs to be applied in scene-linear (the working space of Nuke) and should be baked into all vfx returns. It needs to be applied imediatly after the Input Transform (i.e. the Read node). This is done with a Nuke node located in the ````software/Nuke```` folder of this config. 



Non-vfx can have it applied using the DCTL for [Resolve](Resolve.md) for example. This Nuke node is the fully functioning gamut compression algorythm, as opposed to the 3D LUT approximation contained in the OCIO config, which again is only intended for intermediate viewing purposes. Indeed, if comp were to bake the gamut compression into the EXR plates it sends to CG there would be no need to use the gamut compress View Transform in Maya.




