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

## transfer Mari to Substance

X SP only exports to PSD. No import.

## merge layers
X export and import into fill. 

## stencils hide
Can't hide tile display, so can't move to side. Can't adjust visibility. Does hide when painting.
stencil display opacity in display settings.

## copy color to use as bump?
X nope. Export and import map into fill :P

## try symmetry in SP and Mari
The mirror symmetry can be enabled in the contextual toolbar (top)

## HDR maps and camera import
test camera import, test HDR projection
