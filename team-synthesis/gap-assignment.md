# GAP Assignment — RT-SWR-000-Group6

Ngày: 02/07/2026
Evidence table nhóm: N = 27 paper

---

## Bối cảnh phân công

Sau khi gộp paper từ 4 thành viên và brainstorm GAP, nhóm xác định 
được 4 khoảng trống nghiên cứu rõ ràng từ evidence table. Mỗi GAP 
trỏ về cột khác nhau trong evidence table để đảm bảo không trùng lặp.

---

## Phân công

### Nguyễn Xuân Bách — GAP-T

**GAP được phân công:**
GPT-4 zero-shot thuần chưa được evaluate trực tiếp trên CoEST

**Mô tả chi tiết:**
Các paper LLM hiện có đều dùng kỹ thuật phức tạp hơn zero-shot:
- Wang 2025 dùng CoT + SimCSE
- Fuchß 2025 dùng RAG pipeline
- Hassine 2024 dùng GPT-3.5 (không phải GPT-4) trên security req
- 0/27 paper dùng GPT-4 zero-shot thuần trên CoEST

**Tại sao phân công cho Bách:**
- Bách là PL, có trách nhiệm chọn GAP chính của đề tài
- GAP-T trực tiếp justify cho RQ1 — câu hỏi trung tâm của đề tài
- Bách đã tìm được nhiều paper LLM nhất (6/11 paper về LLM)

**Cột nguồn trong evidence table:** Tool/LLM
**Justify cho RQ:** RQ1

---

### Trần Dương Minh Duy — GAP-M

**GAP được phân công:**
Chưa có benchmark thống nhất so sánh VSM/LSI/BM25 trên cùng 
3 project CoEST với MAP@10

**Mô tả chi tiết:**
- Ngo 2024 dùng MAP nhưng không phải MAP@10, không test EasyClinic
- Comparison IR 2019 so sánh VSM/LSI/BM25 nhưng không dùng CoEST
- Evaluating IR 2021 so sánh IR methods nhưng không dùng CoEST
- 0/27 paper so sánh đủ 3 methods trên cả 3 project CoEST với MAP@10

**Tại sao phân công cho Minh Duy:**
- Minh Duy tìm được nhiều paper IR-based nhất (8/11 paper về IR)
- Hiểu rõ strengths/weaknesses của từng IR method
- GAP-M justify cho baseline của RQ1

**Cột nguồn trong evidence table:** Metric
**Justify cho RQ:** RQ1 (baseline)

---

### Nguyễn Trần Thái Duy Anh — GAP-D

**GAP được phân công:**
Chưa có nghiên cứu đo cross-project variance của LLM trên 
đủ 3 project CoEST mà không retune prompt

**Mô tả chi tiết:**
- Chỉ 3/27 paper test đủ cả 3 project CoEST
- Wang 2025 test 4 dataset nhưng không đo variance
- Bauch 2026 đề cập context varies by project nhưng không đo
- 0/27 paper báo cáo standard deviation across projects

**Tại sao phân công cho Thái Duy Anh:**
- Thái Duy Anh tìm được nhiều paper về LLM prompting nhất
- Hiểu rõ vấn đề generalization của LLM
- GAP-D justify trực tiếp cho RQ2

**Cột nguồn trong evidence table:** Dataset
**Justify cho RQ:** RQ2

---

### Vũ Lộc — GAP-S

**GAP được phân công:**
Hallucination rate — link trỏ đến class không tồn tại — 
chưa được định nghĩa và đo trong bất kỳ paper nào

**Mô tả chi tiết:**
- IR-based methods không thể hallucinate → không ai cần đo trước đây
- LLM mới vào traceability từ 2023-2024 → literature chưa bắt kịp
- 0/27 paper định nghĩa hoặc đo hallucination rate
- Không paper nào đề cập hallucination là rủi ro trong cột Hạn chế

**Tại sao phân công cho Vũ Lộc:**
- Vũ Lộc tìm được nhiều paper CoEST benchmark nhất
- Hiểu rõ ground truth structure của CoEST — cần thiết để 
  detect hallucination
