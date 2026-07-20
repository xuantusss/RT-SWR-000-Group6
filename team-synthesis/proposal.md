# Research Proposal — RT-SWR-000-Group6

**Ngày:** 02/07/2026
**Nhóm:** RT-SWR-000-Group6
**GV hướng dẫn:** L.T.Q.Chi
**Môn:** SWR302 — Research-Based Learning

---

## 1. Tiêu đề

How effectively does GPT-4 zero-shot prompting generate 
class-level requirement-to-code traceability links in software 
projects, compared to IR-based automated methods (VSM, LSI, BM25) 
on CoEST public benchmark datasets?

---

## 2. Motivation

### 2.1 Bối cảnh

Requirement-to-code traceability là quá trình xác định mối liên 
hệ giữa requirements và các class trong source code. Đây là 
hoạt động quan trọng trong software engineering vì:

- Giúp engineer hiểu requirement nào được implement ở đâu
- Hỗ trợ impact analysis khi requirement thay đổi
- Cần thiết cho regression testing và maintenance

### 2.2 Vấn đề hiện tại

**IR-based methods (VSM, LSI, BM25):**
- Là phương pháp phổ biến nhất hiện nay
- Ổn định và có thể dự đoán được
- Bị giới hạn bởi semantic gap — chỉ match từ khóa, 
  bỏ sót requirement dùng từ khác nghĩa với class name
- MAP tốt nhất trên CoEST khoảng 0.55–0.65 (Ngo 2024)

**LLM-based methods:**
- Hiểu ngữ nghĩa tốt hơn IR
- GPT-4 + CoT đã vượt IR rõ ràng (Wang 2025: +125% MAP)
- Nhưng zero-shot thuần chưa được evaluate trên CoEST
- Có rủi ro hallucination — sinh link đến class không tồn tại

### 2.3 GAP từ evidence table (N = 27 paper)

| GAP | Bằng chứng |
|-----|-----------|
| GPT-4 zero-shot chưa test trên CoEST | 0/27 paper |
| Không có MAP@10 benchmark thống nhất | 0/27 paper |
| Cross-project variance chưa đo | 3/27 paper test đủ 3 project |
| Hallucination rate chưa định nghĩa | 0/27 paper |

---

## 3. Research Questions

### RQ1 — Hiệu năng
Do GPT-4 zero-shot generated traceability links achieve 
MAP@10 ≥ 0.70 and Recall ≥ 0.80 at class-level granularity 
on CoEST benchmark datasets, compared to the best-performing 
IR baseline among VSM, LSI, and BM25?

**Justify:**
- IR tốt nhất đạt MAP ~0.55–0.65 (Ngo 2024)
- Ngưỡng 0.70 = vượt IR rõ ràng, có ý nghĩa thực tế
- Recall ≥ 0.80 vì bỏ sót link nguy hiểm hơn link sai

### RQ2 — Generalization
Does GPT-4 zero-shot traceability performance generalize 
consistently across the 3 CoEST projects without prompt 
retuning, and how does its cross-project performance variance 
compare to IR-based methods?

**Justify:**
- Chỉ 3/27 paper test đủ 3 project CoEST
- LLM nhạy với domain — iTrust (healthcare), eTour (tourism), 
  EasyClinic (clinic) — 3 domain khác nhau
- IR thường ổn định hơn LLM across projects

### RQ3 — Reliability
What is the hallucination rate of GPT-4-generated traceability 
links (links to non-existent classes), and does few-shot 
prompting with example requirement-class pairs significantly 
reduce hallucination compared to zero-shot?

**Justify:**
- 0/27 paper định nghĩa hoặc đo hallucination rate
- IR không thể hallucinate → metric mới hoàn toàn
- Few-shot có thể giảm hallucination bằng cách cho ví dụ class thật

---

## 4. Methodology

### 4.1 Dataset

**CoEST Benchmark** — 3 project:

| Project | Domain | Số Req | Số Class | Ground Truth |
|---------|--------|--------|----------|-------------|
| iTrust | Healthcare | 34 | 100 | Có sẵn |
| eTour | Tourism | 42 | 83 | Có sẵn |
| EasyClinic | Clinic Mgmt | 51 | 74 | Có sẵn |
| **Tổng** | | **127** | **257** | **Có sẵn** |

Nguồn: CoEST public repository trên GitHub
License: Public, free for research use

### 4.2 IR Baseline Setup

**VSM (Vector Space Model):**
- Tool: sklearn TfidfVectorizer
- Similarity: cosine similarity
- Preprocessing: lowercase, remove stopwords, stemming

**LSI (Latent Semantic Indexing):**
- Tool: gensim
- Topics: 100 (theo Ngo 2024)
- Similarity: cosine similarity trên LSI space

**BM25 (Best Match 25):**
- Tool: rank_bm25
- Parameters: k1=1.5, b=0.75 (default)
- Preprocessing: tokenize, remove stopwords

### 4.3 LLM Setup

**Model:** GPT-4o (gpt-4o-2024-08-06)
**API:** OpenAI API
**Temperature:** 0 (deterministic)
**Max tokens:** 500

**Prompt template — Zero-shot (RQ1, RQ2):**
