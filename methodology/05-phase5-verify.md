# Phase 5 — Verify (Kiểm tra cuối)

## Mục tiêu

Đảm bảo output đạt chất lượng trước khi交付 cho user.

## Quality Checklist

### 1. Completeness (Độ bao phủ)

```
□ Completeness score ≥85%?
□ Không còn MISSING gap nào?
□ Mỗi chương ★★★ có extract đầy đủ?
□ Data extractor đã capture tất cả số liệu quan trọng?
□ Contrarian extractor đã capture tất cả giới hạn/phản bác?
```

### 2. Accuracy (Độ chính xác)

```
□ Không còn WRONG gap?
□ Mỗi claim có source_quote backing?
□ Data có đúng với nguyên văn?
□ Story có đúng outcome?
```

### 3. Structure (Cấu trúc)

```
□ 4 tầng đầy đủ?
□ Tầng 1 ≤3 trang?
□ Tầng 2 có summary mỗi chương ★★★?
□ Tầng 3 có extract mỗi chương?
□ Tầng 4 có mermaid graph?
□ Links giữa các tầng hoạt động?
```

### 4. Cross-references (Liên kết)

```
□ Knowledge graph có ≥1 edge mỗi node?
□ Contradictions đã được ghi chú?
□ Dependencies đã được xác định?
□ Không có orphan node (node không liên kết)?
```

### 5. User Review

```
□ Executive summary đã让用户 review?
□ User có thắc mắc gì không?
□ User có muốn bổ sung/sửa gì không?
```

## Quy trình Verify

### Bước 5.1 — Auto-check

Chạy checklist trên, đánh dấu PASS/FAIL mỗi mục.

### Bước 5.2 — User review Executive Summary

Hiển thị Tầng 1 cho user, hỏi:
- "Tóm tắt này có đúng với理解 của bạn về sách không?"
- "Có takeaway nào bạn nghĩ quan trọng hơn mà tôi miss không?"
- "Có giới hạn nào mà tôi ghi chưa đúng không?"

### Bước 5.3 — Fix nếu cần

Nếu user phát hiện vấn đề:
- Quay lại Phase 2 hoặc Phase 3 để fix
- Re-encode Phase 4
- Re-verify Phase 5

### Bước 5.4 — Final output

Tạo META.md:

```markdown
# META

## Sách
- **Title:** [Tên sách]
- **Author:** [Tác giả]
- **Pages:** [Số trang]
- **Genre:** [Thể loại]
- **Year:** [Năm]
- **Source:** [File path]

## Distillation
- **Framework:** SIEVE v1.0
- **Date:** [Ngày]
- **Rounds:** [Số vòng teacher-student]
- **Completeness:** [Điểm %]
- **Compression:** [Số trang gốc] → [Số trang output] ([Tỷ lệ %])

## Quality
- **Missing gaps:** [Số]
- **Incomplete gaps:** [Số]
- **Wrong:** [Số]
- **Nuance:** [Số] (ghi chú trong extract)
- **User reviewed:** [Yes/No]

## Reading Guide
- **Muốn nhanh (15 phút):** Đọc TIER-1-EXECUTIVE-SUMMARY.md
- **Muốn overview (1 giờ):** Đọc TIER-2-CHAPTER-SUMMARIES/
- **Muốn chi tiết (2-3 giờ):** Đọc TIER-3-DETAILED-EXTRACTS/
- **Muốn tra cứu:** Đọc TIER-4-KNOWLEDGE-GRAPH/
```

## Output cuối cùng

```
books/<slug>/
├── META.md                      ← Bắt đầu ở đây
├── TIER-1-EXECUTIVE-SUMMARY.md  ← Đọc 15 phút
├── TIER-2-CHAPTER-SUMMARIES/    ← Đọc 1 giờ
├── TIER-3-DETAILED-EXTRACTS/    ← Đọc 2-3 giờ
├── TIER-4-KNOWLEDGE-GRAPH/      ← Tra cứu
├── validation/                  ← Audit trail
└── raw-extracts/                ← Raw data
```

## Ghi chú

- **Phase 5 là bắt buộc**: Không deliver khi chưa verify.
- **User review executive summary là bắt buộc**: Đây là checkpoint cuối.
- **Giữ audit trail**: validation/ và raw-extracts/ để trace lại nếu cần.
- **META.md rất quan trọng**: Cho user biết distillation quality, cách đọc.
