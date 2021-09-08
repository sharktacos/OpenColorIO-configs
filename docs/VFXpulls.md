# ACES for Indie Filmmakers

ACES (short for Academy Color Encoding System) was developed as an industry standard for color management used in every stage of the filmmaking process. It is based on solid color science and a wealth of production experience, and has been widely adopted in major film and VFX studios. Marvel for instance uses ACES for all of their films. However, ACES is not just for major tentpole productions and VFX blockbusters. Its open and independent nature means independent filmmakers can benefit from it too.

The advantage of the ACES color managed workflow is that it ensures that you see the same image throughout every stage of the filmmaking process, from on-set monitoring, to dailies and editorial, to VFX and DI. Everything just looks right everywhere along the pipeline. As cinematographer Erik Messerschmidt says, 

> "As a DP it's very important to me that the choices I make on set with the director perpetuate through the pipeline; from editorial, VFX, all the way to DI. ACES guarantees everyone is looking at a consistent representation of those choices."

Secondly, ACES ensures that the film footage stays at the highest quality, so nothing is lost along the way. Plus the whole pipeline is organized and managed to avoid mistakes and chaos. Using ACES from start to finish ensures continuity of artistic vision. 

Each section below will step you through the following diagram. Note that because of the way this workflow is designed, even if you have already started without ACES, it's not necessarily a problem to introduce ACES at a later stage (the latest being for conform and VFX pulls). The sooner color is managed, the better it will be for everyone.

<p align="center">
<img src="img/pipeline.jpg">
</p>

## On-set Monitoring

