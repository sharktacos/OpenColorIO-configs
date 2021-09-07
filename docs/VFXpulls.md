# ACES for Indie Filmmakers

ACES (short for Academy Color Encoding System) is a color management system designed to work with every stage of the filmaking process, using solid color science and a wealth of production experience. It is used in major tentpole productions and VFX blockbusters, but its open and independant nature also means independant filmmakers can benefit from it too.

The advantage of the ACES color managed workflow is that it ensures that you see the same image throughout every stage of the filmmaking process, from on-set monitoring, to dailies and editorial, to VFX and DI. Everything just looks right everywhere along the pipeline. As cinematographer Erik Messerschmidt says, 

> "As a DP it's very important to me that the choices I make on set with the director perpetuate through the pipeline; from editorial, VFX, all the way to DI. ACES guarantees everyone is looking at a consistent representation of those choices."

Secondly, ACES ensures that the film footage stays at the highest quality, so nothing is lost along the way. Plus the whole pipeline is organized and managed to avoid mistakes and chaos. Using ACES from start to finish ensures continuity of artistic vision. 

Each section below will step you through the following diagram. Note that because of the way this workflow is designed, even if you have already started without ACES, it's not necesarily a problem to introduce ACES at a later stage (the latest being for conform and VFX pulls). The sooner color is managed, the better it will be for everyone.

<p align="center">
<img src="img/pipeline.jpg">
</p>

## On-set Monitoring

Modern  digital  cinema  cameras raw or log modes have a known mathematical relationship to  the  light  in  the  photographed  scene. ACES uses these exact transfer functions supplied by each camera manufacturer to bring it into the ACES color space. This is called an Input Transform. There are options from ACES product partners like [Pomfort LiveGrade Pro](https://pomfort.com/store/livegradepro/subscription/) for ACES on-set monitoring which enable filmmakers to view camera footage through an ACES Input Transform and for a DIT (Digital Image Technician) to use the same tools as DI to create custom looks for on-set. 

There are however also options for low budget productions. You can create LUTs for your camera using the free version of Resolve and use these LUTs, either in-camera or in an external LUT box, for on-set viewing on a standard Rec.709 reference monitor. This ensures that what you see on-set is accurately carried all the way through production and post. See the [Resolve](Resolve.md) doc for details.


## Dailies & Editorial
 
Dailies is where the camera RAW files, which will be used for the conform, are used to generate color-baked dailies and editorial media. The DIT therefore needs a software that can properly debayer RAW camera files in a color managed ACES workflow. There are many software programs that can do this. For the indie filmmaker, a clear choice is [DaVinci Resolve](Resolve.md) due to the low price point. The RAW camera files are read into Resolve using ACES color management, graded (including applying on-set color decisions via ASC CDLs) and then exported out with an ACES Rec.709 Output Transform as simple h.264 clips for Dailies viewing, and as ProRes or DNxHD clips for editorial.

Since editorial is working "offline" with proxy video clips with the ACES look baked-in, editors can work as they are accustomed in their tool of choice without concern for it being compatible with ACES. An important thing to understand about this proxy workflow is that it lets editorial focus on editing, firewalling it off from color correction as well as from concerns with preserving the original camera files dynamic range, which editing software lack the tools to properly handle.
 
## Conform & VFX Pulls
 
The conform is where the proxy files are swapped out in the final edit for the original debayered camera RAW files. For example, working in Resolve with ACES, the DIT uses an EDL/AAL/XML file provided by editorial to swap in the original debayered camera RAW files. This again needs to be done in a software that can properly debayer RAW camera files in a color managed ACES workflow, such as Davinci Resolve. These files are then passed to DI, either as Camera RAW files or in the ACES exchange format: 16-bit OpenEXR in ACES2065-1 color space, which is able to hold all of the quality and dynamic range of the original camera RAW files (see below for mor details on this).

A *VFX pull* involves "pulling" select film plates from the conform and sending them to VFX so they can add their magic to them. This is likewise exported with the ACES  exchange" image format.  Let's take a look at that process in detail:

- **Debayering to OpenEXR.** VFX pulls should be debayered from the original RAW camera files and exported as 16-bit EXR in the ACES AP0 exchange format (ACES2065-1). Netflix Studios has a great [step-by-step guide for Resolve](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360002088888-Color-Managed-Workflow-in-Resolve-ACES-) that will walk you through the process in detail.  

- **Why not DPX?** Traditional 10-bit DPX files are not recommended, as they are [not sufficient](https://acescentral.com/uploads/default/original/1X/25ec1472d70b169ceabb215beacdd501d1a27fac.pdf) to contain all the information captured by modern digital cameras (For example RED camera RAW files are 16-bit). In contrast, [OpenEXR](https://www.openexr.com/) is 16-bit float with a dynamic range of 30+ exposure stops, and a wide gamut color space (ACES2065-1) that contains the full color gamut visible to the human eye (see graphic below). In short: Using 10-bit DPX involves a degradation of quality from the original camera footage, while EXR *more than* covers the full quality and range of any camera RAW file. If you are concerned about file sizes with EXR there's more good news: You can use PIZ lossless compression, and the resulting EXR files will be *smaller* than DPX files! 

<p align="center">
<img src="img/gamuts.jpg" width=70%>
</p>

- **Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull. An easy way to do this is to turn on "Enable Flat Pass" in the Resolve Delivery advanced options (again, see the above step-by-step guide). The basic idea is that VFX returns the ungraded plate to DI, with the VFX added, so that DI gets the full quality film plate back *as if it were filmed that way*. DI can then seamlessly insert it back into the conform and color grade everything together.

- **Color Reference and LUTs.** VFX pulls should include a reference frame for checking color against existing dailies as well as a color ‘recipe’ to achieve dailies color i.e. CDL + LUT, working color space. The LUT's working color space will be ACEScct or ACEScc based on the Project Settings in Resolve. VFX needs to know this in order to properly process the LUT in comp. In Resolve the "generate LUT command can be used to export all enabled grades, both in the timeline and the clip, so it will combine the Look Transform with your shot grades including any CDL all into a single LUT. This can be exported as a *Shot LUT* for VFX to use.

- **VFX Delivery.** VFX can deliver two types of files:
  - *Proxy media to editorial for inclusion in the offline edit.* As in the Dailies process above, the ACES transform is baked into the proxy media in the color space of the reference monitor used by editorial (typically Rec.709 with Rec.1886 gamma). Editorial should provide proxy media format requirements to VFX. 
  - *High resolution ungraded OpenEXR files are sent to DI for the final color grade and finishing.* The EXR files are returned to DI in the same exchange format they were received: ACES2065-1 AP0. This ensures that the master has the highest possible quality, which can accommodate any delivery medium or targeted display type, now and into the future. 


[Back to main](../StdX_ACES)
