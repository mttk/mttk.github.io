---
title: 'Why Self-Attention? A Targeted Evaluation of Neural Machine Translation Architectures'
date: 2018-09-04
permalink: /posts/2018/04/why-self-attention/
tags:
  - Paper notes
  - RNN
  - Transformer
---

Empirical comparison of recurrent and non-recurrent architectures on a diagnostic sample of downstream tasks.

Tang, G., Müller, M., Rios, A., & Sennrich, R. (2018). [Why Self-Attention? A Targeted Evaluation of Neural Machine Translation Architectures](https://arxiv.org/abs/1808.08946).

## Takeaways

- Transformer models are competetive with, but do not outperform recurrent models _on the subject-verb agreement task_
- The number of heads in Transformer multi-head attention strongly affects the ability of long-term dependency modelling
  - for the subject-verb agreement task
  - different attention heads probably have different purposes (different feature _families_) and assuming that longer dependencies are fewer in training data, it is natural that shorter dependencies have priority until the benefit of learning them saturates
  - In contrast with results from [3], where the Transformer network had lesser capacity (most importantly, less attention heads)
- In word sense disambiguation, Transformer networks beat CNN and RNN architectures

## Introduction

In recent work, non-recurrent architectures are becoming increasingly competetive with recurrent ones in terms of performance while beating them with processing speed. Sequence-to-sequence (S2s) is recently dominated with variants of the transformer network **[1]** with convolutional models closely behind **[2]**. The competetiveness of these models has not yet been thoroughly explained nor compared to recurrent ones. *What* makes these attention-based networks so efficient? The authors attempt to answer this question through analysing the performance of recurrent (RNNS2S, RNN-bideep), convolutional (ConvS2S) and purely attentional (Transformers) models on (1) subject-verb agreement and (2) word sense disambiguation (WSD).

## Experimental setup

The authors first train all models on the [WMT17](http://www.statmt.org/wmt17/translation-task.html) (EN-DE) translation task and demonstrate comparable performance w.r.t. Bleu, with Transformer in the lead. To evaluate the performance of the trained _translation_ models on subject-verb-agreement and word sense disambiguation tasks, they adopt a _contrastive_ scheme. In this scheme, each test example is associated with a _correct_ translation and a closely related, but erroneous translation dubbed the _contrastive variant_. The decision of the model is correct if it assigns a higher score to the correct sentence. This setup is meant _"to test the sensitivity of NMT [neural machine translation] models  to  specific  translation  errors"_. 

An example of the contrastive setup for subject-verb agreement:

|Source-EN|[...] plan will be approved|
|Target-DE|[...] Plan verabschiedet wird|
|Contrast-DE|[...] Plan verabschiedet werden|

Similarly, for word sense disambiguation, the correct _translation_ meaning of an ambiguous word is replaced with the other sense. _Schlange_, as a German source word with the correct translation _line_ is replaced with other translations such as _snake_ or _serpent_. 

Essentially, a model trained on machine translation has to produce a higher score for the correct translation. The contrastive setup is a neat way to conduct a probing experiment whether a trained network effectively models a linguistic phenomenon. The datasets used are [_Lingeval97_](https://github.com/rsennrich/lingeval97) for subject-verb agreement and [_ContraWSD_](https://github.com/a-rios/ContraWSD) for word sense disambiguation.

## Experimental results

### Subject-verb agreement 

In the subject-verb agreement task, the recurrent models and the transformer are competetive, while the convolutional approach has an obvious dip in performance the longer the distance between the subject and the verb. An ablation study confirms the results, but to a lesser extent.

The authors also perform a detailed study comparing their results with Tran et al. [3], where it was shown that LSTMs outperform Transformer networks when the distance between the subject and the verb increases. The results were only reproduced when restricting the hyperparameters of the transformer network (essentially reducing its complexity/capacity). **An important finding here is that the number of attention heads increases performance on samples which require longer context drastically.**

The transformer model strongly outperforms other networks for word sense disambiguation, without clear explanations as why is this happening. The authors cite an inconclusive claim from Chen et al. [4] stating that transformer networks are simply better feature extractors than RNN encoders, where RNN networks are stronger in language modelling (essentially modelling infinite context n-gram lookup tables).

## References

[1] Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). [Attention is all you need](https://papers.nips.cc/paper/7181-attention-is-all-you-need.pdf). In Advances in Neural Information Processing Systems (pp. 5998-6008).

[2] Gehring, J., Auli, M., Grangier, D., Yarats, D., & Dauphin, Y. N. (2017, July). [Convolutional Sequence to Sequence Learning](https://arxiv.org/abs/1705.03122). In International Conference on Machine Learning (pp. 1243-1252).

[3] Tran, K., Bisazza, A., & Monz, C. (2018). [The Importance of Being Recurrent for Modeling Hierarchical Structure](https://arxiv.org/abs/1803.03585). arXiv preprint arXiv:1803.03585.

[4] Chen, M. X., Firat, O., Bapna, A., Johnson, M., Macherey, W., Foster, G., ... & Wu, Y. (2018). [The Best of Both Worlds: Combining Recent Advances in Neural Machine Translation](http://aclweb.org/anthology/P18-1008). arXiv preprint arXiv:1804.09849.
