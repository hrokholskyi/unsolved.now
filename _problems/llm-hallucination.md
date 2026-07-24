---
slug: llm-hallucination
name: "Hallucination"
title: "AI still confidently invents facts — and we can't fully make it stop"
field: engineering-ai
statement: "Can language models be made to reliably know — and say — when they don't know, instead of fluently producing plausible falsehoods?"
first_posed: 2018
summary: "Language models sometimes generate fluent, confident statements that are simply false — a failure researchers began calling 'hallucination' in the late 2010s, and which every frontier model still exhibits. In 2024, Oxford researchers published a Nature method using 'semantic entropy' to detect a major class of hallucinations by measuring a model's uncertainty over meanings rather than words. In 2025, an OpenAI and Georgia Tech analysis argued that some hallucination is a statistical inevitability of how models are trained — and that it persists partly because benchmarks reward confident guessing over honest abstention. Retrieval grounding, uncertainty estimation, and abstention training all reduce error rates, but no known technique makes a general-purpose model reliably truthful, especially across the multi-step reasoning chains agents now execute."
why_it_matters: "These systems now draft legal and medical text, answer search queries, and take autonomous actions where a single invented fact can compound into real-world harm. Reliable self-knowledge — an AI that can be trusted to say 'I don't know' — is arguably the gating requirement for delegating consequential work to machines."
progress:
  - "2018 — hallucination is identified and named as a failure mode in neural text generation"
  - "2022 — systematic surveys establish hallucination as a central open problem of natural language generation"
  - "2024 — Farquhar et al. publish semantic-entropy detection of confabulations in Nature"
  - "2025 — Kalai, Nachum, Vempala, and Zhang show statistical pressures make some errors unavoidable and that guess-rewarding benchmarks entrench them"
references:
  - url: "https://arxiv.org/abs/2509.04664"
    source: "arXiv (Kalai et al., 2025)"
    note: "'Why Language Models Hallucinate' — the statistical account of why hallucination arises and persists"
  - url: "https://www.nature.com/articles/s41586-024-07421-0"
    source: "Nature (Farquhar et al., 2024)"
    note: "semantic-entropy method for detecting hallucinated 'confabulations'"
status: curated
date_curated: 2026-07-24
---
