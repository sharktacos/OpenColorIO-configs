# Davinci Resolve

Conceptually a Look Transform (LMT) should be applied across an entire scene or show, downstream of the per shot grades, but before the Output Transform. This can be done in Resolve by applying the LUT to the timeline instead of to an individual clip. To do this, in the Color module Node Editor set the drop-down to timeline.

![Resolve](img/Resolve1.jpg)

You then just click on the node and choose your LUT from the contextual menu. The LUT will then affect all the clips in the timeline, and can be toggled on or off as desired. This fits with the idea of using a Look Transform (LMT) across an entire scene or show.
