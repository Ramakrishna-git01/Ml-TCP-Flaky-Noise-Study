# Correction and Validation

This directory contains the final correction and validation of the LatestFail baseline used for RQ2.

The notebook `LatestFail_correction&Validation.ipynb` corrects the handling of tests with no previously observed failure. Such tests are assigned the lowest LatestFail priority.

The correction was applied to the affected projects and then consolidated with the unchanged legacy projects to produce the final 24-project LatestFail results used in the thesis.

This notebook is the authoritative source for the final RQ2 LatestFail results.
