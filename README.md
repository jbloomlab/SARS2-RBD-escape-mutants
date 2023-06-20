# Design of candidate SARS-CoV-2 "cocktail" vaccines with future mutations

This repo aims to design "cocktail" vaccines of several SARS-CoV-2 spikes that include both a current leading variant (XBB.1.16) and some designed sequences with possible "future" RBD mutations
The design are made by Jesse Bloom.

The future variants are designed by picking mutations that:
 
 - are expected to cause a lot of antigenic escape using the [escape calculator](https://jbloomlab.github.io/SARS2-RBD-escape-calc/)
 - have relatively favorable affects on ACE2 affinity and RBD expression as measured using [deep mutational scanning](https://journals.plos.org/plospathogens/article?id=10.1371/journal.ppat.1010951)
 - are estimated to have favorable effects on viral fitness based on [analysis of natural sequences](https://www.biorxiv.org/content/10.1101/2023.01.30.526314v1)

The configuration for the design is in [config.yaml](config.yaml).
To make the designs, build the `conda` environment in [environment.yml](environment.yml), and then run the Jupyter notebook [design_vax.ipynb](design_vax.ipynb), which does the design.

The results designs are in the following files. If just one cocktail is being tested, we suggeset the one named *cocktail-vax*, but also provide designs for more aggressive cocktail (more mutations per spike) and a more conservative cocktail (fewer mutations per spike) as options.

 - [vax_designs/parent-vax.fa](vax_designs/parent-vax.fa): the *parent* cocktail that just includes the XBB.1.16 sequence.

 - [vax_designs/cocktail-vax.fa](vax_designs/cocktail-vax.fa): the *cocktail* that contains XBB.1.16 parent and designed mutants. There are ten candidate sequences listed here, and they are listed in the order they should be chosen for inclusion in a cocktail. For instance, if you just include five sequences take the first five.

 - [vax_designs/aggressive-cocktail-vax.fa](vax_designs/aggressive-cocktail-vax.fa): a more *aggressive cocktail* with a higher number of mutations per variant.

 - [vax_designs/conservative-cocktail-vax.fa](vax_designs/conservative-cocktail-vax.fa): a more *conservative cocktail* with a lower number of mutations per variant.

The following points should be taken into consideration before starting any experiments:

 - The designed sequences in the aforementioned files are spikes that do **not** contain any stabilizing mutations. For actual vaccine constructs, it may be desirable to add 2P or (preferably) 6P mutations to stabilize the pre-fusion spike.
 - The spikes have not been validated for proper folding or expression, which should be done prior to beginning any vaccination experiments.
 - The idea that these cocktail vaccines would be preferable or even non-inferior to a monovalent vaccine is untested and may not be true.

