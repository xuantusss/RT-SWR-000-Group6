# Research Proposal
## How Effectively Does GPT-4 Zero-Shot Prompting Generate 
## Class-Level Requirement-to-Source-Code Traceability Links 
## Compared to IR-Based Methods on CoEST Benchmark Datasets?

**Nhóm:** RT-SWR-000-Group6  
**Môn:** SWR302 — Research-Based Learning  
**GV hướng dẫn:** L.T.Q.Chi  
**Ngày:** 02/07/2026  
**Thành viên:**
- Nguyễn Xuân Bách — SE203114 (PL/RW)
- Trần Dương Minh Duy — SE203215 (DG)
- Nguyễn Trần Thái Duy Anh — SE205055 (LR)
- Vũ Lộc — SE182231 (MS)

---

## Abstract

Requirement-to-code traceability link recovery (RC-TLR) là 
một trong những hoạt động tốn kém nhất trong software 
maintenance. Các phương pháp Information Retrieval truyền 
thống (VSM, LSI, BM25) đã được nghiên cứu rộng rãi nhưng 
bị giới hạn bởi semantic gap. Sự xuất hiện của Large Language 
Models (LLM) mở ra hướng tiếp cận mới, tuy nhiên GPT-4 
zero-shot thuần chưa được evaluate có hệ thống trên CoEST 
benchmark. Đề tài này đề xuất so sánh trực tiếp GPT-4 
zero-shot với VSM, LSI, BM25 trên 3 project CoEST (iTrust, 
eTour, EasyClinic) theo 3 tiêu chí: hiệu năng (MAP@10, 
Recall, Precision, F1), độ ổn định cross-project, và 
hallucination rate — metric chưa được định nghĩa trong 
bất kỳ paper traceability nào trước đây.

---

## 1. Introduction

### 1.1 Bối cảnh và Tầm quan trọng

Requirement traceability là khả năng theo dõi vòng đời 
của một requirement từ lúc đặt ra đến khi được implement 
trong source code [Gotel & Finkelstein, 1994]. Trong thực 
tế, việc duy trì traceability links thủ công tốn 15-35% 
tổng chi phí phát triển phần mềm [Cleland-Huang et al., 2012].

Automated RC-TLR giải quyết vấn đề này bằng cách tự động 
xác định class nào implement requirement nào. Tuy nhiên, 
sau hơn 20 năm nghiên cứu, accuracy vẫn còn hạn chế do:

