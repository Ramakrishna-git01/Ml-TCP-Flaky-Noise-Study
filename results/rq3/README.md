# RQ3 Results

This directory contains the final results used for the comparative robustness analysis of the four supervised techniques.

`rq3_friedman_holm_omnibus_results.csv` contains the Friedman tests, Holm-adjusted p-values, and Kendall's W values across the tested noise levels.

`rq3_conditional_nemenyi_posthoc.csv` contains the pairwise Nemenyi comparisons performed where the corresponding Friedman test remained significant after Holm correction.

`rq3_average_ranks_by_noise.csv` contains the project-level average ranks of the four supervised techniques.

`rq3_primary_robustness_synthesis.csv` summarizes the predefined APFDc robustness criterion, including the 30%-50% high-noise region.

`rq3_primary_winner_nemenyi_at_50pct.csv` contains the 50% APFDc pairwise comparisons for the robustness winner.

The remaining files provide supporting clean-relative and best-technique summaries used in the RQ3 analysis.
