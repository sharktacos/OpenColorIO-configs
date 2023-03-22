# VFX Show Project Directory Structure and Naming Conventions



## CG Directory Structure

For VFX shows, the project directory is divided into **comp/** and **CG/** folders. Below is a breakdown of where CG files go and how they should be named.

```
CG/
  assets/
     mod/
     rig
     tex/
  shots/
     anim/
     fx/
     light/
     publish/
        Alembic/
        vdb/
        ref_footage/
        neut_footage/
        degrained_footage/
      renders/
      slap_comps/
  textures/
```

Additionally, renders and lighting slap-comps go on the farm exchange. These are then transfered to the appropriate **comp/** directory (CG_elements/) by the VFX lead.

```
[CollabEXCHANGE path]/
     renders/
     comps/
```

## assets/

### &nbsp;&nbsp;&nbsp;mod/
   
- *modeling department: Maya files*
  
  ```[AssetName] / [AssetName]_mod_[ver]_[artist].ma```
  
  example:
  ```
  mod/
    spaceShip/
      spaceShip_mod_v01_bsmith.ma
  ```
### &nbsp;&nbsp;&nbsp;rig/

- *rigging department: Maya files*

  ```[AssetName] / [AssetName]_rig_[ver]_[artist].ma```
  
  example: 
  ```
  rig/
    spaceShip/
      spaceShip_rig_v01_jdoe.ma
  ```


### &nbsp;&nbsp;&nbsp;tex/
  
- *lookdev department: Maya turntable files*
  
  ```maya / [AssetName] / [AssetName]_tex_TT_[ver]_[artist].ma```
  
  example: 
  ```
  tex/
    maya/
      spaceShip/
        spaceShip_tex_TT_v01_kjones.ma
  ```
  
- *lookdev department: Maya published assets*
  
  ```maya / [AssetName] / [AssetName]_tex_[ver]_[artist].ma```
  
  example: 
  ```
  tex/
    maya/
      spaceShip/
        spaceShip_tex_v01_kjones.ma
  ```

  
- *lookdev department: Substance Painter files*
  
  ```painter / [AssetName] / [AssetName]_[ver]_[artist].spp```
  
  example: 
  ```
  tex/
    painter/
      spaceShip/
        spaceShip_v01_kjones.spp
  ```
  



<br><br>
## shots/

See the "Naming Conventions" section below for details on the fields that make up a Shot Name.

### &nbsp;&nbsp;&nbsp;anim/

- *animation department: Maya files*
  
  ```[ShotName] / [ShotName]_anim_[ver]_[artist].ma```
  
  example:
  ```
  anim/
    AGM_067_0015/
      AGM_067_0015_anim_v01_jdoe.ma
  ```
  
### &nbsp;&nbsp;&nbsp;fx/
  
- *effects department: Maya files*
  
  ```maya / [ShotName] / [ShotName]_fx_[ver]_[artist].ma```
  
  example:
  ```
  fx/
    maya/
      AGM_067_0015/
        AGM_067_0015_fx_v01_bsmith.ma
  ```

- *effects department: Houdini files*
  
  ```houdini / [ShotName] / [ShotName]_fx_[ver]_[artist].hip```
  
  example:
  ```
  fx/
    houdini/
      AGM_067_0015/
        AGM_067_0015_fx_v01_bsmith.hip
  ```

### &nbsp;&nbsp;&nbsp;light/
  
- *lighting department: Maya files*
  
  ```maya / [ShotName] / [ShotName]_light_[ver]_[artist].ma```
  
  example:
  ```
  light/
    maya/
      AGM_067_0015/
        AGM_067_0015_light_v01_bsmith.ma
  ```
  
- *lighting department: Nuke files*
  
  ```nuke / [ShotName] / [ShotName]_light_[ver]_[artist].ma```
  
  example:
  ```
  light/
    nuke/
      AGM_067_0015/
        AGM_067_0015_light_v01_bsmith.nk
  ```

  
### &nbsp;&nbsp;&nbsp;publish/
  
- *published files: Alembic caches*
  
  ```Alembic / [ShotName] / [ShotName]_[AssetName]_[ver]_[artist].abc```
  
  example:
  ```
  publish/
    Alembic/
      AGM_067_0015/
        AGM_067_0015_bottleRocket_v01_bsmith.abc
  ```
- *published files: OpenVDB*
  
  ```vdb / [ShotName]/  [ShotName]_[EffectName]_[artist]_[ver].vdb```
  
  example:
  ```
  publish/
    vdb/
      AGM_067_0015/
        AGM_067_0015_smoke_v01_bsmith.vdb
  ```
  
- *published files: downsized JPG sequence for animation (baked view)*
  
  ```ref_footage / [ShotName] / [ShotName]_ref_[ver]_[artist].####.jpg```
  
  example:
  ```
  publish/
    ref_footage/
      AGM_067_0015/
        AGM_067_0015_ref_v01_bsmith.0001.jpg
  ```


- *published files: neutralized plates (ACEScg)*
  
  ```neut_footage / [ShotName] / [ShotName]_neutCG_[ver]_[artist].####.exr```
  
  example:
  ```
  publish/
    neut_footage/
      AGM_067_0015/
        AGM_067_0015_neutCG_v01_bsmith.0001.exr
  ```
  
- *published files: degrained plates (ACEScg)*
  
  ```degrained_footage / [ShotName] / [ShotName]_neutCG_[ver]_[artist].####.exr```
  
  example:
  ```
  publish/
    degrained_footage/
      AGM_067_0015/
        AGM_067_0015_degrain_v01_bsmith.0001.exr
  ```


## renders/

- *lighting department: rendered EXR sequence*
  
  ```[ShotName] / [ShotName]_light_[ver]_[artist].####.exr```
  
  example:
  ```
    AGM_067_0015/
      AGM_067_0015_light_v01_jdoe.0001.exr
  ```

## slapcomp/

- *lighting department: JPG sequqnce of slap comp of render*
  
  ```[ShotName] / [ShotName]_light_[ver]_[artist].####.jpg```
  
  example:
  ```
    AGM_067_0015/
      AGM_067_0015_light_v01_jdoe.0001.jpg
  ```

<br><br>
## textures/
  
- *texture maps (map naming: dif, spc, bmp, nor, dsp, met, msk, lyr)*

  ```[AssetName] / [ShaderName]_[map]_[AssetName}_[ver]_[artist].[ext]```
  
  example:
  ```
  textures/
    spaceShip/
      plastic_dif_bottleRocket_v01_kjones.jpg
  ```





## Naming Conventions

CG files are categorized into either Assets or Shots.

**ASSET NAME** If an *assetName* consists of multiple word descriptors (for example  a bottle rocket) this should be written as one word without underscores, using capital letters for separation (example "bottleRocket").

**SHOT NAME** A *shotName* is composed of *fields* separated by underscores. 

The following is based on the [Netflix VFX Shot and Version Naming Recommendations](https://partnerhelp.netflixstudios.com/hc/en-us/articles/360057627473-VFX-Shot-and-Version-Naming-Recommendations)

**shot fields**

- showID

    A 2-3 character abbreviation for the project name.
    Example: AGM = A Great Movie
    Usage: Required for series projects (except optional for IO). Optional for all other project types.                                                  

- sequence

    A sequence is a 2-3 character abbreviation for a collection of scenes that are considered a VFX sequence. Sequences can also be assigned to numbers.
    Example: TCC = The Car Chase
    Usage: Optional. (Not all projects get broken down by sequence)

- scene

    Scene number from the portion of the script that a VFX shot came from. Usually appears on the slate.
    Example: 067 = shot comes from scene 67
    Usage: Optional but required if project naming does not use sequences.
    Note: Sometimes scene numbers will appear with letters appended to them to indicate inserted scenes, camera setups or plate shoots. Letters can be ignored for shot naming purposes. It's usually simpler to manage shot names without including any scene letters for overall consistency of file naming.

- shotID#

    3-4 digit identifying number assigned chronologically by sequence or by scene.
    Numbers are typically assigned chronologically by sequence or scene and usually increments by 10s, so if a VFX shot is later identified between ID 0010 and ID 0020 it can be given an ID in between, such as 0015
    Example: 0010 = shot’s assigned ID number is 0010 
    Usage: Required.
    
So for a show with no sequences the ShotName would consist of ```[showID]_[scene]_[shotID#]``` for example ```AGM_067_0015```. 


 
<br><br><br>
# Lighting Shot Build Flow Chart

The following flow-chart shows the path that assets take in the construction of a lighting shot build.

![nk](img/Lighting_Shot_Build.png)
