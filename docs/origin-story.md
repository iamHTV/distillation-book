# SIEVE — Lịch sử phát triển

## Bối cảnh

SIEVE ra đời từ cuộc thảo luận về cách chưng cất kiến thức từ sách.

### Điểm xuất phát: Cangjie-skill

Cuộc thảo luận bắt đầu khi phân tích **cangjie-skill** — một framework chưng cất sách thành AI skills.

**Cangjie-skill làm tốt:**
- Pipeline rõ ràng (RIA-TV++)
- 5 extractor song song
- Tam trọng lọc (V1/V2/V3)
- Stress test với bẫy

**Nhưng cangjie-skill có vấn đề:**
- Nén quá mạnh: 500 trang → 12 skill (giữ 5-10%)
- Bỏ data, stories, context
- Chỉ giữ "phương pháp luận có thể dùng lại"
- Không có cơ chế chống miss

### Insight: Hai mục đích khác nhau

| | Cangjie (skill extraction) | Cái cần có (book comprehension) |
|---|---|---|
| **Câu hỏi** | "Sách này có gì dùng được?" | "Sách này nói gì?" |
| **Bộ lọc** | Chỉ giữ phương pháp luận | Giữ mọi thứ有价值 |
| **Kết quả** | 12 skill (dùng được) | 50 pages (hiểu được) |

→ Cần thiết kế khác hoàn toàn.

---

## Quá trình thảo luận

### Bước 1: Phân tích cangjie-skill

Đọc kỹ SKILL.md, methodology, extractors, templates của cangjie-skill.

**Nhận xét:**
- Thiết kế tốt cho mục đích "tạo skill"
- V1/V2/V3 là cơ chế lọc hợp lý
- Nhưng quá aggressive cho mục đích "hiểu sách"

### Bước 2: Xác định vấn đề

User: "Tôi muốn hiểu sách đầy đủ mà không miss nhiều thông tin như skill trên."

**Phân tích:**
- Cangjie: Nén 95%, giữ 5-10%
- User muốn: Nén 90%, giữ 85-92%
- Cần cơ chế chống miss

### Bước 3: Thiết kế Multi-Pass approach

Đề xuất: Thay vì 1 lần đọc + lọc, đọc nhiều lần + kiểm tra.

**Các thành phần:**
1. 5 Extractor (mở rộng từ cangjie)
2. Teacher-Student Loop (innovation mới)
3. 4-Tier Output (layered approach)

### Bước 4: Knowledge Distillation concept

User: "Tôi nghe đến knowledge distillation, nó giống cái mình muốn làm đúng không?"

**Phân tích:**
- Knowledge Distillation (ML): Model lớn → Model nhỏ
- Knowledge Distillation (tri thức): Nguồn phức tạp → Dạng dễ hiểu
- SIEVE là knowledge distillation ở nghĩa rộng

### Bước 5: Hình thành framework

Tổng hợp tất cả thảo luận thành framework hoàn chỉnh:

**SIEVE = Structure → Iterative Extract → Validate → Encode → Verify**

- Phase 1: Hiểu cấu trúc sách
- Phase 2: Trích xuất theo 5 extractor
- Phase 3: Teacher-Student loop (2-3 vòng)
- Phase 4: 4-tier output
- Phase 5: Quality gate + user review

### Bước 6: Triển khai

- Tạo GitHub repo: `distillation-book`
- Viết SKILL.md, methodology, templates
- Cài vào skillshare
- Tạo README (Vietnamese + English)

---

## Các quyết định thiết kế

### Q1: Tại sao 5 extractor mà không phải ít hơn?

**Quyết định:** Giữ 5 extractor từ cangjie nhưng mở rộng.

**Lý do:**
- 3 extractor: Thiếu Data và Contrarian → miss bằng chứng cứng và sắc thái
- 5 extractor: Cover Argument, Data, Narrative, Concept, Contrarian
- 7 extractor: Quá nhiều overlap, tăng thời gian không tăng chất lượng

### Q2: Tại sao cần Teacher-Student loop?

**Quyết định:** Thêm bước validation mà cangjie không có.

**Lý do:**
- Cangjie chỉ validate 1 lần (V1/V2/V3) → có thể miss
- Teacher-Student loop: Dùng output hỏi lại sách gốc → tìm miss → bổ sung → lặp
- Đây là innovation chính, khác biệt lớn nhất với cangjie

### Q3: Tại sao output theo tầng?

**Quyết định:** 4-tier thay vì 1 file.

**Lý do:**
- Mỗi người có nhu cầu khác nhau
- Người bận rộn: chỉ đọc Tầng 1 (15 phút)
- Người muốn chi tiết: đọc Tầng 3 (2-3 giờ)
- Tầng cho phép chọn mức độ phù hợp

### Q4: Tại sao giữ data và stories?

**Quyết định:** Không bỏ data và stories như cangjie.

**Lý do:**
- Data là bằng chứng cứng → bỏ data = mất credibility
- Stories là minh họa thực tế → bỏ stories = mất context
- Cangjie bỏ vì chỉ cần "phương pháp luận", SIEVE giữ vì cần "hiểu sách"

### Q5: Tại sao tách skill folder?

**Quyết định:** SKILL.md + references/ + assets/ trong 1 folder.

**Lý do:**
- Skill-creator convention: SKILL.md ở root, resources trong subfolder
- Progressive disclosure: SKILL.md luôn load, references load khi cần
- README ở ngoài: docs cho repo, không phải skill

---

## Timeline

| Ngày | Sự kiện |
|------|---------|
| 2026-05-09 | Bắt đầu thảo luận về cangjie-skill |
| 2026-05-09 | Phân tích cangjie-skill, xác định vấn đề |
| 2026-05-09 | Thiết kế SIEVE framework |
| 2026-05-09 | Tạo GitHub repo, viết docs |
| 2026-05-09 | Cài vào skillshare |
| 2026-05-09 | Restructure theo skill-creator convention |

---

## Tương lai

Xem `research-notes.md` cho danh sách cải tiến đang nghiên cứu.
