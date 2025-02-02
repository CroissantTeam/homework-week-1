# Homework Week 1: OCR App

## Introduction

This is an OCR app that could read all document and images and extract the texts and their corresponding locations in a json file. This app is helpful for information extraction to digital formats, making them easier to store, search, and manage. This app can support different input file types, such as: ``.png``, ``.heic``, ``.tiff``, ``.pdf``, ``.doc``, ``.docx``.

This app utilizes tech stacks:
- **Read images/docs**: mimetypes, pillow, pillow-heif, PyMuPDF
- **Preprocess images**: numpy, opencv-python
- **OCR**: [pytesseract](https://pypi.org/project/pytesseract/)
- **Save and store outputs**: json, pydrive

## App design


![App design image](docs/code_design.jpg)

### Workflow
1. **Image read and preprocessing**:
- The system accepts various file types (png, heic, tiff, pdf, doc) as input images.
- The ``InputHandler`` reads the file and delegates processing to the appropriate file handler based on the file type. The selected handler processes the file and converts it into an ``OcrImages`` object containing preprocessed image data.
- ``DataPreprocess`` resizes and preprocesses the images to prepare them for OCR.

2. **OCR Model**:
- The ``OCR`` class uses the preprocessed images to extract text lines and generate an ``OcrResults`` object.

3. **Process Output**:
- OutputHandler processes the ``OcrResults`` object from the previous step.
- The ``JsonProcessor`` and ``OutputImageProcessor`` handle converting the OCR results to JSON and PDF formats, respectively.

4. **Uploading**:
- The processed output (JSON and/or PDF) is uploaded to a drive using the ``drive_upload`` function.

## Set up

### Clone this repository
```bash
git clone https://github.com/Croissant-Team-Cinnamon-Bootcamp-2024/homework-week-1.git
cd homework-week-1
```

### Install Dependencies

For Linux, run
```
sudo apt-get install tesseract-ocr libreoffice
pip install -U .
```

For MacOS, run
```
brew install tesseract libreoffice
pip install -U .
```

For Windows, follow the below steps
- Download Tesseract installer for Windows: https://github.com/UB-Mannheim/tesseract/wiki
- Add the path to the directory of Tesseract folder (normally is: ```C:\Program Files\Tesseract-OCR```) to the System Environment Variables (edit the Path variable, click on **New** button and paste the path above).
- Run ```pip install -U .```
- Microsoft Word is expected to be installed on the Window's OS system


## Run OCR script

### Get Google Drive Secret file & Folder ID

1. Follow [this instruction](https://pythonhosted.org/PyDrive/quickstart.html) to get Google Drive Secret file (rename to `client_secrets.json`).
2. Create new `secrets/` folder.
3. Move the secret file to `secrets/` folder.
4. Login to your Google Drive Account
5. Go to the folder you want to save the output to
6. Get the GDrive Folder ID by follow the image below

![alt text](docs/gdrive_folder_id.png)

### Running scripts

For Linux and MacOS, run
```bash
# Skip this step if you do not want to upload to GGDrive
export GGDRIVE_FOLDER_ID=<Google Drive Folder ID>
# Run your own file by changing the path after -f with default secret key, ocr result output in "/secrets" and "/results", respectively.
python scripts/run.py -f assets/ocr-test.pdf --secrets-dir secrets/ --results-dir results/
```

For Windows, run
```pwsh
# Skip this step if you do not want to upload to GGDrive
set GGDRIVE_FOLDER_ID=<Google Drive Folder ID>
# Run your own file by changing the path after -f with default secret key, ocr result output in "/secrets" and "/results", respectively.
python scripts/run.py -f assets/ocr-test.pdf --secrets-dir secrets/ --results-dir results/
```
