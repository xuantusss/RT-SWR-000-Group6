**Output parsing:**
```python
def parse_output(raw_output, valid_classes):
    lines = raw_output.strip().split('\n')
    predicted = []
    hallucinated = []
    for line in lines:
        class_name = line.strip()
        if class_name in valid_classes:
            predicted.append(class_name)
        else:
            hallucinated.append(class_name)
    return predicted, hallucinated
```

**Error handling:**
- Empty response → log as invalid, exclude từ metric
- API timeout → retry 3 lần với exponential backoff
- Rate limit → sleep 60s rồi retry

### 4.6 Metrics Implementation

**MAP@10:**
```python
def mean_average_precision(ranked_lists, ground_truth, k=10):
    aps = []
    for req_id, ranked in ranked_lists.items():
        relevant = ground_truth[req_id]
        ap = average_precision(ranked[:k], relevant)
        aps.append(ap)
    return np.mean(aps)
```

**Hallucination Rate:**
```python
def hallucination_rate(outputs, valid_classes):
    total_links = 0
    hallucinated_links = 0
    for output in outputs:
        predicted, hallucinated = parse_output(output, valid_classes)
        total_links += len(predicted) + len(hallucinated)
        hallucinated_links += len(hallucinated)
    return hallucinated_links / total_links if total_links > 0 else 0
```

**Cross-project CV:**
```python
def coefficient_of_variation(scores_per_project):
    mean = np.mean(scores_per_project)
    std = np.std(scores_per_project)
    return std / mean if mean > 0 else 0
```

### 4.7 Statistical Testing

**Test:** Wilcoxon signed-rank test
**Tại sao:** Không giả định normal distribution — 
phù hợp với score distributions trong IR/NLP

**Cho RQ1:**
```python
from scipy.stats import wilcoxon
stat, p_value = wilcoxon(gpt4_scores, ir_best_scores)
```

**Effect size:** Cohen's d
```python
def cohens_d(group1, group2):
    pooled_std = np.sqrt((np.std(group1)**2 + 
                          np.std(group2)**2) / 2)
    return (np.mean(group1) - np.mean(group2)) / pooled_std
```

**Significance level:** α = 0.05
**Interpretation:**
- p < 0.05 → reject H0
- |d| < 0.2: negligible effect
- 0.2 ≤ |d| < 0.5: small effect
- 0.5 ≤ |d| < 0.8: medium effect
- |d| ≥ 0.8: large effect

### 4.8 Experimental Protocol

**Bước 1 — Pilot (Tuần 7, iTrust, N=34 req):**
- Random seed: 42
- Chạy thử tất cả methods trên iTrust
- Kiểm tra: API hoạt động, metric tính được, 
  output parseable, cost trong budget
- Gate: nếu pilot fail → báo GV trong 24h

**Bước 2 — Full Experiment (Tuần 8):**
- Chạy trên cả 3 project: iTrust, eTour, EasyClinic
- Temperature = 0 (deterministic)
- Log đầy đủ: model version, timestamp, cost/call, 
  raw output, parsed output

**Bước 3 — Analysis (Tuần 8–9):**
- Tính metrics cho từng project
- Chạy statistical tests
- Tính effect sizes
- Vẽ figures

---

## 5. Phân công và Roles

| Role | Người | Trách nhiệm chi tiết |
|------|-------|---------------------|
| PL/RW | Nguyễn Xuân Bách | Điều phối timeline, viết §1 Intro + §7 Conclusion + §6 Threats, tạo figures, format tài liệu, submit GV |
| DG | Trần Dương Minh Duy | Download CoEST datasets, verify ground truth, implement IR methods (VSM/LSI/BM25), tạo pilot_sample.csv |
| LR | Nguyễn Trần Thái Duy Anh | Setup OpenAI API, viết run_experiment.py, log cost/call, chạy zero-shot và few-shot experiments |
| MS | Vũ Lộc | Implement MAP@10, hallucination rate, Wilcoxon test, Cohen's d, vẽ boxplot/violin figures |

**Nguyên tắc bắt buộc:** LR (Thái Duy Anh) và MS 
(Vũ Lộc) không được là cùng 1 người.

---

## 6. Timeline

| Tuần | Hoạt động | Owner | Output |
|------|-----------|-------|--------|
| 5–6 | Viết + nộp proposal | Minh Duy (PL) | proposal.md |
| 6 | GV duyệt proposal | GV | Approved/feedback |
| 7 | Download CoEST, setup API, pilot | DG + LR | pilot_analysis.ipynb |
| 7 | Implement metrics, verify pilot | MS | compute_metric.py |
| 8 | Full experiment 3 project | LR | full_llm_output.csv |
| 8 | Statistical analysis | MS | full_analysis.ipynb |
| 9 | Viết paper | RW + tất cả | report.md |
| 10 | Trình bày | Tất cả | slides_final.pdf |

