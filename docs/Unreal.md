# Unreal Engine

Unreal Engine (UE) applies an ACES sRGB display transform by default ````ACES 1.0 SDR (sRGB - Display)```` with an added 1.45 gain added in. Consequently you don't really need to load OCIO in UE. What you need to do is have a way to view renders from UE in other apps like Nuke. For this we have custom input transforms in the config. More on that below.

The larger issue is how to incorporate UE with the rest of a VFX pipeline. For this we take the LED wall approach, and translate this into a purely digital environment. This begins with recognizing that what UE does best is render massive enviornments photrealistically in realtime. In other words, it makes a great 3D matte painting program i.e. it's great for generating background enviornments. 

What UE does not do as well is render hero elements, whether that's animated characters or FX like explosions. Therefore, we use Maya to render the hero elements and UE to render the environment. The part where we parallel the LED wall approach is in using the UE environment to light our hero elements. We do this through image based lighting (IBL).

## Image based lighting

You can use the [Panoramic Capture plugin](https://docs.unrealengine.com/5.0/en-US/panoramic-capture-tool-quick-start-for-unreal-engine/). The output bitdepth needs to be set to 32 which will then export an EXR. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/a5hy4QdcFGU" title="YouTube video player" frameborder="0" allow="accele rometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

https://forums.unrealengine.com/t/free-360-spherical-panorama-capture-tool-and-getting-trolled-by-marketplace-staff/212902/9



## Comping UE

1. Render the background environment in Unreal
2. Generate an IBL from that enviornment
3. Render CG hero elements in Maya, using the IBL
4. Comp the Unreal environment with the Maya CG in Nuke using the [Bridge](https://learn.foundry.com/nuke/content/comp_environment/unrealreader/unreal-intro.html)



