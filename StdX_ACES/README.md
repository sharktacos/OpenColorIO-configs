Here's an overview of the modifications made in this config to the standard ACES 1.1 config.

# View Transforms
  
The config has several view transforms:
  
  ![view](https://github.com/sharktacos/OpenColorIO-configs/blob/main/docs/img/viewTransforms.jpg)

- **Neutral Look**
   is intended as a neutral starting point for color grading and lookdev work. It reduces contrast (by a factor of 0.85 in log space) pulling the shadows and highlights slightly out of the toe and shoulder curves, to make more of the shot range visible. 
   
- **Filmic Look**
   has a similar filmic look to the standard ACES 1.0 RRT, with a little less contrast, resulting of less crushing of shadows. 
   Both the filmic and neutral looks handle warm light temperatures such as sunshine, fire, and tungsten light bulbs differently than the ACES RRT which renders these in an unnatural over-saturated way. 
   
   ![light](https://github.com/sharktacos/OpenColorIO-configs/blob/main/docs/img/yellow.jpg)
   
   This flourescent "yellow highlighter" look can be particularly unpleasant in clouds.
   
   ![clouds](https://github.com/sharktacos/OpenColorIO-configs/blob/main/docs/img/clouds.png)
   
- **ACES Standard RRT**
- **Show**
- **Un-tone-mapped**
- **Raw**
- **Log**
   - The bottom three view transforms (un-tone-mapped, raw, and log) are parallel to the Maya 2022 default ACES config and are used for diagnostic purposes. Un-tone-mapped is equivalent to the Nuke default view transform which clips values over 1.


  

  
## Gamut Compression

Look transforms include an implementation of the <a href="https://github.com/ampas/aces-vwg-gamut-mapping-2020">ACES gamut compression algorithm</a> as a 3D LUT. Check out some <a href="https://github.com/sharktacos/OpenColorIO-configs/blob/main/docs/gamut.md">pretty pictures</a> showing the gamut compression implementation.<p>
  
# Roles and rules 
**dif**, **BaseColor** and **hdr** color spaces act as aliases using OCIO rule name matching which assigns an input color space if its name appears in the image name. Therefore textures with "dif" (shirt_dif_v02.png) or "BaseColor" in their name will automatically be assigned the *Utility - sRGB - texture* color space. Likewise if "hdr" is in the file name the *scene-linear sRGB* color space will be assigned. All other textures (bump, normal, masks, displacement, etc.) will automatically be assigned the *Utility - Raw* color space (the default role).<p> 
  
## Color Spaces
**Pick - sRGBlin desat**
  
Defined as color picking role to pick colors in sRGB/Rec.709 primaries with slight desaturation (0.85 based on rec709 luma) resulting in colors having around 0.95 max saturation. Standard computer color pickers lead artists to pick extremely saturated neon colors. With the Rec2020 gamut of ACEScg this is exaserbated. The motivation is to have a color picker which encourages artists to pick painterly colors, meaning one has to lower the luminance to achieve deeply saturated colors.<p>

**Input - Premiere Pro - ACEScg**
Input color space for Premiere Pro for EXR files in ACES-2065-1 AP0 color space. Premiere adds a BT.1886 2.4 gamma to EXR files, so this removes that to properly bring the file into scene-linear. Using OCIO you'll want to use this color space for the in and ACEScct for the out in order to grade in log.  

## EOTF
  



