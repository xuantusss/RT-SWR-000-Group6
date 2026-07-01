# Gap Statement — IR-Based Traceability Methods

Evidence table: N = 11 paper

## Các khoảng trống tiềm năng

- GAP-T: Chưa có nghiên cứu nào so sánh trực tiếp VSM, LSI, BM25
  trên cùng 1 benchmark CoEST (iTrust, eTour, EasyClinic) với
  điều kiện thực nghiệm kiểm soát — mỗi paper dùng dataset khác nhau
  nên không so sánh được

- GAP-M: Chưa có paper nào đo MAP@10 như metric chính cho IR-based
  traceability trên CoEST — hầu hết dùng F1 hoặc Precision/Recall
  đơn thuần, không dùng MAP@10

- GAP-D: 9/11 paper không test trên CoEST benchmark — thiếu
  baseline chuẩn để so sánh IR methods với LLM-based approaches
  trên cùng dataset

- GAP-S: 8/11 paper thừa nhận ít nhất 1 trong các hạn chế:
  English-only, small dataset, chưa so sánh với LLM,
  chưa test cross-project

## Nhận xét

Literature về IR-based traceability tập trung vào cải thiện
từng method riêng lẻ nhưng thiếu benchmark thống nhất để so sánh
VSM/LSI/BM25 với LLM-based approaches trên CoEST datasets,
đặc biệt thiếu MAP@10 và cross-project evaluation.
