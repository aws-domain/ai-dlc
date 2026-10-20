# Vòng lặp cộng tác Human–AI (mental model cốt lõi)

## Mô hình tư duy (mental model)

Lõi của AI-DLC là một **vòng lặp lặp đi lặp lại** cho *mọi* hoạt động trong SDLC:

```
┌─────────────────────────────────────────────────────────┐
│  1. Humans Provide Task        (con người giao nhiệm vụ)  │
│          ↓                                                │
│  2. AI Creates Plan & Seeks Clarification                 │
│     (AI lập kế hoạch + hỏi để làm rõ)                     │
│          ↓                                                │
│  3. Humans Provide Clarification (con người làm rõ)       │
│          ↓                                                │
│  4. AI Refines Plan            (AI tinh chỉnh kế hoạch)   │
│          ↓                                                │
│  5. Humans Approve Plan        (con người PHÊ DUYỆT) ★    │
│          ↓                                                │
│  6. AI Executes Plan           (AI thực thi)              │
│          ↓                                                │
│  7. Humans Verify Outcome      (con người kiểm chứng) ★   │
│          ↓                                                │
│         (quay lại bước 1 cho tác vụ tiếp theo)            │
└─────────────────────────────────────────────────────────┘
```

★ = điểm con người giữ quyền quyết định.

> *"This pattern, where AI creates a plan, asks clarifying questions to seek context, and implements solutions only after receiving human validation, repeats rapidly for every SDLC activity..."*
> — [AWS DevOps Blog — "How does AI-DLC work?"](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

> *"Figure 1: AI-DLC workflow: Humans decide and validate, AI plans and executes."*
> — [AWS DevOps Blog — Open-Sourcing Adaptive Workflows](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)

---

## Nguyên tắc "AI không được tự ý giả định"

Một quy tắc (rule) quan trọng trong workflow: **AI bị cấm tự đưa ra giả định thay cho người dùng** — thay vào đó phải **hỏi clarifying questions**. Vì LLM có xu hướng tự giả định và "lao" tới kết quả, nên phải ép rõ ràng để tuân theo kỷ luật kỹ thuật của AI-DLC.

Chi tiết thực tế quan sát được trong blog hướng dẫn:
- AI trình bày câu hỏi dưới dạng **trắc nghiệm (multiple-choice)**, luôn kèm lựa chọn mở **"Other"** để người dùng tự điền.
- AI ghi câu hỏi vào file `requirement-verification-questions.md` để người dùng trả lời **inline** trong file.
- AI **kiểm tra mâu thuẫn / mơ hồ** trong câu trả lời và hỏi lại cho đến khi hai bên thống nhất, rồi mới sang bước tiếp theo.

Nguồn: [AWS DevOps Blog — Building with AI-DLC (Step 6: Requirements Analysis)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

---

## 3 trụ cột để tooling hỗ trợ vòng lặp này

Theo bài open-source, công cụ tốt phải nhấn mạnh:

1. **Promoting stakeholder collaboration** — hệ thống chủ động kêu gọi các nghi thức cộng tác có stakeholder tham gia.
2. **Auditability** — mọi plan & artifact do AI tạo đều phải nêu lý do (rationale), mời review, và **ghi lại mọi tương tác/giám sát của con người**.
3. **Flow awareness** — công cụ phát hiện khi tự động hóa "chạy nhanh hơn" khả năng validate của con người, và **chủ động chậm lại** ở các checkpoint quan trọng.

> Mục tiêu không phải triệt tiêu tự động hóa, mà là **nhúng quyền sở hữu (ownership) của con người** vào quy trình.

Nguồn: [AWS DevOps Blog — Open-Sourcing Adaptive Workflows](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)

---

## Persistent context (giữ ngữ cảnh xuyên suốt)

AI **lưu & duy trì context bền vững** qua mọi phase bằng cách ghi plan, requirements, design artifact vào **repository của dự án** → đảm bảo công việc tiếp nối liền mạch qua nhiều session.

Trong triển khai thực tế, context được lưu dưới dạng các file như `aidlc-state.md` (trạng thái), `audit.md` / thư mục `audit/` (nhật ký mọi quyết định), và các artifact `.md` khác trong thư mục `aidlc-docs/`.

Nguồn:
- [AWS DevOps Blog — nền tảng](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- [AWS DevOps Blog — Building with AI-DLC (Step 5)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

---

## Đọc tiếp
- Thuật ngữ chi tiết → [`03-thuat-ngu.md`](03-thuat-ngu.md)
- 3 phase cốt lõi → [`../02-phases-va-stages/01-ba-phase-cot-loi.md`](../02-phases-va-stages/01-ba-phase-cot-loi.md)
