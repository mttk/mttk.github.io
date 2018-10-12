---
permalink: /
title: ""
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I'm a third year PhD student at the [Text Analysis and Knowledge Engineering Lab](http://takelab.fer.hr/) at the University of Zagreb, supervised by [Jan Šnajder](http://www.zemris.fer.hr/~jan/).

What interests me are recurrent models for processing natural language data and distributed representations of words. In one hand, there's some obvious issues with how recurrent models process text, making it easy to approximate them or even beat their performance with fully connected nets **[1]** or even standard linear models (nbSVM). On the other hand, the standard word representations we use assume that each word can be represented with a single fixed dimensionality vector -- ignoring polysemy **[2]** and the difference in information value between function and content words.

What I work on is improving both the input representations so that recurrent models have an easier task, and identifying and alleviating problems that cause recurrent, _infinite context_ models to not outeperform fixed (or zero) context models.


1. Miller, J., & Hardt, M. (2018). When Recurrent Models Don't Need To Be Recurrent. arXiv preprint arXiv:1805.10369.

2. Arora, Sanjeev, et al. "Linear algebraic structure of word senses, with applications to polysemy." Transactions of the Association of Computational Linguistics 6 (2018): 483-495.
