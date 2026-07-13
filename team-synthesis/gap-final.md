# GAP List — RT-SWR-000-Group6

Ngày: 02/07/2026
Evidence table nhóm: N = 27 paper

## Danh sách GAP tiềm năng

### G1 — GAP-T: GPT-4 Zero-Shot Thuần Chưa Được Evaluate trên CoEST

**Mô tả:**
Chưa có nghiên cứu nào sử dụng GPT-4 zero-shot thuần (không CoT, không RAG, không few-shot) để sinh traceability links trên CoEST benchmark.

**Bằng chứng từ evidence table:**
- Wang 2025 dùng GPT-4 + CoT + SimCSE — không phải zero-shot thuần
- Fuchß 2025 dùng GPT-4 + RAG — không phải zero-shot thuần
- Hassine 2024 dùng GPT-3.5 zero-shot nhưng chỉ trên security requirements, không phải CoEST
- 0/27 paper dùng GPT-4 zero-shot thuần trên iTrust/eTour/EasyClinic

**Tại sao chọn G1 làm GAP chính:**
1. **Practical value cao** — zero-shot là cách dùng đơn giản và rẻ nhất, không cần setup phức tạp. Nếu đã đủ tốt thì engineer có thể dùng ngay mà không cần fine-tune hay RAG
2. **Directly addressable** — CoEST dataset public, GPT-4 có API, có thể chạy thực nghiệm trong 1-2 tuần
3. **Measurable** — MAP@10, Precision, Recall, F1 đều có thể tính được từ ground truth của CoEST
4. **Fills exact gap** — literature đã có GPT-4 với kỹ thuật phức tạp, nhưng chưa có zero-shot baseline → nhóm cung cấp missing baseline này

---

### G2 — GAP-M: Không Có Benchmark Thống Nhất So Sánh VSM/LSI/BM25 Với MAP@10

**Mô tả:**
Các paper IR-based dùng dataset và metric khác nhau nên không so sánh được với nhau hoặc với LLM.

**Bằng chứng từ evidence table:**
- Ngo 2024 dùng MAP, F1 trên CoEST nhưng không dùng MAP@10
- Comparison IR Techniques 2019 dùng Precision/Recall nhưng không dùng MAP
- 0/27 paper dùng MAP@10 làm metric chính
- Mỗi paper test trên dataset khác nhau → không so sánh được

**Tại sao chọn G2 làm GAP phụ:**
- Giải quyết G2 giúp tạo IR baseline chuẩn để so sánh với G1
- Không đứng độc lập được vì thiếu LLM component
- Hỗ trợ trực tiếp cho RQ1

---

### G3 — GAP-D: Cross-Project Variance Của LLM Chưa Được Đo

**Mô tả:**
Chưa có nghiên cứu nào kiểm tra LLM có generalize được across 3 project CoEST mà không retune prompt.

**Bằng chứng từ evidence table:**
- Chỉ 3/27 paper test đủ cả 3 project CoEST
- Wang 2025 test 4 dataset nhưng không đo variance giữa các project
- Alturayeif 2026 test 4 benchmark nhưng không phải CoEST và không đo cross-project stability
- 0/27 paper báo cáo standard deviation hoặc variance across projects

**Tại sao chọn G3 làm GAP phụ:**
- Trả lời câu hỏi thực tế quan trọng: LLM có đáng tin để deploy across projects không
- Không cần dataset mới — chỉ cần chạy trên 3 project CoEST đã có
- Hỗ trợ trực tiếp cho RQ2

---

### G4 — GAP-S: Hallucination Rate Chưa Được Định Nghĩa Và Đo

**Mô tả:**
LLM có thể sinh traceability link trỏ đến class không tồn tại trong codebase — rủi ro này chưa được đo trong bất kỳ paper nào.

**Bằng chứng từ evidence table:**
- 0/27 paper định nghĩa hoặc đo hallucination rate
- IR-based methods không thể hallucinate vì chỉ rank class có sẵn → không ai cần đo trước đây
- LLM mới xuất hiện trong traceability từ 2023-2024 → literature chưa kịp bắt kịp

**Tại sao chọn G4 làm GAP phụ:**
- **Contribution hoàn toàn mới** — nhóm đầu tiên đề xuất đo metric này trong traceability
- Dễ đo — CoEST có ground truth sẵn, chỉ cần đếm link trỏ đến class không có trong danh sách
- Không cần annotation tay
- Hỗ trợ trực tiếp cho RQ3

---

## Tổng hợp lý do chọn 4 GAP này

| GAP | Loại | Justify cho RQ | Feasibility |
|-----|------|---------------|-------------|
| G1 — GPT-4 zero-shot chưa test trên CoEST | GAP-T | RQ1 | ✅ Dataset public, API có sẵn |
| G2 — Không có MAP@10 benchmark thống nhất | GAP-M | RQ1 | ✅ Tính từ ground truth CoEST |
| G3 — Cross-project variance chưa đo | GAP-D | RQ2 | ✅ Chạy trên 3 project có sẵn |
| G4 — Hallucination rate chưa định nghĩa | GAP-S | RQ3 | ✅ Đếm từ output GPT-4 |

## Xác nhận không trùng
- [x] G1 trỏ về cột Tool/LLM
- [x] G2 trỏ về cột Metric
- [x] G3 trỏ về cột Dataset
- [x] G4 trỏ về cột Hạn chế
- [x] Không có 2 GAP mô tả cùng 1 điều

## GAP chính
**G1** — vì directly addressable, practical value cao, và là missing baseline mà cả 3 RQ đều phụ thuộc vào

## GAP phụ
**G2, G3, G4** — bổ sung và làm đầy đủ cho G1
