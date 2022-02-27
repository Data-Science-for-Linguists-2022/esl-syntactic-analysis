# Progress Report

## February 15

Created GitHub repository. Already have general project idea, but needs further refinement. Have been reading SLA literature and resources provided by Dr. Alan Juffs (Intensive English Program document particularly useful; needs further investigation)

## February 27 (First Progress Report)

Downloaded master CSV file for PELIC dataset and began basic data processing and analysis (see `data-overview.ipynb`).
Analyzed distributions of L1 and proficiency level among the students in the dataset since those are the main parameters by which students will be grouped later on.

Also created a small sample of 100 entries of the PELIC dataset (`data_samples/pelic-sample.csv`) since the original is tens of thousands of entries long and therefore far too long to view in its entirety.

Was originally planning on using [LCA](https://aihaiyang.com/software/lca/) for later syntactic analysis, but will likely switch to [TAASCC](https://www.linguisticanalysistools.org/taassc.html) (at the suggestion of Dr. Naismith) since it provides indices for *many* more numerical measures of syntactic, clausal, and phrasal complexity than the former.
Some particular indices of interest include (but aren't limited to):
- Mean length of T-units
- Number of T-units per sentence
- Number of dependent clauses per T-unit
- Number of subordinating conjunctions per clause

The full spreadsheet(s) of available indices for TAASCC is available [here](https://drive.google.com/file/d/1ksJsRJakJrhFZD-_uLlLEpTpaGRqsOff/view).

### Sharing Plan

Given that the PELIC dataset from which all analyses for this project will be derived is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nc-nd/4.0/), whether the data and/or the analyses will be publicly shared will depend on whether they're considered to be a "derivative work".
Regardless, this project will likely also be published under a Creative Commons license, and attribution to the PELIC dataset should be stated as follows:

Juffs, A., Han, N-R., & Naismith, B. (2020). The University of Pittsburgh English Language Corpus (PELIC) [Data set]. http://doi.org/10.5281/zenodo.3991977