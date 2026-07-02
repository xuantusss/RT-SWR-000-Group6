# Gap Statement — CoEST Benchmark and Evaluation for Traceability

Evidence table: N = 9 paper

## Các khoảng trống tiềm năng

- GAP-T: Chưa có đánh giá thống nhất giữa kỹ thuật CoEST Benchmark + Evaluation và baseline khác trên cùng một bộ CoEST đầy đủ.

- GAP-M: Nhiều paper dùng Precision/Recall/F1/MAP nhưng ít paper đo hallucination hoặc invalid-link rate khi model sinh link không tồn tại.

- GAP-D: Dataset thường xoay quanh iTrust/eTour/EasyClinic nhưng kích thước nhỏ và thiếu kiểm tra cross-project variance.

- GAP-S: Phần lớn paper thừa nhận hạn chế về dataset nhỏ, domain hẹp, hoặc chưa kiểm thử trong bối cảnh multilingual/industrial.

## Nhận xét

Literature hiện có đủ baseline để so sánh, nhưng còn thiếu một thiết kế thực nghiệm thống nhất đo cả chất lượng trace link và lỗi sinh link không hợp lệ trên CoEST benchmark.
