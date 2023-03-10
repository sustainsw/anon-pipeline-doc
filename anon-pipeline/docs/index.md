# Introduction
The anonymiser pipeline is program anonymise DICOM files based on Stanford's MIRC-CTP tool. It has following features:

- Deterministic (but anonymous) renaming of a folder of DICOM images (scans contained within subfolders).
- Easy installation of Mirc-Ctp using Docker.
- Record, monitor and summarization of anonymisation process, for both DICOM files and subfolders.
- Configuration and control on running of anonymisation, such as selecting sub-folders to process, problem handlings etc.
- Addtional search for public health information (PHI) on image using text detection and optical character recognition (OCR) models.
- The pipeline is tested using inhouse and public DICOM data, to ensure the pipepline not leaking PHI in tags of anonymised DICOM file.

