# Installation and dataset setup

FeatKT was developed in Google Colab. The notebook downloads the Python packages and `pykt-toolkit` code during setup, and is designed in a way where it reads the dataset and checkpoints from Google Drive. You only need to download the dataset and set its Google Drive location in the notebook's configuration cell.

## 1. Download the dataset

1. Open the [Riiid Answer Correctness Prediction data page](https://www.kaggle.com/competitions/riiid-test-answer-prediction/data)
2. Sign in to Kaggle
3. Download the competition data
4. Extract the downloaded files

The notebook requires these files:

- `train.csv`
- `questions.csv`

## 2. Upload the files to Google Drive

Create a folder in Google Drive. For example:

```text
My Drive/riiid-test-answer-prediction/
```

Upload `train.csv` and `questions.csv` to that folder.

The folder should look like this:

```text
riiid-test-answer-prediction/
├── train.csv
└── questions.csv
```

## 3. Set the dataset path

Open `featkt_notebook.ipynb`. In the configuration cell, set `DATA_DIR` to the Google Drive folder that contains the two files.

```python
DATA_DIR = "/content/drive/My Drive/riiid-test-answer-prediction"
```

Change this path if you used a different folder name or location.

## 4. Configure the experiment

The following values are in the notebook configuration cell:

```python
N_USERS = 5000
SEED = 42
RATIOS = [0.2, 0.4, 0.6, 0.8, 0.9]
CV_FOLDS = [0, 1, 2, 3, 4]
```

- `N_USERS` is the number of students sampled from the full dataset. The default experiment uses 5,000 students.
- `SEED` sets the random seed used when selecting students. Keeping it at `42` reproduces the same sample.
- `RATIOS` lists the observed prefix ratios used for evaluation. For example, `0.4` means the model sees the first 40% of a student's history and predicts the remaining 60%.
- `CV_FOLDS` lists the training folds used for cross-validation of the neural baseline models.

## 5. Run the notebook

Run the cells from the top. The notebook installs the required packages, prepares the data, trains the models, and saves cached files in the dataset folder.

## Notes

- The experiment uses 5,000 sampled students
- The Riiid dataset files and saved checkpoints take up a few gigabytes, make sure your Google Drive has enough free space
- The notebook is configured for Google Colab and uses a GPU when one is available
