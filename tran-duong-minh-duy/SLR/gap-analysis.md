# GAP Analysis — Không Có Benchmark Thống Nhất So Sánh VSM/LSI/BM25 Với MAP@10

**Thành viên:** Trần Dương Minh Duy
**GAP type:** GAP-M
**Ngày:** 02/07/2026
**Evidence table nguồn:** team-synthesis/evidence-table-merged.md (N = 27 paper)

---

## 1. Mô tả GAP

Chưa có nghiên cứu nào so sánh trực tiếp VSM, LSI, BM25 trên 
cùng 3 project CoEST (iTrust, eTour, EasyClinic) với MAP@10 
làm metric chính. Mỗi paper dùng dataset và metric khác nhau 
nên không thể so sánh kết quả với nhau hoặc với LLM-based 
approaches.

**Bằng chứng từ evidence table:**
- Cột Metric: 0/27 paper dùng MAP@10 làm metric chính
- Cột Dataset: mỗi paper test trên dataset khác nhau
- Ngo 2024 dùng MAP nhưng không phải MAP@10, không test 
  EasyClinic
- Comparison IR Techniques 2019 so sánh VSM/LSI/BM25 nhưng 
  không dùng CoEST

**Pattern quan sát từ evidence table:**

| Paper | VSM | LSI | BM25 | CoEST đầy đủ | MAP@10 |
|-------|-----|-----|------|-------------|--------|
| Ngo 2024 | ✅ | ✅ | ✅ | ❌ (thiếu EasyClinic) | ❌ |
| Comparison IR 2019 | ✅ | ✅ | ✅ | ❌ (không CoEST) | ❌ |
| Evaluating IR 2021 | ✅ | ✅ | ✅ | ❌ (không CoEST) | ❌ |
| Hey 2021 | ✅ | ✅ | ✅ | ⚠️ (thiếu EasyClinic) | ❌ (dùng MAP, không MAP@10) |
| **Nhóm đề xuất** | **✅** | **✅** | **✅** | **✅** | **✅** |

---

## 2. Kiểm tra phản chứng

| Paper | Đã làm GAP này không? | Chi tiết |
|-------|----------------------|---------|
| Ngo 2024 | Có (một phần) | Dùng MAP nhưng không MAP@10, thiếu EasyClinic |
| Comparison IR 2019 | Có (một phần) | So sánh VSM/LSI/BM25 nhưng không dùng CoEST |
| Hey 2021 | Có (một phần) | So sánh cả VSM, LSI, BM25 làm baseline rồi mới đề xuất fine-grained IR cải tiến thêm — nhưng dùng MAP (không phải MAP@10) và thiếu EasyClinic (chỉ có iTrust, eTour, eANCI, SMOS) → chưa phủ đủ GAP về metric và dataset |
| Wang 2023 | Không | ML classifiers, không phải VSM/LSI/BM25 |
| Ali 2019 | Không | IR + POS, không so sánh 3 methods trên CoEST |
| IRRT 2022 | Không | IR tool nhưng không so sánh VSM/LSI/BM25 trực tiếp |
| Evaluating IR 2021 | Có (một phần) | So sánh IR methods nhưng không dùng CoEST |
| MLTracer 2024 | Không | ML + IR hybrid, không phải VSM/LSI/BM25 thuần |

**Phân tích chi tiết 4 paper "có một phần":**

- **Ngo 2024**: So sánh nhiều IR methods nhưng dùng MAP 
  (không phải MAP@10) và không test EasyClinic → thiếu 
  cả metric lẫn dataset để phủ GAP này

- **Comparison IR 2019**: So sánh đúng 3 methods VSM/LSI/BM25 
  nhưng trên dataset không phải CoEST → không thể dùng 
  kết quả để so sánh với LLM trên CoEST

- **Evaluating IR 2021**: So sánh IR methods nhưng trên 
  dataset khác CoEST → cùng vấn đề với Comparison IR 2019

