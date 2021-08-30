# Nuke

Nuke currently supports OCIOv1. To load the config Press “S” to access **Project Settings → Color**. Set *color managment* to "OCIO," select "custom" from the *OpenColorIO Config* dropdown and then enter the file path to the  ````StdX_ACES_OCIOv1.config```` file . 

![nk](img/Nuke1.png)

## Input Transforms

In Nuke the input transform is set in the color space dropdown menu of a Read node. 

Let's discuss some of the difficulties with inputting camera footage in VFX and how ACES greatly simplify and improve this. 

Knowing the right color space to choose for film plates can often be confusing. The files, typically DPX sequences or Prores clips, are often in the wrong color space. A client will for example say that the Prores movie is in Rec.709 when it is rather obviously in log, although what particular flavor of log is a mystery. Is it Cineon? Log-C? REDlog? Log3G10? If we knew the camera that was used this would be easier to determine, but this information is often unknown. To make matters worse, it's not uncommon to have a double log space applied, say cineon on top of Log-C. It's really a wild west out there. 

All of that thankfully becomes much simpler with ACES. In it's the core aim of ACES to unify the workflow so that there is consistency and predicability throughout every step of the film prodction pipeline. DPX files are not used at all, and instead the far superior EXR format is used (it is superior because it contains more file information at a smaller size than a DPX, so win win). That brings us down to four color spaces.

- **ACES2065-1** (**AP0** for short) - scene-linear space. This is the color space for EXR files exchanged between DI and VFX. 
- **ACEScg** linear. The color space for CG renders, and also the working space in Nuke.
- **ACEScc** and **ACEScct** - log space. In short these are two flavors of log that a colorist may prefer. ACEScc allows very precise control over deep shadows but can also be difficult to work with when not using the Log style grading tools. ACEScct is a more recent working space that compresses shadows similar to familiar camera log curves and which may be easier to grade. 

It's good practice to append the color space to the end of the file name for clarity: ````name_ap0.exr, name_cg.exr, name_cct.mov````. VFX would deliver the footage back to the client in the same color space it was ingested i.e. the color space on the Read and Write node should be the same so it is effectively a no-op in and out.


## Display Transforms

Nuke traditionally has three display transforms: sRGB, Rec.709, and BT.1886. There is often confusion regarding these. Many people think of Rec.709 as an aesthetic preference, that is, they chose it because they "like the look of it." It's important to understand that this is not the intent of a display transforms. Here's a quote from the Foundry,

> “To use the Viewer space correctly, it should be set to match the colour space of the device/monitor you are viewing it on. For example if you are using an sRGB calibrated monitor, then you should use an sRGB monitor space, or for a DCI-P3 calibrated monitor, you should use a DCI-P3 space in order to display it correctly. If you then have these two correctly calibrated monitors side by side, then the image you perceive from each one should be the same.”

The aim here is that when the same image is viewed side by side on a computer monitor (sRGB) and a HDTV (Rec.709) they will look the same. Rec.709 is the specification for HDTV and sRGB is the specification for a standard computer monitor. So the display transform is asking “What are you displaying this on?” Simply put, we have

- Rec.709 = I’m displaying this on a TV
- sRGB = I’m displaying this on a computer

Another point of confusion is that when DI says to VFX “we are working in Rec.709" because they have broadcast monitors at the DI facility calibrated to Rec.709 this does not mean that a comper should set their display transform to Rec.709 to match. The opposite is the case, if you were to set your sRGB monitor to have a Rec.709 display transform in Nuke, this would mean the images viewed side by side *would not match*. Again, one chooses the display transform based on the calibration of the display they are using. Since we will be doing the majority of our VFX work on the sRGB monitors in the labs, our config defaults to having sRGB selected for the Display transform in both Nuke and Maya. One would only need to change this if, for example, viewing dailies in 400a on an HDTV monitor (in which case it would be set to Rec.709).

Below you can see the display device in parenthesis. Most are in sRGB as this is usually what you are viewing on. The equivalent to Nuke's native sRGB would be un-tone-mapped (sRGB). For an explanation of all of these do, see the [tone mapping](tonemap.md) doc. You'll find information on the gamut compression in the section below. In red you can see the display device *Rec.1886 / Rec.709 video* which is for a Rec.709 broadcast monitor with Rec.1886 gamma (2.4). 

