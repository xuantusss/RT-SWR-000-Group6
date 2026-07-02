# Evidence Table Merged — Traceability Link Generation

N = 27 paper (sau dedup từ 4 thành viên)

| Paper | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế |
|-------|----------|---------|--------|---------|------|---------|
| Wang 2025 (APSEC) | GPT-4 + CoT, SimCSE | iTrust, eTour, eANCI, SMOS | MAP | MAP +125.47% over LSI | N/A | Chỉ test 4 dataset, chưa thử zero-shot thuần |
| Fuchß 2025 (ICSE) | GPT-4o, Claude 3.5, RAG | Req-to-code datasets | F1 | Outperforms SOTA on code tasks | github.com/ArDoCo | RAG chưa đủ tốt cho architecture task |
| Jin 2025 (APSEC) | LLM + HGT (GNN) | 10 open-source projects | F1 | +12.90% F1 over HGNNLink | N/A | Chưa test trên CoEST benchmark |
| Hey 2024 (RE) | NoRBERT (BERT-based) | iTrust, eTour, SMOS, eANCI | F1 | F1 >90% on iTrust/eTour | N/A | External validity: chỉ 4 dataset |
| Hassine 2024 (EASE) | GPT-3.5-turbo zero-shot | Security req + goal models | Precision, Recall | N/A (security domain) | N/A | Chỉ về security req |
| Zhao & Xu 2026 (Information) | GraphRAG, LLM zero-shot | RC-TLR datasets | Precision, Recall | Outperforms IR baselines | N/A | Chưa test cross-project variance |
| Ngo 2024 (JSS) | VSM, LSI, BM25, FTLR, TAROT, CRT | CoEST: iTrust, eTour, eANCI, SMOS | MAP, P, R, F1 | FTLR/CRT/TAROT best on CoEST | N/A | Không include LLM-based methods |
| Wang 2023 (IJCNN) | ML classifiers + DBT | CoEST 7 datasets incl. EasyClinic | Precision, Recall | LR recall +0.5517 with DBT | N/A | Không dùng LLM |
| Ali 2019 (IST) | ConPos (IR + POS) | iTrust, Pooka | F1 | ConPos > VSM/LSI baseline | N/A | English-only |
| Li 2020 (Applied Sciences) | ML + Logical Reasoning + VSM/LSI | Multiple datasets | Precision, Recall | Improves over pure IR | N/A | Dataset nhỏ |
| Zhao 2020 (AIRE) | TLR-KRL | eTour, eANCI, Clinic, iTrust | Precision, Recall | Outperforms IR methods | N/A | Extended abstract |
| Shah 2025 (RE) | GPT-4, Mistral, LLaMA-2 | RE qualitative datasets | Cohen's Kappa | GPT-4 Kappa >0.7 zero-shot | N/A | Zero-shot limited; English-only |
| Zhang 2025 | GPT-4 zero-shot/few-shot | Req-to-code trace datasets | F1 | F1 improvement up to 28.59% | N/A | Generalization not tested |
| Hey 2025 (REFSQ) | LLM + RAG + CoT | 6 benchmark datasets | Performance vs SOTA | Outperforms SOTA | N/A | Needs more validation |
| Bauch 2026 (KIT) | LLM few-shot prompting | Inter-req traceability datasets | TLR performance | Few-shot improves slightly | N/A | Context effect varies by project |
| Alturayeif 2026 (TraceLLM) | 8 SOTA LLMs + prompt engineering | 4 benchmark datasets | F2 Score | SOTA F2, outperforms IR baselines | N/A | Prompt quality critical |
| Lin 2021 (T-BERT) | BERT Single + Siamese | 3 OSS projects issue-commit | MAP | +60.31% MAP over VSM | N/A | Data sparsity |
| IRRT 2022 (IEEE) | IR-based tool | Multiple datasets | Precision, Recall, F1 | Outperforms VSM/LSI | N/A | Chưa test CoEST |
| Evaluating IR Models 2021 (IEEE) | VSM, LSI, BM25 | Multiple req-to-code datasets | MAP, F1 | BM25 best overall | N/A | English-only |
| Comparison IR Techniques 2019 (IEEE) | VSM, LSI, BM25 | Multiple datasets | Precision, Recall, F1 | BM25 > LSI > VSM | N/A | Limited to English |
| MLTracer 2024 (IEEE) | ML + Gradient Boosting + IR | Multiple datasets | F1 | +15% F1 over IR baseline | N/A | Chưa dùng LLM |
| IR Bee Colony 2020 (IEEE) | IR + ABC optimization | Multiple datasets | Precision, Recall | Improves over VSM | N/A | Optimization overhead |
| Recovering Semantic TLR 2021 (IEEE) | IR + Semantic Features | Multiple datasets | Precision, Recall, F1 | Outperforms VSM/LSI | N/A | English-only |
| Al-Msie'Deen 2023 (IST) | IR-based VSM/LSI | OO software datasets | Precision, Recall | VSM competitive with LSI | N/A | Small projects only |
| Preda 2024 (ICSE) | IR + dependency analysis | Multiple datasets | Precision, Recall | Improves correctness | N/A | Requires dependency info |
| Alor 2025 (ACM) | GPT-4, Claude, Gemini | Doc-to-code datasets | F1, Precision, Recall | LLM outperforms IR | N/A | Cost of LLM API |
| Hey 2021 (ICSME) | VSM, LSI, BM25, fine-grained IR | iTrust, eTour, eANCI, SMOS | MAP, Precision, Recall | Fine-grained > coarse IR | github.com/tobhey/finegrained-traceability | English-only |
