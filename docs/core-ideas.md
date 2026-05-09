# SIEVE — Cốt lõi & Triết lý

## Tại sao SIEVE tồn tại?

### Bài toán gốc

Bạn đọc sách nhưng không có thời gian. Bạn muốn **hiểu sách đầy đủ** mà không miss thông tin quan trọng.

### Các framework hiện tại chưa giải quyết được

| Framework | Làm tốt | Vấn đề |
|-----------|---------|--------|
| **Tóm tắt thông thường** | Nhanh, gọn | Nén 98%, mất 70-80% thông tin |
| **Progressive Summarization** | Cá nhân hóa | Không có cơ chế chống miss |
| **Skill extraction (RIA-TV++)** | Tạo tool gọi được | Nén 95%, chỉ giữ "dùng được", bỏ data, stories, context |

### Insight cốt lõi

> **"Không biết mình miss gì" là vấn đề lớn nhất của mọi distillation.**

Khi bạn tóm tắt một cuốn sách, bạn không biết bạn đã bỏ lỡ điều gì. Không có cơ chế nào kiểm tra "tôi đã miss cái gì chưa?"

SIEVE giải quyết vấn đề này bằng **Teacher-Student Loop**: dùng output đã trích (Student) để tạo câu hỏi → hỏi lại sách gốc (Teacher) → tìm chỗ miss → bổ sung → lặp 2-3 vòng.

---

## 5 Nguyên tắc bất biến

### 1. Faithfulness (Trung thực)

Mọi thông tin phải có trong sách. Không bịa, không suy luận, không "dựa trên kiến thức".

**Tại sao quan trọng:** Nếu AI bịa thông tin, người đọc tưởng đó là sách nói → hiểu sai sách.

### 2. Completeness (Đầy đủ)

≥85% thông tin有价值的 phải được capture. Không cố ý bỏ sót.

**Tại sao quan trọng:** Nếu chỉ giữ 50%, người đọc hiểu sai bức tranh tổng thể.

### 3. Structure (Cấu trúc)

Output phải theo 4 tầng, không merge thành 1 file.

**Tại sao quan trọng:** Mỗi người có nhu cầu khác nhau. Người bận rộn chỉ đọc Tầng 1 (15 phút). Người muốn chi tiết đọc Tầng 3 (2-3 giờ). Cấu trúc tầng cho phép chọn mức độ phù hợp.

### 4. Validation (Kiểm chứng)

Phải chạy ≥2 vòng Teacher-Student loop.

**Tại sao quan trọng:** Vòng 1 tìm gap lớn. Vòng 2 tìm gap nhỏ. Không chạy loop = không biết mình miss gì.

### 5. User Involvement (Tham gia của người dùng)

Executive summary phải让用户确认 trước khi交付.

**Tại sao quan trọng:** AI có thể hiểu sai主旨 của sách. User đọc sách → biết AI có tóm tắt đúng không.

---

## 5 Extractor — Tại sao cần 5 góc nhìn?

### Vấn đề: Single-perspective reading

Khi đọc sách, bạn chỉ có 1 góc nhìn. Bạn có thể miss:
- Data mà bạn không chú ý
- Counter-argument mà bạn bỏ qua
- Story mà bạn quên
- Concept mà bạn không nhận ra là quan trọng

### Giải pháp: 5 "chuyên gia" đọc cùng lúc

| Extractor | Chuyên môn | Tìm gì |
|-----------|-----------|--------|
| **Argument** | Logic & reasoning | Luận điểm + bằng chứng + counter-argument |
| **Data** | Evidence & numbers | Số liệu, thống kê, nghiên cứu |
| **Narrative** | Stories & examples | Case study, câu chuyện, outcome |
| **Concept** | Definitions & frameworks | Thuật ngữ, định nghĩa, model |
| **Contrarian** | Limitations & warnings | Phản bác, giới hạn, ngoại lệ |

### Tại sao 5 mà không phải 3 hay 7?

- **<5**: Thiếu góc nhìn. Data và Contrarian thường bị bỏ qua nếu chỉ có 3.
- **>7**: Quá nhiều overlap, tăng thời gian mà không tăng chất lượng.
- **5**: Đủ để cover Argument, Data, Narrative, Concept, Contrarian — 5 loại tri thức chính trong sách.

### Kết quả

5 extractor chạy song song → merge → giảm blind spot so với 1 lần đọc.

---

## Teacher-Student Loop — Innovation chính

### Vấn đề

Sau khi trích xuất, bạn không biết:
- Mình đã miss luận điểm nào?
- Mình đã miss data nào?
- Mình đã miss sắc thái nào?

### Giải pháp

```
Student (output đã trích) → Tạo câu hỏi → Hỏi Teacher (sách gốc) → Tìm gap → Bổ sung → Lặp
```

