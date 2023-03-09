# Get Start


## Installation

### Enviroment
- Linux Unbuntu 22.04

### Pre-requriments
- Github
- Docker
- Python 3.10


### Setup
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

### Quick Run
Try the following code for a quick run with our example data:
```
./anon_pipeline.py example_input/ -p my_results
```
Here, `my_results` will be created containing the anonymised files.

<p>

To anonymise you own data, you can crate a folder with the following structure
```
<input_folder>/
    <accession number 1>/
        <DICOM file 1>
        <DICOM file 2>
    <accession number 2>/
        <DICOM file 1>
        <DICOM file 2>    
    ...

```
and run the following code
```
./anon_pipeline.py <path/to/input_folder> -p <path/to/output_folder>
```
Please note that the input and output folder don't have to be saved in the root folder.






