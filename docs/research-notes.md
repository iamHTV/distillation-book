# SIEVE — Research Notes & Future Improvements

## Trạng thái hiện tại

**Version:** 1.0.0
**Status:** Working prototype, chưa test trên sách thực tế

---

## Cần làm ngay (P0)

### 1. Test trên sách thực tế

**Vấn đề:** Framework chưa được验证 trên sách thật.

**Kế hoạch:**
- Chọn 1 cuốn sách methodology (200-300 trang)
- Chạy toàn bộ pipeline SIEVE
- Đánh giá output: có miss gì không? completeness bao nhiêu?
- Ghi lại lessons learned

**Sách đề xuất test:**
- "Thinking, Fast and Slow" (Daniel Kahneman) — methodology rõ ràng
- "The Lean Startup" (Eric Ries) — nhiều case study
- "Atomic Habits" (James Clear) — dễ验证

### 2. Viết Extractor prompts chi tiết

**Vấn đề:** Hiện tại extractor chỉ có description, chưa có prompt chi tiết cho AI agent.

**Kế hoạch:**
- Viết prompt cho từng extractor (Argument, Data, Narrative, Concept, Contrarian)
- Include: identifying signals, output format, self-check questions
- Test extractor trên 1 chương sách

### 3. Auto-generate questions cho Teacher-Student loop

**Vấn đề:** Hiện tại phải tự generate câu hỏi, chưa có automation.

**Kế hoạch:**
- Thiết kế prompt để AI tự generate 5 loại câu hỏi
- Test quality của câu hỏi generated
- Tune prompt để câu hỏi có chất lượng cao

---

## Cải tiến tiếp theo (P1)

### 4. Completeness scoring algorithm

**Vấn đề:** Hiện tại completeness score dựa trên gap count, chưa có algorithm chính thức.

**Kế hoạch:**
- Thiết kế formula: `completeness = 1 - (gaps / total_questions)`
- Weighted: MISSING gap nặng hơn NUANCE gap
- Threshold: ≥85% = PASS, <85% = cần thêm vòng

### 5. Chapter priority auto-detection

**Vấn đề:** Hiện tại phải tự đánh dấu ★★★/★★/★.

**Kế hoạch:**
- Dựa trên: số lượng arguments, data density, cross-references
- Chương có nhiều arguments + data = ★★★
- Chương có ít = ★

### 6. Cross-book knowledge graph

**Vấn đề:** Hiện tại knowledge graph chỉ trong 1 cuốn sách.

**Kế hoạch:**
- Cho phép link concepts giữa các sách khác nhau
- Ví dụ: "Margin of Safety" (Buffett) ↔ "Antifragile" (Taleb)
- Tạo cross-book INDEX.md

---

## Nghiên cứu dài hạn (P2)

### 7. Multi-modal extraction

**Vấn đề:** Hiện tại chỉ xử lý text.

**Kế hoạch:**
- Xử lý diagrams, charts, tables trong sách
- Extract data từ biểu đồ
- Preserve visual relationships

### 8. Incremental distillation

**Vấn đề:** Hiện tại phải distill toàn bộ sách 1 lần.

**Kế hoạch:**
- Cho phép distill từng chương
- Update knowledge graph incrementally
- Resume từ chỗ dừng

### 9. User feedback loop

**Vấn đề:** Hiện tại user chỉ review executive summary.

**Kế hoạch:**
- User có thể đánh dấu "quan trọng" / "không quan trọng" cho từng phần
- Dùng feedback để tune extraction priority
- Personalize output theo nhu cầu user

### 10. Integration với skill extraction

**Vấn đề:** SIEVE và skill extraction là 2 quá trình riêng biệt.

**Kế hoạch:**
- Pipeline: SIEVE (hiểu sách) → Skill Extraction (tạo skill)
- Dùng SIEVE output làm input cho skill extraction
- Skill extraction sẽ chính xác hơn vì có đầy đủ context

---

## Open Questions

### Q1: Độ nén tối ưu là bao nhiêu?

Hiện tại: 90% (500→50 pages). Nhưng:
- 85% (500→75 pages) có tốt hơn không?
- 95% (500→25 pages) có đủ không?

**Cần test:** Chạy SIEVE với 3 mức nén, so sánh completeness.

### Q2: Số vòng Teacher-Student tối ưu?

Hiện tại: 2-3 vòng. Nhưng:
- 1 vòng có đủ không? (nhanh hơn)
- 5 vòng có tốt hơn không? (chính xác hơn)

**Cần test:** Chạy với 1, 2, 3, 5 vòng, so sánh gap count.

### Q3: Có nên có "confidence score" cho mỗi thông tin?

Hiện tại: Mọi thông tin đều平等. Nhưng:
- Thông tin xuất hiện 3 lần trong sách = quan trọng hơn thông tin xuất hiện 1 lần
- Có nên đánh trọng số không?

**Cần test:** Thêm frequency count, xem có cải thiện quality không.

### Q4: Có nên có "controversy score" cho mỗi luận điểm?

Hiện tại: Mọi luận điểm đều平等. Nhưng:
- Luận điểm có counter-argument = thú vị hơn luận điểm không có
- Có nên highlight controversy không?

**Cần test:** Thêm controversy detection, xem user có thích không.

---

## Tài liệu tham khảo

| Nguồn | Liên quan |
|-------|-----------|
| Mortimer Adler — How to Read a Book | Phase 1: phân tích cấu trúc |
| Tiago Forte — Progressive Summarization | Tầng layered output |
| Niklas Luhmann — Zettelkasten | Liên kết concepts |
| Knowledge Distillation (ML) | Teacher-Student loop |
| RIA-TV++ (赵周) | Multi-extractor approach |

---

## Contributing

Nếu bạn có ý tưởng cải tiến:
1. Tạo issue trên GitHub
2. Mô tả vấn đề + đề xuất giải pháp
3. Nếu có prototype, tạo PR

---

## Cập nhật cuối

- **2026-05-09:** Tạo framework v1.0.0
