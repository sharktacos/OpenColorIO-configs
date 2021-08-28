# Gamut Compression
 
Problems with out-of-gamut colors are caused by an image going from a large color gamut space to a smaller one. The most common example is converting a 
film camera wide-gamut color space (say for an ARRI or RED camera)  to  the  smaller  gamut  of  the  display  devices  (for example Rec.709 video). Similarly in ACES one needs to go from the crazy big AP0 color gamut, which contains more colors than are visible to the human eye, in to the AP1 color space for work in DI (ACEScct) or CG/VFX (ACEScg). 

![gamut](img/gamuts.jpg)

When converted the highly saturated bright colors that were on the edge of the larger gamut space will fall outside  the  target  color  space, resulting  in  negative color values which produce artifacts  and clipping (loss  of  texture detail, intensification  of  color  fringes, and so on). To address this the ACES community established a [Gamut Mapping Virtual  Working  Group  (VWG)](https://github.com/ampas/aces-vwg-gamut-mapping-2020) who developed a Gamut Compression algorthm, published as a [Nuke](Nuke.md) node and DCTL for [Resolve Studio](Resolve.md). Implementation in OCIO is in the works for v2.1, but currently this has not been released. In the meantime gamut compression is provided in this config as a 3D LUT for viewing purposes. Because gamut compression works with negative numbers, the 3D LUT shaper needs to cover large range of negative values. This is done with a logarithmic function with a linear segment, similar to the ACEScct function, but that is also reflected by its intersection point with the Y-axis, essentially mirroring the ACEScct shaper. It's important to note however that this 3D LUT has limitations, for instance it is not invertable. We therefore only use it to view images in OCIO, and never to bake the gamut compression into the image. This again is done with the proper Nuke and DCTL nodes referenced above.
 
If you read through all of that you deserve to see some pretty pictures! Let's begin with several images with colors that are out of gamut, illustrating the problem. Note for instance the blobs of blue on the roof of the bar scene (bottom right), the loss of detail in the red areas in the top two images in their faces and clothing, and the crazy banding or posterizing happening on the spotlight behind the head of the woman (bottom left image).
  
![rrt](img/Gamut_rrt.png)
    
Below are those images with the gamut compression algorithm applied (implemented using the [Nuke blink script tool](https://github.com/jedypod/gamut-compress)). Wow. 
    
 ![nk](img/Gamut_nk.png) 
     
Compare that to the LUT implementation used in this config, shown below. Looks visually identical.  

![lut](img/Gamut_lut.png)
      
Now compare that to the older Blue Light Artifact Fix, pictured below, the results are clearly superior. Ironically the "blue fix" is making blue appear magenta. 

![blue](img/Gamut_bluefix.png)

Gamut compression is meant to replace the Blue Light Artifact Fix and one of the key differences is that the gamut compression algorthm only affects the pixels that are out of gamut, leaving the rest of the image unchanged. So it's not so much color correction, and more "pixel healing."

## Pixel Healing

Let's have a look at the Gamut Compression node in action in Nuke. We begin with some footage with colors that are out of gamut. 

![blue](img/guitar1.png)

Let's say we wanted to use a Color Correct to do some despill of all that blue light in the shot. This looks good on the background room, but we are now seeing the out of gamut pixels more clearly on the performer. There is artifacting and posterization all over him.

![blue](img/guitar2.png)

Now let's look at how that same Color Correct looks when we first apply Gamut Compression. The artifacting is gone. That's the pixel healing effect of Gamut Compression, and the reason it is applied as the first operation immediately after the input transform (i.e. right after the Read node). You want to begin working with healed pixels. Otherwise it's like cooking with spoiled food.

![blue](img/guitar3.png)


[Back to main](../StdX_ACES)
