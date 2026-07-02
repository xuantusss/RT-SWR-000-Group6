# Gap Statement - Nguyễn Trần Thái Duy Anh

Evidence table: N = 8 paper

## Các khoảng trống tiềm năng

- **GAP‑T**: Chưa có nghiên cứu nào sử dụng GPT-4o hoặc các LLM thế hệ mới nhất (Gemini 1.5 Pro, Claude 3 Opus) cho traceability trên dataset **EasyClinic** hoặc **CoEST**. Hầu hết các paper tập trung vào iTrust và eTour.

- **GAP‑M**: Chưa có nghiên cứu nào đo lường **MAP@10** và **F2 Score** cho LLM-based traceability trên dataset **CoEST**. Các nghiên cứu hiện tại chủ yếu sử dụng F1, Precision, Recall hoặc Cohen's Kappa mà chưa áp dụng các metrics đánh giá xếp hạng phổ biến trong IR.

- **GAP‑D**: Thiếu dataset đa dạng cho traceability, đặc biệt là trong các lĩnh vực:
  - **Healthcare** (ngoài iTrust): Chưa có dataset về bệnh án điện tử, quy trình y tế
  - **Aerospace**: Chỉ có 1 dataset được đề cập trong TraceLLM nhưng chưa được khai thác rộng rãi
  - **Regulatory compliance**: Các dataset về quy định pháp lý (GDPR, HIPAA) còn thiếu

- **GAP‑S**: 5/8 paper (62.5%) thừa nhận các hạn chế sau:
  - **Dataset nhỏ**: Alturayeif et al. 2026, Hey et al. 2025, Bauch 2026 đều đề cập đến vấn đề dataset limited
  - **English-only**: Shah et al. 2025 chỉ thử nghiệm trên dữ liệu tiếng Anh
  - **Zero-shot performance**: Shah et al. 2025 chỉ ra zero-shot còn hạn chế
  - **Context sensitivity**: Bauch 2026 chỉ ra context effect varies by project
  - **Generalization**: Zhang et al. 2025 thừa nhận chưa test generalization trên các domain khác

## Nhận xét

Hầu hết các nghiên cứu hiện tại (2021-2026) đã chứng minh tiềm năng của LLM (GPT-4, BERT, LLaMA-2) trong traceability, đặc biệt với các kỹ thuật prompting (zero-shot, few-shot, chain-of-thought) và RAG. Tuy nhiên, các nghiên cứu vẫn còn phân tán, thiếu sự so sánh có hệ thống giữa các LLM khác nhau trên cùng một tập dataset chuẩn. Đặc biệt, **CoEST Benchmark** - một dataset chuẩn mới - vẫn chưa được khai thác đầy đủ với các LLM hiện đại. Điều này mở ra cơ hội nghiên cứu đánh giá toàn diện các LLM (GPT-4o, Gemini, Claude) trên nhiều dataset khác nhau (iTrust, eTour, EasyClinic, CoEST) với bộ metrics đa dạng (F1, MAP@10, F2) để thiết lập baseline cho community.

## Đề xuất hướng nghiên cứu tiếp theo

1. **So sánh có hệ thống**: Đánh giá đồng thời các LLM (GPT-4o, Gemini 1.5 Pro, Claude 3, LLaMA-3) trên cùng tập dataset (CoEST, iTrust, eTour) với cùng bộ metrics (F1, MAP@10, Precision, Recall) để có kết quả so sánh công bằng.

2. **Prompt engineering**: Nghiên cứu tối ưu prompt templates cho từng loại dataset và từng LLM cụ thể, bao gồm few-shot prompting với examples được chọn lọc thông minh.

3. **Mở rộng dataset**: Xây dựng và công bố dataset cho các domain mới (healthcare, regulatory compliance, automotive) để đa dạng hóa thử nghiệm.

4. **Fine-tuning vs Zero-shot**: So sánh hiệu quả giữa fine-tuning LLM trên dữ liệu traceability với zero-shot prompting để xác định trade-off giữa chi phí và hiệu suất.