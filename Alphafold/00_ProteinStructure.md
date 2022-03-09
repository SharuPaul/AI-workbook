---
title: "Protein structure"
layout: single
header:
  overlay_color: "444444"
  overlay_image: /assets/images/margaret-weir-GZyjbLNOaFg-unsplash_dark.jpg
---



# Protein structure

Protein is a biopolymer composed of amino acids connected via a peptide bond. The [primary structure](https://en.wikipedia.org/wiki/Protein_structure#Primary_structure) of a protein is an ordered list of consecutive mers, that is, the amino acid sequence. The three-dimensional organization of atoms in a protein is called a [tertiary structure](https://en.wikipedia.org/wiki/Protein_structure#Tertiary_structure) and determines the spatial shape of a molecule. Protein fragments that maintain a rigid spatial organization under physiological conditions have a specific [secondary structure](https://en.wikipedia.org/wiki/Protein_structure#Secondary_structure) (*helical* or *extended*). In contrast, the highly flexible regions are referred to as [intrinsically disordered](https://en.wikipedia.org/wiki/Intrinsically_disordered_proteins). The shape of a functional complex (**multimer**) composed of two or more protein chains (each is a **monomer**) is called the [quaternary structure](https://en.wikipedia.org/wiki/Protein_structure#Quaternary_structure).

### Source of protein structures
***Where to find a reference protein structure to compare modeling results?***

The structures of biomolecular systems (i.e., proteins and their complexes with nucleic acids and small molecules) are collected in various publicly available databases. The most common is [Protein Data Bank](https://www.rcsb.org) (PDB), the central archive of all experimentally determined protein structures. Some [secondary databases](https://en.wikipedia.org/wiki/Protein_structure_database) use this primary resource as an input for various structure-based analysis and provide the pre-computed results. The other structural databases store three-dimensional protein models predicted in computational modeling (*de novo*, comparative, using AI) or conformation ensembles derived from molecular dynamics simulations. However, when we speak of a *reference structure* or *native structure*, to which we compare our results, we usually mean an experimentally determined structure that is easily available in the PDB database.     
It may be that multiple PDB entries correspond to the same protein but determined by a different research group or in a different bilogical complex. Therefore, it is important to choose the right deposit for your analysis, such as one with a high enough resolution. For benchmarking, it is important to ensure that the set of selected deposits is non-redundant, i.e., does not contain the same or very similar protein chains because this will have the impact on statistics.

### Source of protein sequences
***Where to find the sequence if you want to predict protein structure for the first time?***

#### UniProt Database
Protein sequences are collected in a primary sequence databases, such as [UniProt](https://www.uniprot.org), which is a high-quality and freely accessible resource. You can search proteins by their *UniProt ID* or *common name*, *gene*, *oirganism*, and more. Let's try to find *'Immunoglobulin G-binding protein G'*. On the result page you can see multiple entries, *e.g., P02976, A0A0H3K686, P99134, P06654, P0A015, P38507*. Among them the *P06654* is the one with searched protein name. Clicking on the link will take you to the corresponding entry in the database. There, go to the *'Sequence'* section and copy the text you see in the text area or download the sequence in FASTA format. You can learn more about FASTA format in the *File Formats* [tutorial](https://bioinformaticsworkbook.org/introduction/fileFormats.html#gsc.tab=0).

#### Protein Data Bank (PDB)  
Each deposit in the PDB database has a unique 4-letter identifier composed of letters and numbers, e.g., *[2GB1](https://www.rcsb.org/structure/2GB1)*.     
You can use the advanced search option to filter out a set of results with the required properties (biopolymer type, structural classification, chain length, resolution, method of structure determination, year of deposition, etc.) or if you know the identifier *(PDB code)* for the protein of interest, you can search for it directly. On the entry's page, at the top right of the screen, you will find the buttons `Display Files` and `DownloadFiles`. One of the available options is the *FASTA sequence*. For a single deposit you can copy the text manually or use automatic download. For larger data sets, you can download all data (sequential or structural) with the `wget` command directly in the terminal.

**one-line command**

`for i in PDB1 PDB2 PDB3; do wget https://www.rcsb.org/fasta/entry/$i; done`

**bash script**
```
#!/bin/bash

for i in PDB1 PDB2 PDB3                                 # e.g., 2Gb1 101M 9INS; or read from a one-column file as `cat filename`
do
    wget https://www.rcsb.org/fasta/entry/$i            # to get sequence in FASTA format
    mv $i $i.fasta                                      # to specify file format
    wget https://files.rcsb.org/download/$i.pdb         # to get structure in PDB format
done

```

[AlphaFold index](Alphafold-landingPage.md){: .btn  .btn--primary}
[Next](01-AlphafoldIntroduction.md){: .btn  .btn--primary}
[Table of contents](../index.md){: .btn  .btn--primary}
