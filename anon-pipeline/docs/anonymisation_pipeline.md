
# Introduction

Introduction
# Installation

## Enviroment
- Linux Unbuntu 22.04

## Pre-requriments
- Github
- Docker
- Python 3.10


## Setup
- clone the repository of anonymisation pipeline, for example:

```
git clone https://github.com/plymouth-neuroimaging/anon-pipeline-set.git
```
- run the setup script 
```
./setup.sh
```
- install python packages in requirements.txt. It recommanded to use a virtual enviroment, for example:
```
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
- a copy of file config.py should have been createed. Update the `SALT` variable in the file to desired value. (see ??? for detail about `SALT`).
If the file is not created automatically, it can be copied manually from `templates/config_template.py` to the root folder (`anon-pipeline-set`).

## (optional) Installation for developer
to add

# Run

## Quick Run with example data

Try the following code for a quick run with our example data:
```
./anon_pipeline.py example_input/ -p my_results
```
Here, `my_results` will be created containing the anonymised files.



## Run with your own data

To anonymise you own data, you can crate a folder with the following structure
```
<input_folder>/
    <accession number 1>/
        <DICOM file 1>
        <DICOM file 2>
    <accession number 2>/
        <DICOM file 1>
        <DICOM file 2>    

```
and run the following code
```
./anon_pipeline.py <path/to/input_folder> -p <path/to/output_folder>
```
Please note that the input and output folder don't have to be saved in the root folder.


## Continuous mode and restart mode

In restart mode, the program assume there are no processed files and would raise an error if it found any. This mode is the default.

In continuous mode, if there are processed files in output directory, the program will skip them and continue to prcess the rest. 

To use continuse mode, add option `-c` in command, for example:
```
./anon_pipeline.py <path/to/input_folder> -p <path/to/output_folder> -c
```

**Please note**: the program assume that assession number is used to name the sub-directory (the folder containing the DICOM files), if this is not the case the program will fail to detect processed sub-directories and process them.


## Exit in error
The program is default to continue processing, if a unknown error is encountered when processing a sub-directory.
If this option is on, the program will stop processing. Use `-e` option to enable this option, for example:
```
./anon_pipeline.py <path/to/input_folder> -p <path/to/output_folder> -e
```

## Skip extra checks
If this option is on, the program will skip the optical character recoginition (OCR) search for public health information (PHI) embeded on image. Use `-s` to enable this option, for example:
```
./anon_pipeline.py <path/to/input_folder> -p <path/to/output_folder> -s
```


# Logs
logs and records of an anonymisation process are saved in folder `log/`.

## events.log
This file logs all the relavent information, warning and errors in an anonymisation process. Check this file for details about running of anonymise pipeline.

## mirc-ctp.log
This file logs all the outputs from mirc-ctp tool. Check this file for details about running of mirc-ctp tool.


## prog_recorder.db
This is an sqlite database tracing the status of every DICOM file and its directory in anonymisation process. See <<???>> for more details about the tables in the database.




# Anonymisation summary

to add



# Structure of the code

to add


# Test


to add

# anon_recorder
## database
This is an sqlite database tracing the status of every DICOM file and its directory in anonymisation process. Following tables are contained in the database.
### folders
Record the status of subdirectories that containing DICOM files, with the following columns.
- name: name of the subdirectory
- status: status of process, including
    - unchecked: not been checked by the program
    - checking: being checked by the program
    - checked: checked by the program
- pseudo_name: pseudo_name corresponding to the folder

### folder_process_status
Record the process status of subdirectories that containing DICOM files, with the following columns.
- name: name of the subdirectory
- process: process status (eg: empty folder, some files corrupted). see ??? for more details of the categories.
Please note that each folder can contain multiple process status, eg: a folder can have corrupted files and files with PHI on image.


### folder_process_status_lookup
A look up table for the process status in folder_process_status. They are configured in config.py.
 - status: name of process status for internal use
 - status_name: a name for external use (eg: tables)
 - description: a detailed description for the status
 - action: what action to take when this happen
    - skip: skip the subdirectory
    - warning: log a warning message
    - done: do nothing
 - rank: this is used to determine the priorities in reports.

### files
The table record information about each file. 
- file: file name
- folder: the subdirectory containing the file
- status: status of the file; see ??? for more details.


### file_status_lookup
A look up table for the status in files.
- status: status name
- description: description of the status


### filename_lookup
A look up between filename and new filename
- file: file name
- folder: folder name
- new_name: new file name

### phi_on_image
The table record any public health information (PHI) found a image
- file: file name where the PHI found
- folder: name of the folder containing the file
- text_id: id for the PHI text (multiple PHI text cuold be found on an image)
- phi_text: the original text found










