# Project Directory Structure and Naming Conventions

## assets/
  
<details>
  <summary><b>mod/</b></summary>
  
- *modeling department: Maya files*
  
  ```[AssetName] / [AssetName]_mod_[artist]_[ver].ma```
  
  example:
  ```
  mod/
    spaceShip/
      spaceShip_mod_bsmith_v01.ma
  ```
</details>

<details>
  <summary><b>rig/</b></summary>
  
- *rigging department: Maya files*

  ```[AssetName] / [AssetName]_rig_[artist]_[ver].ma```
  
  example: 
  ```
  rig/
    spaceShip/
      spaceShip_rig_jdoe_v01.ma
  ```
</details>

<details>
  <summary><b>tex/</b></summary>
  
- *lookdev department: Maya files*
  
  ```[AssetName] / [AssetName]_tex_[artist]_[ver].ma```
  
  example: 
  ```
  tex/
    maya/
      spaceShip/
        spaceShip_tex_kjones_v01.ma
  ```
  
- *lookdev department: Substance Painter files*
  
  ```[AssetName] / [AssetName]_[artist]_[ver].spp```
  
  example: 
  ```
  tex/
    painter/
      spaceShip/
        spaceShip_kjones_v01.spp
  ```
  
</details>

## shots/

<details>
  <summary><b>anim</b></summary>

- *animation department: Maya files*
  
  ```[ShotName] / [ShotName]_anim_[artist]_[ver].ma```
  
  example:
  ```
  anim/
    GG_Sc20_50/
      GG_Sc20_50_anim_jdoe_v01.ma*
  ```
  
</details>

<details>
  <summary><b>fx</b></summary>
  
- *effects department: Maya files*
  
  ```[ShotName] / [ShotName]_fx_[artist]_[ver].ma```
  
  example:
  ```
  fx/
    maya/
      GG_Sc20_50/
        GG_Sc20_50_fx_bsmith_v01.ma
  ```

- *effects department: Houdini files*
  
  ```[ShotName] / [ShotName]_fx_[artist]_[ver].hip```
  
  example:
  ```
  fx/
    houdini/
      GG_Sc20_50/
        GG_Sc20_50_fx_bsmith_v01.hip
  ```
</details>

<details>
  <summary><b>light</b></summary>
  
- *lighting department: Houdini files*
  
  ```maya/[ShotName]/[ShotName]_light_[artist]_[ver].ma```
  
  example:
  ```
  light/
    maya/
      GG_Sc20_50/
        GG_Sc20_50_light_bsmith_v01.ma
  ```
  
 - *lighting department: Nuke files*
  
  ```nuke/[ShotName]/[ShotName]_light_[artist]_[ver].ma```
  
  example:
  ```
  light/
    nuke/
      GG_Sc20_50/
        GG_Sc20_50_light_bsmith_v01.nk
  ```

  
</details>

<details>
  <summary><b>publish/</b></summary>
  
- *published files: Alembic caches*
  
  ```Alembic/[ShotName]/[AssetName]_[artist]_[ver].ma```
  
  example:
  ```
  publish/
    Alembic/
      GG_Sc20_50/
        spaceShip_bsmith_v01.abc
  ```

</details>

## textures/
  
  ```[AssetName]/[ShaderName]_[map]_[AssetName}_[artist]_[ver].[ext]```<br>
  example:<br>
  *spaceShip/leather_dif_spaceShip_kjones_v01.jpg*
</details>

<details>
  <summary><b>farm</b></summary>

- **renders**<br>
  ```[ShotName]/[ShotName]_light_[artist]_[ver].####.exr```<br>
  example:<br>
  *GG_Sc20_50/GG_Sc20_50_light_jdoe_v01.0001.exr*
  
- **comps**<br>
  ```[ShotName]/[ShotName]_light_[artist]_[ver].####.jpg```<br>
  example:<br>
  *GG_Sc20_50/GG_Sc20_50_light_bsmith_v01.0001.jpg*
