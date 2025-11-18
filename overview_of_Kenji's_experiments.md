

# From PI to LGM
| suite-id | years     | comment                                   | site |
| -------- | --------- | ----------------------------------------- |------|
| bm847  | - | HadGEM3-GC3.1 N96ORCA1 PI Control for CMIP6 |MetO-Cray|
| by975  | - | PI Control for CMIP6 WITH LGM orbits and CO2 |MetO-Cray|
| bz669  | - | PI LSM, LGM GHGs, orbit & icesheets |MetO-Cray|
| bz669  | - | PI LSM, LGM GHGs, orbit & icesheets |MetO-Cray|
| cj345  | - | HadGEM3-GC3.1 N96ORCA1 - PI Control std Suite for CMIP6 - 1 year test |archer2|
| cj788  | - | HadGEM3-GC3.1 N96ORCA1 - PI Control with the LGM CO2 and orbital parameters (1 year test) from cj345 |archer2|
| cj841  | - | HadGEM3-GC3.1 N96ORCA1 - PI Control with the LGM CO2 and orbital parameters, and ice-sheets on the PI LSM (1 year test) from cj788 |archer2|
| cq703  | - | the most stable simulation for the LGM,This suite is based on nearly the LGM boundary condition, but the Southern Hemisphere (S60-S90) uses a modern land-sea mask with LGM topography because the LGM model errors originated from the Southern Ocean (very close to Antarctica). from cj841|archer2|
| cj986  | - | full LGM simulation for CMIP6-PMIP4. v1 from cj841 |archer2|
| co328  | - | full LGM simulation, crashed every 2-5 years from cj986, the bathymetry of antarctica ocean is set as LGM|archer2|
| cv921  | - | HadGEM3-GC3.1 N96ORCA1 - the LGM full simulation for CMIP6-PMIP4. v7，modified based on cq703, **uses the modern bathymetry of antarctica ocean**  | archer2 |
| cz006  | - | HadGEM3-GC3.1 - the LGM simulation after ARCHER2 OS upgrade |archer2|
| db646  | - | HadGEM3-GC3.1 - the LGM simulation with the ozone remapping scheme after ARCHER2 OS upgrade |archer2|
| dc617  | - | HadGEM3-GC3.1 - a copy of cz006. Archived to the elastic tape, batch number - 98204 |archer2|


diff -ur cj788 cj345
find that
```
  -um_sources=branches/pkg/Share/vn10.7_CMIP6_production_mods@43043 branches/dev/kenjiizumi/vn10.7_orbital_21k
  +um_sources=branches/pkg/Share/vn10.7_CMIP6_production_mods@43043
```
the pathes in fact means the codes stored in the repository: **fcm:um.xm**
```
fcm ls fcm:um.xm/branches/dev/kenjiizumi/vn10.7_orbital_21k
```
checkout it by fcm co fcm:um.xm/branches/dev/kenjiizumi/vn10.7_orbital_21k
the next step is to compare these two resource directory.

## My test ##
u-ds929: copy of u-cv921

