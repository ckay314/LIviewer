# LLAMAICE Viewer
This is the code used to view the LLAMAICE catalog, or to just look at ACE/Wind in situ data. This guide shows how to get the code running and demonstrates basic use. This repo does contain about 450 MB of in situ data so may take a few moments to download.

## Dependencies
The LLAMAICE viewer is a single Python script  using basic packages and does not merit setting up a virtual environment in most cases. It should be kept up to date with the most recent versions, but we list the specific versions used at the time of commit.
- Python 3.12.4
- matplotlib 3.9.0
- numpy 2.0.0
- datetime/sys built into Python so no individual version number

## Set up
Clone the repository. This should download the LIviewer.py folder, a folder with files corresponding to the most recent version of the LLAMAICE data, and the formatted in situ data. Open LIview in a text editor. Lines 8-10 should be edited to match your system and your preferences. These correspond to
- obsDataPath: Where the in situ data will live. It defaults to match what was just pulled but can be changed as needed.
- ICEpics: Where any images are saved. It defaults to a folder named ICEpics that you will need to create in the LIviewer folder.
- llamaFolder: Where the LLAMAICE data from the repo live. It defaults to match what was just pulled but can be changed as needed.

The next two lines set up a prefix for any output images and the type of file generated (either png or pdf)

## In Situ Data
The repo comes with a database of ACE and Wind observations in 5 min resolution and formatted to play nice with the viewer. The different satellites live in their own folders in the ISdata folder and these names should not be edited. The ACE data is taken from SWEPAM and MAG (pulled from [here](https://izw1.caltech.edu/ACE/ASC/browse/browse_data_select.cgi?command=28)). The Wind data is taken from SWE and MFI (pulled from [here](https://cdaweb.gsfc.nasa.gov/pub/data/wind/swe/ascii/2-min/) and [here](https://spdf.gsfc.nasa.gov/pub/data/wind/mfi/ascii/1min_ascii/)). The text files correspond to a single year and have the format date (YYYY-MM-DDTHH:MM), Bx (nT), By (nT), Bz (nT), v (km/s), T (K), and n (cm^-3). All B vector components are in GSE coordinates. At the moment the viewer includes data up through the end of 2024.

# Running LIviewer
The syntax for running the LLAMAICE viewer is simply
```
python3 LIviewer.py CODE
```
where there are several options for CODE. If you want to pull up a LLAMAICE event you can use either the integer ID number or the ID time in the format YYYY-MM-DDTHH:MM. Alternatively, you can just look at in situ data without any of the LLAMAICE information. For this, CODE can be of the format YYYYMMDD, YYYYMMDDHHMM, YYYY-MM-DD, or YYYY-MM-DDTHH:MM, which will set the 'time of interest' for the plotting window. It will show one day before this time to three days after. The '-' in the time formats can be switched to '/', '_', or '.' to allow for some personal preferences.

If a valid version of CODE is passed then the standard Python plot window will appear. This will show, from top to bottom, B, Bx, By, Bz, the magnetic field inclination (theta), the magnetic field longitudinal angle (phi), v, T, n, and beta. The code makes an attempt to automatically scale each panel to nice ranges and is typically successful. The built in zoom and pan options within the Python window can be used and we have set it up so that if one clicks within a panel the corresponding timestamp and y-value will be printed to the terminal. The terminal also automatically displays the times of the boundaries from all catalogs.

## Customizing LIviewer
Some options can easiy be modified in LIviewer.py to customize the figure/interface. Lines 15-20 represent binary options that can be turned on and off.
- justIS: Only plot in situ data and none of the LLAMAICE information.
- shadeICE: Shade in the CME regions using the boundaries established by the LLAMAICE team
- plotCats: Plot vertical lines at the boudaries taken from external catalogs
- plotHSS: Plot bars at the top corresponding to the location of high speed streams according to several external catalogs
- addLabels: Add a legend on the right hand side indicating the colors of the various catalogs/regions
- saveIt: Instead of popping up a display window just save a figure using the figprefix and figtype given in lines 11/12

Lines 22-34 establish the colors used for various items. Line 23 sets the colors of the LLAMAICE regions. Line 26 sets the colors of the different external catalog boundaries. Line 29 sets the relative position and color of the HSS catalogs. Finally lines 32-34 sets the thickness and colors of the in situ satellite data.

# Getting all LLAMAICE figures
If CODE is set to ALL then the LIviewer will not pop a window but instead save a figure for every CME in the LLAMAICE database. This will take a little bit of time for the ~400 events, and it is strongly recommended to have the figFolder setup with a nice spot to contain them. The automatic boundaries should work well for most cases but a handful of events will have less than ideal ranges and can be replaced by hand as needed.

# LLAMAICE Data
We list the contents of the LLAMAICE data files here for completeness.

## HSSsort.dat
This file contains the HSS boundaries pulled from the literature. It has the start and stop time in decimal year, a code for the source catalog, then the start and stop times in YYYY-MM-DD HH:MM. The letter codes correspond to [DONKI](https://kauai.ccmc.gsfc.nasa.gov/DONKI/search/) (D), [Grandin](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2018JA026396) (G), [VARSITI](https://www.geodin.ro/varsiti/) (V), and [Xystouris](https://link.springer.com/article/10.1007/s11207-013-0355-z) (X). 
## LLAMAICE_1.0.csv
This file contains the new boundaries set by the LLAMAICE team. The columns correspond to the event number, any adjacent events that are interacting, the sheath/shock boundary, front mixed boundary, FR front, FR end, back mixed boundary, any HSS catalogs that have an entry at this time, and the comments from the team. Entries without values for a specific column have ``-'' to indicate a null value.

## otherCats_1.0.dat
This file contains the boundaries from the source catalogs. The columns list the LLAMAICE event number, the LLAMAICE time, the source catalog, the sheath/shock boundary, FR front, FR end, and the associated coronal event. Null entries are given as 'None'

## plotBounds_1.0.dat 
This file contains the plot ranges for the LLAMAICE events. The columns correspond to the LLAMAICE ID number, the LLAMAICE ID time, the plot start, and the plot end. All times are in the format YYYY-MM-DDTHH:MM