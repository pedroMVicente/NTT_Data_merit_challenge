# Authors
Pedro Vicente
ist1109852
pedro.costa.vicente@tecnico.ulisboa.pt
Instituto Superior Técnico

Ema Ferrão
ist1109247
emassferrao@tecnico.ulisboa.pt
Instituto Superior Técnico

# TF-IDF Feature Extraction - Setup Guide

This guide will help you set up the virtual environment and install all necessary dependencies for the TF-IDF feature extraction project.

## Prerequisites

- Python 3.7 or higher
- pip (Python package installer)

## Setup Instructions

### 1. Create a Virtual Environment

#### On Windows:
```bash
# Navigate to your project directory
cd path/to/your/project

# Create virtual environment
python -m venv venv

# Activate virtual environment
venv\Scripts\activate
```

#### On macOS/Linux:
```bash
# Navigate to your project directory
cd path/to/your/project

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate
```

### 2. Install Dependencies

Once the virtual environment is activated, install the required packages:

```bash
pip install -r requirements.txt

python -m spacy download pt_core_news_lg
```

### 3. Verify Installation

You can verify that the packages are installed correctly by running:

```bash
pip list
```

You should see scikit-learn and numpy in the list of installed packages.

### All done

After installing the dependencies, you should be able to use the virtual enviroment in order to run the jupiter notebook.

## Deactivating the Virtual Environment

When you're done working, you can deactivate the virtual environment:

```bash
deactivate
```

## Troubleshooting

### Issue: `pip` command not found
- Make sure you have activated the virtual environment
- On Windows, use `python -m pip` instead of `pip`
- On macOS/Linux, use `python3 -m pip` instead of `pip`

### Issue: Permission denied when installing packages
- Make sure the virtual environment is activated
- Do not use `sudo` with pip when working in a virtual environment

### Issue: Virtual environment not activating on Windows
- Try using PowerShell instead of Command Prompt
- If you get an execution policy error, run:
  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```

## Project Structure

```
project/
│
├── venv/                   # Virtual environment (created by you)
├── requirements.txt        # Python dependencies
├── code.ipynb              # Main notebook script
└── README.md               # This file
```