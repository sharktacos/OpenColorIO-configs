# Mari

In Mari our OCIO config is loaded in File>Settings

![mari1](img/mari1.jpg)

In the Mari prefs (edit > Preferences, color tab) set *Color Swatches and Pickers* to “color manager” rather than "OCIO". This give a precise match to the canvas and image viewers, allowing for picking of raw colors (which we need to avoid having colors over 1 in our albedo textures), but viewing the color swatches adjusted to how they will appear in the display space.


![mari2](img/mari2.jpg)

Open the color picker by clicking the foreground color swatch and set *Canvas* to "Pick raw pixels". 

![mari2](img/mari3.jpg)

[Back to main](../StdX_ACES)


