# Phase 3 — Validate: Teacher-Student Loop (CỐT LÕI)

## Mục tiêu

Dùng output đã trích (Student) để tạo câu hỏi → hỏi lại sách gốc (Teacher) → tìm chỗ miss → bổ sung.

**Đây là cơ chế chống thiếu sót chính của SIEVE.**

## Nguyên tắc

```
Student = Phase 2 output (raw-extracts)
Teacher = Full text sách gốc

Student không biết mình miss gì.
Teacher biết tất cả.
Dùng Student để generate questions → hỏi Teacher → tìm gap → refine Student.
```

## Quy trình chi tiết

### Bước 3.1 — Generate Questions từ Student

Từ Phase 2 output, tự动生成 5 loại câu hỏi:

#### Loại 1: Factual Verification (Kiểm tra sự thật)

```
"Mục X trong extract nói rằng [claim]. Điều này có đúng với nguyên văn sách không?"
"Data Y được ghi là [value]. Sách có nói như vậy không? Ở đâu?"
"Story Z kể rằng [outcome]. Sách có ghi outcome này không?"
```

**Mục đích:** Đảm bảo extract không sai lệch so với nguyên văn.

#### Loại 2: Coverage Check (Kiểm tra độ bao phủ)

```
"Chương N nói về chủ đề gì? Extract có cover đầy đủ không?"
"Có luận điểm nào trong chương mà extract bỏ sót không?"
"Chương này có bao nhiêu arguments? Extract ghi được bao nhiêu?"
```

**Mục đích:** Đảm bảo không miss luận điểm chính.

#### Loại 3: Completeness Check (Kiểm tra tính đầy đủ)

```
"Luận điểm A có counter-argument nào trong sách mà extract miss không?"
"Case study B có outcome nào mà extract không ghi?"
"Concept C có điều kiện hóa/hạn chế nào mà extract bỏ qua?"
```

**Mục đích:** Đảm bảo thông tin được ghi đầy đủ, không thiếu chi tiết quan trọng.

#### Loại 4: Cross-Reference Check (Kiểm tra liên kết)

```
"Chương 3 có nhắc đến khái niệm từ chương 1 không? Extract có ghi liên kết không?"
"Có mối liên hệ nào giữa chương 5 và chương 8 mà extract miss không?"
"Tác giả có so sánh X với Y ở đâu không?"
```

**Mục đích:** Đảm bảo knowledge graph đầy đủ edges.

#### Loại 5: Nuance Check (Kiểm tra sắc thái)

```
"Tác giả có điều kiện hóa/hạn chế hóa luận điểm C không?"
"Có ngoại lệ nào cho nguyên tắc D mà extract bỏ sót không?"
"Tác giả có thừa nhận giới hạn của phương pháp E không?"
```

**Mục đích:** Đảm bảo sắc thái, điều kiện hóa không bị mất.

### Bước 3.2 — Query Teacher

Mỗi câu hỏi → tìm trong full text sách → trả lời:

```markdown
## Q: [Câu hỏi]

### Teacher Answer
[Trả lời từ sách, có trích dẫn vị trí chương/trang]

### Source Quote
"[Nguyên văn ≤200 chữ]" — Chương X, trang Y

### Gap Type
NONE / MISSING / INCOMPLETE / WRONG / WEAK_LINK / NUANCE

### Action
[Không cần sửa / Cần bổ sung / Cần sửa]
```

### Bước 3.3 — Gap Analysis

So sánh answer từ teacher với student extract:

