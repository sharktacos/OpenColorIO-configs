# Gamut Compression
 
The config's look transforms include an implementation of the [ACES gamut compression algorithm](https://github.com/ampas/aces-vwg-gamut-mapping-2020) as a 3D LUT. The algorithm is not fully implementable as a 3D LUT, and a proper implementation would be done in [CTL (Color Transformation Language)](https://github.com/ampas/aces-dev/blob/1256fee50ee35548c6eab8eca854ff3349008489/transforms/ctl/lmt/LMT.Academy.GamutCompress.ctl) which is supported in OCIO v2. Currently this has not been implemented in the [ACES 1.3 reference config](https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES/releases). Furthermore many DCC apps do not currently support OCIOv2. In the meantime therefore a LUT based approximation is used here.
 
 Let's begin with several images with colors that are out of gamut, illustrating the problem. Note for instance the blobs of blue on the roof of the bar scene (bottom right), the loss of detail in the red areas in the top two images in their faces and clothing, and the crazy banding or posterizing happening on the spotlight behind the head of the woman (bottom left image).
  
![rrt](img/Gamut_rrt.png)
    
Below are those images with the gamut compression algorithm applied (implemented using the [Nuke blink script tool](https://github.com/jedypod/gamut-compress)). Wow. 
    
 ![nk](img/Gamut_nk.png) 
     
Compare that to the LUT implementation used in this config, shown below. For the most part the LUT appears to faithfully match the algorithm. The one noticeable difference in these images is the spotlight on the bottom left image which is losing some of its chromaticity (color saturation) and going to white a bit, illustrating the limits of what a 3D LUT can do.

![lut](img/Gamut_lut.png)
      
Nevertheless, despite these minor differences, compared to the older Blue Light Artifact Fix, pictured below, the results of the gamut compression LUT are clearly superior. Ironically the "blue fix" is making blue appear magenta. Obviously using a 3D LUT is an interim solution, but this is clearly a huge gain compared to the current available solutions. One can also use this LUT in
programs that do not support OCIO, such as Davinci Resolve.

![blue](img/Gamut_bluefix.png)

[Back to main](../StdX_ACES)
