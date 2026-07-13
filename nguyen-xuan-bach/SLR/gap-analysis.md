# GAP Analysis — GPT-4 Zero-Shot Thuần Chưa Được Evaluate trên CoEST

**Thành viên:** Nguyễn Xuân Bách
**GAP type:** GAP-T
**Ngày:** 02/07/2026
**Evidence table nguồn:** team-synthesis/evidence-table-merged.md (N = 27 paper)

---

## 1. Mô tả GAP

Chưa có nghiên cứu nào sử dụng GPT-4 zero-shot thuần để sinh 
requirement-to-code traceability links trên CoEST benchmark 
(iTrust, eTour, EasyClinic). Các paper hiện có đều dùng kỹ thuật 
phức tạp hơn (CoT, RAG, few-shot) hoặc dùng dataset khác.

**Bằng chứng từ evidence table:**
- Cột Tool/LLM: Wang 2025 dùng GPT-4 + CoT + SimCSE — không phải 
  zero-shot thuần
- Cột Tool/LLM: Fuchß 2025 dùng GPT-4 + RAG — không phải zero-shot
- Cột Tool/LLM: Hassine 2024 dùng GPT-3.5 zero-shot nhưng trên 
  security requirements, không phải CoEST
- Kết luận: 0/27 paper dùng GPT-4 zero-shot thuần trên CoEST

---

## 2. Kiểm tra phản chứng

| Paper | Đã làm GAP này không? | Chi tiết |
|-------|----------------------|---------|
| Wang 2025 | Không | Dùng CoT + SimCSE, không phải zero-shot thuần |
| Fuchß 2025 | Không | Dùng RAG pipeline, không phải zero-shot |
| Hassine 2024 | Có (một phần) | Zero-shot nhưng GPT-3.5, không phải GPT-4, và không dùng CoEST |
| Alturayeif 2026 | Không | Dùng prompt engineering phức tạp, không phải zero-shot thuần |
| Hey 2025 | Không | Dùng RAG + CoT |
| Zhao & Xu 2026 | Có (một phần) | Zero-shot nhưng GraphRAG, không phải GPT-4 vanilla |
| Jin 2025 | Không | Dùng LLM + GNN hybrid |
| Lin 2021 | Không | Dùng BERT fine-tuned, không zero-shot |
| Ngo 2024 | Không | Chỉ IR methods, không có LLM |
| Wang 2023 | Không | ML classifiers, không có LLM |

**Kết luận:** GAP xác nhận ✅ — không paper nào dùng GPT-4 
zero-shot thuần trên CoEST

### Supplementary Validation (N < 10 paper LLM)

| Lớp | Hành động | Kết quả |
|-----|-----------|--------|
| L1 Targeted search | "GPT-4 zero-shot" AND "requirements traceability" AND "CoEST" — Scholar + IEEE — 02/07/2026 | 0 kết quả relevant |
| L2 Forward snowball | Cite Wang 2025 — 8 papers checked | 0 paper dùng GPT-4 zero-shot thuần trên CoEST |
| L3 Survey anchor | Alturayeif 2026 TraceLLM SLR N=4 benchmark | Không đề cập GPT-4 zero-shot trên CoEST |

→ **Kết luận: GAP confirmed ✅**

---

## 3. Feasibility Check

| Tiêu chí | Mức | Ghi chú |
|---------|-----|---------|
| Dataset | ✅ | CoEST public trên GitHub — iTrust, eTour, EasyClinic tải được ngay |
| API/Tool | ✅ | GPT-4 có API, free tier đủ cho pilot N=50 |
| Tính toán | ✅ | Chỉ cần gọi API, không cần GPU |
| Ground truth | ✅ | CoEST đã có ground truth sẵn, không cần annotation tay |
| Code base | ✅ | Chỉ cần Python script gọi API + so sánh output với ground truth |
| Kỹ năng | ✅ | Thư viện openai Python có sẵn, adapter được trong 1 ngày |
| Thời gian | ✅ | Pilot 1 tuần, full experiment 1 tuần — xong trước deadline |

**Kết quả:** 0 ❌ / 0 ⚠️ → **An toàn**

---

## 4. Phát biểu GAP chính thức

Không có nghiên cứu nào đánh giá GPT-4 zero-shot (I) cho việc 
sinh requirement-to-code traceability links (P) trên CoEST benchmark 
gồm iTrust, eTour, EasyClinic (D) bằng MAP@10, Precision, Recall, 
F1 và hallucination rate (O), so sánh với IR baseline tốt nhất 
trong VSM, LSI, BM25.

---

## 5. Đề xuất sơ bộ cho nhóm

**Dataset khả thi:** CoEST benchmark — iTrust (34 req, 100 classes), 
eTour (42 req, 83 classes), EasyClinic (51 req, 74 classes) — 
public trên GitHub, ground truth có sẵn

**Metric đề xuất:** MAP@10 (metric chính), Precision, Recall, F1, 
Hallucination rate — lấy từ cột Metric của evidence table

**LLM/Tool đề xuất:** GPT-4o (gpt-4o-2024-08-06) — zero-shot, 
không CoT, không RAG, không few-shot — chưa paper nào trong SLR 
dùng cấu hình này trên CoEST

**Baseline đề xuất:** BM25 tốt nhất trong 3 IR methods theo Ngo 2024 
(MAP ~0.55–0.65 trên CoEST) — so sánh trực tiếp với GPT-4 zero-shot
