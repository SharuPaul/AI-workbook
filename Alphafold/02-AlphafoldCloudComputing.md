---
title: "AlphaFold Cloud Computing"
layout: single
header:
  overlay_color: "444444"
  overlay_image: /assets/images/margaret-weir-GZyjbLNOaFg-unsplash_dark.jpg
---



# AlphaFold2 pipeline in Cloud via Google Colab

The Colab is an online Colaboratory Google Research platform, free to use by anyone within the [usage limits](https://research.google.com/colaboratory/faq.html#resource-limits). The initiative provides users with computing resources (both CPU and GPU) via the [Jupyter](https://jupyter.org) notebook interface in the browser. The latter supports free software, open standards, facilitate collaboration, and provides web services for interactive computing across all programming languages. For the Colab framework, [Python](https://www.python.org) is the preferred coding language. The notebooks broadly meet the need for an interactive and user-friendly working environment. In a single document, you can combine blocks of executable code, human-readable comments in rich text along with the results of analysis, including graphs, images, HTML, LaTeX and more.

## ColabFold notebook: *AlphaFold2 using MMseqs2*

The *AlphaFold2.ipynb* notebook is available online at [https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb). The current version allows modeling of both monomeric and multimeric protein structures using  [AlphaFold2](https://www.nature.com/articles/s41586-021-03819-2) and [Alphafold2-multimer](https://www.biorxiv.org/content/10.1101/2021.10.04.463034v1), respectively. When you shorten the URL in your browser's search box to [~ColabFold/](https://colab.research.google.com/github/sokrypton/ColabFold/), you'll find a list of other more specialized notebooks, such as for complexes.

Using the Alphafold notebook to predict the structure of a protein is straightforward.

1. First, copy-paste the amino acid sequence in one-letter notation to the `"query_sequence"` input field.

 `query_sequence: "MTYKLILNGKTLKGETTTEAVDAATAEKVFKQYANDNGVDGEWTYDDATKTFTVTE"`

  The example above contains the amino acid sequence in single letter notation for a small globular protein G. For starters, you can use this sequence.


2. Then find "Runtime" in the top menu, click to expand available options, and press "Run all".

The detailed [instructions](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb#scrollTo=UGUBLzB3C6WN) are provided directly in the bottom part of the notebook, including *Limitations, Issues,* and *Troubleshooting*.

### Overall structure of the ColabFold notebook (AlphaFold2)

```
• Input protein sequence(s)
  query_sequence:
  jobname:
  use_amber:
  use_templates:
  save_to_google_drive:

• Advanced settings
  msa_mode:
  model_type:
  pair_mode:
  num_recycles:

• Install dependencies

• Run Prediction

• Display 3D structure
  rank_num:
  color:
  show_sidechains:
  show_mainchains:

• Plots

• Package and download results

```

### ColabFold by Boston Protein Desin @YouTube

To find the scientific insights of AlphaFold modeling as well as to learn useful technical tips & tricks of using the ColabFold implementation, please watch the "*ColabFold - Making protein folding accessible to all via Google Colab!*" movie recorded on August 4th, 2021 presented by Sergey Ovchinnikov and Martin Steinegger, hosted by Chris Bahl.

[![ColabFold Video](https://img.youtube.com/vi/Rfw7thgGTwI/0.jpg)](https://www.youtube.com/watch?v=Rfw7thgGTwI)


[AlphaFold index](Alphafold-landingPage.md){: .btn  .btn--primary}
[Next](03-AlphafoldHPC.md){: .btn  .btn--primary}
[Table of contents](../index.md){: .btn  .btn--primary}
