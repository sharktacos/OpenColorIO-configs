# init.py
Currently Nuke uses the OCIO scene_linear role for both the working space and for float files. We however in ACES we need the working space to be ACEScg and float files to be in ACES-2065-1 the ACES file interchange format. 
The code in this init.py code corrects this so float files default to ACES-2065-1 in the VFX config using the reference role. 
Place the init.py file in your .nuke folder (located in the home directory of your computer) or add its content to the existing init.py file.

# Reference Gamut Compression Gizmo
Nuke Gizmo for Reference Gamut Compression. Place the file in your .nuke folder (located in the home directory of your computer) and add the following to your menu.py file.
````
toolbar = nuke.toolbar("Nodes")
toolbar.addCommand( "Gizmos/ACES_ref_gamut_compress", "nuke.createNode('ACES_ref_gamut_compress')")
````
This adds a menu labeled “Gizmos” to the default Nodes Toolbar with an item labeled “ACES_ref_gamut_compress” that creates an instance of the ACES Reference Gamut Compression node.

# LUT generator Nuke Template
A nuke script template for creating a 3D LUT for the show look in the ANM config.
