# Premiere Pro

The free [OCIO plugin for After Effects](https://fnordware.blogspot.com/2012/05/opencolorio-for-after-effects.html) also works in Premiere Pro. You just need to place it in the common plugin folder, which on Window is:<br>

C:\Program Files\Adobe\Common\Plug-ins\7.0\MediaCore


## Reading EXR Sequences (color space: AP0 ACES-2065-1)

In the Sequence Settings turn  **Max Bit Depth** on if reading EXR files. Otherwise Premiere will clip any image values over 1. Using the OCIOv2 config, you will make two OCIO FXs, one to read in the files, and another to display them, with any image adjustments in between. So your FX layers would be:

   1. **OCIO input** (in: Premiere color space, out: ACEScct)<br>
   The Premiere input spaces are located in ````Input/Adobe````
   3. Grade in Luminare (in ACEScct log space)
   4.  **OCIO display** (in: ACEScct, out: Filmic Look)
   
   ![img](img/Premiere1.jpg)
 
Note that because Premiere adds a gamma adjustment to EXR files to bring it into its BT.1886/Rec.709 working space the config has a color space made for reading EXR files into Premiere: *Input - Premiere Pro - AP0 2.4 gamma* and *Input - Premiere Pro - AP0 2.4 gamma* which would be used as the input color space above. 

## Reading Apple Prores clips (color space: ACEScct)

An alternte approach to the above EXR workflow is to instead use Prores movie files in ACEScct log. These would again be read into Premiere with the OCIO config, with the input space set to ACEScct. This will likely improve interactive speed in Premiere.

[Back to main](../StdX_ACES)
