---
title: "Stat Dirty Data"
date: 2019-09-20T21:43:46-04:00
draft: true
---

bag-of-word approach: use simple word counts as its basis (vectorization).

clustering steps:

- Extract the salient features from each post and store it as a vector per post. 
- Compute clustering on the vectors. 
- Determine the cluster for the post in question. 
- From this cluster, fetch a handful of posts that are different from the post in
question. This will increase diversity.