### Chi tiết

**Vòng 1:** Student ban đầu → 50 câu hỏi → Tìm 15-20 gap → Bổ sung → Student'

**Vòng 2:** Student' → 30 câu hỏi → Tìm 5-8 gap → Bổ sung → Student''

**Vòng 3:** Student'' → 10 câu hỏi → Tìm 1-2 gap nhỏ → Bổ sung → Final

### 5 loại câu hỏi kiểm tra

| Loại | Mục đích | Ví dụ |
|------|----------|-------|
| **Factual Verification** | Kiểm tra sự thật | "Luận điểm X có đúng với nguyên văn không?" |
| **Coverage Check** | Kiểm tra độ bao phủ | "Chương Y nói gì? Extract có miss không?" |
| **Completeness Check** | Kiểm tra tính đầy đủ | "Luận điểm A có counter-argument nào miss không?" |
| **Cross-Reference** | Kiểm tra liên kết | "Chương 3 có nhắc đến khái niệm chương 1 không?" |
| **Nuance Check** | Kiểm tra sắc thái | "Tác giả có điều kiện hóa/hạn chế hóa không?" |

### Tại sao innovation này quan trọng?

Các framework khác (Progressive Summarization, RIA-TV++) **không có bước này**. Họ trích xuất 1 lần và hy vọng không miss. SIEVE trích xuất → kiểm tra → bổ sung → kiểm tra lại → đảm bảo completeness.

---

## 4-Tier Output — Tại sao theo tầng?

### Vấn đề

Mỗi người có nhu cầu khác nhau:
- Người bận rộn: chỉ muốn biết "sách nói gì" trong 15 phút
- Người muốn overview: đọc 1 giờ, hiểu 75%
- Người muốn chi tiết: đọc 2-3 giờ, hiểu 90%
- Người muốn deep dive: tra cứu liên kết

### Giải pháp: 4 tầng

| Tầng | Nội dung | Thời gian | Hiểu được |
|------|----------|-----------|-----------|
| **1: Executive Summary** | Key takeaways, giới hạn, ai nên đọc | 15 phút | 50% |
| **2: Chapter Summaries** | Luận điểm, data, case mỗi chương | 1 giờ | 75% |
| **3: Detailed Extracts** | Mọi thứ chi tiết, có nguyên văn | 2-3 giờ | 90% |
| **4: Knowledge Graph** | Mối liên kết, contradictions | Tra cứu | Liên kết |

### Tại sao không merge thành 1 file?

- File dài quá → người đọc không biết bắt đầu từ đâu
- Không có "mức độ" → người bận rộn bỏ cuộc
- Tầng cho phép **đọc trước, tra cứu sau**

---

## So sánh triết lý với các approach khác

### SIEVE vs Progressive Summarization

| | Progressive Summarization | SIEVE |
|---|---|---|
| **Cơ chế** | Highlight → Tóm tắt highlight → Tóm tắt tóm tắt | 5 extractor + Teacher-Student loop |
| **Chống miss** | Không có | Teacher-Student loop (2-3 vòng) |
| **Output** | Layers trong 1 file | 4 files riêng biệt |
| **Phù hợp** | Ghi chú cá nhân | Hiểu sách đầy đủ |

### SIEVE vs RIA-TV++ (Skill Extraction)

| | RIA-TV++ | SIEVE |
|---|---|---|
| **Mục đích** | Tạo skill gọi được | Hiểu sách |
| **Bộ lọc** | Chỉ giữ "dùng được" | Giữ mọi thứ有价值 |
| **Độ nén** | 95% (500→12 skill) | 90% (500→50 pages) |
| **Data** | Bỏ | Giữ |
| **Stories** | Chỉ giữ "phương pháp" | Giữ outcome + lesson |
| **Validation** | V1/V2/V3 (1 lần) | Teacher-Student (2-3 lần) |

### SIEVE vs Tóm tắt thông thường

| | Tóm tắt | SIEVE |
|---|---|---|
| **Độ nén** | 98% | 90% |
| **Thông tin giữ** | 20-30% | 85-92% |
| **Cấu trúc** | 1 file | 4 tầng |
| **Chống miss** | Không | Teacher-Student loop |

---

## Tóm tắt

SIEVE được thiết kế để giải quyết 1 bài toán cụ thể: **hiểu sách đầy đủ mà không đọc hết**.

Các innovation chính:
1. **5 Extractor** — 5 góc nhìn giảm blind spot
2. **Teacher-Student Loop** — Cơ chế chống miss
3. **4-Tier Output** — Đọc tầng nào hiểu tầng đó

Mục tiêu: Nén 90% (500→50 pages), giữ 85-92% thông tin有价值的.
