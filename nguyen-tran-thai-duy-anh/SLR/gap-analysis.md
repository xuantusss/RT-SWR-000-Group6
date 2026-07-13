# GAP Analysis — Cross-Project Variance Của LLM Chưa Được Đo

**Thành viên:** Nguyễn Trần Thái Duy Anh
**GAP type:** GAP-D
**Ngày:** 02/07/2026
**Evidence table nguồn:** team-synthesis/evidence-table-merged.md (N = 27 paper)

---

## 1. Mô tả GAP

Chưa có nghiên cứu nào kiểm tra LLM có generalize được across 
3 project CoEST (iTrust, eTour, EasyClinic) mà không retune 
prompt. Hầu hết paper chỉ test 1-2 project và không đo 
cross-project variance.

**Bằng chứng từ evidence table:**
- Cột Dataset: chỉ 3/27 paper test đủ cả 3 project CoEST
- Wang 2025 test 4 dataset nhưng không đo variance giữa projects
- Alturayeif 2026 test 4 benchmark nhưng không phải CoEST và 
  không đo cross-project stability
- 0/27 paper báo cáo standard deviation hoặc variance 
  across projects

---

## 2. Kiểm tra phản chứng

| Paper | Đã làm GAP này không? | Chi tiết |
|-------|----------------------|---------|
| Wang 2025 | Không | Test 4 dataset nhưng không đo cross-project variance |
| Alturayeif 2026 | Không | 4 benchmark nhưng không phải CoEST, không đo variance |
| Hey 2025 | Không | 6 benchmark datasets (LLM + RAG + CoT), không đo cross-project variance — không phải inter-req traceability (đó là đặc điểm của Bauch 2026, không phải Hey 2025) |
| Bauch 2026 | Có (một phần) | Đề cập context effect varies by project nhưng không đo variance |
| Shah 2025 | Không | Chỉ 1 dataset, không cross-project |
| Zhang 2025 | Không | Evidence table ghi rõ "Generalization not tested" — paper này chưa hề đo generalization, càng củng cố GAP |
| Lin 2021 | Không | 3 OSS projects nhưng issue-commit, không req-to-code |
| Ngo 2024 | Không | IR methods, không LLM |
| Hey 2024 | Không | 4 dataset nhưng không đo variance |

**Kết luận:** GAP xác nhận ✅ — không paper nào đo 
cross-project variance của LLM trên CoEST

### Supplementary Validation

| Lớp | Hành động | Kết quả |
|-----|-----------|--------|
| L1 Targeted search | "LLM" AND "traceability" AND "cross-project" AND "variance" — Scholar + IEEE — 02/07/2026 | 0 kết quả relevant |
| L2 Forward snowball | Cite Wang 2025 — 8 papers checked | 0 paper đo cross-project variance trên CoEST |
| L3 Survey anchor | Alturayeif 2026 TraceLLM N=4 benchmark | Không đề cập cross-project variance measurement |

→ **Kết luận: GAP confirmed ✅**

---

## 3. Feasibility Check

| Tiêu chí | Mức | Ghi chú |
|---------|-----|---------|
| Dataset | ✅ | CoEST public — iTrust, eTour, EasyClinic tải được ngay |
| API/Tool | ✅ | GPT-4 API có sẵn, free tier đủ cho pilot |
| Tính toán | ✅ | Chỉ gọi API, không cần GPU |
| Ground truth | ✅ | CoEST có ground truth sẵn cho cả 3 project |
| Code base | ✅ | Reuse script từ RQ1, chỉ thêm bước tính variance |
| Kỹ năng | ✅ | Tính standard deviation, coefficient of variation — cơ bản |
| Thời gian | ✅ | Chạy song song với RQ1 trên 3 project — không tốn thêm thời gian |

**Kết quả:** 0 ❌ / 0 ⚠️ → **An toàn**

---

## 4. Phát biểu GAP chính thức

Chưa có nghiên cứu nào đo cross-project variance của GPT-4 
zero-shot (I) khi sinh requirement-to-code traceability links (P) 
across 3 project CoEST gồm iTrust, eTour, EasyClinic (D) 
mà không retune prompt giữa các project (O) — chưa biết 
LLM có generalize được hay chỉ tốt trên 1 project cụ thể.

---

## 5. Đề xuất sơ bộ cho nhóm

**Dataset khả thi:** CoEST benchmark — iTrust, eTour, EasyClinic 
— 3 project khác domain (healthcare, tourism, clinic management) 
đủ đa dạng để đo cross-project variance

**Metric đề xuất:** MAP@10 per project + standard deviation 
across projects + coefficient of variation — đo độ ổn định

**LLM/Tool đề xuất:** GPT-4o zero-shot — cùng prompt template, 
không retune giữa các project — so sánh với IR methods 
(BM25 thường ổn định hơn LLM across projects)

**Baseline đề xuất:** BM25 cross-project variance từ Ngo 2024 
làm reference để so sánh độ ổn định IR vs LLM