```markdown
# Gap Report — Round N

## Thống kê
- Tổng câu hỏi: XX
- NONE (không có gap): XX (XX%)
- MISSING (thiếu hoàn toàn): XX (XX%)
- INCOMPLETE (thiếu chi tiết): XX (XX%)
- WRONG (sai): XX (XX%)
- WEAK_LINK (miss liên kết): XX (XX%)
- NUANCE (miss sắc thái): XX (XX%)

## Chi tiết gap

### MISSING-01: [Thông tin bị miss]
- Chương: X
- Nội dung: [Thông tin có trong sách nhưng extract không trích]
- Hành động: Bổ sung vào chNN-extract.md

### INCOMPLETE-01: [Thông tin thiếu chi tiết]
- Chương: X
- Hiện tại: [Extract ghi gì]
- Cần thêm: [Thông tin cần bổ sung]
- Hành động: Bổ sung vào chNN-extract.md

### WRONG-01: [Thông tin sai] (hiếm)
- Chương: X
- Extract ghi: [Sai]
- Sách nói: [Đúng]
- Hành động: Sửa trong chNN-extract.md

### WEAK_LINK-01: [Liên kết bị miss]
- Chương: X ↔ Chương: Y
- Mối liên hệ: [Gì]
- Hành động: Thêm vào cross-references

### NUANCE-01: [Sắc thái bị miss]
- Chương: X
- Sắc thái: [Điều kiện hóa / ngoại lệ / giới hạn]
- Hành động: Bổ sung vào chNN-extract.md
```

### Bước 3.4 — Refine Student

Dựa trên gap report, cập nhật extract:

1. **MISSING** → Thêm thông tin mới vào extract
2. **INCOMPLETE** → Bổ sung chi tiết
3. **WRONG** → Sửa thông tin sai
4. **WEAK_LINK** → Thêm cross-reference
5. **NUANCE** → Thêm điều kiện hóa / giới hạn

### Bước 3.5 — Lặp lại

```
Vòng 1: Student ban đầu → 50 câu hỏi → Gap Report → Refine → Student'
Vòng 2: Student' → 30 câu hỏi → Gap Report → Refine → Student''
Vòng 3: Student'' → 10 câu hỏi → Gap Report → (gap很小) → Final

Khi nào dừng:
- Số MISSING gap = 0
- Tổng gap < 15% tổng câu hỏi
- Hoặc đã chạy ≥3 vòng
```

## Output Phase 3

```
validation/
├── round1/
│   ├── questions.md        # 50 câu hỏi vòng 1
│   ├── answers.md          # Trả lời từ teacher
│   └── gaps.md             # Gap report
├── round2/
│   ├── questions.md        # 30 câu hỏi vòng 2
│   ├── answers.md
│   └── gaps.md
├── round3/
│   ├── questions.md        # 10 câu hỏi vòng 3
│   ├── answers.md
│   └── gaps.md
├── final-gaps.md           # Gap report cuối cùng
└── COMPLETENESS_SCORE.md   # Điểm bao phủ
```

## COMPLETENESS_SCORE.md

```markdown
# Completeness Score

## Thống kê tổng
- Tổng câu hỏi (3 vòng): 90
- NONE: 75 (83%)
- MISSING: 3 (3%) → đã fix
- INCOMPLETE: 5 (6%) → đã fix
- WRONG: 0 (0%)
- WEAK_LINK: 4 (4%) → đã fix
- NUANCE: 3 (3%) → đã ghi chú

## Điểm bao phủ
**92%** (chỉ còn 3 NUANCE gap nhỏ, đã ghi chú trong extract)

## Đánh giá
PASS — Có thể sang Phase 4
```

## Quality Gate Phase 3

```
□ Đã chạy ≥2 vòng teacher-student?
□ Số MISSING gap = 0?
□ Completeness score ≥85%?
□ Không còn WRONG gap?
□ Các NUANCE gap đã được ghi chú trong extract?
□ Final-gaps.md đã được tạo?
→ Nếu FAIL: chạy thêm vòng hoặc user can thiệp
→ Nếu PASS: sang Phase 4
```

## Lưu ý

- **Chất lượng câu hỏi quyết định chất lượng validation**: Câu hỏi tốt = phát hiện gap tốt. Câu hỏi tồi = miss gap.
- **WRONG gap rất hiếm nhưng rất nguy hiểm**: Nếu có WRONG gap, phải sửa ngay.
- **NUANCE gap quan trọng**: Đây là sắc thái mà大多数 tóm tắt sẽ miss. Ghi chú rõ ràng.
- **Teacher-Student loop là innovation chính**: Cangjie không có bước này, nên miss nhiều.
