# Final Report

###### Tianyi Zheng, tiz65@pitt.edu, May 1, 2022

### Table of Contents
- [Introduction](#Introduction)
- [Dataset](#Dataset)
- [Syntactic Measures](#Syntactic-Measures)
- [References](#References)
- [Computation](#Computation)
- [Analysis](#Analysis)
- [Moving Forward](#Moving-Forward)

## Introduction

The goal of this project was to analyze the syntactic complexity of English as a Second Language (ESL) writing.
More specifically, I had hoped to analyze various numerical measures of syntactic complexity and determine whether they varied between learners based on native language and proficiency level.
Ultimately I was semi-successful in achieving this goal, as I did reach some statistically significant conclusions, albeit with many reservations.
There is still much that can be improved or redone with this project, and my ideas for how one may continue or improve upon my work with this project will be included at the end of this report.

## Dataset

For this project I decided to work with the [Pitt English Language Institute Corpus (PELIC) dataset](https://github.com/ELI-Data-Mining-Group/PELIC-dataset) (Juffs, Han, & Naismith, 2020), which is a longitudinal corpus of writing samples from ESL students at Pitt's English Language Institute.
The corpus is comprised of contributions from students of various native language (L1) backgrounds and proficiency levels, which gives me the opportunity to study how these students' writing samples differ in terms of their syntax by calculating various syntactic measures and performing statistical tests to determine whether there are any statistically significant trends.

## Syntactic Measures

To calculate numerical measures of syntax, I used the [Tool for the Automatic Analysis of Syntactic Sophistication and Complexity (TAASSC)](https://www.linguisticanalysistools.org/taassc.html) (Kyle, 2006) to, as its name suggests, automatically calculate the numerical measures of syntax that I selected for this project (details of which will be discussed below).
I also used TAASSC's Syntactic Complexity Analysis (SCA) (Lu, 2010) features, as in developing TAASSC Kyle builds upon previous work by Lu.


I ultimately settled on the following 6 measures of syntactic complexity:

1) Number of T-units per sentence

2) Mean length of T-units

3) Number of clauses per T-unit

4) Mean length of clauses

5) Number of prepositions per clause

6) Number of subordinating conjunctions per clause

Note that the first 3 measures are defined in terms of T-units.
A T-unit is a definition of a complete thought in language similar to a sentence.
More specifically, a T-unit is defined to be an independent clause along with all of its associated dependent clauses.
Therefore, most sentences consist of exactly 1 T-unit, while compound sentences (which by definition consist of multiple independent clauses) consist of multiple T-units.

I settled on the first 4 measures as a way to measure writing length, as one may reasonably assume that a more proficient writer would be more capable of writing more on a topic than a less proficient one.
For example, a proficient writer may be expected to write longer sentences and utilize complex sentence structures, both of which would be reflected in the counts and mean lengths of T-units and clauses.
In fact, Kyle 2020 cites past research on the topic that demonstrate positive relationships between mean length of T-units and writing proficiency and mean length of clauses and writing proficiency.
I settled on the last 2 measures as a way to measure writing style and familiarity with certain syntactic structures in writing.
For the purposes of this project, counting the number of prepositions and subordinating conjunctions is simply a proxy for analyzing the frequency of prepositional phrases and subordinate clauses.
I chose these structures because I believe that they're very frequently used by native speakers in both speech and writing and therefore comfortable usage of these structures in writing signals a relatively high level of proficiency.

Kyle 2020 provides details on how exactly TAASSC calculates its syntactic measures.
As one would expect, TAASSC first must tag and parse the provided writing sample, or more specifically part-of-speech tagging, constituency parsing, and dependency parsing.
The SCA portion of TAASSC specifically, developed by Lu, uses the Stanford parser to generate parse trees for a writing sample, which are then used to determine the counts of certain syntactical structures.
Once structures such as sentences, T-units, clauses, and phrases have been identified as a result of the constituency and dependency parsing, the numerical measures can be calculated.
For instance, the number of T-units per sentence is simply the total number of T-units in the sample divided by the total number of sentences in the sample.
Likewise, the mean length of T-units is simply the total number of words in the sample divided by the total number of T-units in the sample.

I had originally planned on investigating a 7th syntactic measure, number of discourse markers, but I ended up scrapping the idea because TAASSC was unable to find any discourse markers in any of the student texts.
Kyle 2020 does not explicitly state what is considered a discourse marker (such as whether only spoken, conversational discourse markers are counted), but judging by the example provided, "Well, I like pizza", I suspect that it may only refer to conversational discourse markers.

## Computation

My first step in the computation process is exploratory data analysis of the PELIC dataset, which I performed in [data-overview.ipynb](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/data-overview.ipynb).
This portion of the project was relatively simple as I just generated some basic statistics about the dataset and visualized them using some plots to get a better idea of the distribution of the data.
It was in this portion of the project that I learned that the distribution of L1s in the dataset was highly skewed, with the dataset being heavily dominated by Arabic, Chinese, and Korean speakers; this fact would come in handy for me later in the project when I stratify and sample from the dataset.
I also generated a small sample of the dataset (100 entries) to be used for experimentation in the next step of the project.

After my initial exploratory data analysis, my next step was to prepare the writing samples for TAASSC to generate their syntactactic measures, which I performed in [taassc-prep.ipynb](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/taassc-prep.ipynb).
Before attempting to process the entire dataset using TAASSC, I first experimented with TAASSC by having it generate syntactic measures for the small sample of 100 entries from [data-overview.ipynb](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/data-overview.ipynb).
It was in this portion of the project, while trying to process samples of the dataset of varying sizes using TAASSC, that I realized that TAASSC was incredibly inefficient both in terms of runtime and memory.
Furthermore, I realized that TAASSC was also somewhat sensitive to quirks of non-native writing, specifically to things such as irregular punctuation and sentence fragments.
This became particularly obvious when I visualized the TAASSC results in [taassc-prep.ipynb#TAASSC-Processing](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/taassc-prep.ipynb#TAASSC-Processing) and spotted many "outliers" that were in actuality essays that TAASSC struggled to process correctly.

There were a couple potential remedies to these issues that I'd considered but ultimately decided against implementing.
Regarding the issue of slow processing time, I've considered delegating the TAASSC processing pipeline to the Center for Research Computing (CRC)'s cloud computing resources, but this was something that I've never managed to figure out how to make work.
In particular, it doesn't appear that the Python code for TAASSC was designed to be run independently of the provided GUI, at least according to the documentation that I've been able to find—even the version of TAASSC for Python 2.7 apparently opens the GUI upon running the script.
Thus, I'm not sure how I'd be able to get that working with the CRC's CLI, though it is certainly an interesting possibility to keep in mind.
Regarding the issue of accuracy, there is actually an [updated version of TAASSC on GitHub](https://github.com/kristopherkyle/TAASSC), but unfortunately I am afraid that it might not actually be complete (if the "In Progress" comment in the source code is to be of any indication).
The repository also states that this updated version of TAASSC was going to become a Python package sometime in 2021, but as far as I'm aware no such package yet exists.
If development of this updated version of TAASSC resumes soon, then I believe that it could show real promise of remedying some of the issues that I've run into during my computation process.

With all of these points in mind, I proceeded to generate my final dataset of syntactic measures for my final data analysis in [prepare-final-data.ipynb](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/prepare-final-data.ipynb).
Noting that the distribution of L1s was incredibly skewed and that I must significantly limit the size of my dataset, I decided to stratify and sample essays from the PELIC dataset; more specifically, I filtered for the most prevalent L1s and sampled 10 students from each combination of L1 and proficiency level (where proficiency level was limited to 3, 4, and 5).
The essays from these students were processed by TAASSC and used to generate my final dataset of syntactic measures.
This (mostly) solved the issue of the skewed L1 distribution (see [final-analysis.ipynb#Exploratory-Data-Analysis](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/final-analysis.ipynb#Exploratory-Data-Analysis)) and also allowed me to create a reasonably sized dataset in a reasonable amount of time.

## Analysis

Following my computation phase of the project came the analysis, and for this portion of the project I had to keep the issues that I had run into in mind, as they can have a significant impact on the results of my analysis.
Most notably, the "outliers" caused by TAASSC's sensitivity to some quirks of non-native writing were very noticeable when I visualized the distributions of the syntactic measures in [final-analysis.ipynb#Analysis-of-Syntactical-Measures-by-L1](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/final-analysis.ipynb#Analysis-of-Syntactical-Measures-by-L1).

I had originally planned to stop my analysis at the exploratory data analysis and visualizations due to the potential for outliers to skew the results of statistical tests, but I decided to continue with some basic statistical analyses after following some recommendations that Sean had provided during my presentation.
Following Sean's advice, I decided to filter for the middle 90% of data points (in other words, excluding anything below the 5th percentile and anything above the 95th percentile) while analyzing each statistical measure.
Although I was technically excluding reasonable essays that should not have been considered outliers, it still did a reasonable job of reducing the significant skew in the data, which gave me confidence to continue with statistical testing.
My process for cleaning the data and running statistical tests for each measure can be found in [final-analysis.ipynb#Analysis-of-Syntactical-Measures-by-L1](https://nbviewer.org/github/Data-Science-for-Linguists-2022/esl-syntactic-analysis/blob/main/final-analysis.ipynb#Analysis-of-Syntactical-Measures-by-L1).
To determine whether a measure varied significantly between L1s, I simply performed one-way ANOVA tests, and to determine whether a measure on average differed significantly between proficiency levels within an L1, I simply performed one-sided two-sample t-tests.

Despite the issues with the data, I was still able to arrive at some statistically significant results.
Pretty much every single ANOVA test returned statistically significant, which was not particular surprising since the generated boxplots of the data showed differences in values across L1s.
However, one result that *was* surprising was that statistical tests performed on the syntactic measures of the essays written by Chinese speakers *always* returned statistically significant.
To be precise, the t-tests showed that the Chinese essays had a statistically significant increase in every measure as proficiency level increased, while the same could not be said about any other L1 to the same extent.
In a way, the Chinese essays seemed to fit my expectations for the data—that one should expect the syntactic measures to increase in value as proficiency level increases—surprisingly well.
I'm not sure why the Chinese essays in particular demonstrated such consistent statistical results, but I suspect that it could be due to the effects of outliers; this would require further investigation of the data and more accurate syntactic processing to be sure.

## Moving Forward

Of course, there is still much that can be done to improve the computation and analysis involved in the project.
One idea that I could tackle is switching from TAASSC to SpaCy, a Python package for NLP, which should hopefully provide much more accurate results in terms of calculating the syntactic measures.
Otherwise, I could also take the time to figure out how to clean and normalize the essays (properly formatting punctuation, etc.) in order to mitigate some of the issues that TAASSC had with the student essays.
I'd then be able to run TAASSC on the whole PELIC dataset, which would allow me to perform statistical tests with larger, more varied samples and therefore arrive at conclusions with greater confidence.

## References

Juffs, A., Han, N-R., & Naismith, B. (2020). The University of Pittsburgh English Language Corpus (PELIC) [Data set]. http://doi.org/10.5281/zenodo.3991977

Kyle, K. (2006). *Measuring syntactic development in L2 writing: Fine grained indices of syntactic complexity and usage-based indices of syntactic sophistication.* (Doctoral dissertation).

Lu, X. (2010). Automatic analysis of syntactic complexity in second language writing. *International Journal of Corpus Linguistics*, 15(4):474-496.
