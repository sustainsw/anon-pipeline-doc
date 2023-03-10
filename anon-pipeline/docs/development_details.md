
# Developer installation

After the installation of anonymisation pipeline, install additional Linux libararies for testing. 
```
./dev-tools/setup-dev.sh
```

Install additional python packages for testing
```
pip install -r /dev-tools/requirements-dev.txt
```




# Logs
logs and records of an anonymisation process are saved in folder `log/`.


## events.log
This file logs all the relavent information, warning and errors in an anonymisation process. Check this file for details about running of anonymise pipeline.

## mirc-ctp.log
This file logs all the outputs from mirc-ctp tool. Check this file for details about running of mirc-ctp tool.


## prog_recorder.db
This is an sqlite database tracing the status of every DICOM file and its directory in anonymisation process. See [database](development_details.md#database) for more details about the tables in the database.



# modules
The program is consist of following modules/scripts. 

### anon_pipeline.py
The `AnonPipeline` class in the module run the complete anonymisation process. Member function `anonymise` can be used for anonymisation.

### anon_recorder.py
The module records status of files and sub-directory in anonymisation process. The information is stored into a splite database whose default path is `log/prog_recorder.db`.

### anon_phi_examiner.py
The module

### anon_summary.py
The module performs anonymisation summary as in [anonymisation summary](getting_start.md#anonymisation-summary).

### id_generator.py
The module generate pseudo id for accession number and patient numbers.

### ocdr.py
The module is for text dectection and optical character recognition. Function `text_detection_and_recognition` detect text in given image using EAST model of OpenCV and recognise characters on the image using Tesseract.

### phi_text_examiner.py
The module check if a given piece of text contain public health information (PHI) in a DICOM file, by comparing the tags with a series of tags of the DICOM (eg: patient name). 
- See function `check_phi_in_text`
- The tags for reference are configured in `PHI_TAGS_CHECK_LIST` variable in config.py.
- The tags are classified into different types where different methods for searching PHI are used accordingly.

### conig.py
The script contains all the configurations for all above modules. It would be copied from `template/config_template.py` when the program is setup in the first time.



# Test
Tests are in folder `test`. `Pytest` should be used to run these tests, whose configuration file is in `pytest.ini`. See docstring for details of each test.


# database
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
- process: process status (eg: empty folder, some files corrupted). see `FOLDER_STATUS` in `config.py` for more details of the categories.
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
- status: status of the file; see ?? for more details.


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










