# Unreal Engine

Unreal Engine (UE) applies an ACES sRGB display transform by default ````ACES 1.0 SDR (sRGB - Display)```` with an added 1.45 gain added in. Consequently you don't really need to load OCIO in UE. What you need to do is have a way to view renders from UE in other apps like Nuke. For this we have custom input transforms in the config. More on that below.

The larger issue is how to incorporate UE with the rest of a VFX pipeline. For this we take the LED wall approach, and translate this into a purely digital environment. This begins with recognizing that what UE does best is render massive enviornments photrealistically in realtime. In other words, it makes a great 3D matte painting program i.e. it's great for generating background enviornments. 

What UE does not do as well is render hero elements, whether that's animated characters or FX like explosions. Therefore, we use Maya to render the hero elements and UE to render the environment. The part where we parallel the LED wall approach is in using the UE environment to light our hero elements. We do this through image based lighting (IBL).

## Image based lighting

You can use the [Panoramic Capture plugin](https://docs.unrealengine.com/5.0/en-US/panoramic-capture-tool-quick-start-for-unreal-engine/). The output bitdepth needs to be set to 32 which will then export an EXR. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/a5hy4QdcFGU" title="YouTube video player" frameborder="0" allow="accele rometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

https://forums.unrealengine.com/t/free-360-spherical-panorama-capture-tool-and-getting-trolled-by-marketplace-staff/212902/9

1. With your project open, select Edit > Plugins from the main menu. 
2. From the Plugins menu, under Movie Capture, enable the Panoramic Capture plugin. Restart the editor when prompted. 
3. By default, the Content Drawer does not show plugin content. To change this, select Settings (located in the top right corner of the Content Browser), then enable Show Engine Content and Show Plugin Content.
4. In the Content Drawer, browse to ```EngineData > Plugins > PanoramicCapture Content > Assets```
5. Drag the BP_Capture Blueprint onto the scene.
6. Double-click BP_Capture Blueprint to open the blueprint.
7. In the blueprint, change the Output Bitdepth to 32. This will generate an EXR render. The default output of the BP_Capture Blueprint is 8-bit (.png), with 32-bit (.exr) as an optional setting in the Blueprint.  
8. Set the SP.OutputDir to ```SP.OutputDir``` which will output the render somewhere next to your unreal engine folder. Then, you’ll get the images in your project folder/Saved/StereoPanorama by default. For UE 5 there is a problem with the OutputDir string checking inside SceneCapturer.cpp that the devs should look into.
9. has a valid path for saving the render to disc. Note that on Windows you need to use back slashes (\).
10. Set the 
11. Click Play to kick off the BP_Capture and start the capture process. 

During the capture process, the editor might appear to be frozen or unresponsive for a few seconds up to a few minutes. This is due to the demanding rendering requirements of the Panoramic Capture plugin. When the editor becomes responsive again, you will be able to find the screenshots in the following location.

    Unreal Projects\[Project Name]\Saved\SterioPanorama\[Date & Time]\FinalColor\Frame_00000_FinalColor.png 


## Comping UE

1. Render the background environment in Unreal
2. Generate an IBL from that enviornment
3. Render CG hero elements in Maya, using the IBL
4. Comp the Unreal environment with the Maya CG in Nuke using the [Bridge](https://learn.foundry.com/nuke/content/comp_environment/unrealreader/unreal-intro.html)
5. 


