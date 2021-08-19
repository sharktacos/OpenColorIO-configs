Both the Filmic and Neutral looks handle warm light temperatures such as sunshine, fire, and tungsten light bulbs differently than the ACES RRT which renders these in an unnatural over-saturated way. Both the Filmic and Neutral Look Transforms therefore slightly lower the saturation in the image highlights, using the [ZoneSatLog Nuke tool](https://community.acescentral.com/t/look-transforms/3885/39). This gives luminous things like the fire and light bulbs, seen in the images below, a more natural appearance compared to the ACES Output Transform: 
   
   ![light](img/kelvin_rrt.png)
   ![light2](img/kelvin_filmic.png)
   
A good deal of this is already done by the [gamut compression](gamut.md). The zoneSat just gives it a little nudge on its path to white as the luminance approaches display max. Here's a look at the affect of each part:

   ![light3](img/kelvin_base.png)
   ![light4](img/kelvin_gamut.png)
   ![light5](img/kelvin_zone.png)
   

