# Evidence Table — Traceability Link Generation

N = 11 paper included

| Paper | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế |
|-------|----------|---------|--------|---------|------|---------|
| IRRT 2022 (IEEE) | IR-based tool | Multiple datasets | Precision, Recall, F1 | Outperforms VSM/LSI baseline | N/A | Chưa test trên CoEST |
| Evaluating IR Models 2021 (IEEE) | VSM, LSI, BM25 | Multiple req-to-code datasets | MAP, F1 | BM25 best overall | N/A | English-only |
| Enhancing Unsupervised TLR 2019 (IEEE) | IR + Sequential Semantics | Multiple datasets | Precision, Recall | Improves over VSM/LSI | N/A | Small dataset |
| Comparison of IR Techniques 2019 (IEEE) | VSM, LSI, BM25 | Multiple datasets | Precision, Recall, F1 | BM25 > LSI > VSM | N/A | Limited to English |
| MLTracer 2024 (IEEE) | ML + Gradient Boosting + IR | Multiple datasets | F1 | +15% F1 over IR baseline | N/A | Chưa dùng LLM |
| IR-Based Artificial Bee Colony 2020 (IEEE) | IR + ABC optimization | Multiple datasets | Precision, Recall | Improves over VSM | N/A | Optimization overhead |
| Enhancing Req-to-Code via CoT 2025 (IEEE) | LLM + CoT prompting | iTrust, eTour | MAP | MAP +125% over LSI | N/A | Chưa thử zero-shot thuần |
| Recovering Semantic Traceability 2021 (IEEE) | IR + Semantic Features | Multiple datasets | Precision, Recall, F1 | Outperforms VSM/LSI | N/A | English-only |
| Recovering TLR Object-oriented 2023 (IST) | IR-based (VSM/LSI) | OO software datasets | Precision, Recall | VSM competitive with LSI | N/A | Small projects only |
| Fine-Grained Dependencies TLR 2024 (ICSE) | IR + dependency analysis | Multiple datasets | Precision, Recall | Improves correctness | N/A | Requires dependency info |
| Evaluating LLMs Doc-to-Code TLR 2025 (ACM) | GPT-4, Claude, Gemini | Doc-to-code datasets | F1, Precision, Recall | LLM outperforms IR | N/A | Cost of LLM API |
