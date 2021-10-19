# Substance Painter 

## dodge and burn
Substance does not have a dodge and burn brush like Photoshop or Mari does. Dodge and burn come from photography development and thus affect exposure (i.e. linear gain). 
The idea for painting is that we want to darken a color (burn), rather than painting black on top of it and brighten a color (dodge) rather than adding white on top. That is we want to retain the color and brighten or darken it.

**Burn (darken color)**
Our work-around is to create a layer to darken the color layers below, setting the layer mode to "Soft Light." You then paint black. 


mode with black color to burn (darken). white color works for dodge (lighten), but using "value" mode with retain saturation.

## Ambient Occlusion mask

Drag AO texture into mask on fill layer (into fill in mask). Add paint layer into mask stack to modify AO.

## dirt

Drag noise/grunge texture into stencil for paint. Also use brushes (charcoal etc) 

## stencils hide
Can't hide tile display, so can't move to side. Does hide when painting. Stencil display opacity in display settings.

## symmetry in SP 
The mirror symmetry can be enabled in the contextual toolbar (top)

## HDR maps and camera import
camera import works, HDR projection works, test projection from camera accuracy.
Test sphere projection for panorama HDR

# Missing features

## transfer Mari to Substance

X SP only exports to PSD. No import.

## merge layers
X export and import into fill. 

## copy color to use as bump?
X nope. Export and import map into fill :P


# NoOp

A material has properties that can either be driven with a slider (a value) or a texture map (i.e. and image). In Substance there are only texture maps, so to get a value one needs to use a fill. It does not make sense to export this single value texture map as it would slow the render and lock off the parameter from being edited in Maya. So we have the NoOp section of channels that are not included in our Output Template for texture export. Because these are fill nodes they can be linked to a particular channel (as opposed to a paint layer).

# Color

## paint layer gotcha
A Material is composed of multiple channels (basecolor, height, roughness, etc.). In most programs a layer is an part of a channel (i.e. associated with that channel) and thus feely interchangable between channels. For example a layer in the color channel could be coppied and used in the height channel. In Substance the channel changes with the current paint tool settings (properties). It is not possible therefore to set a particular paint layer to *hight* or *color* as this changes with the current tool settings. This makes organization difficult. and can lead to inadvertly painting bump channel info into a color layer.

It is also not possible currently to transfer one channel to another, for example a painted color channel to the bump, nor is is possible to merge layers. The cumbersone workaroud is to export the texture and import it back in to SP.

## No dodge and burn. 

Substance does not have a dodge and burn brush like Photoshop or Mari does. Dodge and burn come from photography development and thus affect exposure (i.e. linear gain). 
The idea for painting is that we want to darken a color (burn), rather than painting black on top of it and brighten a color (dodge) rather than adding white on top. That is we want to retain the color and brighten or darken it.

# bump
exr. base color grey. layer channel dropdown for opacity. paint layer gotcha. bell alpha.
