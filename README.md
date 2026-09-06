# Ml-TCP-Flaky-Noise-Study
Replication package for the study on simulated flaky tests verdict noise in supervised ML-based TCP
This repository contains the replication materials for the master's thesis:

**Quantifying the Impact of Flaky Test Noise on Supervised Machine Learning-Based Test Case Prioritization in Continuous Integration Environments**

The study investigates how simulated flaky-test verdict noise in historical training data affects supervised machine learning-based test case prioritization (ML-TCP).

## Study Overview

The experiment was conducted using 24 open-source Java projects from the TCP-CI benchmark. 
The TCP-CI benchmark contains 25 open-source Java projects. One project, "Graylog2@graylog2-server", was excluded because its chronological evaluation partition contained no recorded test failures.

**The main experimental settings were:**
- 75/25 chronological training and evaluation split
- Nine simulated training-verdict noise levels: 0%, 5%, 10%, 15%, 20%, 25%, 30%, 40%, and 50%
- 30 fixed repetition seeds
- Four supervised techniques:
  - Random Forest
  - XGBoost
  - LightGBM
  - Gaussian Naive Bayes
- Three non-ML baselines:
  - Random
  - LatestFail
  - QTF-Avg
- APFDc as the primary effectiveness measure
- APFD as the secondary effectiveness measure

Noise was introduced only into the historical training verdicts. The evaluation verdicts and execution times were kept unchanged.

After verdict corruption, the 13 verdict-dependent REC features were recomputed from the condition-specific history, while the six verdict-independent REC features were preserved.

**Dataset:**
The experiment uses the TCP-CI benchmark introduced by Yaraghi et al. 

- [TCP-CI GitHub repository](https://github.com/Ahmadreza-SY/TCP-CI)
- [TCP-CI dataset on Zenodo](https://zenodo.org/records/6415365)


## Repository Structure

config/      Experiment configuration and repetition seeds
src/         Experiment and analysis source code
results/     Final results used for RQ1, RQ2, and RQ3
metadata/    Project information and supporting metadata
docs/        Additional replication notes








