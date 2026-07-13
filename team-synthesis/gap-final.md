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
- Wang 2025 test 4
