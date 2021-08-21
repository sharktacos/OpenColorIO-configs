# Photoshop

There is a free [OCIO plugin for Photoshop](http://fnordware.blogspot.com/2017/02/opencolorio-for-photoshop.html) which lets you apply OCIO transforms as a filter, baking it into the file, which is a destructive workflow. What you can do with the plugin is write out ICC profiles. This config contains ICC profiles for all if the Look Transforms for the various workflows, which are described below. These ICC profiles are located in the  ````software/Photoshop```` in the config. To install the icc profile on Windows, right-click the file and choose install profile. On a Mac copy the profiles into the ````/Users/[username]/Library/ColorSync/Profiles```` folder.

## EXR Files in Photoshop

Photoshop has a very limited toolset in 32 bit mode (meaning most of your faviorite tools in Photoshop wont be available). So if you're wanting to edit scene-linear EXR files, a better option is Affinity Photo, which is free.

## Matte Painting DPX log footage

Let's assume that we are beginning with a 10-bit Log DPX film plate in ACEScct color space.  Photoshop will read this in 16-bit integer mode. Next, we need to assign our film emulation profile to our Log file so it will display properly. Select the menu option *edit > assign profile* and in the window that opens, select the desired profile from the "profile" drop-down menu. 



. Photoshop will read this in 16-bit integer mode. Next, we need to assign our film emulation profile to our Log file so it will display properly. Select the menu option edit > assign profile. In the window that opens, select the desired profile from the "profile" drop-down menu. 

For editing 16-bit log or 8-bit files in display-referred sRGB images there is a free [OCIO plugin for Photoshop](http://fnordware.blogspot.com/2017/02/opencolorio-for-photoshop.html). Download the plugin and place it in your Photoshop plugins directory. On Windows that's (currently):