**Hard deadline:** Proposal GV duyệt trước cuối 
Tuần 6. Nếu chưa duyệt → Downscope Protocol: 
chỉ làm RQ1, bỏ RQ2 và RQ3.

---

## 7. Expected Outputs

**Deliverables:**
- Traceability link generation tool với documented 
  prompt templates (zero-shot và few-shot)
- Benchmark evaluation report covering 3 CoEST 
  projects (iTrust, eTour, EasyClinic)
- Kết quả per project: MAP@10, Recall, Precision, 
  F1, Hallucination Rate
- Statistical comparison: p-value, effect size 
  GPT-4 vs IR best
- Cross-project variance analysis: CV của GPT-4 
  vs VSM/LSI/BM25

**Scientific contribution:**
- First evaluation of GPT-4 zero-shot on CoEST 
  benchmark
- First definition and measurement of hallucination 
  rate in RC-TLR literature
- Reproducible experiment với public dataset, 
  documented prompt templates, open-source code

---

## 8. Threats to Validity

### 8.1 Internal Validity
**Threat:** Temperature setting ảnh hưởng kết quả
**Mitigation:** Temperature = 0 cho deterministic 
output — chạy lại cùng input cho cùng output

**Threat:** Prompt wording ảnh hưởng GPT-4 output
**Mitigation:** Cùng 1 prompt template cho tất cả 
3 project, không retune giữa các project (đúng 
tinh thần zero-shot)

**Threat:** IR preprocessing ảnh hưởng kết quả
**Mitigation:** Dùng settings chuẩn từ literature 
(Ngo 2024) — Porter Stemmer, NLTK stopwords, 
BM25 k1=1.5 b=0.75

### 8.2 External Validity
**Threat:** Chỉ test trên Java projects
**Mitigation:** Ghi rõ limitation — CoEST chỉ 
có Java projects, kết quả có thể khác với Python 
hay C++ projects

**Threat:** Chỉ dùng GPT-4o — kết quả có thể 
khác với GPT-3.5, Claude, Gemini
**Mitigation:** Ghi rõ model version 
(gpt-4o-2024-08-06), log API response để 
reproducible

### 8.3 Construct Validity
**Threat:** MAP@10 có thể không phản ánh 
real-world usage
**Mitigation:** Bổ sung Recall, Precision, F1 
— bộ metrics đầy đủ theo literature

**Threat:** Hallucination rate là metric mới, 
chưa có định nghĩa chuẩn
**Mitigation:** Định nghĩa rõ ràng trong 
Section 4.6 — bất kỳ class name không có 
trong CoEST class list = hallucinated

### 8.4 Conclusion Validity
**Threat:** N = 127 req có đủ statistical power không?
**Mitigation:** Wilcoxon signed-rank test phù hợp 
cho small-to-medium sample. Effect size Cohen's d 
đo practical significance độc lập với sample size.

**Threat:** Multiple comparisons (3 RQ, 3 projects)
**Mitigation:** Bonferroni correction nếu cần — 
α = 0.05/3 = 0.017 cho multiple RQ tests

---

## 9. Budget

| Hạng mục | Tính toán | Chi phí |
|---------|-----------|--------|
| Pilot zero-shot | 34 req × 600 tokens × $0.005/1K | $0.10 |
| Full zero-shot | 127 req × 600 tokens × $0.005/1K | $0.38 |
| Full few-shot (RQ3) | 127 req × 900 tokens × $0.005/1K | $0.57 |
| Buffer 50% | | $0.53 |
| **Tổng** | | **~$1.58** |

---

## 10. References

[Ali et al., 2019] Ali, N., Cai, H., Hamou-Lhadj, A., 
& Hassine, J. (2019). Exploiting Parts-of-Speech for 
effective automated requirements traceability. 
Information and Software Technology, 106, 126-141.

[Alturayeif et al., 2026] Alturayeif, N. et al. (2026). 
TraceLLM: Leveraging LLMs for Traceability Link Recovery. 
arXiv:2602.01253.

[Fuchß et al., 2025] Fuchß, D. et al. (2025). LiSSA: 
Toward Generic Traceability Link Recovery Through 
Retrieval-Augmented Generation. ICSE 2025.

[Hey et al., 2024] Hey, T. et al. (2024). Requirements 
Classification for Traceability Link Recovery. RE 2024.

[Lin et al., 2021] Lin, B. et al. (2021). T-BERT: 
BERT for Issue-Commit Traceability. arXiv:2102.04411.

[Ngo et al., 2024] Ngo, V. et al. (2024). Empirical 
Study of SOTA Requirement-to-Code Traceability Methods. 
Journal of Systems and Software, 112056.

[Wang et al., 2025] Wang, X. et al. (2025). Enhancing 
R2C Traceability via CoT Prompting. APSEC 2025.

[Zhao & Xu, 2026] Zhao, Z. & Xu, X. (2026). GraphRAG 
Dual-Path RC-TLR. Information, 17(6), 541.
