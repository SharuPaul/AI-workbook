---
title: "Introduction to AlphaFold"
layout: single
header:
  overlay_color: "444444"
  overlay_image: /assets/images/margaret-weir-GZyjbLNOaFg-unsplash_dark.jpg
---


# Protein structure prediction

Protein structure prediction, that is, the determination of the three-dimensional shape of a protein by computational methods starting from the primary sequence, is a challenge that structural bioinformatics has been grappling with since the 60s of the 19th century. During this time, systematic progress was made, and the state-of-the-art  tools were selected in subsequent editions of the [CASP](https://predictioncenter.org) (*Critical Assessment of protein Structure Prediction*) competition. Various approaches have been developed, including [comparative modeling](https://en.wikipedia.org/wiki/Homology_modeling) using templates and [*de novo* modeling](https://en.wikipedia.org/wiki/De_novo_protein_structure_prediction). In the early 2000s, methods using machine learning and artificial intelligence began to have significant success. An undeniable breakthrough came in the [CASP14 edition](https://onlinelibrary.wiley.com/doi/10.1002/prot.26171), where the novel AlphaFold method was the top-ranked predictor and provided previously unattainable high-quality predictions. If you are curious about the details of this achievement, I refer you to an informative and truly enjoyable analysis published by the [Oxford Protein Informatics Group](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/).


# AlphaFold by DeepMind

> AlphaFold is an artificial intelligence (AI) program developed by Alphabets's/Google's DeepMind which performs predictions of protein structure. The program is designed as a deep learning system. <br>
A team that used AlphaFold 2 (2020) [...] scored above 90 for around two-thirds of the proteins in CASP's global distance test (GDT), a test that measures the degree to which a computational program predicted structure is similar to the lab experiment determined structure, with 100 being a complete match.<br>
Some researchers noted that the accuracy is not high enough for a third of its predictions, and that it does not reveal the mechanism or rules of protein folding for the protein folding problem to be considered solved. Nevertheless, there has been widespread respect for the technical achievement.<br>
<p style="text-align: right; font-style: italic;"> <a href="https://en.wikipedia.org/wiki/AlphaFold">Wikipedia/AlphaFold</a></p


**Explore other resources**

1. [DeepMind:](https://deepmind.com/blog/article/alphafold-a-solution-to-a-50-year-old-grand-challenge-in-biology) *AlphaFold: a solution to a 50-year-old grand challenge in biology*
2. [Oxford Protein Informatics Group](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/) *CASP14: what Google DeepMind’s AlphaFold 2 really achieved, and what it means for protein folding, biology and bioinformatics*
3. [AlphaFold Database](hhttps://alphafold.ebi.ac.uk) *AlphaFold DB provides open access to protein structure predictions for the human proteome and other organisms*

**Cite AlphaFold**

1. Jumper, J et al. *Highly accurate protein structure prediction with AlphaFold*. Nature (2021).
2. Mirdita M, Schütze K, Moriwaki Y, Heo L, Ovchinnikov S, Steinegger M. *ColabFold - Making protein folding accessible to all*. bioRxiv, 2021


# AlphaFold Computing Solutions

## AlphaFold2 installation on your local machine

If you were going to run AlphaFold using the direct computing power of your local machine (whether a workstation or laptop) you should be warned that you will need close to 2TB of disk space just for the AlphaFold-related databases alone. This can be a serious limitation and then it is better to go straight to the tutorial section on using AlphaFold via HPC infrastructure (ISU HPC, SciNet HPC) or cloud computing with [Google Colab](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb).

In case you have sufficient resources, you can have AlphaFold running locally by following the instructions provided by [github.com/kalininalab](https://github.com/kalininalab/alphafold_non_docker). You can also find the singularity container for AlphaFold2 at [github.com/hyoo](https://github.com/hyoo/alphafold_singularity).

## AlphaFold2 pipeline in Cloud via Google Colab

The Colab is a freely accessible online Colaboratory Google Research platform, where you can easily run the AlphaFold pipeline using [ColabFold notebook](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb). The more detailed instructions are provided in a separate tutorial, [AlphaFold Cloud Computing Solutions](02-AlphafoldCloudComputing.md).

## AlphaFold2 *standalone* preinstalled on HPC infrastructure

The general instructions of using AlphaFold2 preinstalled as a standalone module on various High Performance Computing infrastructures are provided in the [AlphaFold High Performance Computing](03-AlphafoldHPC.md) section. In addition, a detailed description of how AlphaFold2 is configured on Iowa State University's HPC infrastructure and SCINet HPC is available in the [AlphaFold via the ISU HPC infrastructure](03A-Alphafold-ISU.md) and [AlphaFold via the SCINet HPC infrastructure](03B-Alphafold-SCINet.md) sections, respectively.



[AlphaFold index](Alphafold-landingPage.md){: .btn  .btn--primary}
[Next](02-AlphafoldCloudComputing.md){: .btn  .btn--primary}
[Table of contents](../index.md){: .btn  .btn--primary}
