# DESIGN.md — Resume Mockup Redesign

## 1. Design Direction

Thiết kế resume theo hướng **professional, tối giản, hiện đại và premium corporate**.  
Phong cách tổng thể cần giữ sự nghiêm túc của hồ sơ kỹ thuật / BIM / structural drafting, nhưng tinh tế hơn bản hiện tại.

Từ source hiện tại, resume đang dùng layout 2 cột với `Inter`, nền giấy off-white, sidebar trái và main content phải. Bản mockup mới tiếp tục giữ cấu trúc này nhưng nâng cấp mạnh về hierarchy, visual rhythm, portrait area, icon system và background treatment.

---

## 2. Core Visual Style

### Keywords

- Professional
- Minimal
- Modern
- Premium
- Engineering / BIM inspired
- Recruiter-friendly
- Print-friendly
- Clean editorial layout

### Không nên

- Không dùng màu quá sặc sỡ.
- Không dùng background đậm làm giảm khả năng đọc.
- Không dùng quá nhiều hiệu ứng nổi khối.
- Không biến resume thành poster / brochure.
- Không để icon hoặc họa tiết blueprint cạnh tranh với nội dung chính.

---

## 3. Page Layout

### Page

- Kích thước: A4 portrait.
- Nền giấy: off-white / warm white, không dùng trắng tinh hoàn toàn.
- Bo góc nhẹ: `6px – 10px`.
- Shadow rất nhẹ khi preview trên web.
- Khi print/PDF: loại bỏ shadow, giữ layout sạch.

```css
--bg-screen: #f3f4f6;
--bg-paper: #fbfaf6;
--text-main: #111827;
--text-muted: #4b5563;
--text-light: #6b7280;
--accent: #0f3a63;
--line: #d9dee7;
```

### Grid

Dùng layout 2 cột bất đối xứng:

```css
.cv-grid {
  display: grid;
  grid-template-columns: 280px 1fr;
  gap: 44px;
}
```

- Cột trái: portrait, name, contact, skills, education, languages.
- Cột phải: summary, work experience, featured projects.
- Thêm vertical divider mảnh giữa 2 cột.

```css
.main-col {
  border-left: 1px solid rgba(15, 58, 99, 0.22);
  padding-left: 36px;
}
```

---

## 4. Portrait Area

### Vị trí

Ảnh chân dung đặt ở đầu sidebar trái, phía trên tên.

### Style

- Hình tròn.
- Kích thước đề xuất: `150px – 170px`.
- Căn giữa theo sidebar.
- Viền navy mảnh.
- Có khoảng trắng giữa ảnh và viền để trông premium hơn.
- Có thể dùng grayscale hoặc ảnh màu đã cân bằng trắng tốt.

```css
.portrait-wrap {
  width: 164px;
  height: 164px;
  border-radius: 50%;
  padding: 6px;
  border: 2px solid var(--accent);
  margin: 0 auto 22px;
  background: #fff;
}

.portrait {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  filter: grayscale(100%);
}
```

### Ghi chú

Ảnh chân dung nên là headshot chuyên nghiệp, nền studio sáng, khuôn mặt rõ, expression neutral-friendly.  
Không dùng ảnh quá cinematic hoặc quá casual.

---

## 5. Header / Name Block

Tên nên lớn, rõ, tạo điểm neo thị giác.

```css
.name {
  font-size: 48px;
  font-weight: 800;
  line-height: 0.95;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: var(--text-main);
}
```

Title nằm dưới tên:

```css
.title {
  margin-top: 12px;
  font-size: 15px;
  font-weight: 700;
  line-height: 1.35;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--accent);
}
```

Nên giữ tên ở sidebar vì bản mockup có portrait + name tạo thành personal identity block rất mạnh.

---

## 6. Background Treatment

Nền trắng hiện tại hơi đơn điệu, nên thêm background rất nhẹ nhưng vẫn print-friendly.

### Hướng đề xuất

Dùng **architectural blueprint / structural wireframe line art** ở opacity thấp.

Vị trí:

- Góc trên phải.
- Góc dưới phải.
- Một phần rất nhẹ ở đáy sidebar trái.

Không đặt họa tiết dưới vùng text dày.

```css
.sheet::before {
  content: "";
  position: absolute;
  inset: 0;
  background-image: url("./blueprint-lines.svg");
  background-repeat: no-repeat;
  background-position: top right, bottom right;
  background-size: 360px auto, 420px auto;
  opacity: 0.055;
  pointer-events: none;
}
```

Nếu không dùng SVG riêng, có thể tạo bằng CSS line pattern:

```css
.sheet::after {
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  width: 420px;
  height: 360px;
  opacity: 0.06;
  background:
    linear-gradient(30deg, transparent 48%, var(--accent) 49%, transparent 50%),
    linear-gradient(150deg, transparent 48%, var(--accent) 49%, transparent 50%);
  pointer-events: none;
}
```

### Mức độ

- Opacity: `0.04 – 0.08`.
- Line width: `1px`.
- Màu: navy hoặc slate gray.
- Không dùng pattern quá dày.

---

## 7. Accent System

Mockup dùng các accent sau:

### Vertical Navy Strip

Một dải navy mảnh ở mép trái giúp resume bớt phẳng.

```css
.sheet::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 16px;
  background: var(--accent);
}
```

Có thể thêm notch nhỏ để tạo cảm giác kỹ thuật:

```css
.accent-notch {
  position: absolute;
  left: 16px;
  top: 260px;
  width: 10px;
  height: 32px;
  background: var(--accent);
  clip-path: polygon(0 0, 100% 50%, 0 100%);
}
```

