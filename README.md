# Blender ASE Export Script

This is a fork from the [original project](http://code.google.com/p/ase-export-vmc/) by MCampagnini. The script has been upgraded to support Blender 4.1.
This version creates a folder with the name of the ASE file and saves the ASE file to it. A folder with the name "textures" is then created, in which the applied textures are saved.

## Videos
* Blender 4.1.1 https://youtu.be/7gP3b-AP-lo?si=uZzMC_PZCQQ7dmJ1

## Installation
* Download and extract the ASE Export Script.
* In Blender, Edit, Preferences.
* Go to the Add-Ons Tab.
* Install an Add-On bar, select the python script.
* Click Save preferences on bottom left icon to enable the script every time Blender loads (optional) or select auto-save.

You will find a new export option in File / Export called Ascii Scene Export (.ase).  If you do not see the script in the export menu after following the installation instructions, open the Add-On tab and find the script under Import-Export: ASCII Scene Exporter.  Be sure that it is enabled by checking the box next to the add-on name.  Contact me on my website if you still have problems exporting.

In order to export any mesh without issues follow below conditions:

## Mesh Requirements
* All non-collision geometries must be UV unwrapped.
* All non-collision meshes must have at least one material assigned using an image texture applied with Principled BSDF shader node only.
* All non-collision meshes must have one UVmap per material only.

## Optional
* Mesh may have more than one material
* Mesh may have more than one UV texture and/or a lightmap texture.
* Mesh may be assigned as a collision object.
* Mesh may have more than one collision object to determine collision borders.
* Mesh may be assigned smoothing groups.

## Collision Objects
Assign a mesh as a collision object by prefixing each object name with UCX_NAME, where NAME can be anything you would like (case-insensitive).

## Smoothing Groups
Assign smoothing groups by edge selecting the border of the faces you want assigned to a smoothing group, press ctrl+e and mark sharp.  Any face group separated with sharp edges will be assigned a smoothing group.

## Vertex Painting
Apply vertex painting in Blender as normal, be sure that you have at least two uv texture slots.  This is not a technical limitation, but due to time constraints I left the vertex painting code inside of a conditional that requires two uv textures.  In order to view your vertex painting in UDK you will have to import and set up your materials correctly within UDK.

## Issues
This version clones selected meshes to avoid triangulation on original mesh. Case it stops suddenly, as it happens during export errors, duplicates could appear in outliner window. They will show names like co#pia or UCX_co#pia as prefix and numbers like. 001, .002, 003 as suffix. Simply delete them.
This add-on didn't work with bad topology meshes. It fails often when importing 3d models from other blender versions or imported models. It's best to work them inside Blender before exporting (cleanup meshes and assign new materials).

Common errors:

- *TypeError: 'float' object cannot be interpreted as an integer :

       More than one UVmap assigned per material. Remove UVmaps keep only one UVmap for each material.
 
- *AttributeError: 'NoneType' object has no attribute 'name':

       Image Texture is choosen but it was not loaded. Get the texture where you placed it.

- *IndexError: tuple index out of range:

       Base color slot has no image texture assigned. Click on it and choose Image Texture.

- *io_export_ase -RSmod.Error:

       Mesh must have at least one applied material. A material need to be assigned.

- *IndexError: bpy_prop_collection[index]: index 0 out of range, size 0

      Material slot has one mesh without assigned material. Get a material for each mesh or meshes before trying to export.

## Notes
I'm not a phython expert. This upgrade took me a lot of time trying to learn a new language. The script works as long as the necessary requirements are met.
