

# Deterministic renaming of folder names

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
The anonymisation rename the subfolder and DICOM files.

```
<output_folder>/
    <pseudo folder name 1>/
        001.dcm
        002.dcm
    <pseudo folder name 2>/
        001.dcm
        002.dcm  

```
Rename subfolder containing a particular study:
- Patient ID: 10 char hex
- Accession number: 12 char hex
An adjustable salt is used to ensure additional anonymisation.

**Please note:** It's recommanded to use accession number as subfolder name so that the program can efficiently trace which of them has been processed.


All DICOM files are sequentially renamed within each subdirectory

