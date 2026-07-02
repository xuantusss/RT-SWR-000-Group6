# Evidence Table — CoEST Benchmark and Evaluation for Traceability

N = 9 paper included

| Paper | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế |
|-------|----------|---------|--------|---------|------|---------|
| Ngo 2024 (JSS) DOI:10.1016/j.jss.2024.112056 | VSM, LSI, BM25, FTLR, TAROT, CRT | CoEST: iTrust, eTour, eANCI, SMOS + 9 others | MAP, Precision, Recall, F1 | FTLR/CRT/TAROT best on CoEST; BM25 competitive | N/A | Không include LLM-based methods |
| Hey 2023 (Zenodo) DOI:10.5281/zenodo.7867845 | VSM, LSI, BM25, FTLR | iTrust, eTour, eANCI, SMOS | MAP, F1 | FTLR outperforms VSM/LSI/BM25 on all 4 datasets | github.com/tobhey/finegrained-traceability | Chưa test LLM, chỉ IR methods |
| Hey 2021 (ICSME) DOI:10.1109/ICSME52107.2021.00034 | VSM, LSI, BM25, fine-grained IR | iTrust, eTour, eANCI, SMOS | MAP, Precision, Recall | Fine-grained > coarse-grained IR trên 4 datasets | github.com/tobhey/finegrained-traceability | English-only, 4 projects chưa đủ đa dạng |
| Wang 2023 (IJCNN) DOI:10.1109/IJCNN54540.2023.10191386 | ML classifiers + DBT (SVM, KNN, LR) | CoEST 7 datasets incl. EasyClinic | Precision, Recall | LR recall +0.5517 với DBT trên EasyClinic | N/A | Không dùng LLM, chỉ ML truyền thống |
| Zhao 2020 (AIRE) DOI:10.1109/AIRE51212.2020.00010 | TLR-KRL (Knowledge Representation) | eTour, eANCI, Clinic, iTrust | Precision, Recall | Outperforms IR methods trên 4 datasets | N/A | Extended abstract, kết quả chưa đầy đủ |
| Li 2020 (Applied Sciences) DOI:10.3390/app10207253 | ML + Logical Reasoning + VSM/LSI | Multiple datasets | Precision, Recall | Improves over pure IR baseline | N/A | Dataset nhỏ, chưa test CoEST đầy đủ |
| Zhao 2026 (Information) DOI:10.3390/info17060541 | GraphRAG, LLM zero-shot | RC-TLR datasets | Precision, Recall | Outperforms IR baselines | N/A | Chưa test cross-project variance |
| Hey 2024 (RE) DOI:10.1109/RE59067.2024.00024 | NoRBERT (BERT-based) | iTrust, eTour, SMOS, eANCI | F1 | F1 >90% trên iTrust/eTour | N/A | External validity: chỉ 4 dataset |
| Rodriguez 2020 (IEEE) DOI:10.1109/EIT48999.2020.9208233 | VSM, LSI, BM25, NSGA-II | Multiple datasets | Precision, Recall | NSGA-II optimization improves IR | N/A | Optimization overhead, chưa test CoEST |
