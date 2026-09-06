# Replication Guide

This repository contains the experiment notebooks, configuration files, metadata, and final result files used in our thesis study on flaky-test noise and machine-learning-based test case prioritization.
The experiments were carried out mainly in Google Colab using the TCP-CI dataset. Because the full experiment was large, the execution was divided across several notebooks and, for some projects, across separate worker notebooks for different seed ranges.

## 1. Dataset

The experiments use the TCP-CI dataset.
The dataset is not redistributed in this repository. It should be downloaded separately from the original TCP-CI source and stored in a location that can be accessed by the notebooks.
The notebooks were originally executed from Google Colab with Google Drive mounted. Therefore, several notebooks contain paths beginning with:

`/content/drive/MyDrive/Thesis_Experiment/`

If the experiment is reproduced in another environment, these paths need to be changed to match the local dataset and result directories.

## 2. Python Environment

The main Python dependencies are listed in the root `requirements.txt` file.
They can be installed using:

`pip install -r requirements.txt`

The software versions used during the final experiment are also recorded in:

`metadata/software_versions.csv`

## 3. Experiment Configuration

The main experiment settings are provided in:

`config/experiment_config.json`

The study uses:

- 24 included Java projects
- a chronological 75% training and 25% evaluation split
- simulated training-verdict noise at 0%, 5%, 10%, 15%, 20%, 25%, 30%, 40%, and 50%
- 30 repetition seeds
- Random Forest, XGBoost, LightGBM, and Gaussian Naive Bayes
- Random, LatestFail, and QTF-Avg as non-ML baselines
- APFDc as the primary evaluation metric
- APFD as the secondary evaluation metric

The repetition seeds used in the experiment are listed in:

`config/seeds.txt`

The list of candidate and included projects is available in:

`metadata/project_list.csv`

## 4. Running the Project Experiments

The original project-level experiment notebooks are stored in:

`src/notebooks/project_runs/`

These notebooks contain the main experiment execution for the 24 included projects.
The experiments were executed in batches rather than through one single notebook. This was mainly done because of the size of the experiment and the runtime and memory limitations of Google Colab.
The project notebooks perform the main steps of the experiment, including:

1. loading the TCP-CI project data;
2. creating the chronological training and evaluation partitions;
3. applying simulated verdict noise only to the training data;
4. recomputing verdict-dependent historical features;
5. training the supervised learning techniques;
6. generating test rankings;
7. evaluating the rankings using APFDc and APFD;
8. storing project-level outputs for later analysis.

## 5. Worker Notebooks

Some of the later projects were divided into separate worker notebooks to reduce execution time and make the seed-based runs easier to manage.
These notebooks are stored in:

`src/notebooks/worker_runs/`

The worker notebooks execute subsets of the 30 repetition seeds and produce partial outputs that are later combined by the corresponding project-level workflow.
They are part of the original experiment execution history and should be used together with the related project notebook if the full experiment is reproduced.

## 6. Global Analysis

The main cross-project statistical analysis notebook is:

`src/notebooks/analysis/Thesis_Global_Analysis.ipynb`

This notebook contains the final RQ1 and RQ3 analyses used in the thesis.
The RQ2 part of this notebook was produced before the final LatestFail correction. It is therefore retained only as part of the experiment history and should not be treated as the final RQ2 result.

## 7. Final LatestFail Correction for RQ2

The final corrected LatestFail analysis is stored in:

`src/notebooks/correction/LatestFail_correction&Validation.ipynb`

This notebook corrects the handling of test cases with no previously observed failure.
In the final implementation, tests with a previous failure are prioritized according to recency, while tests with no previous failure receive the lowest LatestFail priority.
The correction affected 14 projects, while the remaining 10 projects were unchanged.
The corrected outputs were then combined across all 24 projects and used as the final RQ2 results in the thesis.
For RQ2, this correction notebook and the files in `results/rq2/` should be treated as the authoritative final results.

## 8. Final Result Files

The final compact result files used in the thesis are stored under:

`results/`

The folders are organized as:

- `results/rq1/` – final noisy-versus-clean comparison results
- `results/rq2/` – final corrected crossover and LatestFail results
- `results/rq3/` – final robustness comparison results

The result folders contain the final statistical tables, summaries, validation information, and supporting files used to produce the thesis findings.

## 9. Reproduction Order

A full reproduction can be carried out in the following order:

1. download and prepare the TCP-CI dataset;
2. install the Python dependencies;
3. update the dataset and output paths in the notebooks;
4. run the project-level notebooks;
5. run the worker notebooks where required;
6. collect the project-level outputs;
7. run the global analysis notebook for RQ1 and RQ3;
8. run the LatestFail correction notebook for the final RQ2 results;
9. compare the generated outputs with the files in the `results/` directory.

Because the original experiment was executed incrementally in Google Colab, the notebooks are provided mainly as the original experiment record rather than as one fully automated end-to-end pipeline.

