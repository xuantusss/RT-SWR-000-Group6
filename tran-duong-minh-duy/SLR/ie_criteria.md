
# Inclusion/Exclusion Criteria — Traceability Link Generation

## Inclusion Criteria (IC)

| Mã   | Ý nghĩa                                                                 |
|------|-------------------------------------------------------------------------|
| IC-L | Paper viết bằng tiếng Anh                                               |
| IC-T | Đăng trên conference hoặc journal (không phải blog, thesis)             |
| IC-E | Có ít nhất 1 con số kết quả trong Table hoặc Figure                    |
| IC-Y | Từ 2019 trở đi — vì GPT/BERT-era bắt đầu ảnh hưởng traceability từ đây |
| IC-P | Task phải là requirement-to-code traceability (class hoặc method level) |
| IC-I | Dùng LLM (GPT, BERT, T5...) hoặc IR-based (VSM, LSI, BM25, TF-IDF)    |

## Exclusion Criteria (EC)

| Mã   | Ý nghĩa                                                                          |
|------|----------------------------------------------------------------------------------|
| EC-D | Trùng với paper đã có                                                            |
| EC-A | Không tải được full-text                                                         |
| EC-S | Dưới 4 trang (abstract, poster)                                                  |
| EC-N | Không có thực nghiệm (vision paper, tutorial)                                    |
| EC-O | Không về req-to-code traceability: loại bug traceability, test traceability,     |
|      | architecture recovery, commit traceability                                        |