Modern digital cinema cameras raw or log modes have a known mathematical relationship to the light in the photographed scene, which ACES uses to bring it into the ACES color space. This is called an Input Transform. There are options from ACES product partners like [Pomfort LiveGrade Pro](https://pomfort.com/store/livegradepro/subscription/) for ACES on-set monitoring which enables filmmakers to view a live preview of the camera signal in the ACES color pipeline, and for a DIT (Digital Image Technician) to use the same tools as DI to create custom looks for on-set. 

There are however also options for low budget productions. You can create LUTs for your camera using the free version of Resolve and use these LUTs, either in-camera or in an external LUT box, for on-set viewing on a standard Rec.709 reference monitor. This ensures that what you see on-set is accurately carried all the way through production and post. See the [Resolve](Resolve.md) page for details.


## Dailies & Editorial
 
Dailies is where the camera RAW files, which will be used for the conform, are used to generate color-baked dailies and editorial media. The DIT therefore needs a software that can properly debayer RAW camera files in a color managed ACES workflow. There are many software programs that can do this. For the indie filmmaker, a clear choice is [DaVinci Resolve](Resolve.md) due to the low price point. The RAW camera files are read into Resolve using ACES color management, graded (including applying on-set color decisions via ASC CDLs) and then exported out with an ACES Rec.709 Output Transform as simple h.264 clips for Dailies viewing, and as ProRes or DNxHD clips for editorial.

Since editorial is working "offline" with proxy video clips with the ACES look baked-in, editors can work as they are accustomed in their tool of choice without concern for it being compatible with ACES. 
 
## Conform & VFX Pulls
 
The conform is where the proxy files are swapped out in the final edit for the original debayered camera RAW files. For example, working in Resolve with ACES, the DIT uses an EDL/AAF/XML file provided by editorial to swap in the original debayered camera RAW files. This again needs to be done in a software that can properly debayer RAW camera files in a color managed ACES workflow, such as DaVinci Resolve. In a traditional workflow these files are then passed to DI, either as Camera RAW files on rare occasion or more typically as integer log DPX files. The ACES workflow replaces this with its official interchange and archival format: 16-bit OpenEXR in ACES2065-1 color space. The advantage is that the ACES interchange format is able to hold all of the quality and dynamic range of the original camera RAW files whereas DPX cannot.

Traditional 10-bit DPX files are not recommended, as they are [not sufficient](https://acescentral.com/uploads/default/original/1X/25ec1472d70b169ceabb215beacdd501d1a27fac.pdf) to contain all the information captured by modern digital cameras (For example RED camera RAW files are 16-bit). In contrast, [OpenEXR](https://www.openexr.com/) is 16-bit float with a dynamic range of 30+ exposure stops, and a wide gamut color space (ACES2065-1) that contains the full color gamut visible to the human eye (see graphic below). In short: Using 10-bit DPX involves a degradation of quality from the original camera footage, while EXR *more than* covers the full quality and range of any camera RAW file. If you are concerned about file sizes with EXR there's more good news: You can use PIZ lossless compression, and the resulting EXR files will be *smaller* than DPX files! 

<p align="center">
<img src="img/gamuts.jpg" width=70%>
</p>

A *VFX pull* involves "pulling" select film plates from the conform and sending them to VFX so they can add their magic to them. This is likewise exported with the ACES  "interchange" image format.  Let's take a look at that process in detail:

- **Debayering to OpenEXR.** VFX pulls should be debayered from the original RAW camera files and exported as 16-bit EXR in the ACES AP0 interchange format (ACES2065-1). Netflix Studios has a great [step-by-step guide for Resolve](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360002088888-Color-Managed-Workflow-in-Resolve-ACES-) that will walk you through the process in detail.  

- **Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull. An easy way to do this is to turn on "Enable Flat Pass" in the Resolve Delivery advanced options (again, see the above step-by-step guide). The basic idea is that VFX returns the ungraded plate to DI, with the VFX added, so that DI gets the full quality film plate back *as if it were filmed that way*. DI can then seamlessly insert it back into the conform and color grade everything together.

- **Color Reference and LUTs.** VFX pulls should include a reference frame for checking color against existing dailies as well as a color ‘recipe’ to achieve dailies color i.e. CDL + LUT, working color space. The LUT's working color space will be ACEScct or ACEScc based on the Project Settings in Resolve. VFX needs to know this in order to properly process the LUT in comp. In Resolve the "generate LUT" command can be used to export all enabled grades, both in the timeline and the clip, so it will combine the Look Transform with your shot grades including any CDL all into a single LUT. This can be exported as a *Shot LUT* for VFX to use.

- **VFX Delivery.** VFX can deliver two types of files:
  - *Proxy media to editorial for inclusion in the offline edit.* As in the Dailies process above, the ACES transform is baked into the proxy media in the color space of the reference monitor used by editorial (typically Rec.709 with Rec.1886 gamma). Editorial should provide proxy media format requirements to VFX. 
  - *High resolution ungraded OpenEXR files are sent to DI for the final color grade and finishing.* The EXR files are returned to DI in the same interchange format they were received: ACES2065-1 AP0. This ensures that the master has the highest possible quality, which can accommodate any delivery medium or targeted display type, now and into the future. 


## Digital Intermediate, Mastering, and Delivery

From [Cinematic Color](https://raw.githubusercontent.com/jeremyselan/cinematiccolor/master/ves/Cinematic_Color_VES.pdf),
> "Digital intermediate (DI) is the process where the entire motion-picture is loaded into a dedicated hardware device, for the purpose of color-correcting in an environment that exactly mirrors the final exhibition (e.g., in a theater). Viewed in this final environment, DI is where per-shot color corrections are added, and the visual look of the film is finalized. DI is also referred to as “color timing,” or “grading.” The final step of baking in view transforms specific to an output device, and final color correction, is known as mastering."

In our ACES workflow DI reads in the the files from conform, as well as VFX shots, into an ACES capable color corrector (Resolve, Baselight, etc.) and grades the film, viewing this through the appropriate ACES Output Transform for the targeted display. For example the Output Transform would be set to DCI-P3 for viewing on a film projector.

Typically one particular viewing environment is identified as the “gold standard,” and the majority of the artistic time is spent correcting the images to look perfect on that display device. Once the main color grade is complete, additional masters are handled as *trim passes*. A trim pass involves relatively minor adjustments, made atop the reference master, needed to make the film look great in the different viewing environment. Traditionally theatrical digital projection was most often the appropriate master to treat as the "gold" reference. As HDR displays become more common this is changing and an HDR display is used as the "gold" starting point, with SDR trim passes made from it. [Nick Shaw](https://community.acescentral.com/t/odt-without-changing-the-grade-and-round-trip-from-premier/2258/2) explains,

> "The intent is that your grade will look “the same” on different displays each with the appropriate Output Transform. There are, of course a few caveats, which mean that a trim pass done in the intended viewing environment on a particular display type is important. But just switching Output Transform will give you a good start point. <br><br>Where a display type has a wider dynamic range and/or gamut that the one you used when initially grading, you will see aspects of the image that it was not possible to see originally. You may well want to adjust the grade if a practical light or background sky becomes distractingly bright, or a colour distractingly saturated. <br><br>Equally, if you do your initial grade in a wide gamut and/or high dynamic range format you are able to do things which cannot be replicated in Rec. 709. The default result of switching Output Transform may lose some of the creative intent, and it may be necessary to make slightly different choices for each scene and shot to maintain the intended look. <br><br>Although, for example, Rec. 709 and DCI-P3 versions may be “the same” when the appropriate Output Transforms are used, because the screen size, absolute luminance, display technology (emissive vs. reflective) and viewing environment are different, the same image may be perceived differently by the audience. Therefore you should trim the two versions so that they “feel the same” when viewed separately, rather than “look the same” when viewed side by side."

[Back to main](../StdX_ACES)
