# VFX Pulls and ACES Color Management

Cameras are able to capture high dynamic range images, containing a huge gamut of colors and multiple stops of exposure. This is known as *scene-referred* data because it captures the light values of the physical scene the camera was pointing at. However, displays are not as capable as cameras in terms of dynamic range and color. So in order to look correct on a display, some of the image data must be thrown away in order to fit or limit the data to the range of the particular display, whether that's a computer monitor, a TV, an HDR display, or a movie projector. This is known as *display-referred* or *display-encoded* data where the data is limited to fit onto the particular display.

For a VFX pull, the camera RAW files need to be debayerd and saved out in a format that preserves the full quality and dynamic range of the original camera RAW files in scene-referred space. The basic idea is that VFX returns the ungraded plate to DI, with the VFX added, so that DI gets the full quality film plate back *as if it were filmed that way*. DI can then seamlessly insert it back into the conform, and color grade everything together. This ensures that the master contains all the original camera data so it can accommodate any delivery medium or targeted display type. 

Many editing programs (for example Premiere Pro) lack the ability to properly process and display these scene-referred files. Therefore the common practice is for VFX to deliver both the wide gamut high dynamic range files to the conform and DI, and also deliver display-encoded proxy media to (offline) editorial. Typically this would be Prores or DNxHD files in Rec709 color space, which is the standard for broadcast HDTV. This workflow is shown in the diagram below. 

<p align="center">
<img src="img/pipeline.jpg">
</p>

Our preferred format for these scene-referred files is ACES, the Academy Color Encoding System. If you are unfamiliar with ACES, [this video](https://www.youtube.com/watch?v=vdmFjFoE2YA&list=PLsJrJgQkAdTnNB5sbmkRLZaZkcd63W8Nb&index=8), created by Netflix Studios, offers a great overview of the advantages of an ACES color managed workflow for filmmakers. Specifically for VFX work, the two main reasons we use ACES are quality and control. First, ACES ensures that your film footage stays at the absolute highest dynamic range and color fidelity. As shown in the graphic below, the ACES interchange format, known as ACES2065-1 (AP0) has a wide gamut color space that contains every color visible to the human eye, meaning it can accommodate any delivery medium or targeted display type, now and into the future. 

<p align="center">
<img src="img/gamuts.jpg">
</p>

Additionally, these files are 16-bit float with a dynamic range of over 30 exposure stops. As a point of comparison, the most of any digital cinema camera RAW file is 15 stops. So ACES files far exceed the dynamic range of any camera RAW file, at a file size that is smaller than a DPX! The second benefit is consistency and control. Unlike DPX files, which can have any number of log color spaces with no way of knowing which one you have, because the ACES image format represents an industry (SMPTE) standard, the whole image pipeline is controlled and managed, taking out the guesswork and avoiding mistakes and chaos when passing images between facilities.

# <a name="require"></a>VFX Pull Requirements

**Debayering to OpenEXR.** VFX pulls should be debayered from the original RAW camera files and exported in the ACES file interchange format (ACES2065-1) with PIZ lossless compression. 

 - Format: OpenEXR 16-bit half float
 - Compression: PIZ lossless compression
 - Color Space: ACES2065-1 (AP0)
 - All color grades disabled 
 - ACES Gamut Compression disabled

This should be done in a software that supports an ACES color managed workflow and can properly debayer the camera RAW files. A great choice for the filmmaker on a budget is DaVinci Resolve. The free version has a resolution limit of Ultra HD (3840 x 2160), but the full software is just $300 dollars for a permanent license, which is a steal for people being able to afford a subscription for Adobe, and certainly less than paying a DI facility to perform a VFX pull!

The guide below will walk you through the process:
 - [VFX Pulls with Resolve](ResolvePull.md)

**Color Reference and LUTs.** VFX pulls should include:
  - *A reference frame for checking color against existing dailies.* <br>This should be an 8-bit JPG or PNG in sRGB color space. A screengrab works fine.
  - *A "shot LUT" to achieve dailies color, along with the working color space.* <br>In Resolve the "generate LUT" command can be used to export all enabled color grades, both in the timeline and the clip, including any CDLs, all into a single *Shot LUT* for VFX to use. The LUT's working color space, i.e. the color space it was created in, should be noted in the file name, (for example ````shot01_ACEScct.cube```` for Resolve). VFX needs to know this in order to properly process the LUT in comp.

# <a name="vfx-deliver"></a>VFX Delivery

VFX can deliver two types of files:
  - *Proxy media to editorial for inclusion in the offline edit.* <br> The ACES transform (as well as any client provided shot LUTs) are baked into the proxy media in the color space of the reference monitor used by editorial (typically Rec.709 with Rec.1886 gamma). Editorial should provide proxy media format requirements to VFX. 
  - *High resolution ungraded OpenEXR files with VFX added are sent to DI for the final color grade and finishing.* <br>The EXR files are returned to DI in the same interchange format they were received: ACES2065-1 AP0. 



[Back to main](../StdX_ACES)
