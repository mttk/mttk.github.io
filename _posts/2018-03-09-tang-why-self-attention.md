---
title: 'Why Self-Attention? A Targeted Evaluation of Neural Machine Translation Architectures'
date: 2018-03-09
permalink: /posts/2018/04/why-self-attention/
tags:
  - Paper notes
  - RNN
  - Transformer
---

Empirical comparison of recurrent and non-recurrent architectures on a diagnostic sample of downstream tasks.

Tang, G., Müller, M., Rios, A., & Sennrich, R. (2018). Why Self-Attention? A Targeted Evaluation of Neural Machine Translation Architectures. [link](https://arxiv.org/abs/1808.08946)

## Introduction

In recent work, non-recurrent architectures are becoming increasingly competetive with recurrent ones in terms of performance while beating them with processing speed. Sequence-to-sequence (S2s) is recently dominated with variants of the transformer network [1] with convolutional models closely behind [2]. The competetiveness of these models has not yet been thoroughly explained nor compared to recurrent ones. *What* makes these attention-based networks so efficient? The authors attempt to answer this question through analysing the performance of recurrent (RNNS2S), convolutional (ConvS2S) and purely attentional (Transformers) models on (1) subject-verb agreement and (2) word sense disambiguation (WSD).

## Setup

The authors first train all models on the WMT17 (EN-DE) translation task and demonstrate comparable performance w.r.t. Bleu, with Transformer in the lead. To evaluate the performance of the trained _translation_ models on subject-verb-agreement and word sense disambiguation tasks, they adopt a _contrastive_ scheme. In this scheme, each test example is associated with a _correct_ translation and a closely related, but erroneous translation dubbed the _contrastive variant_. The decision of the model is correct if it assigns a higher score to the correct sentence. This setup is meant _"to test the sensitivity of NMT [neural machine translation] models  to  specific  translation  errors"_.

An example of the contrastive setup for subject-verb agreement:

|Source-EN|[...] plan will be approved|
|Target-DE|[...] Plan verabschiedet wird|
|Contrast-DE|[...] Plan verabschiedet werden]|

Similarly, for word sense disambiguation, the correct _translation_ meaning of an ambiguous word is replaced with the other sense. _Schlange_, as a German source word with the correct translation _line_ is replaced with other translations such as _snake_ or _serpent_. 

## References

[1] Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). Attention is all you need. In Advances in Neural Information Processing Systems (pp. 5998-6008).

[2] Gehring, J., Auli, M., Grangier, D., Yarats, D., & Dauphin, Y. N. (2017, July). Convolutional Sequence to Sequence Learning. In International Conference on Machine Learning (pp. 1243-1252).

[3] Tran, K., Bisazza, A., & Monz, C. (2018). The Importance of Being Recurrent for Modeling Hierarchical Structure. arXiv preprint arXiv:1803.03585.
