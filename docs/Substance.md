# Substance Painter

As of v7.4 Substance Painter supports OCIOv2! In the initial release OCIO roles were not yet supported so the color spaces needed to be set manually when creating a new project `File > new` or in the Project Configuration `Edit > Project Configuration`. Below the proper settings are pictured. 

![img](img/substance-ocio.jpg)

As of v7.4.2 OCIO roles are supported, and defined in the configs here on this repo.

This replaces the older workaround described below.

## Color picker

As of version 8.1.2 the color picker can correctly pick the channel color if you hold down the shift key, otherwise it will pick the color that is displayed in the viewport, including shading. The colors are blended in the working color space, ACEScg. The OCIO color picking role is still not respected.


[Back to main](../StdX_ACES)
