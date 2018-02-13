---
layout: post
title: "Spectral Clustering Exploration"
date: 2018-01-10
categories: project
---
Working with two other classmates, we conducted an in-depth analysis and exploration of [spectral clustering](https://en.wikipedia.org/wiki/Spectral_clustering), an unsupervised learning technique. 


[Click here](https://drive.google.com/open?id=1To4uUZMtSgFMj_56U9FGK_WIyJNUZHlH) for our paper.  
[Click here](https://github.com/blubars/Spectral-Clustering) for our code.  

We were interested in spectral clustering because of its theoretical depth and its impressive performance. In our analysis, we: 
1. Explored the theoretical basis for the algorithm
2. Read several research papers exploring the technique
3. Created an implementation
4. Experimented with our implementation on several unique datasets, comparing results with other clustering algorithms
5. Made our own novel modification to the algorithm to improve the running time (since running time is the biggest drawback to spectral clustering)

Spectral clustering is a fascinating approach to clustering wherin we interpret the dataset as a graph. This allows us to apply the relatively new field of spectral graph theory: using a graph's spectral decomposition to approximately solve a [graph partitioning problem (NP-complete)](https://en.wikipedia.org/wiki/Graph_partition).

Our implementation of spectral clustering is based on [Andrew Ng et al.'s cornerstone paper](http://ai.stanford.edu/~ang/papers/nips01-spectral.pdf) on the technique. Our code is [here in github](https://github.com/blubars/Spectral-Clustering). We also created a short [jupyter notebook](https://github.com/blubars/Spectral-Clustering/blob/master/jupyter/spectral-clustering-notebook.ipynb) explaining it in detail.

For the extension, I created a version of the algorithm that randomly sampled a subset of the examples to run spectral clustering on. I then clustered those, and used K-Nearest Neighbors to classify the remaining examples into one of the clusters found by spectral clustering. This resulted in a massive speed boost, since spectral clustering time complexity is approximately **O(n^3)** where **n** is the number of examples. See the paper for details and empirical results.

This was a very fun and challenging project, requiring us to explore linear algebra and graph theory in-depth on our own, as well as collect empirical results on unusual datasets ranging from toy datasets to image segmentation to clustering letters as vowels or consonants. 


