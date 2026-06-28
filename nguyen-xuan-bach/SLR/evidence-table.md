# Evidence Table — Traceability Link Generation

N = 11 paper included

| Paper | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế |
|-------|----------|---------|--------|---------|------|---------|
| Wang 2025 (APSEC) | GPT-4 + CoT, SimCSE | iTrust, eTour, eANCI, SMOS | MAP | MAP +125.47% over LSI | N/A | Chỉ test trên 4 dataset, chưa thử zero-shot thuần |
| Fuchß 2025 (ICSE) | GPT-4o, Claude 3.5, RAG | Req-to-code, doc-to-code | F1 | Outperforms SOTA on code tasks | github.com/ArDoCo | RAG chưa đủ tốt cho architecture task |
| Jin 2025 (APSEC) | LLM + HGT (GNN) | 10 open-source projects | F1 | +12.90% F1 over HGNNLink | N/A | Chưa test trên CoEST benchmark cụ thể |
| Hey 2024 (RE) | NoRBERT (BERT-based) | iTrust, eTour, SMOS, eANCI | F1 | F1 >90% on iTrust/eTour | github.com/ArDoCo | External validity: chỉ 4 dataset |
| Hassine 2024 (EASE) | GPT-3.5-turbo zero-shot | Security req + goal models | Precision, Recall | N/A (security domain) | N/A | Chỉ về security req, bukan source code |
| Zhao & Xu 2026 (Information) | GraphRAG, LLM zero-shot | RC-TLR datasets | Precision, Recall | Outperforms IR baselines | N/A | Chưa test cross-project variance |
| Ngo 2024 (JSS) | VSM, LSI, BM25, FTLR, TAROT, CRT | CoEST: iTrust, eTour, eANCI, SMOS + 9 others | MAP, Precision, Recall, F1 | FTLR/CRT/TAROT best on CoEST | N/A | Không include LLM-based methods |
| Wang 2023 (IJCNN) | ML classifiers + DBT (SVM, KNN, LR) | CoEST 7 datasets incl. EasyClinic | Precision, Recall | LR recall +0.5517 with DBT on EasyClinic | N/A | Không dùng LLM, chỉ ML truyền thống |
| Ali 2019 (IST) | ConPos (IR + POS tagging) | iTrust, Pooka, etc. | F1 | ConPos > VSM/LSI baseline | N/A | English-only, chưa multilingual |
| Li 2020 (Applied Sciences) | ML + Logical Reasoning + VSM/LSI | Multiple datasets | Precision, Recall | Improves over pure IR | N/A | Dataset nhỏ, chưa test CoEST đầy đủ |
| Zhao 2020 (AIRE) | TLR-KRL (Knowledge Representation) | eTour, eANCI, Clinic, iTrust | Precision, Recall | Outperforms IR methods | N/A | Extended abstract — kết quả chưa đầy đủ |