**Semantic gap:** Requirements thường được viết bằng ngôn 
ngữ business (ví dụ: "hệ thống phải cho phép bệnh nhân 
đặt lịch hẹn"), trong khi class name thường ngắn gọn 
về mặt kỹ thuật (ví dụ: AppointmentManager). IR methods 
chỉ match từ khóa nên dễ bỏ sót những cặp semantically 
related nhưng lexically different.

**Sự xuất hiện của LLM** — đặc biệt GPT-4 — mở ra khả 
năng bridge semantic gap này nhờ khả năng hiểu ngữ nghĩa 
sâu hơn. Tuy nhiên, LLM mang theo rủi ro mới: hallucination 
— sinh ra class name trông hợp lý nhưng không tồn tại 
trong codebase. Đây là rủi ro mà IR methods hoàn toàn 
không có vì chúng chỉ rank class đã có sẵn.

### 1.2 Motivation từ Literature

Phân tích 27 paper (2019–2026) cho thấy 3 xu hướng rõ ràng:

**Giai đoạn 2019–2020 — IR thuần:**
VSM, LSI, BM25 chiếm chủ yếu. Kết quả ổn định nhưng 
bị giới hạn bởi semantic gap. MAP tốt nhất trên CoEST 
khoảng 0.55–0.65 [Ngo, 2024].

**Giai đoạn 2021–2023 — ML Hybrid:**
Bắt đầu kết hợp ML với IR. BERT xuất hiện (T-BERT, 
Lin 2021: +60.31% MAP over VSM). Kết quả cải thiện 
nhưng vẫn cần fine-tuning tốn kém.

**Giai đoạn 2024–2026 — LLM:**
GPT-4 + CoT vượt IR rõ ràng (Wang 2025: +125.47% MAP 
over LSI). Nhưng zero-shot thuần — cách đơn giản và 
rẻ nhất — chưa ai test trên CoEST.

### 1.3 Problem Statement

Literature cho thấy LLM có tiềm năng vượt IR nhưng 
còn 3 câu hỏi chưa được trả lời:

1. GPT-4 zero-shot thuần — không CoT, không RAG — 
   có đủ tốt hơn IR không?
2. GPT-4 có ổn định across 3 project CoEST khác domain 
   mà không cần retune prompt không?
3. GPT-4 có hallucinate class không tồn tại không, 
   và ở mức độ nào?

---

## 2. Related Work

### 2.1 IR-Based Traceability Methods

IR-based methods là nhóm được nghiên cứu nhiều nhất 
trong RC-TLR, chiếm 10/27 paper trong SLR của nhóm.

**Vector Space Model (VSM)** đại diện requirement và 
class dưới dạng TF-IDF vectors, tính cosine similarity 
để rank. VSM đơn giản, hiệu quả nhưng hoàn toàn dựa 
trên lexical matching [Ali et al., 2019].

**Latent Semantic Indexing (LSI)** cải thiện VSM bằng 
cách dùng SVD decomposition để tìm latent semantic 
relationships. LSI có thể match synonyms nhưng vẫn 
bị giới hạn bởi training corpus [Hey et al., 2021].

**BM25** là probabilistic IR model cải thiện TF-IDF 
với term frequency saturation và document length 
normalization. Ngo 2024 cho thấy BM25 thường outperforms 
VSM và LSI trên CoEST benchmark.

**Hạn chế chung:** Tất cả IR methods bị giới hạn bởi 
vocabulary mismatch — không thể match requirement và 
class khi chúng dùng từ khác nhau để mô tả cùng 1 
concept. Đây là lý do MAP tốt nhất của IR trên CoEST 
chỉ đạt ~0.65 sau hơn 20 năm nghiên cứu.

### 2.2 ML-Based và Hybrid Methods

**T-BERT** (Lin et al., 2021) dùng BERT để encode 
requirement và code, tạo ra semantic embeddings tốt 
hơn IR. Đạt +60.31% MAP improvement over VSM trên 
issue-commit traceability. Tuy nhiên cần fine-tuning 
tốn kém và không test trên CoEST.

**MLTracer** (2024) kết hợp ML với IR, đạt +15% F1 
over IR baseline. Vẫn dùng IR làm foundation, không 
tận dụng được LLM capabilities.

**Data Balancing + ML** (Wang et al., 2023) test trên 
CoEST 7 datasets bao gồm EasyClinic. Kết quả tốt 
nhưng không dùng LLM.

### 2.3 LLM-Based Methods

**CoT Prompting** (Wang et al., 2025) là paper gần 
nhất với đề tài, dùng GPT-4 + Chain-of-Thought + SimCSE 
trên iTrust, eTour, eANCI, SMOS. Đạt MAP +125.47% 
over LSI. Tuy nhiên CoT và SimCSE là 2 kỹ thuật bổ sung 
— không phải zero-shot thuần.

**LiSSA** (Fuchß et al., 2025) dùng RAG pipeline với 
GPT-4o, outperforms SOTA trên req-to-code tasks. RAG 
phức tạp hơn zero-shot đáng kể.

**TraceLLM** (Alturayeif et al., 2026) evaluate 8 SOTA 
LLMs với prompt engineering trên 4 benchmark datasets. 
Đạt SOTA F2 score, outperforms IR và fine-tuned models. 
Tuy nhiên không test trên CoEST và không dùng zero-shot 
thuần.

**Hassine 2024** dùng GPT-3.5 zero-shot cho security 
requirements traceability. Là paper gần nhất với RQ3 
nhưng dùng GPT-3.5 (không phải GPT-4) và không dùng 
CoEST dataset.

### 2.4 Tổng hợp GAP

| Dimension | Literature | GAP |
|-----------|-----------|-----|
| Model | GPT-4 + CoT/RAG | GPT-4 zero-shot thuần |
| Dataset | iTrust hoặc eTour (riêng lẻ) | Cả 3 CoEST cùng lúc |
| Metric | MAP, F1, Precision, Recall | MAP@10 + hallucination rate |
| Evaluation | Single project | Cross-project variance |

---

## 3. Research Questions và Hypotheses

### RQ1 — Hiệu năng

**Câu hỏi:** Do GPT-4 zero-shot generated traceability 
links achieve MAP@10 ≥ 0.70 and Recall ≥ 0.80 at 
class-level granularity on CoEST benchmark datasets, 
compared to the best-performing IR baseline among 
VSM, LSI, and BM25?

**Hypotheses:**
- H0₁: MAP@10(GPT-4) ≤ MAP@10(IR_best)
- H1₁: MAP@10(GPT-4) > MAP@10(IR_best)
- H0₁ᵣ: Recall(GPT-4) ≤ 0.80
- H1₁ᵣ: Recall(GPT-4) > 0.80

**Tại sao ngưỡng 0.70 và 0.80:**
- MAP@10 ≥ 0.70: vượt IR best (~0.65) một khoảng 
  có ý nghĩa thực tế — engineer có lý do để chuyển 
  từ IR sang GPT-4
- Recall ≥ 0.80: trong traceability, bỏ sót link 
  (false negative) nguy hiểm hơn link sai (false 
  positive) vì engineer cần tìm đủ class liên quan

### RQ2 — Generalization

**Câu hỏi:** Does GPT-4 zero-shot traceability 
performance generalize consistently across the 3 
CoEST projects without prompt retuning, and how 
does its cross-project performance variance compare 
to IR-based methods?

**Hypotheses:**
- H0₂: CV(GPT-4) ≥ CV(IR_best) 
  [GPT-4 không ổn định hơn IR]
- H1₂: CV(GPT-4) < CV(IR_best) 
  [GPT-4 ổn định hơn IR across projects]

Trong đó CV = Coefficient of Variation = σ/μ

**Tại sao RQ2 quan trọng:**
GPT-4 rất nhạy với domain. iTrust (healthcare), 
eTour (tourism), EasyClinic (clinic) là 3 domain 
khác nhau. Kết quả tốt trên 1 project không đảm 
bảo tốt trên project khác mà không retune prompt.

### RQ3 — Reliability

**Câu hỏi:** What is the hallucination rate of 
GPT-4-generated traceability links (links to 
non-existent classes), and does few-shot prompting 
with example requirement-class pairs significantly 
reduce hallucination compared to zero-shot?

**Hypotheses:**
- H0₃: HR(zero-shot) = HR(few-shot)
  [Few-shot không giảm hallucination]
- H1₃: HR(zero-shot) > HR(few-shot)
  [Few-shot giảm hallucination có ý nghĩa]

Trong đó HR = Hallucination Rate

**Tại sao RQ3 là contribution mới:**
IR methods có HR = 0% vì chỉ rank class có sẵn. 
LLM có thể sinh class name không tồn tại — rủi ro 
thực tế chưa được đo trong bất kỳ paper nào. 
Nhóm đề xuất đây là lần đầu tiên định nghĩa và 
đo metric này trong RC-TLR literature.

---

## 4. Methodology

### 4.1 PICO Framework

| Element | Nội dung |
|---------|---------|
| **P** (Population) | Requirement-to-code trace datasets từ CoEST benchmark: iTrust, eTour, EasyClinic |
| **I** (Intervention) | GPT-4o zero-shot prompting (gpt-4o-2024-08-06, temperature=0) |
| **C** (Comparison) | IR-based methods: VSM (TF-IDF cosine), LSI (gensim, 100 topics), BM25 (rank_bm25) |
| **O** (Outcome) | MAP@10, Recall, Precision, F1, Hallucination Rate, Cross-project CV |

### 4.2 Dataset

**CoEST Benchmark** — 3 project:

| Project | Domain | Req | Classes | Links | Ground Truth |
|---------|--------|-----|---------|-------|-------------|
| iTrust | Healthcare | 34 | 100 | 239 | Có sẵn |
| eTour | Tourism | 42 | 83 | 167 | Có sẵn |
| EasyClinic | Clinic Mgmt | 51 | 74 | 203 | Có sẵn |
| **Tổng** | | **127** | **257** | **609** | **Có sẵn** |

**Tại sao chọn CoEST:**
- Public, free for research use
- Ground truth có sẵn — không cần annotation
- Được dùng bởi 15/27 paper trong SLR — kết quả 
  có thể so sánh với literature
- 3 domain khác nhau — phù hợp để đo cross-project 
  variance (RQ2)

### 4.3 Preprocessing Pipeline
