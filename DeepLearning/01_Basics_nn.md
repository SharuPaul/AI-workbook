---
title: "Basics of Neural Networks"
layout: single
author: Sharu Paul
author_profile: TRUE
header:
  overlay_color: "444444"
  overlay_image: /assets/images/pattern.png
---

{% include toc %}


# Introduction
A Neural Network consists of interconnected neurons arranged in layers. It "learns" through a feedback loop, constantly improving its accuracy by adjusting itself based on the difference between its predictions and the actual outcomes. 

## Layers of a Neural Network

- **Input Layer:** The first layer that receives the input data. The dimensions or size of the input layer depend on the type and dimensions of the input data for which it is made.
- **Hidden Layers:** Layers between the input and output that perform computations. These layers are where most of the processing happens.
- **Output Layer:** Produces the final output, which corresponds to the network's prediction. The number of neurons in this layer depends on the number of possible outputs the network is designed to produce.
<br>
<br>

# Types of Neural Networks

There are many different ways in which neural networks can be categorized. The following are the common types of deep neural networks.

## Convolutional Neural Network (CNN)

CNNs are designed for processing data that has a grid-like topology, such as images, which can be considered as a 2D grid of pixels. The key components of CNNs are convolutional layers that apply a convolution operation to the input, passing the result to the next layer. This allows CNNs to capture spatial hierarchies in data. CNNs have applications in Image Classification and Object Detection.

CNNs have been adapted for genomic sequences analysis, treating DNA sequences as one-dimensional grids. They can identify patterns within genomic sequences, such as motifs and regulatory elements, and are used in tasks like predicting the effects of genetic variants.

## Recurrent Neural Network (RNN)

RNNs are designed for sequential data, such as time series or text. RNNs have connections that form directed cycles, where output is fed back into the network, which allows information from previous steps to persist. This memory-like feature makes them suitable for tasks where context is important like in Natural Language Processing (NLP) applications.

RNNs can analyze sequential data such as nucleotide sequences, while being aware of the dependencies between different elements of the sequence. This makes RNNs good choice for working with sequence data where the order is important.

## Long Short-Term Memory Network (LSTM)

LSTMs are a special kind of RNNs capable of learning long-term dependencies. They are made up of units that consist of a "cell" and three "gates" that regulate the flow of information which address the vanishing gradient problem of traditional RNNs. The cell remembers values over arbitrary time intervals and the three gates regulate the flow of information into and out of the cell.

LSTMs can model complex biological sequences, capturing dependencies spanning longer sequences compared to simple RNNs.


## Transformers 

Transformer Networks are designed to handle sequential data using a mechanism called "attention" to weigh the importance of different parts of the input data differently. This allows them to capture complex relationships between elements of the sequence, regardless of their distance from each other. The key innovation of transformers is the self-attention mechanism, which enables the model to consider the entire sequence of data at once, making it highly parallelizable and efficient in processing large sequences of data. This aspect makes transformers particularly well-suited for tasks in Natural Language Processing, such as translation, text summarization, and sentiment analysis.

The ability to capture relationships between elements present at a long distance within the sequence make transformers well suited for genomics datasets. 

## Autoencoders

Autoencoders are a type of neural network used for unsupervised learning. They work by compressing input into a latent-space representation (dimensionality reduction)  and then reconstructing the output from this representation. This process enables them to learn efficient representations of the data.

## Generative Adversarial Network (GAN)

GANs consist of two networks, a generator and a discriminator, that are trained simultaneously. The generator learns to generate data similar to the input data, while the discriminator learns to distinguish between the real and generated data.

GANs have potential applications in generating synthetic genomic data for research, improving the robustness of models by providing additional training data.
<br>
<br>

 
___
# Further Reading
* []()
* []()
* []()

___

[Homepage](../index.md){: .btn  .btn--primary}
[Section Index](){: .btn  .btn--primary}  <!-- link to Landing Page -->
[Previous](){: .btn  .btn--primary}  <!-- link to previous article in the section -->
[Next](){: .btn  .btn--primary}  <!-- link to next article in the section -->
[Next](#introduction){: .btn  .btn--primary}
