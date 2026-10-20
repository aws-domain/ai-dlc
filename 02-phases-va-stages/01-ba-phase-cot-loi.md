# 3 phase cốt lõi: Inception → Construction → Operations

Đây là mô hình **gốc** của AI-DLC như công bố trong blog nền tảng. (Workflow open-source sau này mở rộng thành 5 phase / 33 stages — xem file [`02-5-phases-33-stages.md`](02-5-phases-33-stages.md).)

> *"The software development in AI-DLC takes place in three straightforward phases."*
> — [AWS DevOps Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

```
┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│   INCEPTION   │ ──► │ CONSTRUCTION  │ ──► │  OPERATIONS   │
│  (planning +  │     │  (design +    │     │ (deploy +     │
│   requirements)│     │ implementation)│     │  monitoring)  │
│               │     │               │     │               │
│ Mob           │     │ Mob           │     │ team          │
│ Elaboration   │     │ Construction  │     │ oversight     │
└───────────────┘     └───────────────┘     └───────────────┘
      │                     │                     │
      └── context ──────────┴── context ──────────┘
           (mỗi phase cung cấp context giàu hơn cho phase sau)
```

> *"Each phase provides richer context for the next, thus enabling AI to provide increasingly informed suggestions."*
> — [AWS DevOps Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

---

## 1. Inception Phase (Khởi tạo)

**Mục tiêu:** AI biến **business intent** thành **requirements, stories, Units** chi tiết.

- Nghi thức: **Mob Elaboration** — cả team chủ động validate câu hỏi & đề xuất của AI.
- Hoạt động: phân tích yêu cầu, định nghĩa NFR, đánh giá rủi ro (risk assessment).
- Steering Files được tạo tại đây và dùng xuyên suốt.

## 2. Construction Phase (Xây dựng)

**Mục tiêu:** Dùng context đã validate từ Inception, AI đề xuất **logical architecture, domain model, code solution, và test**.

- Nghi thức: **Mob Construction** — team cung cấp làm rõ về quyết định kỹ thuật & kiến trúc theo thời gian thực.
- Đây là nơi **execution** thực sự xảy ra: cùng viết, test, deploy code.

## 3. Operations Phase (Vận hành)

**Mục tiêu:** AI dùng context tích lũy từ các phase trước để quản lý **Infrastructure as Code (IaC)** và **deployment**, dưới sự giám sát của team.

- Dùng business requirements (từ Inception) + technical decisions (từ Construction) để quản lý deploy, tự động hóa hạ tầng, và monitor hệ thống live.

Nguồn cho cả 3 phase: [AWS DevOps Blog — "How does AI-DLC work?"](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) · [IBM Think — "The AI-DLC framework"](https://www.ibm.com/think/topics/ai-dlc)

---

## Mô hình 3 phase trong triển khai Amazon Q / Kiro

Blog hướng dẫn thực hành mô tả workflow adaptive với 3 phase (xanh/vàng = bắt buộc/điều kiện):

- **Inception Phase** — Workspace Detection, Requirements Analysis, Workflow Planning (bắt buộc); Reverse Engineering, User Stories, Application Design, Units Generation (điều kiện).
- **Construction Phase** — Functional Design, NFR Requirements, NFR Design, Infrastructure Design (điều kiện); **Code Generation, Build and Test** (bắt buộc, lặp cho từng Unit).
- **Operations Phase** — Operations.

> Lưu ý: workflow **adaptive** — "Simple bug fixes skip planning. They go directly to code generation. Complex features need requirements analysis..."

Nguồn: [AWS DevOps Blog — Building with AI-DLC (Figure 1)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

---

## Đọc tiếp
- Chi tiết 5 phase / 33 stages (open-source) → [`02-5-phases-33-stages.md`](02-5-phases-33-stages.md)
- Walkthrough thực tế từng bước → [`../03-cong-cu-va-trien-khai/02-vi-du-thuc-te.md`](../03-cong-cu-va-trien-khai/02-vi-du-thuc-te.md)
