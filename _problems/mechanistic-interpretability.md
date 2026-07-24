---
slug: mechanistic-interpretability
name: "Mechanistic Interpretability"
title: "We deploy AI systems whose inner workings nobody can explain"
field: engineering-ai
statement: "Can we trace, step by step, how a trained neural network actually computes its answers — well enough to catch it being wrong, deceptive, or unsafe before it acts?"
first_posed: 2020
posed_by: "Chris Olah and collaborators, in the 'Circuits' research program"
summary: "The most consequential software artifacts of the decade are billions of learned numbers that no human wrote and no human can read. Mechanistic interpretability tries to reverse-engineer them: sparse autoencoders extracted millions of human-recognizable 'features' from a frontier model in 2024, and in 2025 Anthropic's attribution-graph work traced actual circuits in Claude — revealing, for instance, that the model plans rhymes ahead before writing a line of poetry, and exposing internal mechanisms behind hallucination and jailbreaks. Yet current techniques explain only a fraction of any model's behavior, can miss what the model doesn't verbalize, and don't yet scale to auditing a frontier system's full computation. The field's own 2025 review catalogues exactly how far there is to go."
why_it_matters: "You cannot debug, certify, or fully trust what you cannot inspect — and AI systems now write code, advise doctors, and act as autonomous agents. Interpretability is also the only realistic path to detecting a model that has learned to behave differently when it is being watched."
progress:
  - "2020 — 'Zoom In: An Introduction to Circuits' articulates the reverse-engineering agenda for neural networks"
  - "2023 — Anthropic's 'Towards Monosemanticity' shows sparse autoencoders can decompose model activations into interpretable features"
  - "2024 — 'Scaling Monosemanticity' extracts millions of interpretable features from a production frontier model"
  - "2025 — attribution graphs trace multi-step circuits in a deployed model; the field's open problems are formally catalogued; Dario Amodei publishes 'The Urgency of Interpretability'"
  - "2026 — circuit-tracing tools are open-sourced and replicated across Gemma, Llama, and Qwen models"
references:
  - url: "https://transformer-circuits.pub/2025/attribution-graphs/biology.html"
    source: "Anthropic (Transformer Circuits)"
    note: "'On the Biology of a Large Language Model' — circuit tracing inside a deployed frontier model"
  - url: "https://arxiv.org/abs/2501.16496"
    source: "arXiv (Sharkey et al., 2025)"
    note: "'Open Problems in Mechanistic Interpretability' — the field's own map of what remains unsolved"
  - url: "https://www.darioamodei.com/post/the-urgency-of-interpretability"
    source: "Dario Amodei"
    note: "2025 essay arguing interpretability must outpace capability growth"
status: curated
date_curated: 2026-07-24
---