- GAP-S justify trực tiếp cho RQ3

**Cột nguồn trong evidence table:** Metric + Hạn chế
**Justify cho RQ:** RQ3

---

## Tổng hợp

| Thành viên | GAP | Loại | Cột nguồn | Justify RQ |
|-----------|-----|------|-----------|-----------|
| Nguyễn Xuân Bách | GPT-4 zero-shot chưa test trên CoEST | GAP-T | Tool/LLM | RQ1 |
| Trần Dương Minh Duy | Không có MAP@10 benchmark thống nhất | GAP-M | Metric | RQ1 baseline |
| Nguyễn Trần Thái Duy Anh | Cross-project variance chưa đo | GAP-D | Dataset | RQ2 |
| Vũ Lộc | Hallucination rate chưa định nghĩa | GAP-S | Metric + Hạn chế | RQ3 |

---

## Xác nhận không trùng
- [x] Mỗi GAP trỏ về cột khác nhau trong evidence table
- [x] Không có 2 GAP mô tả cùng 1 điều theo cách khác
- [x] Mỗi thành viên đồng ý với GAP được phân công
- [x] Mỗi GAP justify cho ít nhất 1 RQ trong proposal
- [x] Tất cả GAP đều feasible trong thời gian còn lại


## Giải trình overlap cột nguồn (Minh Duy & Vũ Lộc)

Cả 2 GAP đều trỏ về cột **Metric** trong evidence table, nhưng nhóm 
xác nhận đây không phải GAP trùng lặp. Lý do:

### Tại sao chấp nhận overlap này (tại sao làm)

Cột Metric trong evidence table chứa 2 loại thiếu sót độc lập nhau:

1. **Thiếu sự thống nhất giữa các metric đã có** (GAP của Minh Duy):
   27 paper dùng metric khác nhau (MAP, F1, Precision/Recall, Cohen's 
   Kappa, F2 Score...) nhưng không paper nào dùng MAP@10 trên đủ 3 
   project CoEST → đây là vấn đề "thiếu benchmark thống nhất giữa 
   các metric IR truyền thống".

2. **Thiếu một loại metric hoàn toàn chưa tồn tại** (GAP của Vũ Lộc):
   0/27 paper có bất kỳ metric nào đo hallucination rate — không phải 
   vì các paper đo sai hay không thống nhất, mà vì **loại rủi ro này 
   (link trỏ đến class không tồn tại) chỉ phát sinh khi dùng LLM**, 
   và literature về LLM trong traceability còn quá mới nên chưa ai 
   định nghĩa metric cho nó.

→ Nói cách khác: Minh Duy làm về "metric đã có nhưng thiếu 
chuẩn hóa", Vũ Lộc làm về "metric chưa hề tồn tại". Hai vấn đề 
này không thể gộp thành 1 GAP vì hướng giải quyết khác nhau — 
Minh Duy cần chạy lại 3 IR method trên cùng dataset để tạo 
benchmark, còn Vũ Lộc cần định nghĩa và implement một metric 
mới (hallucination rate) không có trong bất kỳ paper nào.

### Tại sao không tách hoặc gộp lại (tại sao không làm)

- **Không gộp thành 1 GAP:** vì mỗi GAP justify cho 1 RQ khác nhau 
  trong proposal (Minh Duy → RQ1 baseline, Vũ Lộc → RQ3) — gộp lại 
  sẽ làm proposal mất rõ ràng về scope của từng RQ.
- **Không đổi cột nguồn của 1 trong 2 người sang cột khác:** vì cột 
  Metric là cột duy nhất trong evidence table thực sự chứa bằng 
  chứng cho cả 2 GAP này — ép sang cột khác (vd: Dataset, Hạn chế) 
  sẽ làm bằng chứng yếu đi và không còn evidence-based đúng nghĩa.

**Kết luận:** Overlap cột nguồn là hợp lệ vì bản chất 2 GAP khác 
nhau (chuẩn hóa metric hiện có vs. tạo metric mới), không vi phạm 
nguyên tắc "không có 2 GAP mô tả cùng 1 điều theo cách khác".
