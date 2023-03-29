# Introduction
The anonymiser pipeline is program anonymising DICOM files based on [RSNA Clinical Trials Processor](https://mircwiki.rsna.org/index.php?title=MIRC_CTP). It has following features:

- Deterministic (but anonymous) renaming of a folder of DICOM images (scans contained within sub-folders).
- Easy installation of the Mirc-Ctp tool using Docker.
- Record, monitor and summarization of anonymisation process, for both DICOM files and folders.
- Configuration and control on running of anonymisation, such as selecting folders to process, problem handlings etc.
- Additional search for protected health information (PHI) on image using text detection and optical character recognition (OCR) models.
- The pipeline is tested using in-house and public DICOM data, to ensure the pipeline not leaking PHI in anonymised DICOM file.

