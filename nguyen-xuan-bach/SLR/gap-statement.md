# Gap Statement — Traceability Link Generation

Evidence table: N = 11 paper

## Các khoảng trống tiềm năng

- GAP-T: Chưa có nghiên cứu nào đánh giá GPT-4 **zero-shot thuần** 
  cho req-to-code traceability trên CoEST benchmark — Wang 2025 
  dùng CoT+SimCSE, Fuchß 2025 dùng RAG, không paper nào 
  dùng zero-shot GPT-4 đơn giản

- GAP-M: Chưa có paper nào định nghĩa và đo **hallucination rate** 
  (link trỏ đến class không tồn tại) trong traceability — 
  cột Hạn chế: không paper nào đề cập metric này

- GAP-D: Chỉ 2/11 paper test đủ cả 3 project CoEST (iTrust, eTour, 
  EasyClinic) — hầu hết chỉ test 1-2 project, không đo 
  cross-project variance

- GAP-S: 7/11 paper thừa nhận ít nhất 1 trong các hạn chế sau: 
  English-only, dataset nhỏ, chưa test CoEST đầy đủ, 
  chưa so sánh với LLM

## Nhận xét

Literature hiện tại tập trung vào IR-based và hybrid methods 
trên CoEST, nhưng chưa có nghiên cứu nào đánh giá trực tiếp 
GPT-4 zero-shot so với VSM/LSI/BM25 trên cả 3 project CoEST 
(iTrust, eTour, EasyClinic) với đo lường hallucination rate.
