Here's an overview of the modifications made in this config to the standard ACES 1.1 config.

<h1>Look Transforms</h1>
</h2>Gamut Compression</h2>
Look transforms include an implementation of the <a href="https://github.com/ampas/aces-vwg-gamut-mapping-2020">ACES gamut compression algorithm</a> as a 3D LUT. The algorithm is not fully implementable as a 3D LUT, and a proper implementation <a href="https://github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES/releases/tag/v0.1.1">would be done in CTL (Color Transformation Language)</a> which is supported in OCIO v2. Since Foundry Nuke and Houdini do not currently support OCIO v2, a LUT based approximation is used here.<p>
  
  Check out some <a href="https://github.com/sharktacos/OpenColorIO-configs/blob/main/docs/gamut.md">pretty pictures</a> showing the gamut compression implementation.<p>

<b>Tonemapping</b><br> 
  
<h2>Roles and rules</h2>
<b>dif</b>, <b>BaseColor</b> and <b>hdr</b> color spaces act as aliases using OCIO rule name matching which assigns an input color space if its name appears in the image name. Therefore textures with "dif" (shirt_dif_v02.png) or "BaseColor" in their name will automatically be assigned the <i>Utility - sRGB - texture</i> color space. Likewise if "hdr" is in the file name the <i>scene-liner sRGB</i> color space will be assigned. All other textures (bump, normal, masks, displacement, etc.) will automatically be assigned the <i>Utility - Raw</i> color space (the default role).<p> 
  
<h2>Color Spaces</h2>
<b>Pick - sRGBlin desat</b><br> 
Defined as color picking role to pick colors in sRGB/Rec.709 primaries with slight desaturation (0.85 based on rec709 luma) resulting in colors having around 0.95 max saturation. Standard computer color pickers lead artists to pick extremely saturated neon colors. With the Rec2020 gamut of ACEScg this is exaserbated. The motivation is to have a color picker which encourages artists to pick painterly colors, meaning one has to lower the luminance to achieve deeply saturated colors.<p>

<b>Input - Premiere Pro - ACEScg</b><br>
Input color space for Premiere Pro for EXR files in ACES-2065-1 AP0 color space. Premiere adds a BT.1886 2.4 gamma to EXR files, so this removes that to properly bring the file into scene-linear. Using OCIO you'll want to use this color space for the in and ACEScct for the out in order to grade in log.  

<b>EOTF</b><br>
  



