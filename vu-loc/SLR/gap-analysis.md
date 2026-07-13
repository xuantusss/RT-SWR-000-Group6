# GAP Analysis — Hallucination Rate Chưa Được Định Nghĩa Và Đo

**Thành viên:** Vũ Lộc
**GAP type:** GAP-S
**Ngày:** 02/07/2026
**Evidence table nguồn:** team-synthesis/evidence-table-merged.md (N = 27 paper)

---

## 1. Mô tả GAP

Chưa có nghiên cứu nào định nghĩa và đo hallucination rate 
trong requirement-to-code traceability — tức là tỉ lệ LLM sinh 
traceability link trỏ đến class không tồn tại trong codebase. 
IR-based methods không thể hallucinate nên metric này chưa 
bao giờ cần thiết, nhưng với LLM thì đây là rủi ro thực tế.

**Bằng chứng từ evidence table:**
- Cột Metric: 0/27 paper định nghĩa hoặc đo hallucination rate
- Cột Hạn chế: không paper nào đề cập hallucination là rủi ro
- IR-based papers (10/27): không thể hallucinate vì chỉ rank 
  class có sẵn trong codebase
- LLM-based papers (12/27): đều bỏ qua vấn đề link không hợp lệ

---

## 2. Kiểm tra phản chứng

| Paper | Đã làm GAP này không? | Chi tiết |
|-------|----------------------|---------|
| Wang 2025 | Không | Đo MAP nhưng không đo hallucination rate |
| Fuchß 2025 | Không | Đo F1 nhưng không kiểm tra link không hợp lệ |
| Hassine 2024 | Không | Đo Precision/Recall nhưng không đo hallucination |
| Alturayeif 2026 | Không | Đo F2 Score nhưng không đo hallucination |
| Zhao & Xu 2026 | Không | Đo Precision/Recall nhưng không đo hallucination |
| Jin 2025 | Không | Đo F1 nhưng không kiểm tra invalid links |
| Shah 2025 | Không | Đo Cohen's Kappa nhưng không đo hallucination |
| Zhang 2025 | Không | Đo F1 nhưng không đo hallucination |
| Hey 2025 | Không | Đo performance vs SOTA nhưng không đo hallucination |
| Lin 2021 | Không | Đo MAP nhưng không đo hallucination |

**Kết luận:** GAP xác nhận ✅ — 0/27 paper đo hallucination rate

### Supplementary Validation

| Lớp | Hành động | Kết quả |
|-----|-----------|--------|
| L1 Targeted search | "hallucination" AND "traceability" AND "LLM" — Scholar + IEEE — 02/07/2026 | 0 kết quả relevant |
| L2 Forward snowball | Cite Alturayeif 2026 — 5 papers checked | 0 paper đo hallucination trong traceability |
| L3 Survey anchor | Alturayeif 2026 TraceLLM SLR N=4 benchmark | Không đề cập hallucination rate |

→ **Kết luận: GAP confirmed ✅**

---

## 3. Feasibility Check

| Tiêu chí | Mức | Ghi chú |
|---------|-----|---------|
| Dataset | ✅ | CoEST có danh sách class thật sẵn — dùng để verify link |
| API/Tool | ✅ | GPT-4 API có sẵn |
| Tính toán | ✅ | Chỉ cần đếm link trỏ đến class không có trong danh sách |
| Ground truth | ✅ | Không cần annotation — chỉ cần danh sách class trong CoEST |
| Code base | ✅ | 5 dòng Python: so sánh output GPT-4 với danh sách class CoEST |
| Kỹ năng | ✅ | String matching cơ bản |
| Thời gian | ✅ | Tính song song với RQ1 — không tốn thêm thời gian |

**Kết quả:** 0 ❌ / 0 ⚠️ → **An toàn**

---

## 4. Phát biểu GAP chính thức

Chưa có nghiên cứu nào định nghĩa và đo hallucination rate (O) 
của GPT-4 zero-shot (I) khi sinh requirement-to-code traceability 
links (P) trên CoEST benchmark (D) — tức là tỉ lệ link trỏ đến 
class không tồn tại trong codebase — và chưa ai kiểm tra 
few-shot prompting có giảm hallucination không.

---

## 5. Đề xuất sơ bộ cho nhóm

**Dataset khả thi:** CoEST benchmark — iTrust, eTour, EasyClinic 
— danh sách class trong codebase dùng làm ground truth để 
detect hallucination

**Metric đề xuất:** 
Hallucination rate = số link trỏ đến class không tồn tại / 
tổng số link GPT-4 sinh ra

**LLM/Tool đề xuất:** 
- GPT-4o zero-shot — đo hallucination rate baseline
- GPT-4o few-shot — đo xem few-shot có giảm hallucination không
- So sánh 2 cấu hình → trả lời RQ3

**Baseline đề xuất:** IR methods (VSM/LSI/BM25) có 
hallucination rate = 0% vì chỉ rank class có sẵn — 
đây là baseline tự nhiên để so sánh
