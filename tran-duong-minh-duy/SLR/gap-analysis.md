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
nên không thể so sánh kết quả với nhau.

**Bằng chứng từ evidence table:**
- Cột Metric: 0/27 paper dùng MAP@10 làm metric chính
- Cột Dataset: mỗi paper test trên dataset khác nhau
- Ngo 2024 dùng MAP nhưng không phải MAP@10, và không test 
  đủ 3 project CoEST cùng lúc
- Comparison IR Techniques 2019 so sánh VSM/LSI/BM25 nhưng 
  không dùng CoEST

---

## 2. Kiểm tra phản chứng

| Paper | Đã làm GAP này không? | Chi tiết |
|-------|----------------------|---------|
| Ngo 2024 | Có (một phần) | Dùng MAP nhưng không phải MAP@10, không test EasyClinic |
| Comparison IR 2019 | Có (một phần) | So sánh VSM/LSI/BM25 nhưng không dùng CoEST |
| Hey 2021 | Không | Dùng MAP nhưng chỉ fine-grained IR, không so sánh VSM/LSI/BM25 |
| Wang 2023 | Không | ML classifiers, không phải VSM/LSI/BM25 |
| Ali 2019 | Không | IR + POS, không so sánh 3 methods trên CoEST |
| IRRT 2022 | Không | IR tool nhưng không so sánh VSM/LSI/BM25 trực tiếp |
| Evaluating IR 2021 | Có (một phần) | So sánh IR methods nhưng không dùng CoEST |
| MLTracer 2024 | Không | ML + IR hybrid, không phải VSM/LSI/BM25 thuần |

**Kết luận:** GAP xác nhận ✅ — không paper nào so sánh 
VSM/LSI/BM25 trên cả 3 project CoEST với MAP@10

### Supplementary Validation

| Lớp | Hành động | Kết quả |
|-----|-----------|--------|
| L1 Targeted search | "VSM" AND "LSI" AND "BM25" AND "CoEST" AND "MAP@10" — Scholar + IEEE — 02/07/2026 | 0 kết quả relevant |
| L2 Forward snowball | Cite Ngo 2024 — 6 papers checked | 0 paper so sánh đủ 3 methods trên CoEST với MAP@10 |
| L3 Survey anchor | Alturayeif 2026 TraceLLM N=4 benchmark | Không đề cập MAP@10 cho IR methods trên CoEST |

→ **Kết luận: GAP confirmed ✅**

---

## 3. Feasibility Check

| Tiêu chí | Mức | Ghi chú |
|---------|-----|---------|
| Dataset | ✅ | CoEST public — iTrust, eTour, EasyClinic tải được ngay |
| API/Tool | ✅ | VSM/LSI/BM25 implement bằng sklearn, không cần API |
| Tính toán | ✅ | CPU laptop đủ, không cần GPU |
| Ground truth | ✅ | CoEST có ground truth sẵn |
| Code base | ✅ | sklearn TfidfVectorizer, gensim LSI, rank_bm25 — thư viện có sẵn |
| Kỹ năng | ✅ | IR methods đơn giản, implement trong 1-2 ngày |
| Thời gian | ✅ | Xong trước deadline với ≥ 1 tuần dự phòng |

**Kết quả:** 0 ❌ / 0 ⚠️ → **An toàn**

---

## 4. Phát biểu GAP chính thức

Chưa có nghiên cứu nào so sánh trực tiếp VSM, LSI, BM25 (I) 
trên cùng 3 project CoEST gồm iTrust, eTour, EasyClinic (D) 
với MAP@10 làm metric chính (O) — thiếu IR baseline chuẩn 
để so sánh với LLM-based approaches.

---

## 5. Đề xuất sơ bộ cho nhóm

**Dataset khả thi:** CoEST benchmark — iTrust, eTour, EasyClinic 
— public trên GitHub, ground truth có sẵn

**Metric đề xuất:** MAP@10 (metric chính), Precision@10, 
Recall, F1 — đồng nhất với metric của RQ1 để so sánh trực tiếp

**LLM/Tool đề xuất:** VSM (TF-IDF cosine), LSI (gensim, 
100 topics), BM25 (rank_bm25) — chạy trên cùng 3 project CoEST

**Baseline đề xuất:** Ngo 2024 làm reference — MAP ~0.55–0.65 
trên CoEST datasets
