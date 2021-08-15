<h1>ACES-stdX config modifications</h1>
<h2>Look Transforms</h2>
<h2>Roles and rules</h2>
dif and BaseColor Assigns an input color space if its name appear in the image name.
roles:
  color_picking: Pick - sRGBlin desat
  color_timing: ACES - ACEScct
  compositing_linear: ACES - ACEScg
  compositing_log: ACES - ACEScct
  data: Utility - Raw
  default: Utility - Raw
  matte_paint: Output - sRGB
  reference: Utility - Raw
  rendering: ACES - ACEScg
  scene_linear: ACES - ACEScg
  texture_paint: ACES - ACEScct
<h2>Color Spaces</h2>
<b>Pick - sRGBlin desat</b> Color picking in sRGB/Rec.709 primaries with slight desaturation (0.85 based on rec709 luma)