### Section Heading Line

Mỗi section title có icon tròn + heading + line kéo dài + dot ở cuối.

```css
.section-heading {
  display: flex;
  align-items: center;
  gap: 14px;
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-weight: 800;
}

.section-heading::after {
  content: "";
  flex: 1;
  height: 1px;
  background: var(--accent);
  opacity: 0.45;
}
```

---

## 8. Icon System

Icon nên dùng line icon đơn giản, cùng stroke width.

### Style

- Icon trong circle navy cho main sections.
- Icon nhỏ trong sidebar contact/language/education.
- Icon skill nằm trong ô nhỏ bên trái mỗi skill row.

```css
.icon-circle {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  display: grid;
  place-items: center;
}
```

### Nguyên tắc

- Không dùng quá nhiều style icon khác nhau.
- Không dùng icon quá chi tiết.
- Stroke icon nên đồng nhất khoảng `1.75px – 2px`.

---

## 9. Contact Section

Contact nên chuyển từ label dọc sang row có icon để hiện đại hơn.

```html
<div class="contact-item">
  <span class="contact-icon">...</span>
  <a href="mailto:phubui277@gmail.com">phubui277@gmail.com</a>
</div>
```

```css
.contact-item {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 12px;
  color: var(--text-main);
}
```

---

## 10. Skills & Tools

Thay chip nhỏ bằng skill row có icon để dễ scan hơn.

```css
.skill-row {
  display: grid;
  grid-template-columns: 32px 1fr;
  align-items: center;
  min-height: 30px;
  border: 1px solid rgba(15, 58, 99, 0.14);
  border-radius: 6px;
  background: rgba(255, 255, 255, 0.55);
}
```

### Skills cần có

- Allplan (Expert)
- BIM Implementation
- DIN 1045-1
- SIA 262
- Eurocode 2
- PythonParts API
- SmartParts
- Python
- Team Coordination
- QA / QC
- Mentoring

---

## 11. Main Content

### Professional Summary

Chia thành 2 đoạn ngắn thay vì một đoạn dài.

Mục tiêu:

- Đoạn 1: năng lực chuyên môn + tiêu chuẩn + thị trường Germany/Switzerland.
- Đoạn 2: leadership + automation.

### Work Experience

Header nên có:

- Role bold.
- Company navy.
- Date align right.
- Location italic/muted.

Bullet nên ngắn, scan nhanh, có bold keyword:

- hundreds of structural projects
- DIN and SIA
- Allplan 3D workflow
- PythonParts
- 300+ reusable structural details

---

## 12. Featured Projects

Nên dùng numbered project list để tạo cảm giác portfolio/proof-of-work.

```css
.project-item {
  display: grid;
  grid-template-columns: 36px 1fr;
  gap: 14px;
  padding: 14px 0;
  border-bottom: 1px dashed rgba(15, 58, 99, 0.24);
}

.project-number {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  display: grid;
  place-items: center;
  font-weight: 800;
}
```

### Project meta

Meta line nên dùng navy italic hoặc semi-muted:

```css
.project-meta {
  color: var(--accent);
  font-size: 11px;
  font-style: italic;
}
```

---

## 13. Typography

Font chính: `Inter`.

```css
--font-sans: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
```

### Size đề xuất

- Name: `46px – 52px`
- Title: `14px – 15px`
- Section heading: `13px`
- Body: `12px – 12.5px`
- Sidebar text: `11px – 12px`
- Project title: `14px`
- Meta: `10.5px – 11px`

### Letter spacing

- Section title: `0.10em – 0.14em`
- Name: `0.02em – 0.05em`

---

## 14. Print / PDF Notes

Resume vẫn cần export PDF tốt.

```css
@media print {
  body {
    background: #fff;
    padding: 0;
  }

  .sheet {
    box-shadow: none;
    border-radius: 0;
    width: 210mm;
    min-height: 297mm;
  }

  .no-print {
    display: none !important;
  }

  .sheet::before,
  .sheet::after {
    print-color-adjust: exact;
    -webkit-print-color-adjust: exact;
  }
}
```

Lưu ý: background blueprint phải cực nhẹ để khi in không bị bẩn giấy.

---

## 15. Implementation Checklist

- [ ] Tăng sidebar từ `200px` lên khoảng `270px – 290px`.
- [ ] Thêm portrait circular frame ở đầu sidebar.
- [ ] Chuyển name/title sang uppercase block lớn dưới portrait.
- [ ] Thêm vertical navy accent strip ở mép trái.
- [ ] Thêm background off-white thay vì white/cream phẳng.
- [ ] Thêm blueprint/wireframe line art opacity thấp.
- [ ] Đổi section title thành icon circle + heading line + end dot.
- [ ] Chuyển contact thành icon rows.
- [ ] Chuyển skills chip thành skill rows có icon.
- [ ] Dùng numbered badges cho Featured Projects.
- [ ] Dùng dashed divider giữa project items.
- [ ] Giữ toàn bộ text readable, không để pattern nằm dưới text chính quá rõ.
- [ ] Kiểm tra lại bản print/PDF.

---

## 16. Final Design Summary

Bản resume mới nên giữ tính chuyên nghiệp của bản cũ nhưng có identity rõ hơn nhờ portrait circular frame, name block lớn, navy accent strip và blueprint background rất nhẹ. Tổng thể phải giống một CV cao cấp cho người làm structural drafting / BIM automation: sạch, kỹ thuật, đáng tin cậy, dễ scan và vẫn đủ hiện đại để nổi bật hơn resume trắng truyền thống.
