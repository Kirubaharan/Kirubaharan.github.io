---
layout: post
title: Installing/Compiling Modflow in Ubuntu
tags: Ubuntu, Modflow, Installation
---
# Why you need to install modflow in Ubuntu?
 
To combine Modflow with [Flopy](https://github.com/modflowpy/flopy). Flopy is an excellent python library to automate the Modflow processing process. In Ubuntu/Linux systems, the Modflow needs to be be compiled manually from source, which may sound complicated but its not an impossible task. I have to thank few people esp the developers of Flopy and Modflow, and Juan Castilla.

# Installation steps.
1. Download the source code for Modflow (Unix file structure) from [http://water.usgs.gov/ogw/modflow/MODFLOW.html#downloads](http://water.usgs.gov/ogw/modflow/MODFLOW.html#downloads).
2. Move the zip file to `/usr/local/share` and uncompress it.
3. In case you didnt install gfortran in your computer, install it using 

    `sudo apt-get install gfortran`

4. Open the makefile (`/usr/local/share/mf2005/Unix/src/makefile`) in your favourite text editor and make the following changes:
   
    F90=gfortran
   
    CC= gfortran          

5. You can also use CC=gcc if you have installed gcc in your computer.
6. Then the most important step to make Flopy read the .hds file created by Modflow is to make the following changes in openspec.inc ( `Unix/src/openspec.inc` ):

    `DATA ACCESS/'SEQUENTIAL'/` to `DATA ACCESS/'STREAM'/` 

    `DATA FORM/'BINARY'/` to `DATA FORM/'UNFORMATTED'/`

7. Save both the files and exit and make sure your current directory is `/usr/local/share/mf2005/Unix/src`.
8. Then compile using `sudo make`

You can also check out how to install Flopy from their github page [Flopy](https://github.com/modflowpy/flopy).

Also see a sample python script running Modflow in Ubuntu: [gw_tut.py from github](https://github.com/Kirubaharan/hydrology/blob/master/gw_tut.py)

