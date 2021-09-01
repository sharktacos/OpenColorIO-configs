# ACES for Indie Filmmakers

<p align="center">
<img src="img/pipeline.jpg">
</p>



## Dailies & Editorial
 
Dailies is where the camera RAW files, which will be used in finishing, are used to generate color-baked dailies and editorial media. One therefore needs a software that can properly debayer RAW camera files in a color managed ACES workflow. There are many software that can do this. For the indie filmmaker, a clear choice is [DaVinci Resolve](Resolve.md), since it is free. The RAW camera files would be read into Resolve, on-set color decisions can be communicated via ASC CDLs and be passed along into ALEs, and clips are exported out in Rec.709 color space as h.264 for Dailies viewing, and as ProRes or DNxHD for editorial. Since editorial is working with proxy video clips with the look baked-in, you can use whatever editing software you like.
 
## Conform & VFX Pulls
 
Similar to the *conform*, a *VFX pull* is where these proxy files are swapped out for the high res files used for the final delivery to DI. The basic idea is that VFX returns the plate, with the VFX on it, *as if it were filmed that way*.
 
The following guidance is compiled from the Nexflix Studio's [VFX Best Practices](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360000611467-VFX-Best-Practices) document.

- **Debayering.** In an ACES pipeline VFX pulls should be debayered from the original RAW camera files and exported as 16-bit EXR in the ACES AP0 exchange format (ACES2066-1). Again, there are many choices for color correction software. Let's assume we are using Resolve. For hi-res 4k output you might have to get the paid Resolve Studio, which is around 200 bucks. Netflix has a great [step-by-step guide for Resolve](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360002088888-Color-Managed-Workflow-in-Resolve-ACES-) that will walk you through the process in detail.  

- **Image Format.** Traditional 10-bit DPX files are not recommended, as they are unable to contain all the information captured by modern digital cameras. OpenEXR in contrast has a dynamic range of 30+ exposure stops with a wide gamut color space (ACES2065-1) that contains the full gamut of what is visible to the human eye. If you are concerned about file sizes you can use PIZ lossless compression. The resulting EXR files will be *smaller* than a DPX file and even smaller than a PNG!

- **Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull. An easy way to do this is to turn "Enable Flat Pass" in the Resolve Delivery options (again, see the above step-by-step guide). The goal is to apply the VFX as if it was filmed that way, so only the pixels that have VFX on them are changed, ensuring a perfect round-trip integration with the rest of the film footage. 

- **Color Reference and LUTs.** VFX pulls should include a color ‘recipe’ to achieve dailies color (i.e. CDL + LUT, working color space), and a reference frame for checking color against existing dailies. These are essential in order to send completed VFX shots back into the editorial cut with matching color to the surrounding shots. This LUT can be made in Resolve (the LUT's working/processing space will be ACEScc), and will include all enabled grades, both in the timeline and the clips, so it will combine the Look Transform with your shot grade into a single LUT. This can be used as the *Shot LUT* for dailies contained in the OCIO config. Editorial should provide proxy media format requirements for VFX proxy media that is to be delivered by VFX  for inclusion in the offline project. This again involves writing out the clip with the look baked-in. This is covered in the [Nuke doc](Nuke.md).


[Back to main](../StdX_ACES)
