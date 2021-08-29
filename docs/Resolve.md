# Davinci Resolve

## scene-referred vs display-referred 

Traditionally colorists work in what is called a *display-referred* workflow, meaning the colorist needs to *refer* to the *display* and basically just eyeball footage to manually get it to look good. If one were for example reading in footage from a RED camera, they would read in the raw camera file in IPP2 using Log3G10 REDwideGamutRGB and see the washed out image below. The colorist would begin with this washed out image in log space, and grade it manually until it looked nice.

![pic](img/Resolve10.png)

ACES instead works in a *scene-referred* workflow, meaning film footage is input using the mathematical transform provided by the camera maufacturer to read in the raw footage. Here's that same RED footage in ACES. This is the starting point that the colorist then begins with, allowing them to focus on the artistic look of the film, beginning with a digital image that has been digitally “developed” according to the exact mathematical specifications of each particular camera manufacturer. 

![pic](img/Resolve11.png)

However, while everyone is happy with these ACES Input Transforms, a lot of colorists (DITs) are not as happy with the ACES Output Transform which they find has too much of a "look" on it. They would prefer a more *neutral* starting point to begin their grading work from. That's the motivation for the [Look Transforms](tonemap.md) of this config. Here's a side by side comparison of the ACES Output Transform and the **Neutral Look** transform. You can read more details about these Look Transforms [here](tonemap.md).

![pic](img/Resolve12.png)


## Viewing Looks in the *ACES Output Device Transform*

To use the *Filmic* and *Neutral* Look LUTS, the .cube files need to be placed into the Davinci Resolve LUT directory, which you can get to by clicking "Open LUT folder" in the Preferences, copying the files, and then clicking "update lists" to refresh. 

![Resolve](img/Resolve2.jpg)

The two .cube Look LUT files are called:

````studio/LMT_filmic_AP1_shaper.cube```` <br>
````studio/LMT_neutral_AP1_shaper.cube````

A colorist may wish to use the Neutral Look for example as a starting place for grading instead of the default ACES Output Transform which many find to not be very neutral. See the [tone mapping](tonemap.md) doc for details and pretty pics.

## Gamut Compression

Gamut compression is done in Davinci Resolve Studio using a DCTL file which you will find in the ````software/Resolve/GamutCompress.dctl```` folder of the config. Place this into the Davinci Resolve LUT directory as described above. 

Gamut compression needs to be applied before anything else, immediately after the Input Transform (IDT) so that all grading operations are downstream of the compression. Gamut compression should be disabled when delivering a VFX pull so it is not baked into the EXR on export. 

See the [Nuke](Nuke.md) section on gamut compression for more details on this workflow, and the [Gamut Compression](gamut.md) doc for an overview with example pics. 

## Timeline vs Clip

Gamut compression can be applied to an individual clip or blanket applied to all footage since, unlike the former “Blue Light LMT” the algorithm only affects the necessary pixels of the image leaving the rest untouched.

Similarly, a Look Transform (LMT) conceptually should be applied across an entire scene or show, before the Output Transform. This can be done in Resolve by applying the LUT to the timeline instead of to an individual clip. To do this, in the Color module Node Editor set the drop-down to timeline. The first node would be the gamut compress, with a serial node for the Look Transform, for example using the Neutral Look as a starting point for grading.

![Resolve](img/Resolve1.jpg)

To apply these, just click on the node and choose your LUT from the contextual menu. The LUT will then affect all the clips in the timeline, and can be toggled on or off as desired. For example when passing a clip to VFX the Look should be disabled so it is not baked into the EXR on export. 

The “process node LUTs in” in the ACES Color management Settings should be set to AP1 when using these .cube LUTs with the shaper built in (Log2 48 nits shaper ACEScc). 

![Resolve](img/Resolve3.jpg)

## Delivering to VFX

To output a VFX pull you would first disable any Look Transforms that you do not intend to bake into the footage. If desired you can also write out a 3D LUT to pass to VFX to use as a *Shot LUT*. This will include all enabled grades both in the timeline and the clip so it will combine the Look Transform with your shot grade into a single LUT. This LUT will be in ACEScc processing space.

Next, temporarily set the display to linear by setting the *ACES Output Device Transform* in the project settings to "No output transform." This will export the sequence in ACES2065-1 AP0 exchange color space. It's good practice to append this to the file name, for example ````MyFilm_shot22_ap0.0001.exr```` and also to communicate the Look Transforms (if any) that are being used. Then on the Delivery page export EXR files in 16-bit half float (which Davinci calls "RGB half"). 

![exr](img/Resolve5.jpg)

Note that sequences in ACES are not output as DPX files, but as OpenEXR format. DPX is an older method which encodes the 0-1 image in log format allowing for storing a wide dynamic range (i.e. multiple camera exposures) in a small file size. However DPX is limited in the range it can hold, as opposed to an EXR which can go far beyond the 0-1 range and thus have a far larger dynamic range than a DPX file can. The ACES2065-1 archival/interchange color space contains the full gamut of what is visible to the human eye which is way more than an HDTV or sRGB monitor can display. If you are concerned about file sizes you can use Piz lossless compression. These EXR files will be smaller than a DPX file and even smaller than a PNG.

[Back to main](../StdX_ACES)
