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
- a copy of file config.py should have been createed. Update the `SALT` variable in the file to desired value. (see [features](features.md#deterministic-renaming-of-folder-names) for detail about salt).
If the file is not created automatically, it can be copied manually from `templates/config_template.py` to the root folder (`anon-pipeline-set`).

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
**Please note** that the input and output folder don't have to be saved in the root folder.



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


