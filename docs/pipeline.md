# Pipeline

The workflow for ACES going from DI (for example [Davinci Resolve](Resolve.md)) to VFX ([Nuke](Nuke.md)) would be to initially input all the different camera footage using the appropriate camera manufacturer input transforms, work in ACEScc or ACEScct log space, and then output this as  ACES2065-1.  ACES2065-1 is the color space intended for transfer of files and for archiving. 

````Input: RAW CAMERA   >  Working: ACEScc  >  Output:  ACES2065-1````

Note that this is not output as a DPX file, but as an EXR file. DPX encodes the 0-1 image in log format which allows for storing a wide dynamic range (i.e. multiple camera exposures) in a small file size. However DPX is limited in the range it can hold, as opposed to an EXR which can go far beyond the 0-1 range and thus have a far larger dynamic range than a DPX file can. Despite the huge color gamut and dynamic range of the ACES2065-1 archival/interchange color space (it contains the full gamut of what is visible to the human eye which is way more than an HDTV or sRGB monitor can display), with Piz lossless compression these EXR files are nevertheless the same size as a DPX file if not smaller. So it’s really a win-win.

Therefore, the ACES pipeline for compositing when receiving ACES footage would be:

````Input: ACES2065-1  >  Working: ACEScg  >  Display: sRGB````


Likewise, the delivery of VFX to DI from Nuke would be written  to ACES2065-1 (that is,  ACES2065-1 would be the color space on the Nuke write node). 

````Input: ACES2065-1 > Working: ACEScg  > Output: ACES2065-1````

As you can see, once the footage is input in and converted into ACES, one does not need to keep track of all the different color spaces because it’s always in the ACES exchange color space.

For reading renders into Nuke, since the EXR files are already in ACEScg the input (i.e the color space of the read node) would be  ACEScg.
	
````Input: ACEScg  >  Working: ACEScg >  Display: sRGB````

If you want to simply output a PNG sequence to make a Quicktime movie in Media Encoder (or output a Quicktime movie directly from Nuke) then the display transform is baked into the media (as set on the color space of the Nuke write node). This is the process of delivery and involves leaving the wide gamut working space of ACES, and encoding the image with the limited display space of the intended viewing device. If you want to view this on the web or on a computer monitor it would be sRGB. You would also want to make in whatever [tone mapping](tonemap.md) you are viewing. So if you are viewing *Filmic (sRGB)* and want to deliver so it looks like that you would choose that in the color space for your write node for output.
	
````Working: ACEScg >  Output: Filmic (sRGB)````

If you are delivering for broadcast television you would then choose 

````Working: ACEScg >  Output: Filmic (Rec.1886/Rec.709 video)````


