# AI-DLC là gì?

## Định nghĩa

**AI-DLC** (*AI-Driven Development Life Cycle* — Vòng đời phát triển phần mềm do AI dẫn dắt) là một **methodology** phát triển phần mềm lấy AI làm trung tâm, do AWS giới thiệu. Thay vì coi AI là công cụ hỗ trợ bên lề, AI-DLC đặt AI (một hoặc nhiều LLM) làm **cộng tác viên tích cực (active collaborator)** xuyên suốt mọi bước của vòng đời phát triển.

> "AI-DLC is an AI-centric transformative approach to software development..." — [AWS DevOps Blog, 31/07/2025](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

> "AI-DLC... signifies a software development methodology completely built around AI, treating a large-language model (LLM), or group of models, as an active collaborator throughout every step of software development." — [IBM Think](https://www.ibm.com/think/topics/ai-dlc)

Nói ngắn gọn: AI-DLC là câu trả lời cho câu hỏi **"SDLC sẽ trông như thế nào nếu AI đã tồn tại ngay từ đầu?"** — tức là thiết kế lại (reimagine) quy trình, chứ không "lắp thêm" (retrofit) AI vào quy trình cũ.

---

## Vì sao cần một cách tiếp cận "biến đổi" (transformative)?

AWS lập luận rằng các phương pháp phát triển phần mềm hiện tại được thiết kế cho **quy trình do con người dẫn dắt, kéo dài** — product owner, developer, architect dành phần lớn thời gian cho các hoạt động **không cốt lõi**: họp hành, lập kế hoạch, và các "nghi thức" (rituals) của SDLC.

Chỉ đơn thuần gắn AI vào như một "trợ lý" (assistant) vừa **giới hạn khả năng của AI**, vừa **củng cố những điểm kém hiệu quả cũ**.

Nguồn: [AWS DevOps Blog — "Why do we need a transformative approach to AI in software?"](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

---

## Hai anti-pattern mà AI-DLC muốn khắc phục

Tại session re:Invent 2025 (DVT214), Anupam Mishra và Raja SP (AWS) — đúc kết từ việc làm việc với **hơn 100 công ty** — chỉ ra 2 anti-pattern phổ biến:

| Anti-pattern | Mô tả | Vấn đề |
|---|---|---|
| **AI-assisted approach** | AI chỉ xử lý các tác vụ hẹp (code completion, viết doc, test) | AI bị "nhốt" trong việc vặt, không khai thác hết năng lực |
| **AI-managed / AI-autonomous approach** | Kỳ vọng AI tự xây dựng toàn bộ hệ thống không cần con người | Mất kiểm soát, chất lượng không đảm bảo, lệch khỏi mục tiêu nghiệp vụ |

> Cả hai đều cho ra kết quả **dưới mức tối ưu (suboptimal)** về cả velocity lẫn chất lượng — đây chính là khoảng trống AI-DLC nhắm tới.

Nguồn:
- [AWS DevOps Blog (31/07/2025)](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- [AWS re:Invent 2025 — DVT214 (dev.to tóm tắt)](https://dev.to/kazuya_dev/aws-reinvent-2025-introducing-ai-driven-development-lifecycle-ai-dlc-dvt214-32b)
- [Zenn.dev — tóm tắt session DVT214](https://zenn.dev/kiiwami/articles/45a7ac851f2aeb27?locale=en)

---

## Hai "chiều" (dimensions) cốt lõi của AI-DLC

Theo blog gốc của AWS, AI-DLC nhấn mạnh 2 chiều:

1. **AI Powered Execution with Human Oversight** (AI thực thi, con người giám sát)
   AI chủ động tạo kế hoạch chi tiết, tích cực hỏi để làm rõ, và **nhường các quyết định quan trọng cho con người** — vì chỉ con người mới có bối cảnh và hiểu biết nghiệp vụ để đưa ra lựa chọn đúng.

2. **Dynamic Team Collaboration** (Cộng tác nhóm năng động)
   Khi AI gánh phần việc lặp lại, nhóm con người tụ họp trong các **không gian cộng tác (collaborative spaces)** để giải quyết vấn đề real-time, tư duy sáng tạo và ra quyết định nhanh.

Nguồn: [AWS DevOps Blog — "What is AI-DLC?"](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

---

## Phân biệt AI-DLC với các khái niệm gần giống

- **AI-DLC ≠ "AI lifecycle"**: "AI lifecycle" nói về cách các *mô hình AI* được xây dựng; còn AI-DLC nói về cách *dùng AI để phát triển phần mềm*.
- **AI-DLC ≠ Agile + AI**: Chỉ thêm AI vào Agile giống như tạo ra "một con ngựa chạy nhanh hơn" (faster horse). AI-DLC là bước tiến hóa cơ bản hơn — ví von của whitepaper: giống như **ô tô thay thế xe ngựa**.

Nguồn: [IBM Think — "The AI-DLC, explained"](https://www.ibm.com/think/topics/ai-dlc)

---

## Lợi ích AWS tuyên bố

| Lợi ích | Nội dung |
|---|---|
| **Velocity** | AI tạo & tinh chỉnh artifact (requirements, stories, design, code, test) nhanh — việc tốn hàng tuần nay làm trong vài giờ/ngày |
| **Innovation** | Giải phóng thời gian cho con người sáng tạo, khám phá giải pháp |
| **Quality** | Nhờ liên tục làm rõ (continuous clarification), sản phẩm bám sát ý định; AI áp dụng nhất quán coding standard, design pattern, yêu cầu bảo mật của tổ chức |
| **Market Responsiveness** | Chu kỳ ngắn → phản hồi thị trường nhanh |
| **Developer Experience** | Giảm tải nhận thức (cognitive load), developer tập trung vào vấn đề quan trọng |

Nguồn: [AWS DevOps Blog — "What are the benefits of this methodology?"](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

---

## Đọc tiếp

- Lịch sử hình thành → [`../00-tong-quan/02-lich-su-hinh-thanh.md`](02-lich-su-hinh-thanh.md)
- 10 nguyên tắc nền tảng → [`../01-nguyen-ly-va-khai-niem/01-10-nguyen-tac.md`](../01-nguyen-ly-va-khai-niem/01-10-nguyen-tac.md)
