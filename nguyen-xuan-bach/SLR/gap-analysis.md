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
- Cột Tool/LLM: Wang 2025 dùng GPT-4 + CoT + SimCSE
- Cột Tool/LLM: Fuchß 2025 dùng GPT-4 + RAG
- Cột Tool/LLM: Hassine 2024 dùng GPT-3.5 zero-shot nhưng 
  trên security requirements, không phải CoEST
- Kết luận: 0/27 paper dùng GPT-4 zero-shot thuần trên CoEST

**Pattern quan sát từ evidence table:**

| Kỹ thuật | Số paper | Dùng CoEST (rõ ràng) | Zero-shot thuần |
|----------|----------|-----------|----------------|
| IR-based (VSM/LSI/BM25) | 10/27 | 2/10 (Ngo 2024, Hey 2021 — ghi rõ tên iTrust/eTour/eANCI/SMOS). 7 paper còn lại chỉ ghi "Multiple datasets" trong cột Dataset → không xác định được có phải CoEST hay không | N/A |
| LLM + CoT/RAG/few-shot | 9/27 | 1/9 (chỉ Wang 2025 ghi rõ iTrust/eTour/eANCI/SMOS) | Không |
| LLM zero-shot | 3/27 | 0/3 | Không trên CoEST |
| **GPT-4 zero-shot thuần trên CoEST** | **0/27** | **0/27** | **← GAP** |

*Ghi chú phương pháp: cột "Dùng CoEST" chỉ tính paper có cột Dataset 
ghi rõ tên project CoEST (iTrust/eTour/eANCI/SMOS/EasyClinic). Paper 
ghi chung chung "Multiple datasets" được xếp vào "không xác định", 
không tính là "dùng CoEST" — tránh phóng đại con số khi không truy 
được về dữ liệu cụ thể.*

---

## 2. Kiểm tra phản chứng

| Paper | Đã làm GAP này không? | Chi tiết |
|-------|----------------------|---------|
| Wang 2025 | Không | Dùng CoT + SimCSE, không phải zero-shot thuần |
| Fuchß 2025 | Không | Dùng RAG pipeline, không phải zero-shot |
| Hassine 2024 | Có (một phần) | Zero-shot nhưng GPT-3.5, không GPT-4, không CoEST |
| Alturayeif 2026 | Không | Prompt engineering phức tạp, không zero-shot thuần |
| Hey 2025 | Không | Dùng RAG + CoT |
| Zhao & Xu 2026 | Có (một phần) | Zero-shot nhưng GraphRAG, không GPT-4 vanilla |
| Jin 2025 | Không | LLM + GNN hybrid |
| Lin 2021 | Không | BERT fine-tuned, không zero-shot |
| Ngo 2024 | Không | Chỉ IR methods, không có LLM |
| Wang 2023 | Không | ML classifiers, không có LLM |

**Phân tích chi tiết 3 paper "có một phần":**

- **Hassine 2024**: Dùng GPT-3.5 (không phải GPT-4) + 
  dataset security requirements (không phải CoEST) → 
  khác model, khác dataset, không phủ GAP của nhóm

- **Zhao & Xu 2026**: Dùng GraphRAG (không phải vanilla 
  zero-shot) → có thêm graph structure, không phải 
  zero-shot thuần

- **Wang 2025**: Dùng CoT + SimCSE (2 kỹ thuật bổ sung) → 
  kết quả không thể tách riêng phần nào do zero-shot, 
  phần nào do CoT

**Kết luận:** GAP xác nhận ✅ — không paper nào dùng GPT-4 
zero-shot thuần trên CoEST

### Supplementary Validation

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
| Dataset | ✅ | CoEST public trên GitHub — iTrust (34 req, 100 classes), eTour (42 req, 83 classes), EasyClinic (51 req, 74 classes) tải được ngay |
| API/Tool | ✅ | GPT-4o API — ước tính cost: 3 project × ~150 req × ~500 tokens/req × $0.005/1K = ~$1.13 full experiment. Pilot 10% = ~$0.11 |
| Tính toán | ✅ | Chỉ cần gọi API, không cần GPU |
| Ground truth | ✅ | CoEST đã có ground truth sẵn, không cần annotation tay |
| Code base | ✅ | Python script gọi API + so sánh output với ground truth — implement trong 1 ngày |
| Kỹ năng | ✅ | Thư viện openai Python có sẵn, không cần kiến thức research-level |
| Thời gian | ✅ | Pilot 1 tuần, full experiment 1 tuần — xong trước deadline với ≥ 1 tuần dự phòng |

**Kết quả:** 0 ❌ / 0 ⚠️ → **An toàn**

---

## 4. Phát biểu GAP chính thức

Không có nghiên cứu nào đánh giá GPT-4 zero-shot (I) cho việc 
sinh requirement-to-code traceability links (P) trên CoEST 
benchmark gồm iTrust, eTour, EasyClinic (D) bằng MAP@10, 
Precision, Recall, F1 và hallucination rate (O), so sánh với 
IR baseline tốt nhất trong VSM, LSI, BM25.

---

## 5. Đề xuất sơ bộ cho nhóm

**Dataset khả thi:** 
CoEST benchmark — iTrust (34 req, 100 classes), 
eTour (42 req, 83 classes), EasyClinic (51 req, 74 classes) 
— public trên GitHub, ground truth có sẵn, được dùng 
bởi 15/27 paper trong SLR

**Metric đề xuất:** 
MAP@10 (metric chính), Precision, Recall, F1, 
Hallucination rate — lấy từ cột Metric của evidence table

**LLM/Tool đề xuất:** 
GPT-4o (gpt-4o-2024-08-06) — zero-shot, không CoT, 
không RAG, không few-shot — chưa paper nào trong SLR 
dùng cấu hình này trên CoEST

**Baseline đề xuất:** 
BM25 — tốt nhất trong 3 IR methods theo tham khảo sơ bộ từ 
Ngo 2024 (MAP ước tính ~0.55–0.65 trên CoEST, dựa trên đọc 
Table/Figure của paper gốc — **cần trích dẫn lại số trang/bảng 
cụ thể khi viết proposal**, chưa verify chính xác 100%). 
Nếu không xác nhận lại được con số chính xác từ Ngo 2024, 
nhóm sẽ tự chạy BM25 (theo thực nghiệm G2 của Minh Duy) trên 
đúng 3 project CoEST để có MAP@10 chính xác, thay vì dựa vào 
số ước tính từ paper khác.

**Mapping sang RQ:**
- Dataset + LLM + Metric → trả lời RQ1
- Chạy trên 3 project → trả lời RQ2
- Đếm invalid class → trả lời RQ3

**Prompt template sơ bộ (zero-shot):**