- **Hey 2021**: So sánh đúng cả 3 methods VSM/LSI/BM25 trên gần đủ CoEST 
  (thiếu EasyClinic) — đây là phản chứng gần sát nhất, nhưng vẫn không 
  phủ GAP hoàn toàn vì (1) dùng MAP thay vì MAP@10, và (2) thiếu 1/3 
  project CoEST → GAP vẫn hợp lệ nhưng ở phạm vi hẹp hơn ("chưa ai làm 
  đủ cả 3 project VÀ đúng MAP@10 cùng lúc")

**Kết luận:** GAP xác nhận ✅ — không paper nào so sánh 
VSM/LSI/BM25 trên cả 3 project CoEST (đủ cả iTrust, eTour, EasyClinic) 
với MAP@10 làm metric chính

### Supplementary Validation

| Lớp | Hành động | Kết quả |
|-----|-----------|--------|
| L1 Targeted search | "VSM" AND "LSI" AND "BM25" AND "CoEST" AND "MAP@10" — Scholar + IEEE — 02/07/2026 | 0 kết quả relevant |
| L2 Forward snowball | Cite Ngo 2024 — 6 papers checked | 0 paper so sánh đủ 3 methods trên CoEST với MAP@10 |
| L3 Survey anchor | Alturayeif 2026 TraceLLM SLR N=4 benchmark | Không đề cập MAP@10 cho IR methods trên CoEST |

→ **Kết luận: GAP confirmed ✅**

---

## 3. Feasibility Check

| Tiêu chí | Mức | Ghi chú |
|---------|-----|---------|
| Dataset | ✅ | CoEST public — iTrust (34 req, 100 classes), eTour (42 req, 83 classes), EasyClinic (51 req, 74 classes) tải được ngay |
| API/Tool | ✅ | VSM: sklearn TfidfVectorizer. LSI: gensim (100 topics). BM25: rank_bm25. Tất cả miễn phí, không cần API key |
| Tính toán | ✅ | CPU laptop đủ, không cần GPU — IR methods nhẹ |
| Ground truth | ✅ | CoEST có ground truth sẵn cho cả 3 project |
| Code base | ✅ | sklearn + gensim + rank_bm25 — implement trong 1-2 ngày, không cần code từ đầu |
| Kỹ năng | ✅ | IR methods đơn giản, thư viện có documentation tốt |
| Thời gian | ✅ | Xong trước deadline với ≥ 1 tuần dự phòng |

**Kết quả:** 0 ❌ / 0 ⚠️ → **An toàn**

---

## 4. Phát biểu GAP chính thức

Chưa có nghiên cứu nào so sánh trực tiếp VSM, LSI, BM25 (I) 
trên cùng 3 project CoEST gồm iTrust, eTour, EasyClinic (D) 
với MAP@10 làm metric chính (O) — thiếu IR baseline chuẩn 
để so sánh công bằng với GPT-4 zero-shot trong cùng điều kiện 
thực nghiệm.

---

## 5. Đề xuất sơ bộ cho nhóm

**Dataset khả thi:**
CoEST benchmark — iTrust, eTour, EasyClinic — public trên 
GitHub, ground truth có sẵn, được dùng bởi 15/27 paper 
trong SLR

**Metric đề xuất:**
MAP@10 (metric chính), Precision@10, Recall, F1 — 
đồng nhất với metric của RQ1 để so sánh trực tiếp 
GPT-4 vs IR

**Tool đề xuất:**
- VSM: TF-IDF cosine similarity (sklearn)
- LSI: Latent Semantic Indexing 100 topics (gensim)
- BM25: Best Match 25 (rank_bm25)
Chạy trên cùng 3 project CoEST với cùng ground truth

**Baseline đề xuất:**
Ngo 2024 làm reference — MAP ~0.55–0.65 trên CoEST datasets

**Mapping sang RQ:**
- So sánh VSM/LSI/BM25 → xác định IR baseline tốt nhất → 
  dùng làm đối chiếu trong RQ1
- Chạy trên 3 project → đo cross-project variance của IR → 
  so sánh với LLM variance trong RQ2

