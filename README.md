# cnn-rcnn
kaggle eeg


### Description

Seizure Prediction

- [Competition page at Kaggle](https://www.kaggle.com/c/melbourne-university-seizure-prediction)
- This is a proof-of-concept for applying deep learning techniques to EEG data converted into spectrograms.

### Usage

These steps take about 4 hours on a system with 4 processors, a single GPU and a spinning hard-disk. **Tested only on Ubuntu**.

1. Download and install [neon](https://github.com/NervanaSystems/neon) **1.6.0**

    ```
    git clone https://github.com/NervanaSystems/neon.git
    cd neon
    git checkout v1.6.0
    make
    source .venv/bin/activate
    ```
2. Verify neon installation

    Make sure that this command does not result in any errors:
    ```
    ./examples/cifar10_msra.py -e1
    ```

3. Install prerequisites

    ```
    pip install scipy sklearn scikits.audiolab
    ```
4. Download the data files from [Kaggle](https://www.kaggle.com/c/melbourne-university-seizure-prediction/data):

    a. Save all files to a directory (referred to as /path/to/data below) and unzip the .zip files.
    b. Run the conversion script to move data around and exclude bad data.

5. Clone this repository

    ```
    git clone https://github.com/bigsnarfdude/cnn-rcnn.git
    cd cnn-rcnn
    ```
6. Train models and generate predictions

    ```
    ./run.sh /path/to/data /path/to/output 2>&1 | tee run.log
    ```
    where /path/to/data must contain the data subdirectories (train_1, train_2 etc.) as well as sample_submission.csv
    and /path/to/output is a new directory that will be created to store intermediate output files.

7. Evaluate predictions

    Submit subm.csv to [Kaggle](https://www.kaggle.com/c/melbourne-university-seizure-prediction/submissions/attach)

### Notes
- The model needs 4GB of device memory.
- The first run takes longer due to conversion of .mat files into .wav files.
- Conversion of data to spectrograms is performed on the fly by neon.

.