Finally, it's worth noting that when a client says they are working in Rec.709 they almost certainly mean gamma 2.4 (Rec.1886). Nuke's native Rec.709 has a non-standard gamma of approximately 1.95 which is much darker.

![img](img/Nuke4.png)

## Input/Output pipeline

Based on the above understandings, let's step back and overview the input and output pipeline. Remember in Nuke the input color space is set in the Read node and the output color space is set in the Write node.

The workflow for ACES going from DI (for example [Davinci Resolve](Resolve.md)) to VFX would be to initially input all the different camera footage using the appropriate camera manufacturer input transforms, work in ACEScc or ACEScct log space, and then output this as  ACES2065-1.  ACES2065-1 is the color space intended for transfer of files and for archiving. 

````Input: RAW CAMERA   >  Working: ACEScct  >  Output:  ACES2065-1````

Therefore, the ACES pipeline for compositing when receiving ACES footage would be:

````Input: ACES2065-1  >  Working: ACEScg  >  Display: sRGB````

Likewise, the delivery of VFX to DI from Nuke would be written  to ACES2065-1 (that is,  ACES2065-1 would be the color space on the Nuke write node). 

````Input: ACES2065-1 > Working: ACEScg  > Output: ACES2065-1````

As you can see, once the footage is input in and converted into ACES, one does not need to keep track of all the different color spaces because it’s always in the ACES exchange color space.

For reading renders into Nuke, since the EXR files are already in ACEScg the input (i.e the color space of the read node) would be  ACEScg.
	
````Input: ACEScg  >  Working: ACEScg >  Display: sRGB````

If you want to simply output a PNG sequence to make a Quicktime movie in Media Encoder (or output a Quicktime movie directly from Nuke) then the display transform is baked into the media (as set on the color space of the Nuke write node). This is the process of delivery and involves leaving the wide gamut working space of ACES, and encoding the image with the limited display space of the intended viewing device. The idea is that you want people to view things the same way you see them. So if you are viewing *Filmic (sRGB)* and what to make a movie to be viewed on the web you would choose that in the color space for your write node for output.
	
````Working: ACEScg >  Output: Filmic (sRGB)````

If you are delivering for viewing of dailies on a broadcast HDTV monitor you would set your output to 

````Working: ACEScg >  Output: Filmic (Rec.1886/Rec.709 video)````


## Gamut Compression and Nuke

Nuke is the primary place where gamut compression is applied. To understand this it's important to differentiate between two concepts:
 1. Gamut correction applied to the *view transform* which does not alter the image in any way.
 1. Gamut correction baked into an image

For phases of production such as on set monitoring, dailies, editorial, etc. it can be beneficial to *see* footage with gamut compression in order to get an idea of the final look, just as it can be good to see footage through a LUT. However, the gamut compression should not be applied to the footage. For this purpose the config contains View Transforms with gamut compression. 

![nk](img/Nuke2.png)

However, for VFX pulls a compositor will want to have unaltered footage. When that footage contains negative pixel values it can be really hard to do common compositing tasks like pull a key, denoise, or blur an image. This is where gamut compression comes in. Because the gamut compression algorithm only affects the pixels that are out of gamut, gamut compression in Nuke and VFX work can be thought of as "pixel healing" rather than color correction. 

Nuke is the ideal place to apply this gamut compression because the algorithm is designed to be applied in scene-linear (the working space of Nuke), and should be baked into all vfx returns. This is done with a Nuke node located in the ````software/Nuke```` folder of this config. This needs to be applied immediately after the Input Transform (i.e. directly after the Read node).

![nk](img/Nuke3.png)

This Nuke node is the fully functioning gamut compression algorithm, as opposed to the 3D LUT approximation contained in the OCIO config, which again is only intended for intermediate viewing purposes. Indeed, if comp were to bake the gamut compression into the EXR plates it sends to CG there would be no need to use the gamut compress View Transform in Maya.

Check out the [gamut compression](gamut.md) doc for more details and pretty pics!



[Back to main](../StdX_ACES)

