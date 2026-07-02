# Inclusion / Exclusion Criteria

## Inclusion Criteria (IC)
- **IC‑P**: Paper must address **requirements traceability** or **trace link recovery**.
- **IC‑I**: Uses **information retrieval** methods (VSM, LSI, BM25, TF‑IDF) **or** large language models (GPT‑4, ChatGPT, BERT, LLM).
- **IC‑E**: Includes **empirical evaluation** (experiment, benchmark, case study) with quantitative results.
- **IC‑D**: Uses at least one relevant dataset: **CoEST, iTrust, eTour, EasyClinic**.
- **IC‑Y**: Published in **2019 or later**.

## Exclusion Criteria (EC)
- **EC‑Y**: Year < 2019.
- **EC‑O**: Off‑topic (not traceability, or focuses on vulnerability, security, or non‑software artifacts).
- **EC‑N**: No empirical experiment (vision paper, survey, tutorial).
- **EC‑A**: Full‑text not accessible (paywall / not available).
- **EC‑D**: Duplicate (same DOI or same title/author as another record).

## Decision Rules
- **INCLUDE** if **all IC** are satisfied and **none of the EC** apply (based on title + abstract for v1; based on full‑text for v2).
- **EXCLUDE** if any EC applies – record the specific code and a brief reason.