# Substance Painter

Substance Painter does not currently work with OCIO, so we need to use a workaround using these EXR files as LUTs, which will allow us to view our asset through the  Filmic and Neutral Look transforms.

[StdX_ACES/software/SubstancePainter](https://github.com/sharktacos/OpenColorIO-configs/tree/main/StdX_ACES/software/SubstancePainter)

These files need to be copied into the Substance Painter shelf folder. On Windows that's in

````C:\Users\ *username* \Documents\Adobe\Adobe Substance 3D Painter\shelf\colorluts\````


In the Display Settings, enable Activate Post Effects and Tone Mapping. Set *function* to Log and slide the *mapping factor* to the max (63.99). This will tonemap scene-linear into a 0-1 range so speculars do not clip in the view.

![sp1](img/substance_painter_aces_setup_01_tonemapping.png)

Check *activate color profile* and choose the colorlut profile you just put there.

![sp2](img/Substance2.jpg)

Note these view transforms assume you are in sRGB scene-linear working space in Substance Painter, and that the HDR environment maps are all in sRGB scene-linear (which is the default).





