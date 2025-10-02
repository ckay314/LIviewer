# LLAMAICE Viewer
This is the code used to view the LLAMAICE catalog, or to just look at ACE/Wind in situ data. This guide shows how to get the code running and demonstrates basic use.

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
The viewer needs a database of ACE and Wind data to run.