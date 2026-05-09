# SIEVE Methodology — Tổng quan

## Tên gọi

**SIEVE** = **S**tructure → **I**terative Extract → **V**alidate (Teacher-Student) → **E**ncode → **V**erify

## Triết lý cốt lõi

**"Chưng cất kiến thức, giữ tối đa thông tin有价值的."**

## Tại sao cần Teacher-Student Loop

Vấn đề cốt lõi của mọi distillation: **không biết mình miss gì.**

Giải pháp: Dùng output đã trích (Student) để tạo câu hỏi → hỏi lại sách gốc (Teacher) → tìm chỗ miss → bổ sung.

```
Student: "Tôi nghĩ sách nói A, B, C"
Teacher: "Đúng, nhưng bạn miss D và E, và A cần điều kiện F"
Student: "Cảm ơn, tôi bổ sung D, E, F"
Teacher: "Bây giờ bạn miss G (nhỏ hơn)"
Student: "Thêm G"
→ Lặp 2-3 vòng cho đến khi gap很小
```

## 5 Phase

| Phase | Tên | Mục tiêu | Thời gian (500 trang) |
|-------|-----|----------|----------------------|
| 1 | Structure | Hiểu cấu trúc sách | 15 phút |
| 2 | Extract | Trích xuất theo chương | 40 phút |
| 3 | Validate | Teacher-Student loop | 30 phút |
| 4 | Encode | Cấu trúc hóa 4 tầng | 15 phút |
| 5 | Verify | Quality gate + user review | 10 phút |

## Tại sao 5 Extractor

Mỗi extractor có "con mắt" khác nhau, giảm blind spot:

| Extractor | Nhìn thấy | Bỏ qua |
|-----------|-----------|--------|
| Argument | Luận điểm + logic | Data, stories |
| Data | Số liệu, thống kê | Luận điểm抽象 |
| Narrative | Câu chuyện, case | Data thuần túy |
| Concept | Định nghĩa, thuật ngữ | Application |
| Contrarian | Phản bác, giới hạn | Mainstream观点 |

5 extractor chạy song song → merge → giảm miss so với 1 lần đọc.

## Output 4 tầng

```
Tầng 1: Executive Summary    → Đọc 15 phút → Hiểu 50% sách
Tầng 2: Chapter Summaries    → Đọc 1 giờ   → Hiểu 75% sách
Tầng 3: Detailed Extracts    → Đọc 2-3 giờ → Hiểu 90% sách
Tầng 4: Knowledge Graph      → Tra cứu     → Hiểu liên kết
```

User chọn tầng phù hợp với thời gian và nhu cầu.

## Invariants (không vi phạm)

1. **Faithfulness**: Mọi thông tin phải có trong sách. Không bịa.
2. **Completeness**: ≥85% thông tin有价值的 phải được capture.
3. **Structure**: Output phải theo 4 tầng, không merge.
4. **Validation**: Phải chạy ≥2 vòng teacher-student.
5. **User involvement**: Executive summary phải让用户确认.
6. **Audit trail**: Giữ lại validation/, raw-extracts/ để trace.

## Tham khảo

| Nguồn |借鉴内容 |
|-------|---------|
| Mortimer Adler — How to Read a Book | Phase 1: phân tích cấu trúc |
| Tiago Forte — Progressive Summarization | Tầng layered output |
| Niklas Luhmann — Zettelkasten | Liên kết concepts |
| Knowledge Distillation (ML) | Teacher-Student loop |
