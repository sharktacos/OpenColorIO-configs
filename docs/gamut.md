# Gamut Compression
 
The config's look transforms include an implementation of the [ACES gamut compression algorithm](https://github.com/ampas/aces-vwg-gamut-mapping-2020). Currently the proper way to do this is with a [Nuke](Nuke.md) node or with a DCTL for [Resolve Studio](Resolve.md). Implementation in OCIO is in the works for v2.1, but currently this has not been released. In the meantime gamut compression is provided in this config as a 3D LUT for viewing purposes. Because gamut compression works with negative numbers, the 3D LUT shaper needs to cover large range of negative values. This is done with a logarithmic function with a linear segment, similar to the ACEScct function, but that is also reflected by its intersection point with the Y-axis, essentially mirroring the ACEScct shaper. It's important to note however that this 3D LUT has limitations, for instance it is not invertable. We therefore only use it to view images in OCIO, and never to bake the gamut compression into the image. This again is done with the proper Nuke and DCTL nodes referenced above.
 
If you read through all of that you deserve to see some pretty pictures! Let's begin with several images with colors that are out of gamut, illustrating the problem. Note for instance the blobs of blue on the roof of the bar scene (bottom right), the loss of detail in the red areas in the top two images in their faces and clothing, and the crazy banding or posterizing happening on the spotlight behind the head of the woman (bottom left image).
  
![rrt](img/Gamut_rrt.png)
    
Below are those images with the gamut compression algorithm applied (implemented using the [Nuke blink script tool](https://github.com/jedypod/gamut-compress)). Wow. 
    
 ![nk](img/Gamut_nk.png) 
     
Compare that to the LUT implementation used in this config, shown below. Looks visually identical.  

![lut](img/Gamut_lut.png)
      
Now compare that to the older Blue Light Artifact Fix, pictured below, the results are clearly superior. Ironically the "blue fix" is making blue appear magenta. 

![blue](img/Gamut_bluefix.png)

Gamut compression is meant to replace the Blue Light Artifact Fix and one of the key differences is that the gamut compression algorthm only affects the pixels that are out of gamut, leaving the rest of the image unchanged. So it's not so much color correction, and more "pixel healing."

[Back to main](../StdX_ACES)
