# VFX Show Project Directory Structure and Naming Conventions

## Directory Structure

For VFX shows, the project directory is divided into **comp/** and **CG/** folders. Within **CG/** this is further divided into an **assets** folder for the modeling, rigging, and lookdev departments, and a **shots** folder for the animation, FX, and lighting departments. Additionally we have the **textures**, **farm**, and **publish** folders. 

## assets/

### &nbsp;&nbsp;&nbsp;mod/
   
- *modeling department: Maya files*
  
  ```[AssetName] / [AssetName]_mod_[artist]_[ver].ma```
  
  example:
  ```
  mod/
    spaceShip/
      spaceShip_mod_bsmith_v01.ma
  ```
### &nbsp;&nbsp;&nbsp;rig/

- *rigging department: Maya files*

  ```[AssetName] / [AssetName]_rig_[artist]_[ver].ma```
  
  example: 
  ```
  rig/
    spaceShip/
      spaceShip_rig_jdoe_v01.ma
  ```


### &nbsp;&nbsp;&nbsp;tex/
  
- *lookdev department: Maya turntable files*
  
  ```maya / [AssetName] / [AssetName]_tex_[artist]_TT_[ver].ma```
  
  example: 
  ```
  tex/
    maya/
      spaceShip/
        spaceShip_tex_kjones_TT_v01.ma
  ```
  
- *lookdev department: Maya published assets*
  
  ```maya / [AssetName] / [AssetName]_tex_[artist]_[ver].ma```
  
  example: 
  ```
  tex/
    maya/
      spaceShip/
        spaceShip_tex_kjones_v01.ma
  ```

  
- *lookdev department: Substance Painter files*
  
  ```painter / [AssetName] / [AssetName]_[artist]_[ver].spp```
  
  example: 
  ```
  tex/
    painter/
      spaceShip/
        spaceShip_kjones_v01.spp
  ```
  



<br><br>
## shots/

### &nbsp;&nbsp;&nbsp;anim/

- *animation department: Maya files*
  
  ```[ShotName] / [ShotName]_anim_[artist]_[ver].ma```
  
  example:
  ```
  anim/
    AGM_067_0015/
      AGM_067_0015_anim_jdoe_v01.ma
  ```
  
### &nbsp;&nbsp;&nbsp;fx/
  
- *effects department: Maya files*
  
  ```maya / [ShotName] / [ShotName]_fx_[artist]_[ver].ma```
  
  example:
  ```
  fx/
    maya/
      AGM_067_0015/
        AGM_067_0015_fx_bsmith_v01.ma
  ```

- *effects department: Houdini files*
  
  ```houdini / [ShotName] / [ShotName]_fx_[artist]_[ver].hip```
  
  example:
  ```
  fx/
    houdini/
      AGM_067_0015/
        AGM_067_0015_fx_bsmith_v01.hip
  ```

### &nbsp;&nbsp;&nbsp;light/
  
- *lighting department: Maya files*
  
  ```maya / [ShotName] / [ShotName]_light_[artist]_[ver].ma```
  
  example:
  ```
  light/
    maya/
      AGM_067_0015/
        AGM_067_0015_light_bsmith_v01.ma
  ```
  
- *lighting department: Nuke files*
  
  ```nuke / [ShotName] / [ShotName]_light_[artist]_[ver].ma```
  
  example:
  ```
  light/
    nuke/
      AGM_067_0015/
        AGM_067_0015_light_bsmith_v01.nk
  ```

  
### &nbsp;&nbsp;&nbsp;publish/
  
- *published files: Alembic caches*
  
  ```Alembic / [ShotName] / [ShotName]_[AssetName]_[artist]_[ver].abc```
  
  example:
  ```
  publish/
    Alembic/
      AGM_067_0015/
        AGM_067_0015_bottleRocket_bsmith_v01.abc
  ```
- *published files: OpenVDB*
  
  ```vdb / [ShotName]/  [ShotName]_[EffectName]_[artist]_[ver].vdb```
  
  example:
  ```
  publish/
    vdb/
      AGM_067_0015/
        AGM_067_0015_smoke_bsmith_v01.vdb
  ```

- *published files: neutralized plates (ACEScg)*
  
  ```neut_footage / [ShotName] / [ShotName]_neutCG_[artist]_[ver].####.exr```
  
  example:
  ```
  publish/
    neut_footage/
      AGM_067_0015/
        AGM_067_0015_neutCG_bsmith_v01.0001.exr
  ```
  
- *published files: degrained plates (ACEScg)*
  
  ```degrained_footage / [ShotName] / [ShotName]_neutCG_[artist]_[ver].####.exr```
  
  example:
  ```
  publish/
    degrained_footage/
      AGM_067_0015/
        AGM_067_0015_degrain_bsmith_v01.0001.exr
  ```





<br><br>
## textures/

### &nbsp;&nbsp;&nbsp;textures/
  
- *texture maps (map naming: dif, spc, bmp, nor, dsp, met, msk, lyr)*

  ```[AssetName] / [ShaderName]_[map]_[AssetName}_[artist]_[ver].[ext]```
  
  example:
  ```
  textures/
    spaceShip/
      plastic_dif_bottleRocket_kjones_v01.jpg
  ```


<br><br>
## farm/

### &nbsp;&nbsp;&nbsp;renders/

- *lighting department: renders*

  ```[ShotName] / [ShotName]_light_[artist]_[ver].####.exr```
  
  example:
  ```
  renders/
    AGM_067_0015/
      AGM_067_0015_light_jdoe_v01.0001.exr
  ```
  
### &nbsp;&nbsp;&nbsp;comps/

- *lighting department: slap comp tests*
  
  ```[ShotName] / [ShotName]_light_[artist]_[ver].####.jpg```
  
  example:
  ```
  renders/
    AGM_067_0015/
      AGM_067_0015_light_jdoe_v01.0001.jpg
  ```


## Naming Conventions

**VERSIONING** Always make sure you version up an asset when you do any work on it. The simple rule with versioning is "add 1" so if you are starting work as a modeler on a model already in progress that is v23, yours should start at (+1) v24. The only time versions should start at v01 is when it is the first version of that task. For example when model v24 gets passed to rigging it would begin at rig v01.

**ASSET NAME** If an *asset name* consists of multiple word descriptors (for example  a bottle rocket) this should be written as one word without underscores, using capital letters for seperation (example "bottleRocket").

**SHOT NAME** A *shot name* is composed of *fields* seperated by underscores. 

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
    
So for a show with no sequences the shot name would consist of ```showID_scene_shotID#``` for example ```AGM_067_0015```




<br><br><br>
# Lighting Shot Build Flow Chart



![nk](img/Lighting_Shot_Build.png)
