---
slug: deep-learning-generalization
name: "The Generalization Puzzle"
title: "Deep learning works far better than our math says it should"
field: engineering-ai
statement: "Why do giant neural networks — big enough to simply memorize their training data — instead learn rules that work on data they have never seen?"
first_posed: 2016
posed_by: "Chiyuan Zhang, Samy Bengio, Moritz Hardt, Benjamin Recht, and Oriol Vinyals"
summary: "Classical learning theory says a model with far more parameters than training examples should overfit: memorize the data and fail on anything new. Deep networks blow through that prediction daily, and a landmark 2016 experiment made the paradox undeniable — the same networks that generalize beautifully can also perfectly memorize completely random labels, so the standard theoretical guarantees explain essentially nothing about why they work. Since then the mystery has deepened with strange, reproducible phenomena: 'double descent', where making a model bigger first hurts and then helps, and 'grokking', where a network suddenly snaps from memorization to perfect generalization long after it seemed hopelessly overfit. Partial accounts exist, but no accepted theory yet predicts when and why deep learning generalizes."
why_it_matters: "Trillions of dollars of infrastructure now rest on an empirical recipe we cannot mathematically explain. A real theory would tell us how much data and compute a capability actually requires, when a model will fail on out-of-distribution inputs, and whether surprises like grokking lurk in the systems we deploy."
progress:
  - "2016 — Zhang et al. show state-of-the-art networks can perfectly fit random labels, demolishing classical explanations of their generalization"
  - "2018 — Belkin et al. describe 'double descent': test error falls again beyond the point where models perfectly fit their training data"
  - "2022 — Power et al. report 'grokking': sudden generalization on algorithmic tasks long after overfitting"
  - "2026 — unifying frameworks (circuit competition, learning-speed decompositions) link grokking, double descent, and emergence, but remain partial and contested"
references:
  - url: "https://arxiv.org/abs/1611.03530"
    source: "arXiv (Zhang et al., 2016)"
    note: "the random-label experiment that crisply posed the modern generalization puzzle"
  - url: "https://arxiv.org/abs/1812.11118"
    source: "arXiv (Belkin et al., 2018)"
    note: "'Reconciling modern machine-learning practice and the classical bias–variance trade-off' — the double-descent curve"
  - url: "https://arxiv.org/abs/2201.02177"
    source: "arXiv (Power et al., 2022)"
    note: "'Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets'"
status: curated
date_curated: 2026-07-24
---
