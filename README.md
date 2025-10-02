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
-obsDataPath: Where the in situ data will live. It defaults to match what was just pulled but can be changed as needed.
-ICEpics: Where any images are saved. It defaults to a folder named ICEpics that you will need to create in the LIviewer folder.
-llamaFolder: Where the LLAMAICE data from the repo live. It defaults to match what was just pulled but can be changed as needed.

The next two lines set up a prefix for any output images and the type of file generated (either png or pdf)

## In Situ Data
The repo comes with a database of ACE and Wind observations in 5 min resolution and formatted to play nice with the viewer. The different satellites live in their own folders in the ISdata folder and these names should not be edited. The ACE data is taken from SWEPAM and MAG (pulled from [here](https://izw1.caltech.edu/ACE/ASC/browse/browse_data_select.cgi?command=28)). The Wind data is taken from SWE and MFI (pulled from [here](https://cdaweb.gsfc.nasa.gov/pub/data/wind/swe/ascii/2-min/) and [here](https://spdf.gsfc.nasa.gov/pub/data/wind/mfi/ascii/1min_ascii/)). The text files correspond to a single year and have the format date (YYYY-MM-DDTHH:MM), Bx (nT), By (nT), Bz (nT), v (km/s), T (K), and n (cm^-3).

# Running LIviewer
The syntax for running the LLAMAICE viewer is simply
```
python3 LIviewer.py CODE
```
where there are several options for '''CODE'''