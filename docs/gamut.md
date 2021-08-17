 <h3>Gamut Compression</h3>
 
The config's look transforms include an implementation of the <a href="https://github.com/ampas/aces-vwg-gamut-mapping-2020">ACES gamut compression algorithm</a> as a 3D LUT. The algorithm is not fully implementable as a 3D LUT, and a proper implementation <a href="https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES/releases/tag/v0.1.1">would be done in CTL (Color Transformation Language)</a> which is supported in OCIO v2. Since Foundry Nuke and Houdini do not currently support OCIO v2, a LUT based approximation is used here.<p>
 
 Let's begin with several images with out of gamut colors, illustrating the problem. 
 Note for instance the blobs of blue on the roof of the bar scene (bottom right), the loss of detail in the red areas in the top two images in thier faces and clothing, 
 and the crazy banding or posterizing happening on the spotlight behind the head of the woman (bottom left image).<p>
  
  <img src="img/Gamut_rrt.png"> <p>
    
Below are those images with the gamut compression algorithm applied (implemented using the <a href="https://github.com/jedypod/gamut-compress">Nuke blink script tool</a>). 
  Wow. <p>
    
   <img src="img/Gamut_nk.png"> <p>  
     
Compare that to the LUT implementation used in this config, shown below. For the most part the LUT appears to faithfully match the algorithm. 
     The one noticeable difference in these images is the spotlight on the bottom left image which is losing some of its chromaticity (color saturation) and going to white a bit, 
     illustrating the limits of what a 3D LUT can do. <p>
<img src="img/Gamut_lut.png"> <p> 
      
Nevertheless, despite these minor differences, compared to the older Blue Light Artifact Fix, pictured below, the results of the gamut compression LUT are clearly superior. Ironically the "blue fix" is making blue appear magenta.
Obviously using a 3D LUT is an interim solution, but this is clearly a huge gain compared to the current avaialbe solutions. Once can also use this LUT in
programs that do not support OCIO, such as Davinci Resolve.<p>
<img src="img/Gamut_bluefix.png"> <p>  
