# Chroma Adjustments

The current ACES Output Transform has a number of hue shifts and skews. This is largely due to the per-channel approach of the RRT, and the current proposal for the ACES 2.0 output Transform, called [OpenDRT](https://github.com/jedypod/open-display-transform), will fix this using a hue-preserving approach. These changes are obviously not possible to implement with a Look Transform. Nevertheless, a few tweaks have been made affecting chromaticities, in particular for blues which sit at the edge of the AP1 color space. 


