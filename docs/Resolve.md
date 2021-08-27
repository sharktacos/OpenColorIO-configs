# Davinci Resolve

## Using ACES

ACES is loaded in the Color Management section of the Project Settings.

![Resolve](img/Resolve4.jpg)

To output a VFX pull you would temporarily set the display to linear by setting the *ACES Input Device Transform* in the project settings above to "No output transform" and then on the Delivery page exporting EXR files. This will export an EXR sequence in ACES2065-1 AP0 exchange color space. It's good practice to append this to the file name, for example ````MyFilm_shot22_ap0.0001.exr````.

![exr](img/Resolve.5.jpg)

Note that this is not output as a DPX file, but as an EXR file. DPX encodes the 0-1 image in log format which allows for storing a wide dynamic range (i.e. multiple camera exposures) in a small file size. However DPX is limited in the range it can hold, as opposed to an EXR which can go far beyond the 0-1 range and thus have a far larger dynamic range than a DPX file can. The ACES2065-1 archival/interchange color space contains the full gamut of what is visible to the human eye which is way more than an HDTV or sRGB monitor can display. If you are concerned about file sizes you can use Piz lossless compression. These EXR files will be smaller than a DPX file and even smaller than a PNG.

## Looks and Gamut Compression

To use the *Filmic* and *Neutral* Look LUTS, the .cube files need to be placed into the Davinci Resolve LUT directory, which you can get to by clicking "Open LUT folder" in the Preferences, copying the files, and then clicking "update lists" to refresh. 

![Resolve](img/Resolve2.jpg)

The two .cube Look LUT files are called:

````studio/LMT_filmic_AP1_shaper.cube```` <br>
````studio/LMT_neutral_AP1_shaper.cube````

Gamut compression is done in Davinci Resolve Studio using a DCTL file which you will find in the ````software/Resolve/GamutCompress.dctl```` folder of the config. Place this into the Davinci Resolve LUT directory as described above. 


## Usage

Gamut compression needs to be applied before anything else, immediately after the Input Transform (IDT) so that all grading operations are downstream of the compression.
It can be applied to an individual clip or blanket applied to all footage since, unlike the former “Blue Light LMT” the algorithm only affects the necessary pixels of the image leaving the rest untouched.

Similarly, a Look Transform (LMT) conceptually should be applied across an entire scene or show, before the Output Transform. This can be done in Resolve by applying the LUT to the timeline instead of to an individual clip. To do this, in the Color module Node Editor set the drop-down to timeline. The first node would be the gamut compress, with a seriel node for the Look Transform, for example using the Neutral Look as a starting point for grading.

![Resolve](img/Resolve1.jpg)

To apply these, just click on the node and choose your LUT from the contextual menu. The LUT will then affect all the clips in the timeline, and can be toggled on or off as desired. For example when passing a clip to VFX the Look should be disabled so it is not baked into the EXR on export. 

The “process node LUTs in” in the ACES Color management Settings should be set to AP1 when using these .cube LUTs with the shaper built in (Log2 48 nits shaper ACEScc). 

![Resolve](img/Resolve3.jpg)

[Back to main](../StdX_ACES)
