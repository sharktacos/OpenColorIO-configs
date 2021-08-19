# Substance Painter

Substance Painter does not currently work with OCIO, so we need to do use a workaround using these EXR files as LUTs, which will allow is to view our asset through to Filmic and Neutral Look transforms.

[StdX_ACES/software/SubstancePainter](https://github.com/sharktacos/OpenColorIO-configs/tree/main/StdX_ACES/software/SubstancePainter)

These files need to be coppied into the Substnace Painter shelf folder. On Windows that's in

````C:\Users\ *username* \Documents\Adobe\Adobe Substance 3D Painter\shelf\colorluts\````


In the Display Settings, enable Activate Post Effects and Tone Mapping. Set *function* to Log and slide the *mapping factor* to the max (63.99). This will tonemap scene linear into a 0-1 range.

![sp1](img/substance_painter_aces_setup_01_tonemapping.png)

Check *activate color profile* and choose the colorlut profile you just put there.

![sp2](img/Substance2.jpg)

Note these view tranforms assume you are working in sRGB scene-linear in Substance Painter, and that the HDR enviornment maps are all in sRGB scene-linear (the default). 





