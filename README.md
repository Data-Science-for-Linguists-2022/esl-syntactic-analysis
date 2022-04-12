# esl-syntactic-analysis

Tianyi Zheng, tiz65@pitt.edu

This project will analyze written data from ESL learners and identify differences in syntax of different ESL learners based on their native language and proficiency level.
The goal is to determine how quantitative measures of syntactic complexity differ between more advanced learners and less advanced learners and to determine whether they differ between learners based on their L1.

## Repo Contents

```
./
|--data_samples/
|  |--pelic-sample.csv          # First 100 rows of PELIC dataset
|  |--taassc.csv                # Clause complexity measures for pelic-sample.csv
|  |--taassc_sca.csv            # SCA complexity measures for pelic-sample.csv
|--data-overview.ipynb          # Initial exploratory data analysis
|--LICENSE.md                   # License for project
|--prepare-final-data.ipynb     # Preparation of final dataset
|--progress-report.md           # Progress reports for project
|--project-plan.md              # Initial description of project plans
|--README.md                    # This README file
|--taassc-prep.ipymb            # Exploratory data analysis of TAASSC output
```

## Glossary

- TAASSC: The Tool for the Automatic Analysis of Syntactic Sophistication and Complexity (TAASSC) is a program that calculates numerical measures of syntactic complexity.

- T-unit: A T-unit is a generalization of a sentence. More specifically, a T-unit consists of an independent clause and all of its associated dependent clauses:
  - "Because the sentence only has one independent clause, it has one T-unit." has one T-unit.
  - "This is a compound sentence because it has two independent clauses; as a result, it has two T-units." has two T-units.

## References

Juffs, A., Han, N-R., & Naismith, B. (2020). The University of Pittsburgh English Language Corpus (PELIC) [Data set]. http://doi.org/10.5281/zenodo.3991977

Kyle, K. (2006). *Measuring syntactic development in L2 writing: Fine grained indices of syntactic complexity and usage-based indices of syntactic sophistication*. (Doctoral dissertation).

Lu, X. (2010). Automatic analysis of syntactic complexity in second language writing. International Journal of Corpus Linguistics, 15(4):474-496.

## License

TBD
