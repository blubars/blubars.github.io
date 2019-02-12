---
layout: post
title: "Infinite Jest Nets"
date: 2018-12-20 23:37:15
categories: project
---
\[[View the visualization here!](https://hneutr.github.io/infinite_jest_webweb/)\] Does a fictional story structurally mirror our world, or is it fundamentally different? How does a story's structure impact its narrative? We analyze David Foster Wallace's <i>Infinite Jest</i> to attempt an answer to a variant of these two questions. Specifically, we represent the book as a growing network, with characters as nodes and character co-mentions as weighted edges. In a liberal interpretation, this gives an approximation a character-interaction network. Using standard static analysis techniques (degree distribution, transitivity, modularity, assortativity, and centralities), as well as dynamic techniques (sparsification vs densification, by examining largest component size, number of components, degree, and mean geodesic path as a function of book progress), we answer two questions:

1. Is the character interaction network structurally the same as real-world social networks? If not, how does it differ?
2. Why did the author choose to structure the narrative out of chronological order?

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/149630921@N02/40104972043/in/datetaken-public/" title="labeled_community_with_labels"><img src="https://farm8.staticflickr.com/7816/40104972043_b383401937_z.jpg" width="640" height="604" alt="labeled_community_with_labels"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

To the first point: Yes and no. The network does display the small-world effect. However, the degree distribution is not scale-free, and we see a much higher local clustering coefficient (0.3930) than compared to the averaged 5 smallest networks in the FB100 dataset (0.2403). Additionally, we observe slight degree disassortativity (-0.0945) on the unweighted network, suggesting star-like configurations. Real-world social networks typically have positive degree assortativity, due to core-periphery structures and community structures.

Towards the question of the non-chronologically ordering, the dynamic analysis shows that in both story arc follows an apparent pattern of sparsification followed by densification when around 2/3 of all nodes have been added. 
However, the booktime ordering displays a higher degree and a lower average geodesic path than the chronological ordering. And most strikingly, the number of components is drastically lower in the book ordering -- a maximum of 12 instead of 19! This means that chronologically, you would have had to keep 19 separate story-lines going in your head before they finally start connecting together. Imagine trying to keep track of that many! The authored book ordering must knit more storylines together through present-day context before introducing their backstories.

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/149630921@N02/40104974283/in/datetaken-public/" title="dynamics-num-components"><img src="https://farm8.staticflickr.com/7899/40104974283_4a56f2d698_z.jpg" width="640" height="480" alt="dynamics-num-components"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

This project was a team effort! The dream team: [Hunter Wapman](http://hneutr.github.io/) and [Carl Mueller](https://www.carl-mueller.com/).
This work was done as our end-of-term project for Network Analysis and Modeling (CSCI 5352), perhaps my favorite class so far.

