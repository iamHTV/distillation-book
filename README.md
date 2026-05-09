# SIEVE — Book Knowledge Distillation Framework

<div align="center">

### Chưng cất kiến thức từ sách, giữ 85-92% thông tin

[![Framework: SIEVE](https://img.shields.io/badge/Framework-SIEVE-2ea44f.svg)](./SKILL.md)
[![Compression: 90%](https://img.shields.io/badge/Compression-90%25-blue.svg)](./methodology/00-overview.md)
[![Retention: 85-92%](https://img.shields.io/badge/Retention-85--92%25-green.svg)](./methodology/03-phase3-validate.md)

</div>

## Tại sao làm cái này?

Bạn đọc sách nhưng không có thời gian. Bạn muốn **hiểu sách đầy đủ** mà không miss thông tin quan trọng.

Các framework hiện tại:

| Framework | Vấn đề |
|-----------|--------|
| **Tóm tắt thông thường** | Nén 98%, mất 70-80% thông tin |
| **Progressive Summarization** | Không có cơ chế chống miss, dễ bỏ sót |

**SIEVE** giải quyết bằng cách:
1. **5 extractor song song** — 5 góc nhìn khác nhau, giảm blind spot
2. **Teacher-Student loop** — Dùng output hỏi lại sách gốc, tìm chỗ miss
3. **4-tier output** — Đọc tầng nào hiểu tầng đó, muốn sâu thì đọc tầng dưới

## SIEVE là gì?

**S**tructure → **I**terative Extract → **V**alidate (Teacher-Student) → **E**ncode → **V**erify

```
Input: Sách 500 trang
         │
         ▼
Phase 1: Structure      → Book Map + Backbone + Glossary
Phase 2: Extract        → 5 extractors × N chapters
Phase 3: Validate       → Teacher-Student loop (2-3 rounds)
Phase 4: Encode         → 4-tier output (~50 pages)
Phase 5: Verify         → Quality gate + user review
         │
         ▼
Output: ~50 trang (nén 90%, giữ 85-92%)
```

## Output 4 tầng

```
Tầng 1: Executive Summary     (2-3 trang)  → Đọc 15 phút → Hiểu 50%
Tầng 2: Chapter Summaries     (10-15 trang) → Đọc 1 giờ   → Hiểu 75%
Tầng 3: Detailed Extracts     (20-30 trang) → Đọc 2-3 giờ → Hiểu 90%
Tầng 4: Knowledge Graph       (5-10 trang)  → Tra cứu     → Hiểu liên kết
```

## Tại sao giữ được 85-92%?

### 5 Extractor (giảm blind spot)

| Extractor | Tìm gì | Tại sao cần |
|-----------|--------|-------------|
| **Argument** | Luận điểm + evidence + counter | Giữ logic của sách |
| **Data** | Số liệu, thống kê, research | Giữ bằng chứng cứng |
| **Narrative** | Case study, stories, examples | Giữ minh họa thực tế |
| **Concept** | Định nghĩa, thuật ngữ, framework | Giữ ngôn ngữ riêng |
| **Contrarian** | Phản bác, giới hạn, warnings | Giữ sắc thái |

### Teacher-Student Loop (chống miss)

```
Student: "Tôi nghĩ sách nói A, B, C"
Teacher: "Đúng, nhưng bạn miss D và E, và A cần điều kiện F"
Student: "Cảm ơn, tôi bổ sung D, E, F"
Teacher: "Bây giờ bạn miss G (nhỏ hơn)"
→ Lặp 2-3 vòng cho đến khi gap rất nhỏ
```

Đây là **innovation chính** của SIEVE.

## So sánh với alternatives

| Framework | Mục đích | Nén | Giữ lại | Output |
|-----------|----------|-----|---------|--------|
| **SIEVE** | Hiểu sách | 90% | 85-92% | 50 trang layered |
| **Progressive Summarization** | Ghi chú cá nhân | 80% | 60-70% | Highlight layers |
| **Tóm tắt thông thường** | Overview nhanh | 98% | 20-30% | 2-3 trang |

## Repo Structure

```
distillation-book/
├── SKILL.md                    # Skill definition (cho AI agent)
├── README.md                   # Bạn đang đọc
├── methodology/                # Chi tiết từng phase
│   ├── 00-overview.md          # Tổng quan SIEVE
│   ├── 01-phase1-structure.md  # Phase 1: Hiểu cấu trúc
│   ├── 02-phase2-extract.md    # Phase 2: Trích xuất
│   ├── 03-phase3-validate.md   # Phase 3: Teacher-Student loop
│   ├── 04-phase4-encode.md     # Phase 4: 4-tier output
│   └── 05-phase5-verify.md     # Phase 5: Quality gate
├── templates/                  # Output templates
│   ├── EXECUTIVE-SUMMARY.md.template
│   ├── CHAPTER-SUMMARY.md.template
│   ├── DETAILED-EXTRACT.md.template
│   └── KNOWLEDGE-GRAPH.md.template
├── extractors/                 # Extractor prompts (cho AI agent)
│   └── (coming soon)
└── examples/                   # Ví dụ output
    └── (coming soon)
```

## Sử dụng

### Cách 1: Dùng như AI Skill

Cài đặt qua skillshare:
```bash
skillshare install iamHTV/distillation-book --all
skillshare sync
```

Sau đó nói với AI agent:
> "Tóm tắt cuốn [tên sách] cho tôi, dùng SIEVE framework"

### Cách 2: Đọc methodology và tự làm

1. Đọc `methodology/00-overview.md` để hiểu flow
2. Đọc từng phase (01 → 05) để hiểu chi tiết
3. Dùng templates trong `templates/` để tạo output

## Thời gian ước tính

| Sách | Phase 1 | Phase 2 | Phase 3 | Phase 4 | Phase 5 | Tổng |
|------|---------|---------|---------|---------|---------|------|
| 200 trang | 10 phút | 20 phút | 15 phút | 10 phút | 5 phút | ~1 giờ |
| 500 trang | 15 phút | 40 phút | 30 phút | 15 phút | 10 phút | ~2 giờ |
| 1000 trang | 25 phút | 60 phút | 45 phút | 20 phút | 15 phút | ~3 giờ |

## Contributing

Framework đang được phát triển. Các phần cần cải thiện:
- [ ] Extractor prompts chi tiết (cho AI agent)
- [ ] Ví dụ output thực tế
- [ ] Auto-generate questions cho Teacher-Student loop
- [ ] Completeness scoring algorithm

## License

MIT

## Liên hệ

- GitHub: [iamHTV](https://github.com/iamHTV)
- Repo: [distillation-book](https://github.com/iamHTV/distillation-book)
