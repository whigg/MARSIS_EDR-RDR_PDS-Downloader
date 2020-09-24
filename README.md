# SCRIPT for search and download MARSIS FlashMemory RAW geometry files and radargrams
### @author: Giacomo Nodjoumi - g.nodjoumi@jacobs-university.de

# README
________________________________________________________________________________
# Table of Contents

* [Pipeline/workflow description](#Pipeline/workflow descriptione)
* [CONDA Environment](#CONDA Environment)
    * [Install Anaconda](##Install anaconda)
    * [Create the environment using the yml](## Create the environment using the yml)
    * [Activate MARSIS_py38 environment](## Activate MARSIS_py38 environment)
* [Script execution](# Script execution)
    * [Arguments to be passed](## Arguments to be passed)
* [Examples](# Examples)
    * [Conda environment installation and script execution](## Conda environment installation and script execution)
    * [General Example](## General example)
    * [Test example](## Test example)

________________________________________________________________________________
# Pipeline/workflow description

The script in brief:

* Retreive file geometry list from the ftp server
* Search user_requested orbits
* Report missing orbits
* Ask for download RAW geometry files and PNG files
* Computer Size of the download and ask for confirmation
* Download requested orbits and ask if user want to download more

** See example at the end of this readme**

The script can work both passing some/all arguments or none ***If NO argument is passed, defaults are used and interactively requested the others.***

# CONDA environment

To best use the script a conda environment configuration file is provided: ***MARSIS_py38.yml***

## Install anaconda

Installer of anaconda for different operating systems are provided on the official page. [Anaconda Installers](https://www.anaconda.com/products/individual)

To install conda on linux, download [this](https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh) file, 
with terminal move to the downloaded folder and run:
* `sudo chmod +x Anaconda3-VERSION-Linux-x86_64.sh` (replace VERSION with the proper filename)
* `sudo ./Anaconda3-VERSION-Linux-x86_64.sh`

## Create the environment using the yml

Using the terminal, move to the folder where is located MARSIS_py38.yml and run:
`conda env create -f MARSIS_py38.yml`

## Activate MARSIS_py38 environment

Just run:
`conda activate MARSIS_py38`

# Script execution

To execute, simple run the following code `python MARSIS_FTP_RETREIVER.py`
It will ask every arguments.

## Arguments to be passed

### Server
-- server : ip address of common name of the server.
default is : 150.146.129.243'
### FlashMemory ftp path
--fmdir : flashmemory full path where are store the *.DAT and PNG.
default is: '/MARSIS_Flash_Memory_geometry/Mars
### User
--user : ftp login user
### Password
--pwd : ftp login passeord
### Orbits numbers csv
--orbits: csv file containing all orbit to download.

This csv can be manually created or generated by QGIS


*  **MANUAL CSV**
Is as a one-column csv with "Orbit" (without quotes) as first row
and orbit numbers as new rows. e.g.

| Orbit |
| ----- |
| 02445 |
| 01865 |
| 10231 |
| ..... |

* **QGIS CSV**
Simply is a csv created by saving selected features directly in QGIS.



**See below for details**

### Download directory
--ddir : is the folder where the files will be downloaded
default is a folder called "downloads+datetime".
Automatically created in the directory where is executed the script



________________________________________________________________________________________________

# QGIS CSV CREATION 

## Manually orbit by orbit
**Orbit numbers can be retreived from QGIS**
**Step 1m - You can interrogate every orbit by using the info tool**
![alt text](Readme_images/Feat_info_1.jpg?raw=true "Step 1m")

**Step 2m - Left click on each track of interest, a side panel will open with all relative informations, take notes of the orbit number and create a CSV file as described above.**
![alt text](Readme_images/Feat_info_2.jpg?raw=true "Step 2m")

## Manually multiple orbits 

**Step 1 - Activate the feature selection tool**
![alt text](Readme_images/Feat_sel_1.jpg?raw=true "Step 1")

**Step 2 - select features of interests**
![alt text](Readme_images/Feat_sel_2.jpg?raw=true "Step 2")

**Step 3 - Right click on the geopackage layer and select export->save selected features as**
![alt text](Readme_images/Feat_sel_3.jpg?raw=true "Step 3")

**Step 4 - In the opened windows select:**
* **Format**: Comma Separated Value[CSV]
* **File name**: selecte path and savename of choice
* Then expand "Select fields to export and their export options" and flag ONLY **Orbit**
* **Click on ok**

![alt text](Readme_images/Feat_sel_4.jpg?raw=true "Step 4")

# Examples

## Conda environment installation and script execution 
Thanks to @aprossi
[Report](https://gist.github.com/aprossi/5962b7fca2fbea465a00534c66b3e2a0)

## General example

Just run `python MARSIS_FTP_RETREIVER.py --ddir=/path-to-download-folder --orbits=/path-to-csv-orbit-file`

## Test example

Here the example code shown in the image
`python MARSIS_FTP_DATA_RETRIEVER.py --ddir=/media/gnodj/W-DATS/MARSIS_Data/ --orbits=/media/gnodj/W-DATS/MARSIS_Data/req_orbits_qgis.csv`

![alt text](Readme_images/terminal_run.jpg?raw=true "Test")



