

<p align="center">
<img src="img/pipeline.jpg">
</p>

# <a name="require"></a>VFX Pull requirements:

**Debayering to OpenEXR.** VFX pulls should be debayered from the original RAW camera files and exported as 16-bit EXR in the ACES AP0 interchange format (ACES2065-1) with PIZ lossless compression. This can be done in either Resolve or Premiere. Note that the process in Resolve is much more streamlined and robust than in Premiere, which was not designed for color management or ACES workflows.

 - [VFX Pulls with Resolve](ResolvePull.md)
 - [VFX Pulls with Premiere](PremierePull.md)

**Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull. An easy way to do this is to turn on "Enable Flat Pass" in the Resolve Delivery advanced options (again, see the above step-by-step guide). The basic idea is that VFX returns the ungraded plate to DI, with the VFX added, so that DI gets the full quality film plate back *as if it were filmed that way*. DI can then seamlessly insert it back into the conform and color grade everything together.

**Color Reference and LUTs.** VFX pulls should include 
  - *A reference frame for checking color against existing dailies.* <br>This should be an 8-bit JPG or PNG in sRGB color space. A screen grab works fine.
  - *A "shot LUT" to achieve dailies color, along with the working color space.* <br>In Resolve the "generate LUT" command can be used to export all enabled grades, both in the timeline and the clip, including any CDLs, all into a single *Shot LUT* for VFX to use. The LUT's working color space, i.e. the color space it ws created in, should be noted in the file name (For example ````shot01_ACEScct.cube```` for Resolve and ````shot01_Rec709.cube```` for Premiere). VFX needs to know this in order to properly process the LUT in comp. 

# <a name="vfx-deliver"></a>VFX Delivery.

VFX can deliver two types of files:
  - *Proxy media to editorial for inclusion in the offline edit.* <br>As in the Dailies process above, the ACES transform (as well as any client provided shot LUTs) are baked into the proxy media in the color space of the reference monitor used by editorial (typically Rec.709 with Rec.1886 gamma). Editorial should provide proxy media format requirements to VFX. 
  - *High resolution ungraded OpenEXR files with VFX added are sent to DI for the final color grade and finishing.* <br>The EXR files are returned to DI in the same interchange format they were received: ACES2065-1 AP0. This ensures that the master has the highest possible quality, which can accommodate any delivery medium or targeted display type. 



[Back to main](../StdX_ACES)
