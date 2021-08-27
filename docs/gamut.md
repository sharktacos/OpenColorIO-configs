# Gamut Compression
 
The config's look transforms include an implementation of the [ACES gamut compression algorithm](https://github.com/ampas/aces-vwg-gamut-mapping-2020). Currently the proper way to do this is with a [Nuke](https://github.com/ampas/aces-vwg-gamut-mapping-2020/tree/master/model) node or with a DCTL for [Resolve Studio](Resolve.md). Implementation in OCIO is in the works, but currently this has not been implemented in the [ACES 1.3 reference config](https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES/releases). 

In the meantime gamut compression is provided in this config as a 3D LUT. It's important to note that this has limitations, for instance it is not invertable. So *hic sunt dracones!*. Because gamut compression works with negative numbers, the 3D LUT shaper needs to cover large range of negative values. This is done with a logarithmic function with a linear segment, similar to the ACEScct function, but that is also reflected by its intersection point with the Y-axis, essentially mirroring the ACEScct shaper.
 
If you read through all of that you deserve to see some pretty pictures! Let's begin with several images with colors that are out of gamut, illustrating the problem. Note for instance the blobs of blue on the roof of the bar scene (bottom right), the loss of detail in the red areas in the top two images in their faces and clothing, and the crazy banding or posterizing happening on the spotlight behind the head of the woman (bottom left image).
  
![rrt](img/Gamut_rrt.png)
    
Below are those images with the gamut compression algorithm applied (implemented using the [Nuke blink script tool](https://github.com/jedypod/gamut-compress)). Wow. 
    
 ![nk](img/Gamut_nk.png) 
     
Compare that to the LUT implementation used in this config, shown below. Looks visually identical.  

![lut](img/Gamut_lut.png)
      
Now compare that to the older Blue Light Artifact Fix, pictured below, the results are clearly superior. Ironically the "blue fix" is making blue appear magenta. Obviously using a 3D LUT is an interim solution, but this is clearly a huge gain compared to the current available solutions. 

![blue](img/Gamut_bluefix.png)

[Back to main](../StdX_ACES)
