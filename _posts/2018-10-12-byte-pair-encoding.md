---
title: 'Byte pair encoding'
date: 2018-10-12
permalink: /posts/2018/10/byte-pair-encoding/
tags:
  - BPE
  - NLP
---

_A brief overview of the byte pair encoding technique._

**Introduced in:** Sennrich, R., Haddow, B., & Birch, A. (2015). Neural machine translation of rare words with subword units. [\[**arXiv**\]](https://arxiv.org/pdf/1508.07909.pdf)

Byte pair encoding (BPE), when applied to text (where the notion of 'bytes' is loosened to mean 'characters') extracts the most common subwords and represents them as a single token.
This could be useful for preserving similarity between lexically similar words (ex. "fish, fisherman, fishing").

Required input: a word:count dictionary representing the frequencies of each word in the relevant dataset.

Operations used: 
- merge (merges two byte[pair]s to create a new byte pair) 
- reducing frequencies of neighboring bytes after merges (a b c d) -> (a bc d): reduce freq of (ab) & (cd), then increase freq of (a(bc)) and ((bc)d)

[incomplete]
