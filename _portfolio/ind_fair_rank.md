---
title: "Individually Fair Rankings"
excerpt: "An algorithm for training individually fair learning-to-rank systems using optimal transport tools."
header:
   teaser: /assets/images/ind_fair_rank/ndcg.png
---

This is joint work with [Amanda Bower](https://amandarg.github.io), [Mikhail Yurochkin](https://moonfolk.github.io) and [Yuekai Sun](https://yuekai.github.io) and was accepted to ICLR 2021 for a poster presentation.

Abstract: We develop an algorithm to train individually fair learning-to-rank (LTR) models. The proposed approach ensures items from minority groups appear alongside similar items from majority groups. This notion of fair ranking is based on the definition of individual fairness from supervised learning and is more nuanced than prior fair LTR approaches that simply ensure the ranking model provides underrepresented items with a basic level of exposure. The crux of our method is an optimal transport-based regularizer that enforces individual fairness and an efficient algorithm for optimizing the regularizer. We show that our approach leads to certifiably individually fair LTR models and demonstrate the efficacy of our method on ranking tasks subject to demographic biases.
One-sentence Summary: We present an algorithm for training individually fair learning-to-rank systems using optimal transport tools.



Openreview page: [https://openreview.net/forum?id=71zCSP_HuBN](https://openreview.net/forum?id=71zCSP_HuBN).
