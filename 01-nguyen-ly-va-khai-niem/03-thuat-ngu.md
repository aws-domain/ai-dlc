# Thuật ngữ AI-DLC (Glossary)

AI-DLC giới thiệu **thuật ngữ & nghi thức mới** để phản ánh cách tiếp cận AI-driven, cộng tác cao. Nhiều thuật ngữ Agile quen thuộc được "đặt lại tên".

> *"AI-DLC introduces new terminology and rituals to reflect its AI-driven, highly collaborative approach."*
> — [AWS DevOps Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

---

## Bảng ánh xạ thuật ngữ cũ → mới

| Agile truyền thống | AI-DLC | Ý nghĩa |
|---|---|---|
| Sprint | **Bolt** | Chu kỳ làm việc ngắn, cường độ cao — tính bằng **giờ/ngày** thay vì tuần |
| Epic | **Unit of Work** (Unit) | Đơn vị công việc; tập hợp task thể hiện đường đi của AI để hoàn thành một intent |
| (yêu cầu đầu vào) | **Intent** | Mô tả ý định cấp cao của con người — điểm khởi đầu của mọi việc |

Nguồn: [AWS DevOps Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) · [IBM Think](https://www.ibm.com/think/topics/ai-dlc)

---

## Các thuật ngữ cốt lõi

### Intent (Ý định)
Mô tả cấp cao của con người về cái muốn xây. AI-DLC "emphasizes **intents** rather than rigid processes" — tức là nhấn mạnh **spec-driven development (SDD)**: con người nêu intent, AI tự tìm cách hiện thực hóa. Từ intent, AI dẫn xuất ra các **Unit**.

### Unit (of Work)
Tập các task đại diện cho con đường AI đi tới hoàn thành intent. Trong workflow open-source, Unit được sinh ở stage *Units Generation* (2.7), kèm **dependency DAG** (`unit-of-work-dependency.md`) để biết Unit nào phụ thuộc Unit nào.

### Bolt
"Iteration by which units of work are executed" — một vòng lặp thực thi các Unit. Khác biệt chính so với sprint: **rất ngắn** (vài giờ đến vài ngày), nhấn mạnh tốc độ & giao hàng liên tục. Kế hoạch Bolt được ghi ở `bolt-plan.md`.

> *"A key characteristic is moving forward in small increments via 'Bolts' — lasting from a few hours to a few days — rather than long iterations equivalent to traditional sprints."*
> — [Zenn.dev](https://zenn.dev/ebisawa/articles/b9b775ef8aa639?locale=en)

### Mob Elaboration (nghi thức ở Inception)
Nghi thức cộng tác nơi **cả team cross-functional + hệ thống AI cùng làm việc** để biến ý tưởng nghiệp vụ cấp cao thành **requirements, user stories, Unit**. Team **chủ động validate** câu hỏi & đề xuất của AI.

### Mob Construction (nghi thức ở Construction)
Nghi thức nơi team con người + AI **cùng viết, test, deploy code**. Team cung cấp làm rõ về **quyết định kỹ thuật & lựa chọn kiến trúc** theo thời gian thực.

> Cả hai "Mob" đều nhằm đảm bảo đề xuất của AI **không bị chấp nhận một cách mù quáng**.
> — [AWS DevOps Blog — Open-Sourcing Adaptive Workflows](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)

### Steering Files
Các tài liệu **markdown lưu trong repo**, định nghĩa **rules, constraints, architectural standards, workflows** mà agent phải tuân theo. Được tạo ở phase Inception nhưng dùng xuyên suốt cả 3 phase. Đóng vai trò **nguồn chân lý bền vững (persistent source of truth)** cho các AI agent.
→ Trong Amazon Q Developer, cơ chế tương đương là **Project Rules**; trong Kiro là **Steering**.

Nguồn: [IBM Think](https://www.ibm.com/think/topics/ai-dlc) · [Kiro docs — Steering](https://kiro.dev/docs/steering/)

### Human-in-the-loop
Nguyên tắc con người luôn validate & phê duyệt tại các checkpoint quan trọng. Trong AI-DLC đây **không phải một ô tick (checkbox)** mà là "nền tảng của trust, accountability, và correctness".

### NFR (Non-Functional Requirements)
Các yêu cầu phi chức năng: performance, security, scalability, reliability, observability. Được định nghĩa & thiết kế riêng (ví dụ stage 3.2 NFR Requirements, 3.3 NFR Design trong workflow mở rộng).

### Greenfield vs Brownfield
- **Greenfield**: dự án mới, không có code sẵn → đi thẳng tới Requirements Analysis.
- **Brownfield**: dự án đã có code → chạy **Reverse Engineering** trước để AI hiểu codebase.

Nguồn: [AWS DevOps Blog — Building with AI-DLC (Step 5: Workspace Detection)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

### Adaptive Workflow
Workflow tự điều chỉnh **breadth** (chọn stage nào) và **depth** (sâu đến đâu) theo độ phức tạp của intent — hiện thực hóa nguyên tắc 10.

### Verification Gate
Kiểm tra tự động ở ranh giới giữa các phase: xác nhận artifact bắt buộc tồn tại, các liên kết truy vết (traceability) còn nguyên vẹn, không có artifact mồ côi.

### Audit Trail
Nhật ký ghi lại **mọi quyết định, input, phản hồi** để truy vết (traceability) — lưu trong `audit.md` / thư mục `audit/`. Engine 2.0 phân loại thành **119 audit event types** (tài liệu gốc của bộ này ghi 118 — chênh do version drift).

---

## Thuật ngữ bổ sung từ nghiên cứu Gemini (bản 2.0 & re:Invent)

### Deployment Unit
Tạo phẩm **đã kiểm chứng** của phase Construction (mã nguồn + test suite đã pass + build/configuration instructions), đóng gói sẵn sàng bàn giao sang Operations để deploy. Tương đương *Release Candidate / Deliverable Build Package* kiểu cũ.

### 1-Pizza AI Pods & AI-Native Trailblazers
Cấu trúc đội **tinh gọn mới**: vì AI xóa nhòa ranh giới chuyên môn hẹp, quy mô nhóm giảm từ **2-Pizza Teams (8–10 người)** xuống **1-Pizza AI Pods**. Thành viên hoạt động như **AI-Native Trailblazers** — chuyên gia đa năng điều phối AI, lặp lại công việc ở *"speed of judgment"* (tốc độ của sự phán đoán).

### Bounded Autonomy
Cơ chế cho phép AI **tự động thực thi** các hành động thường nhật, kiểm chứng được, **nhưng nằm nghiêm ngặt bên trong ranh giới con người đã phê duyệt trước**. Đi kèm với **Approval Gates** — chốt chặn bắt buộc cuối mỗi stage (Approve / Request Changes).

### Harness
Thuật ngữ trong `aidlc-workflows` chỉ **công cụ/môi trường agent đích** mà lõi AI-DLC tích hợp vào. Hiện hỗ trợ **7 harnesses**: Claude Code, Kiro CLI, Kiro IDE, Codex CLI, Cursor, opencode, GitHub Copilot. Triết lý: *"One Core, Many Harnesses"*.

### Memory Bank
Các tệp Markdown versioned trong Git (`AGENTS.md`, `aidlc-state.md`, `.kiro`, `.claude`...) đóng vai trò **"AI-executable knowledge assets"** — lưu trạng thái quy trình, chuẩn kiến trúc, lịch sử quyết định xuyên suốt các session. Là phiên bản "có cấu trúc, thực thi được" thay cho wiki/Confluence/tribal knowledge rời rạc.

### Intent (ẩn dụ Google Maps) — _bổ sung cách giải thích_
Cách whitepaper minh họa đảo chiều hội thoại: giống **Google Maps** — con người chỉ **chọn điểm đến** (Intent), còn AI **tính lộ trình từng bước** và con người **giám sát hành trình**. Khác hẳn việc ra lệnh từng cú rẽ.

---

## Đọc tiếp
- 3 phase cốt lõi (nơi các nghi thức diễn ra) → [`../02-phases-va-stages/01-ba-phase-cot-loi.md`](../02-phases-va-stages/01-ba-phase-cot-loi.md)
- Mô hình 5 phase / 33 stages (bản mở rộng) → [`../02-phases-va-stages/02-5-phases-33-stages.md`](../02-phases-va-stages/02-5-phases-33-stages.md)
