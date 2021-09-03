# ACES for Indie Filmmakers

<p align="center">
<img src="img/pipeline.jpg">
</p>

The advantage of the ACES color managed workflow is that it ensures that you see the same image throughout every stage of the filmmaking process, from on-set monitoring, to dailies and editorial, to VFX and DI. Everything just looks right everywhere along the pipeline. Plus it is at the highest quality so nothing is lost. And the whole thing is organized and managed to avoid mistakes and chaos. Using ACES from start to finih ensures continuity of artistic vision. However, if you are already started without ACES it's not a problem to introduce ACES at a later stage in the pipeline.

## On-set Monitoring

There are options from ACES product partners like [Pomfort LiveGrade Pro](https://pomfort.com/store/livegradepro/subscription/) for ACES on-set monitoring which enable filmmakers to view camera footage through an ACES transform on set. For low budget productions, ACES also gives [this advice](https://community.acescentral.com/uploads/default/original/1X/b8efb030fe699b9491fda084030779134c656cb3.pdf), 

> "On set, LUTs can be used, either in-camera   or in an external LUT box, that preview the base look in an ACES-based pipeline. These are available for [download at ACESCentral.com](https://community.acescentral.com/t/luts-that-emulate-the-aces-workflow/1334).  Even  without  a  dedicated  ACES  LUT,  if  the  default  Rec.  709  output  from  most cameras  is  used  for  on-set  monitoring,  it  is  similar  enough  to  the  look  of  ACES-based  content  that surprises   are   unlikely   when   ACES   is   used   in   post-production   (although   testing   is   strongly recommended)."



## Dailies & Editorial
 
Dailies is where the camera RAW files, which will be used in finishing, are used to generate color-baked dailies and editorial media. One therefore needs a software that can properly debayer RAW camera files in a color managed ACES workflow. There are many software that can do this. For the indie filmmaker, a clear choice is [DaVinci Resolve](Resolve.md) due to the low price point. The RAW camera files would be read into Resolve, on-set color decisions can be communicated via ASC CDLs and be passed along into ALEs. The clips are then exported out in Rec.709 color space as h.264 for Dailies viewing, and as ProRes or DNxHD for editorial. 

Since editorial is working with proxy video clips with the look baked-in, you can use whatever editing software you like. In other words, editorial is not working in ACES, but rather is working with proxy files that have the look of ACES baked into them. There is therefore no problem with software compatibility with ACES, and can work as they are accustomed with clips that look great, seeing in the edit suite the film as the director wants it to look. 

 
## Conform & VFX Pulls
 
Similar to the *conform*, a *VFX pull* is where these proxy files are swapped out for the high res files used for the final delivery to DI. The basic idea is that VFX returns the plate, with the VFX on it, *as if it were filmed that way*.
 
The following guidance is compiled from the Nexflix Studio's [VFX Best Practices](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360000611467-VFX-Best-Practices) document.

- **Debayering.** In an ACES pipeline VFX pulls should be debayered from the original RAW camera files and exported as 16-bit EXR in the ACES AP0 exchange format (ACES2066-1). Again, there are many choices for color correction software. Let's assume we are using Resolve. Netflix Studios has a great [step-by-step guide for Resolve](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360002088888-Color-Managed-Workflow-in-Resolve-ACES-) that will walk you through the process in detail.  

- **Image Format.** Traditional 10-bit DPX files are not recommended, as they are unable to contain all the information captured by modern digital cameras. OpenEXR in contrast has a dynamic range of 30+ exposure stops with a wide gamut color space (ACES2065-1) that contains the full gamut of what is visible to the human eye. If you are concerned about file sizes you can use PIZ lossless compression. The resulting EXR files will be *smaller* than a DPX file and even smaller than a PNG!

- **Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull. An easy way to do this is to turn "Enable Flat Pass" in the Resolve Delivery options (again, see the above step-by-step guide). The goal is to apply the VFX as if it was filmed that way, so only the pixels that have VFX on them are changed, ensuring a perfect round-trip integration with the rest of the film footage. 

- **Color Reference and LUTs.** VFX pulls should include a color ‘recipe’ to achieve dailies color (i.e. CDL + LUT, working color space), and a reference frame for checking color against existing dailies. These are essential in order to send completed VFX shots back into the editorial cut with matching color to the surrounding shots. This LUT can be made in Resolve (the LUT's working/processing space will be ACEScct or ACEScc based on the Project Settings), and will include all enabled grades, both in the timeline and the clips, so it will combine the Look Transform with your shot grade into a single LUT. This can be used as the *Shot LUT* for dailies contained in the OCIO config. Editorial should provide proxy media format requirements for VFX proxy media that is to be delivered by VFX  for inclusion in the offline project. This again involves writing out the clip with the look baked-in. This is covered in the [Nuke doc](Nuke.md).


[Back to main](../StdX_ACES)
