---
name: sieve-book-distillation
version: 1.0.0
description: |
  Chưng cất kiến thức từ sách, giữ 85-92% thông tin有价值的.
  Dùng khi: user muốn hiểu một cuốn sách mà không có thời gian đọc hết,
  hoặc muốn tóm tắt sách ở mức chi tiết (không phải tóm tắt sơ lược).
  Không dùng khi: user muốn tóm tắt 1-2 trang (dùng summarize thông thường).
  Trigger: "tóm tắt sách", "phân tích sách", "đọc sách giúp tôi",
  "chưng cất sách", "distill book", "book summary detailed",
  "hiểu sách mà không đọc", "rút gọn sách".
---

# SIEVE — Book Knowledge Distillation Framework

## Sứ mệnh

Chưng cất tri thức từ sách thành dạng **đọc nhanh mà không miss**, giữ 85-92% thông tin有价值的.
Output ~50 trang từ sách 500 trang (nén 90%), cấu trúc theo tầng.

## Khi nào gọi skill này

User nói类似:
- "Tóm tắt cuốn [tên sách] cho tôi"
- "Phân tích sách [tên sách]"
- "Đọc sách [tên sách] giúp tôi, tôi không có thời gian"
- "Tôi muốn hiểu sách này mà không đọc hết"
- "Chưng cất kiến thức từ cuốn [tên sách]"
- "Distill this book: [đường dẫn file]"
- "Rút gọn sách [tên sách] nhưng giữ chi tiết"

## Khi nào KHÔNG gọi

- User muốn tóm tắt 1-2 câu → dùng summarize thông thường
- User muốn review/đánh giá sách → dùng general chat
- Sách là tiểu thuyết/fiction (không có tri thức để chưng cất)

## Input yêu cầu

Trước khi bắt đầu **phải xác nhận** từ user:
1. **File sách**: PDF / EPUB / TXT đường dẫn. Không có file → hỏi user cung cấp.
2. **Tên sách + tác giả + năm**: để metadata.
3. **Mức độ chi tiết**: 
   - `full` (mặc định): giữ tối đa, ~50 trang từ 500 trang
   - `compact`: giữ luận điểm + data chính, ~25 trang
   - `summary`: chỉ executive summary + chapter summaries, ~15 trang
4. **Ưu tiên chương nào?** (nếu user có nhu cầu特定)

## Pipeline SIEVE (5 Phase)

```
Phase 1: STRUCTURE    → Book Map + Backbone + Seed Glossary
Phase 2: EXTRACT      → 5 extractors × N chapters (song song)
Phase 3: VALIDATE     → Teacher-Student loop (2-3 vòng)
Phase 4: ENCODE       → 4-tier layered output (~50 pages)
Phase 5: VERIFY       → Quality gate + user review
```

Chi tiết: xem `methodology/00-overview.md`

## Output Structure

```
books/<slug>/
├── META.md                          # Metadata sách + distillation info
├── TIER-1-EXECUTIVE-SUMMARY.md      # Tầng 1: 2-3 trang, đọc 15 phút
├── TIER-2-CHAPTER-SUMMARIES/        # Tầng 2: 10-15 trang, đọc 1 giờ
│   ├── 00-overview.md
│   ├── ch01-summary.md
│   └── ...
├── TIER-3-DETAILED-EXTRACTS/        # Tầng 3: 20-30 trang, đọc khi cần
│   ├── ch01-extract.md
│   └── ...
├── TIER-4-KNOWLEDGE-GRAPH/          # Tầng 4: 5-10 trang, tra cứu
│   ├── graph.md                     # Mermaid diagram
│   ├── cross-references.md
│   └── contradictions.md
├── validation/                      # Audit trail (Phase 3)
│   ├── round1-questions.md
│   ├── round1-answers.md
│   ├── round1-gaps.md
│   ├── round2-questions.md
│   ├── round2-answers.md
│   ├── round2-gaps.md
│   ├── final-gaps.md
│   └── COMPLETENESS_SCORE.md
└── raw-extracts/                    # Phase 2 output (trước khi encode)
    ├── ch01-extract.md
    └── ...
```

## Quy tắc chất lượng (vi phạm = dừng)

1. **Không "tưởng tượng"**: Mọi thông tin phải có trong sách. Không bịa.
2. **Không bỏ data**: Số liệu, thống kê, nghiên cứu phải giữ.
3. **Không bỏ context**: Câu chuyện, case study phải giữ outcome + lesson.
4. **Teacher-Student ≥2 vòng**: Phải chạy validate loop ít nhất 2 lần.
5. **Completeness ≥85%**: Điểm bao phủ phải đạt 85% trước khi xuất.
6. **User review executive summary**: Phase 5 phải让用户确认 Tầng 1.

## Thời gian ước tính

| Sách | Phase 1 | Phase 2 | Phase 3 | Phase 4 | Phase 5 | Tổng |
|------|---------|---------|---------|---------|---------|------|
| 200 trang | 10 phút | 20 phút | 15 phút | 10 phút | 5 phút | ~1 giờ |
| 500 trang | 15 phút | 40 phút | 30 phút | 15 phút | 10 phút | ~2 giờ |
| 1000 trang | 25 phút | 60 phút | 45 phút | 20 phút | 15 phút | ~3 giờ |

## So sánh với alternatives

| Framework | Mục đích | Nén | Giữ lại | Output |
|-----------|----------|-----|---------|--------|
| **SIEVE** (này) | Hiểu sách | 90% | 85-92% | 50 trang layered |
| **Progressive Summarization** | Ghi chú cá nhân | 80% | 60-70% | Highlight layers |
| **Tóm tắt thông thường** | Overview nhanh | 98% | 20-30% | 2-3 trang |

## Ghi chú cho AI caller

- **Luôn đọc file sách trước** — không "dựa trên kiến thức" mà không có text.
- **Báo cáo progress giữa các phase** — không chạy silent rồi dump kết quả.
- **Phase 3 là bắt buộc** — không skip teacher-student loop.
- **4-tier output là bắt buộc** — không merge thành 1 file.
- **User có thể dừng giữa chừng** — lưu progress, có thể resume sau.
