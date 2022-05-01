# esl-syntactic-analysis

Tianyi Zheng, tiz65@pitt.edu, May 1, 2022

For fellow LING 1340 students, here's a link to my [guestbook](https://github.com/Data-Science-for-Linguists-2022/Class-Lounge/blob/main/guestbooks/guestbook_tianyi.md).

This final project for LING 1340 (Data Science for Linguists) will analyze written data from ESL learners and identify differences in syntax of different ESL learners based on their native language and proficiency level.
The goal is to determine how quantitative measures of syntactic complexity differ between more advanced learners and less advanced learners and to determine whether they differ between learners based on their L1.

The project processes and analyzes written ESL samples from the [PELIC dataset](https://github.com/ELI-Data-Mining-Group/PELIC-dataset) (Juffs, Han, & Naismith, 2020) using the TAASSC program (Kyle, 2006) with its SCA features (Lu, 2010).

For an overview of the goals of project, see `project-plan.md`.
For an overview of the development of the project, see `progress-report.md`.
The Jupyter notebooks, which contain the data cleaning and analysis, should be approached in the following order:

1) [`data-overview.ipynb`](https://github.com/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/data-overview.ipynb) ([nbviewer version](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/data-overview.ipynb))

2) [`taassc-prep.ipynb`](https://github.com/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/taassc-prep.ipynb) ([nbviewer version](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/taassc-prep.ipynb))

3) [`prepare-final-data.ipynb`](https://github.com/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/prepare-final-data.ipynb) ([nbviewer version](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/prepare-final-data.ipynb))

4) [`final-analysis.ipynb`](https://github.com/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/taassc-prep.ipynb) ([nbviewer version](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/final-analysis.ipynb))

Data samples for both PELIC and TAASSC used in the analysis can be found under `data_samples/`.

## Repo Contents

```
./
|--data_samples/
|  |--pelic-sample.csv          # First 100 rows of PELIC dataset
|  |--taassc.csv                # Clause complexity measures for pelic-sample.csv
|  |--taassc_sca.csv            # SCA complexity measures for pelic-sample.csv
|--data-overview.ipynb          # Initial exploratory data analysis
|--final-analysis.ipynb         # Final data visualization and analysiis
|--LICENSE.md                   # License for project
|--prepare-final-data.ipynb     # Preparation of final dataset
|--presentation.pdf             # Project presentation
|--progress-report.md           # Progress reports for project
|--project-plan.md              # Initial description of project plans
|--README.md                    # This README file
|--taassc-prep.ipymb            # Exploratory data analysis of TAASSC output
```

## Glossary

- ESL: English as a Second Language

- L1: First language

- PELIC: The Pitt English Language Institute Corpus (PELIC) is a dataset of written samples from ESL students at the English Language Institute at the University of Pittsburgh (Pitt).

- TAASSC: The Tool for the Automatic Analysis of Syntactic Sophistication and Complexity (TAASSC) is a program developed by K. Kyle (see references) that calculates numerical measures of syntactic complexity.

- T-unit: A T-unit is a generalization of a sentence. More specifically, a T-unit consists of an independent clause and all of its associated dependent clauses:
  - "Because the sentence only has one independent clause, it has one T-unit." has one T-unit.
  - "This is a compound sentence because it has two independent clauses; as a result, it has two T-units." has two T-units.

- SCA: The Syntactic Complexity Analyzer (SCA) is a program developed by X. Lu (see references) that calculates numerical measures of syntactic complexity.
TAASSC builds upon SCA by including all of the measures from SCA as well as many new measures.

<div style="text-align: center">
  <table>
    <thead>
      <tr>
        <th colspan=3>Proficiency Level Codes</th>
      </tr>
      <tr>
        <th><code>level_id</code></th>
        <th>Level Description</th>
        <th>CEFR Level</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>2</td>
        <td>Pre-Intermediate</td>
        <td>A2 - B1</td>
      </tr>
      <tr>
        <td>3</td>
        <td>Intermediate</td>
        <td>B1</td>
      </tr>
      <tr>
        <td>4</td>
        <td>Upper-Intermediate</td>
        <td>B1 - B2</td>
      </tr>
      <tr>
        <td>5</td>
        <td>Advanced</td>
        <td>B2 - C1</td>
      </tr>
    </tbody>
  </table>
</div>

## References

Juffs, A., Han, N-R., & Naismith, B. (2020). The University of Pittsburgh English Language Corpus (PELIC) [Data set]. http://doi.org/10.5281/zenodo.3991977

Kyle, K. (2006). *Measuring syntactic development in L2 writing: Fine grained indices of syntactic complexity and usage-based indices of syntactic sophistication*. (Doctoral dissertation).

Lu, X. (2010). Automatic analysis of syntactic complexity in second language writing. *International Journal of Corpus Linguistics*, 15(4):474-496.

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This project is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.
