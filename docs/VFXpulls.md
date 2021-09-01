## VFX Pulls

<p align="center">
<img src="img/pipeline.jpg">
</p
 


Edit and Dailies typically work with lower resolution proxy files. Similar to the *conform*, a *VFX pull* is where these proxy files are swapped out for the high res files used for the final delivery to DI. The basic idea is that VFX returns the plate, with the VFX on it, *as if it were filmed that way*.

- **Debayering.** In an ACES pipeline VFX pulls should be debayered from the original raw camera files and exported as 16-bit EXR in the ACES AP0 exchange format (ACES2066-1). This should be done in a software that can properly debayer files in a color managed ACES workflow, such as DaVinci Resolve. Netflix has a great [step-by-step guide for Resolve](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360002088888-Color-Managed-Workflow-in-Resolve-ACES-) that will walk you through the process in detail. It's recommended that pulls are debayered and exported from the DI facility or a dedicated vendor who is aligned with the DI facility’s pipeline and setup in order to avoid debayering inconsistencies. 

- **Image Format.** Traditional 10-bit DPX files are not recommended, as they are unable to contain all the information captured by modern digital cameras. OpenEXR in contrast contains 30+ stops of exposure, and is the official ACES container format for the ACES2065-1 archival/interchange color space which contains the full gamut of what is visible to the human eye. If you are concerned about file sizes you can use PIZ lossless compression. The resulting EXR files will be *smaller* than a DPX file and even smaller than a PNG!

- **Ungraded footage.** All color correction and grades should be *disabled* for a VFX pull. An easy way to do this is to turn "Enable Flat Pass" in the Resolve Delivery options (again, see the above step-by-step guide). The goal is to apply the VFX as if it was filmed that way, so only the pixels that have VFX on them are changed, ensuring a perfect round-trip integration with the rest of the film footage. 

- **Color Reference and LUTs.** VFX pulls should include dailies color reference (QuickTime or reference frames) along with any CDLs and/or LUTs used in the dailies process. A .cube 3D LUT can be exported from Resolve, and will include all enabled grades, both in the timeline and the clips, so it will combine the Look Transform with your shot grade into a single LUT. This can be used as the *Shot LUT* for dailies. Editorial should provide proxy media format requirements for VFX proxy media that is to be delivered by the VFX vendor for inclusion in the offline project. This again involves applying the CDL or LUT in the color space in which it was created in order to match original dailies color.


[Back to main](../StdX_ACES)
