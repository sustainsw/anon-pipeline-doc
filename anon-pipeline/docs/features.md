
# Features

## Deterministic renaming of folder names

Recall the structure of input folder
```
<input_folder>/
    <accession number 1>/
        <DICOM file 1>
        <DICOM file 2>
    <accession number 2>/
        <DICOM file 1>
        <DICOM file 2>    

```
The anonymisation rename the subfolder and DICOM files in output. 

```
<output_folder>/
    <pseudo folder name 1>/
        001.dcm
        002.dcm
    <pseudo folder name 2>/
        001.dcm
        002.dcm  

```
It renames subfolder containing a particular study:
- Patient ID: 10 char hex
- Accession number: 12 char hex
An adjustable salt is used to ensure additional anonymisation, configured in `SALT` in `config.py`. 
See module [id_generatorpy](development_details.md#id_generatorpy).

All DICOM files are sequentially renamed within each subdirectory

**Please note:** It's recommended to use accession number as subfolder name so that the program can efficiently trace which of them has been processed.


## Public health information (PHI) searching in anonymised DICOM
The program search for PHI in pixel (image) data and in text of tag values in DICOM file. See [anon_phi_examiner](development_details.md#anon_phi_examiner).

The feature depends on two modules:
- `ocdr`: text detection and optical character recognition. See [ocdr](development_details.md#ocdr).
- `phi_text_examiner`: checking if a given piece of text contain public health information (PHI) in a DICOM file, by referring to a series of tags. See [phi_text_examiner](development_details.md#phi_text_examiner).




## Recording anonymisation process
The program trace the status of every DICOM file and its directory in anonymisation process, and record them in a sqlite database. See [database](development_details.md#database)



