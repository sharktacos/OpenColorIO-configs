# ANM and VFX Configs

The ANM config ````config_ANM.ocio```` is designed for work on CG animation shorts and features. The VFX config ````config_VFX.ocio```` in contrast is designed for intgrating CG and VFX with live action film. Consequently each has different Display Transforms geared for its particular pipeline needs.

## ANM Config

![img](img/nuke6.jpg)

The Display Transforms for the above ANM config are all in sRGB display for viewing on artist's monitors, and contain the Reference Gamut Compression (RGC) baked into the view to componsate for hue skews with highly saturated colors in CG (see the [gamut](gamut.md) page. They contain the [Neutral and Filmic](tonemap.md) looks, as well as a Show Look. Neutral Look is intended for lookdev work, and Filmic Look is intended for shot lighting.

## VFX Config

![img](img/nuke5.jpg)

The Display Transforms for the above VFX config contain both sRGB and Rec.709 display types depending on whether a shot is being viewed on an artist's monitor (sRGB) or on an HDTV display for dailies. As explained above, gamut compression is applied as a node in VFX and thus not included in the Display Transform. The views include standard an ACES 1.0 RRT in both sRGB and Rec.709, the shot look both sRGB and Rec.709 displays, as well as several diagnostic views (un-tone-mapped, Raw, Log). Un-tone-mapped is the equivalent to Nuke's native sRGB which is a simple sRGB Gamma function without tonemapping.  

## Shot Look

The shot Look Display Transform in the VFX config works with context variables. You will need to insert the following code into your Nuke menu.py file:

```py  
# OCIO Shot Look custom defaults: 
def _setOCIODisplayContext():
    node = nuke.thisNode()
    node.knob('key1').setValue("SHOW")
    node.knob('key2').setValue("SHOT")
    node.knob('key3').setValue("VER")
    node.knob('key4').setValue("SHAPER")
    
    node.knob('value1').setValue("Show")
    node.knob('value2').setValue("shotNum") 
    node.knob('value3').setValue("version")
    node.knob('value4').setValue("ACEScct")
    
nuke.addOnCreate(_setOCIODisplayContext, nodeClass="OCIODisplay")
```

Then in Nuke select the "view panel" menu from the View Transform menu

![img](img/nuke2.jpg)

This will open up a properties window. Open the Context tab and you will see that it has been populated with template values. As a friendly hint for artists that this needs to be replaced with the actual shot values this template LUT is black and white.

![img](img/nuke3.jpg)

Replace the value fields for your shot LUT. The shot_lut directory of the config contains all of the shot LUTS for the show. For example if you were working on the DSOM show on shot 22 and the client LUT was called ````DSOM_022_v02_ACEScct.cube```` you would write the following:

![img](img/nuke4.jpg)

Alternatley, you can simply edit your menu.py file to input the values. In our example that would be

````py
    node.knob('value1').setValue("DSOM")
    node.knob('value2').setValue("022") 
    node.knob('value3').setValue("v02")
    node.knob('value4').setValue("ACEScct")
````

Nuke will open with these values, pointing to your shot look LUT.

In Maya you can similarly edit your Maya.env file and enter the following (again using the above example):
````
SHOW = DSOM
SHOT = 022
VER = v02
SHAPER = ACEScct
````
If you want to change the values in a Maya session you can use the following MEL code:
````py
putenv "SHOW" "DSOM";
putenv "SHOT" "022";
putenv "VER" "v02";
putenv "VER" "ACEScct";
colorManagementPrefs -refresh;
````
