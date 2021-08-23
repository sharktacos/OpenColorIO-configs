# Lower Contrast Tone Mapping

Perhaps the top request of the ACES Output Transform (RRT) is that it be more neutral with less contrast. The [ACES Retrospective and Enhancements](https://community.acescentral.com/uploads/default/original/1X/38d7ee7ca7720701873914094d6f4a1d4ca031ef.pdf) paper states for example,

> “The defined ACES rendering intent has been questioned by a number of expert users... It is not uncommon to hear people saying they do not like the cumulative effects: crushing effect on shadows, and heavy highlight roll off, with too much look”

The two Look Transforms therefore lower the contrast of the ACES tone curve, the **Filmic** is 0.9 and **Neutral** is 0.8. This pulls the shadows and highlights slightly out of the toe and shoulder curves, resulting in less crushing of shadows and more gentle highlight rolloff. Note in the images below the details visible in the shadow areas compared to the ACES 1.0 Output Transform:

![rrt](img/tone_rrt.png)
![rrt](img/tone_filmic9.png)
![rrt](img/tone_neutral8.png)

This is done with a Nuke node provided by the amazing [Jed Smith](https://github.com/jedypod) which adjusts the contrast of the ACES tone curve, keeping the pivot at 0.18 for middle grey. Using a “gamma” function here doesn’t work well because it does different things to values above 1 and below 1, and of course EXR files have plenty of values above 1. Here's the contrast function as a [desmos plot](https://www.desmos.com/calculator/zuxtjn6wmu). 


