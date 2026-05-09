# Phase 2 — Iterative Extract (Trích xuất theo chương)

## Mục tiêu

Trích xuất **mọi thông tin有价值的** từ sách, theo chương, qua 5 góc nhìn khác nhau.

**Khác cangjie-skill:**
- Cangjie: Chỉ giữ "dùng được" → bỏ data, stories, context
- SIEVE: Giữ mọi thứ有价值 → data, stories, context, nuance đều giữ

## 5 Extractor

### Extractor 1: Argument (Luận điểm)

**Tìm gì:**
- Luận điểm chính + bằng chứng
- Logic / reasoning path
- Counter-argument (nếu có)
- Điều kiện hóa / hạn chế

**Không tìm:** Data thuần túy, stories không có lesson

**Identifying signals:**
- "Vì vậy..." / "Do đó..." / "Kết luận là..."
- "Bằng chứng cho thấy..." / "Nghiên cứu chỉ ra..."
- "Tuy nhiên..." / "Nhưng..." / "Mặt khác..."

**Output format:**
```yaml
- id: arg-ch01-01
  chapter: 1
  claim: "[Luận điểm]"
  evidence: "[Bằng chứng]"
  counter: "[Phản bác, nếu có]"
  conditions: "[Điều kiện, nếu có]"
  importance: ★★★ / ★★ / ★
  source_quote: "[Nguyên văn ≤200 chữ]"
```

### Extractor 2: Data (Số liệu)

**Tìm gì:**
- Số liệu, thống kê, tỷ lệ phần trăm
- Nghiên cứu, experiment, survey
- Nguồn trích dẫn (tên nghiên cứu, tác giả, năm)
- Dữ liệu so sánh (trước/sau, nhóm A/nhóm B)

**Không tìm:** Số liệu minh họa无关紧要

**Identifying signals:**
- Số + đơn vị (% , người, USD, năm...)
- "Theo nghiên cứu..." / "Dữ liệu cho thấy..."
- "Năm XXXX..." / "Từ năm... đến năm..."
- Bảng, biểu đồ

**Output format:**
```yaml
- id: data-ch01-01
  chapter: 1
  data_point: "[Số liệu]"
  context: "[Ngữ cảnh: nói về cái gì]"
  source: "[Nghiên cứu/tác giả, nếu có]"
  comparison: "[So sánh, nếu có]"
  source_quote: "[Nguyên văn ≤200 chữ]"
```

### Extractor 3: Narrative (Câu chuyện)

**Tìm gì:**
- Case study (tác giả hoặc người khác)
- Câu chuyện minh họa
- Ví dụ thực tế
- Outcome (kết quả) + Lesson learned (bài học)

**Không tìm:** Fiction,寓言 không có lesson rõ

**Identifying signals:**
- "Năm XXXX, tôi..." / "Có lần..."
- "Công ty X đã..." / "Người Y..."
- "Ví dụ..." / "Chẳng hạn..."
- Past tense + reflection

**Output format:**
```yaml
- id: story-ch01-01
  chapter: 1
  title: "[Tên câu chuyện]"
  who: "[Ai]"
  what: "[Chuyện gì]"
  outcome: "[Kết quả]"
  lesson: "[Bài học]"
  linked_to: "[Concept/argument nào]"
  source_quote: "[Nguyên văn ≤200 chữ]"
```

### Extractor 4: Concept (Khái niệm)

**Tìm gì:**
- Định nghĩa thuật ngữ
- Framework / model / matrix
- Phân loại / taxonomy
- Nguyên tắc (principle)

**Không tìm:** Từ thường, không có định nghĩa riêng

**Identifying signals:**
- "所谓 X, 是指..." / "X được định nghĩa là..."
- "Có N loại..." / "Phân thành..."
- "Mô hình X..." / "Framework Y..."
- "Nguyên tắc:..."

**Output format:**
```yaml
- id: concept-ch01-01
  chapter: 1
  term: "[Thuật ngữ]"
  definition: "[Định nghĩa tác giả]"
  key_distinction: "[Khác nghĩa thường?]"
  related_concepts: "[Liên quan concept nào]"
  source_quote: "[Nguyên văn ≤200 chữ]"
```

### Extractor 5: Contrarian (Phản bác / Giới hạn)

**Tìm gì:**
- Cảnh báo, hạn chế, giới hạn
- Phản bác, counter-argument
- Ngoại lệ
- "Nhưng thực tế..."
- Tác giả thừa nhận sai / giới hạn

**Không tìm:** Phê bình无关紧要

**Identifying signals:**
- "Tuy nhiên..." / "Nhưng..." / "Mặt khác..."
- "Hạn chế là..." / "Giới hạn của..."
- "Ngoại lệ:..." / "Trừ khi..."
- "Tôi sai khi..." / "Thực tế cho thấy..."
- "Nhiều người nghĩ X, nhưng..."

**Output format:**
```yaml
- id: contra-ch01-01
  chapter: 1
  challenge: "[Phản bác / giới hạn]"
  target: "[Chống lại luận điểm nào]"
  evidence: "[Bằng chứng]"
  implication: "[Hàm ý]"
  source_quote: "[Nguyên văn ≤200 chữ]"
```

## Quy trình theo chương

```
For each chapter (★★★ trước, ★★ sau, ★ cuối):
  
  1. Đọc toàn bộ chương
  2. Chạy 5 extractor (song song nếu có thể, hoặc tuần tự)
  3. Merge kết quả → raw-extracts/chNN-extract.md
  4. Đánh dấu:
     - Mức quan trọng: ★★★ / ★★ / ★
     - Mức liên kết: chương này liên quan chương nào
     - Gap: chương này có gì mờ nhạt không?
  5. Tự hỏi:
     - Chương này có data nào mà tôi chưa trích?
     - Có story nào mà tôi miss?
     - Có counter-argument nào mà tôi bỏ qua?
```

## Output Phase 2

```
raw-extracts/
├── ch01-extract.md
├── ch02-extract.md
├── ...
└── chNN-extract.md
```

Mỗi file có cấu trúc:

```markdown
# Chương X: [Tên chương]

## Metadata
- Mức quan trọng: ★★★
- Liên quan: Chương Y, Chương Z
- Gaps đã phát hiện: [nếu có]

## Arguments
[...merged từ Argument extractor...]

## Data
[...merged từ Data extractor...]

## Stories
[...merged từ Narrative extractor...]

## Concepts
[...merged từ Concept extractor...]

## Contrarian
[...merged từ Contrarian extractor...]

## Cross-references
- Liên quan chương Y: [mối liên hệ]
- Phụ thuộc chương Z: [tại sao]
```

## Quality Gate Phase 2

```
□ Mỗi chương ★★★ đã có extract?
□ Mỗi extract có ≥3/5 loại (arguments/data/stories/concepts/contrarian)?
□ Không có chương nào bị bỏ qua hoàn toàn?
□ Raw extracts đã được merge vào raw-extracts/?
→ Nếu FAIL: đọc lại chương, bổ sung extractor bị thiếu
→ Nếu PASS: sang Phase 3
```

## Lưu ý

- **Không bỏ data**: Đây là khác biệt lớn nhất với cangjie. Data看起来无聊 nhưng rất quan trọng.
- **Giữ outcome**: Story không có outcome = story vô dụng. Phải ghi "kết quả là gì".
- **Điều kiện hóa**: Khi tác giả nói "trừ khi...", "chỉ khi...", phải ghi rõ. Đây là nuance rất dễ miss.
- **Nguyên văn ≤200 chữ**: Mở rộng từ 150 của cangjie, vì cần context nhiều hơn.
