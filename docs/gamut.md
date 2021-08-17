# Gamut Compression
 
The config's look transforms include an implementation of the [ACES gamut compression algorithm](https://github.com/ampas/aces-vwg-gamut-mapping-2020) as a 3D LUT. The algorithm is not fully implementable as a 3D LUT, and a proper implementation would be done in [CTL (Color Transformation Language)](https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES/releases/tag/v0.1.1) which is supported in OCIO v2. Since Foundry Nuke and Houdini do not currently support OCIO v2, a LUT based approximation is used here.
 
 Let's begin with several images with out of gamut colors, illustrating the problem. Note for instance the blobs of blue on the roof of the bar scene (bottom right), the loss of detail in the red areas in the top two images in thier faces and clothing, and the crazy banding or posterizing happening on the spotlight behind the head of the woman (bottom left image).
  
![rrt](img/Gamut_rrt.png)
    
Below are those images with the gamut compression algorithm applied (implemented using the [Nuke blink script tool](https://github.com/jedypod/gamut-compress)). Wow. 
    
 ![nk](img/Gamut_nk.png) 
     
Compare that to the LUT implementation used in this config, shown below. For the most part the LUT appears to faithfully match the algorithm. The one noticeable difference in these images is the spotlight on the bottom left image which is losing some of its chromaticity (color saturation) and going to white a bit, illustrating the limits of what a 3D LUT can do.

![lut](img/Gamut_lut.png)
      
Nevertheless, despite these minor differences, compared to the older Blue Light Artifact Fix, pictured below, the results of the gamut compression LUT are clearly superior. Ironically the "blue fix" is making blue appear magenta. Obviously using a 3D LUT is an interim solution, but this is clearly a huge gain compared to the current avaialbe solutions. Once can also use this LUT in
programs that do not support OCIO, such as Davinci Resolve.

![blue](img/Gamut_bluefix.png)

