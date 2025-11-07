# IIITH_asignment
Forced Alignment with MFA on Google Colab

This repository contains the outputs and script for a forced alignment task performed using the Montreal Forced Aligner (MFA). The entire process was run in a Google Colab environment to manage dependencies.

Contents

/aligned: This directory contains the final .TextGrid alignment files for all audio segments.

MFA_Alignment_Script.ipynb: The Google Colab Notebook (.ipynb file) containing the full Python script used to run the alignment.

report.pdf: An analysis of the alignment accuracy, with examples.

Setup and Replication Steps

Here are the clear steps and example commands to replicate this alignment process using the provided notebook in Google Colab.

1. Install MFA in Colab

First, we need to install Miniconda in the Colab environment, as MFA runs on Conda.

# Download and install Miniconda
!wget -q [https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh](https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh)
!bash Miniconda3-latest-Linux-x86_64.sh -b -p /usr/local/miniconda3

# Add conda to the environment path
import os
os.environ['PATH'] = '/usr/local/miniconda3/bin:' + os.environ['PATH']

# Install the Montreal Forced Aligner
!/usr/local/miniconda3/bin/conda install -y -c conda-forge montreal-forced-aligner


2. Prepare the Dataset

This step involves uploading the raw data and formatting it into the flat structure that MFA requires (a directory containing all .wav and corresponding .lab files).

Upload Data: The script will prompt you to upload your dataset.zip file.

Run Prep Script: The notebook script automatically:

Finds the wav and transcripts folders.

Matches audio files (e.g., f2bjrlp1.wav) to transcript files (f2bjrlp1.txt).

Cleans the transcript text (removes punctuation, converts to uppercase).

Saves the cleaned text as a .lab file (e.g., f2bjrlp1.lab).

Copies both the .wav and new .lab files into a single directory: /content/corpus.

3. Download Alignment Models

Before aligning, you must download the pre-trained acoustic model and pronunciation dictionary. We used the standard US English models.

# Download the English (US) dictionary
!/usr/local/miniconda3/bin/mfa model download dictionary english_us_arpa

# Download the English (US) acoustic model
!/usr/local/miniconda3/bin/mfa model download acoustic english_us_arpa


4. Run the Alignment

This is the final command that tells MFA to align the corpus.

# Example command:
# mfa align <corpus_directory> <dictionary_path> <acoustic_model_path> <output_directory>
!/usr/local/miniconda3/bin/mfa align /content/corpus english_us_arpa english_us_arpa /content/aligned -v


This command takes the prepared /content/corpus directory, uses the english_us_arpa models, and outputs the final .TextGrid files into the /content/aligned directory.

To Inspect the Outputs

Install Praat: Download and install Praat (a free scientific software for speech analysis) for your operating system.

Open Files:

Open the Praat application.

Go to Open > Read from file...

Select one of the .wav audio files (you must have these locally) and its corresponding .TextGrid file from the /aligned directory.

Select both objects in the Praat Objects window and click View & Edit.
