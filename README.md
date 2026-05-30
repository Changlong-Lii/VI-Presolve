## Online Supplement of:

# *Exploiting Variable Implications in Presolve for Mixed Integer Programming*

##### Wei-Kun Chen, Chang-Long Li, Zhao-Wei Wang, Yu-Hong Dai, Zi-Shuo Li, and Meng Lu

---

This online supplement provides a CSV file with detailed results of the computational experiments conducted for the paper *Exploiting Variable Implications in Presolve for Mixed Integer Programming*.

The experiments evaluated two presolve techniques for mixed integer programming (MIP): variable implication aggregation (`VIA`) and variable implication-aware linear constraint propagation (`VILCP`). Both techniques were implemented in the open-source MIP solver HiGHS 1.12.0. The default setting of HiGHS was used as the main baseline; standard clique merging and standard linear constraint propagation were already implemented in HiGHS, and were included in all experiments.

The experiments were executed with the serial version of HiGHS and a time limit of 7200 seconds for each run.

As test set, we used the MIPLIB 2017 benchmark test set. To address performance variability, all experiments were run on 240 benchmark problems with five different random seeds, and each problem-seed pair was treated as an independent observation.

All data provided in this repository represents observations where all settings considered in the corresponding experiment finished without error (e.g., numerical violations). Thus, for some problems fewer than five observations are available.

#### Repository organization

The repository is organized as follows:

* `summary.csv`: detailed per-observation computational results for all solver settings considered in the experiments.

#### Experiments

The following experiments were conducted:

* HiGHS default settings (`Default`) vs. HiGHS with variable implication aggregation (`VIA`)
* HiGHS default settings (`Default`) vs. HiGHS with variable implication-aware linear constraint propagation (`VILCP`)
* The state-of-the-art approach of Achterberg et al. (2013) (`Achterberg2013`) vs. variable implication-aware linear constraint propagation (`VILCP`)
* The state-of-the-art approach of Achterberg et al. (2013) (`Achterberg2013`) vs. variable implication-aware linear constraint propagation without the two enhancements (`VILCP'`)
* Variable implication-aware linear constraint propagation without the two enhancements (`VILCP'`) vs. variable implication-aware linear constraint propagation with the two enhancements (`VILCP`)
* HiGHS default settings (`Default`) vs. HiGHS with both proposed presolve techniques enabled (`All`)

#### Solver settings

All instance features, e.g., solving time, explored tree nodes, and model statistics, are given for each of the following setting:

* `Default`: HiGHS 1.12.0 with default settings.
* `VIA`: HiGHS 1.12.0 with the proposed variable implication aggregation.
* `VILCP`: HiGHS 1.12.0 with the proposed variable implication-aware linear constraint propagation.
* `Achterberg2013`: HiGHS 1.12.0 with the state-of-the approach of Achterberg et al. (2013).
* `VILCP'`: HiGHS 1.12.0 with the proposed variable implication-aware linear constraint propagation applied only to linear constraints, without the two enhancements.
* `All`: HiGHS 1.12.0 with both proposed presolve techniques enabled, i.e., `VIA` and `VILCP`.

#### CSV data details

The CSV file `summary.csv` contains the following columns:

* `ProblemName`: name of the MIPLIB 2017 problem.
* `Seed`: random seed used in the run.
* `T_s`: absolute solving time in seconds for setting `s`.
* `N_s`: absolute number of explored branch-and-bound tree nodes for setting `s`.
* `T_presolve_VIA`: CPU time in seconds spent in the proposed variable implication aggregation routine. This corresponds to `T_VIA` reported in the paper and is not indexed by setting `s`.
* `T_presolve_VILCP`: CPU time in seconds spent in the proposed variable implication-aware linear constraint propagation routine. This corresponds to `T_VILCP` reported in the paper and is not indexed by setting `s`.
* `Rows_s`: number of rows reported for setting `s`.
* `Cols_s`: number of columns reported for setting `s`.
* `Nnz_s`: number of nonzero coefficients in the constraint matrix reported for setting `s`.

Here, `s` can be one of the following settings:

* `Default`
* `VIA`
* `VILCP`
* `Achterberg2013`
* `VILCP'`
* `All`

#### Notes on aggregation

The CSV file provides per-observation raw data. The performance tables in the paper are computed from these observations using shifted geometric means, all with a shift of 1.

A setting is considered to solve an observation if it proves the instance within the time limit. Observations that reach the time limit are still included when at least one setting considered in the corresponding experiment solves them.
