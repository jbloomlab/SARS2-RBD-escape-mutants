# Design of SARS-CoV-2 mutant spike RBDs with potential future antigenic mutation

This repo aims to design SARS-CoV-2 spikes with mutated RBDs that represent the types of mutations that might occur in the future, and so could be used for purposes like antibody screening.
The design are made by Jesse Bloom.

To make the designs, build the conda environment in [environment.yml](environment.yml), activate it with:

    conda activate SARS2-RBD-escape-mutants

and then run the Jupyter notebook [design_mutants.ipynb](design_mutants.ipynb).
That notebook prints some information about the design, which themselves are described in [designed_mutants.csv](designed_mutants.csv).

The configuration for the design is in [config.yaml](config.yaml), which for each parent in turns points to a parent-specific configuration in the [parent_specs/](parent_specs) subdirectory.

The future variants are designed by picking mutations that:
 
 - are expected to cause a lot of antigenic escape using the RBD [escape calculator](https://jbloomlab.github.io/SARS2-RBD-escape-calc/), which is based on yeast-display RBD escape measurements on monoclonal antibodies
 - have  favorable affects on ACE2 affinity and RBD expression as measured using [yeast display RBD deep mutational scanning](https://www.science.org/doi/10.1126/science.abo7896)
 - are estimated to have favorable effects on viral fitness based on [analysis of natural sequences](https://academic.oup.com/ve/article/9/2/vead055/7265011) both across all SARS-CoV-2 sequences and just recent clades
 - have favorable effects on serum antibody escape, cell entry, and ACE2 binding as measured in [full spike deep mutational scanning](https://www.biorxiv.org/content/10.1101/2023.11.13.566961v1)
 - there is also an option in the configuration for each parent to manually up- or down-weight mutations if you have other information you want to use to favor / disfavor some.

The design process works as follows.
Each mutation is assigned a score based on its escape from the RBD escape calculator (raised to the power of a weight) times the exponential of all of the other phenotypes (times a weight).
These weights are specified in the configuration, and determine how important each phenotype is.
The top-scoring mutation is then added to the mutant, and this process is iterated but requiring each mutation to be at a new site.
When designing multiple mutants from a parent, mutations that have already been included are down-weighted to make it less likely (but not impossible) to include the same mutation in multiple mutants.