we carefully compared cv921 and cj345.
We found that the boundary condition of cv921 are modified into a LGM style. 
```
--- /work/y07/shared/umshared/ancil/data/ancil_versions/n96e_orca1/GA7.1/v2/ancils      2017-10-02 11:10:18.000000000 +0100
+++ /work/n02/n02/kizumi/ancils/um_ancils_PILGM4        2022-09-09 14:14:45.000000000 +0100
@@ -7,6 +7,7 @@

 # File containing filenames version file
 UM_ANCIL_FILENAMES=${UM_ANCIL_FILENAMES:-$UMDIR/ancil/data/ancil_versions/filenames/v9/ancils}
+#UM_ANCIL_FILENAMES=/work/n02/n02/kizumi/ancils/ancils_version_info

 # Source in filenames
 . $UM_ANCIL_FILENAMES
@@ -19,17 +20,41 @@
 export UM_ANCIL_DIR=$UM_ANCIL_N96EDIR
 export UM_ANCIL_OCEANDIR=$UM_ANCIL_N96EORCA1DIR

-export UM_ANCIL_MASK_DIR=$UM_ANCIL_N96EORCA1DIR/land_sea_mask/etop01/v2
-export UM_ANCIL_OROG_DIR=$UM_ANCIL_N96EORCA1DIR/orography/globe30/v6
-export UM_ANCIL_SST_DIR=$UM_ANCIL_N96EORCA1DIR/sst/reynolds/1981_2012_360/v3
-export UM_ANCIL_SEAICE_DIR=$UM_ANCIL_N96EORCA1DIR/seaice/reynolds/1981_2012_360/v4
-
-export UM_ANCIL_SOILDUST_DIR=$UM_ANCIL_N96EORCA1DIR/soil_dust/hwsd/v4
-export UM_ANCIL_SOIL_DIR=$UM_ANCIL_N96EORCA1DIR/soil_parameters/hwsd_vg/v4
-
-export UM_ANCIL_VEGFRAC_DIR=$UM_ANCIL_N96EORCA1DIR/vegetation/fractions_igbp/v4
-export UM_ANCIL_VEGFUNC_DIR=$UM_ANCIL_N96EORCA1DIR/vegetation/func_type_modis/v4
-export UM_ANCIL_OZONE_DIR=$UM_ANCIL_N96EDIR/ozone/sparc/1994-2005/v3
+#export UM_ANCIL_MASK_DIR=$UM_ANCIL_N96EORCA1DIR/land_sea_mask/etop01/v2
+export UM_ANCIL_MASK_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/land_sea_mask/etop01/PILGM4
+
+#export UM_ANCIL_OROG_DIR=$UM_ANCIL_N96EORCA1DIR/orography/globe30/v6
+export UM_ANCIL_OROG_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/orography/globe30/PILGM4
+
+#export UM_ANCIL_SST_DIR=$UM_ANCIL_N96EORCA1DIR/sst/reynolds/1981_2012_360/v3
+export UM_ANCIL_SST_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/sst/PILGM4
+
+#export UM_ANCIL_SEAICE_DIR=$UM_ANCIL_N96EORCA1DIR/seaice/reynolds/1981_2012_360/v4
+export UM_ANCIL_SEAICE_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/seaice/PILGM4
+
+#export UM_ANCIL_SOILDUST_DIR=$UM_ANCIL_N96EORCA1DIR/soil_dust/hwsd/v4
+export UM_ANCIL_SOILDUST_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/soil_dust/PILGM4
+
+#export UM_ANCIL_SOIL_DIR=$UM_ANCIL_N96EORCA1DIR/soil_parameters/hwsd_vg/v4
+#export UM_ANCIL_SOIL_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/soil_parameters/PILGM4
+export UM_ANCIL_SOIL_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_PI/soil_parameters/hwsd_vg/PILGM4
+
+#export UM_ANCIL_VEGFRAC_DIR=$UM_ANCIL_N96EORCA1DIR/vegetation/fractions_igbp/v4
+#export UM_ANCIL_VEGFRAC_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/vegetation/fractions_igbp/PILGM4
+export UM_ANCIL_VEGFRAC_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_PI/vegetation/fractions_igbp/PILGM4
+
+#export UM_ANCIL_VEGFUNC_DIR=$UM_ANCIL_N96EORCA1DIR/vegetation/func_type_modis/v4
+#export UM_ANCIL_VEGFUNC_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/vegetation/func_type_modis/PILGM4
+export UM_ANCIL_VEGFUNC_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_PI/vegetation/func_type_modis/PILGM4
+
+#export UM_ANCIL_OZONE_DIR=$UM_ANCIL_N96EDIR/ozone/sparc/1994-2005/v3
+export UM_ANCIL_OZONE_DIR=/work/n02/n02/kizumi/projects/n96e_orca/n96e_orca1_go6/ozone/sparc/1994-2005/LGM
```
### Coupling weights
As mentioned in hadgem3-eocene/Eocene configuration.md, in the set of Eocene suites, the coupling weights (`coupled > env > RMP_DIR` in the rose editor) was changed to a new one building by Seb. However, this process wasn't done in all the suites of Kenji. Why this step was ignored in the setting of LGM configuration?
**waiting for Charlie's response**


