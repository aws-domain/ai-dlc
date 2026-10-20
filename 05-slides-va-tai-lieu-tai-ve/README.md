# Slides & tài liệu tải về

Thư mục này tổng hợp các **tài liệu/slide tải được** về AI-DLC, cùng trạng thái thu thập.

---

## ✅ Đã tải được

| File | Mô tả | Nguồn gốc |
|---|---|---|
| [`tai-lieu-pdf/Dedicatted-AI-DLC-Guide.pdf`](tai-lieu-pdf/Dedicatted-AI-DLC-Guide.pdf) | Guide PDF ~675 KB: *"From AI-assisted to AI-driven: adopting AWS AI-DLC in enterprise delivery"* — hướng dẫn áp dụng AI-DLC trong 90 ngày, mọi hình đều attribute nguồn đã công bố. Đây là tài liệu bên thứ ba (Dedicatted), **không phải slide chính thức AWS**, nhưng là tài liệu dạng "deck/guide" có cấu trúc tốt nhất tải được. | [media.dedicatted.com](https://media.dedicatted.com/wp-content/uploads/2026/08/Dedicatted-AI-DLC-Guide-1.pdf) |

---

## ⚠️ Về "slide chính thức từ AWS" — trạng thái thực tế

Tôi đã tìm kỹ. Kết luận trung thực:

- **AWS KHÔNG phát hành file slide (PPT/PDF) chính thức tải trực tiếp** cho AI-DLC. Session re:Invent 2025 **DVT214 — "Introducing AI-driven development lifecycle (AI-DLC)"** (Anupam Mishra & Raja SP) được công bố dưới dạng **video trên YouTube (kênh AWS Events)**, không kèm deck tải về.
  - Xem/nghe lại session: [Class Central — link tới video YouTube của AWS Events](https://www.classcentral.com/course/youtube-aws-re-invent-2025-introducing-ai-driven-development-lifecycle-ai-dlc-dvt214-509425)
- **Whitepaper "AI-DLC Method Definition Paper"** là bản gốc chứa nội dung "slide-like" (10 nguyên tắc, framework), nhưng được xuất bản dưới dạng **web app** (Amplify), **không phải PDF**, nên không tải thành file được:
  - [https://prod.d13rzhkk8cj2z0.amplifyapp.com/](https://prod.d13rzhkk8cj2z0.amplifyapp.com/) (cần bật JavaScript để đọc)
- Các "hình/diagram chính thức" (3 phase, vòng lặp Human–AI, sơ đồ 5-phase/33-stage) nằm **inline trong các blog post và docs**, không tách thành bộ slide riêng. Nội dung của chúng đã được tôi mô tả lại (dưới dạng bảng + sơ đồ ASCII/Mermaid) trong các file:
  - [`../02-phases-va-stages/01-ba-phase-cot-loi.md`](../02-phases-va-stages/01-ba-phase-cot-loi.md)
  - [`../02-phases-va-stages/02-5-phases-33-stages.md`](../02-phases-va-stages/02-5-phases-33-stages.md)
  - [`../01-nguyen-ly-va-khai-niem/02-vong-lap-cong-tac.md`](../01-nguyen-ly-va-khai-niem/02-vong-lap-cong-tac.md)

---

## 📥 Muốn tự lấy "slide" từ nguồn gốc? Vài cách

1. **Xem video DVT214** rồi chụp màn hình các slide bạn cần (video là nguồn "slide" chính thức duy nhất).
2. **Đọc whitepaper web app** và dùng chức năng *Print → Save as PDF* của trình duyệt để lưu lại (vì nó là web app, bản in sẽ gần giống một bộ slide/deck).
3. **Clone repo docs** `awslabs/aidlc-workflows` — các sơ đồ Mermaid trong docs có thể render thành ảnh:
   ```
   git clone https://github.com/awslabs/aidlc-workflows.git
   ```

---

## Ghi chú
Nếu sau này AWS phát hành deck PDF chính thức (ví dụ trên AWS Events hoặc SpeakerDeck), có thể bổ sung vào thư mục `tai-lieu-pdf/` này.
