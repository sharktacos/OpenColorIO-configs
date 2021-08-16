<h1>ACES-stdX config modifications</h1>
<h2>Look Transforms</h2>
<b>Gamut Compression</b><br> 
Look transforms include an implementation of the <a href="https://github.com/ampas/aces-vwg-gamut-mapping-2020">ACES gamut compression algorythm</a> as a 3D LUT. The algorithm is not fully implementable as a 3D LUT, and a proper implementation <a href="https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES/releases/tag/v0.1.1">would be done in CTL (Color Transformation Language)</a> which is supported in OCIO v2. Since Foundry Nuke and Houdini do not currently support OCIO v2, a LUT based approximation is used here. Here's a comparision of how the different approaches look, beginning with several images with out of gamut colors illustrating the problem:<p>
  
  <img src="../docs/img/Gamut_rrt.png"> <p>
    
Here are those images with the gamut compress algorthm applied (implemented using the <a href="https://github.com/jedypod/gamut-compress">Nuke blinkscript tool</a>):<p>
    
   <img src="../docs/img/Gamut_nk.png"> <p>  
     
Compare that to the LUT implemenation used in this config. You can see for example that the spotlight is going to white, illustrating the limits of what a 3D LUT can do.<p>
<img src="../docs/img/Gamut_lut.png"> <p> 
      
However, compared to the older "Blue Light Artifact Fix" the results are clearly superior. Ironically the "blue fix" is making blue appear magenta<p>
<img src="../docs/img/Gamut_bluefix.png"> <p>  


<h2>Roles and rules</h2>
<b>dif</b>, <b>BaseColor</b> and <b>hdr</b> color spaces act as aliases using OCIO rule name matching which assigns an input color space if its name appears in the image name. Therefore textures with "dif" (shirt_dif_v02.png) or "BaseColor" in their name will automatically be assigned the <i>Utility - sRGB - texture</i> color space. Likewise if "hdr" is in the file name the <i>scene-liner sRGB</i> color space will be assigned. All other textures (bump, normal, masks, displacement, etc.) will automatically be assigned the <i>Utility - Raw</i> color space (the default role).<p> 
  
<h2>Color Spaces</h2>
<b>Pick - sRGBlin desat</b><br> 
Defined as color picking role to pick colors in sRGB/Rec.709 primaries with slight desaturation (0.85 based on rec709 luma) resulting in colors having around 0.95 max saturation. Standard computer color pickers lead artists to pick extremely saturated neon colors. With the Rec2020 gamut of ACEScg this is exaserbated. The motivation is to have a color picker which encourages artists to pick painterly colors, meaning one has to lower the luminance to achieve deeply saturated colors.<p>

<b>Input - Premiere Pro - ACEScg</b><br>
Input color space for Premiere Pro for EXR files in ACES-2065-1 AP0 color space. Premiere adds a BT.1886 2.4 gamma to EXR files, so this removes that to properly bring the file into scene-linear. Using OCIO you'll want to use this color space for the in and ACEScct for the out in order to grade in log.  

<b>EOTF</b><br>
  



