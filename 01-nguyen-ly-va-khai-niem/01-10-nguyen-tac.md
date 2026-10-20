# 10 nguyên tắc nền tảng của AI-DLC

Whitepaper **"AI-Driven Development Lifecycle (AI-DLC) Method Definition"** của Raja SP định nghĩa **10 nguyên tắc (principles)** làm nền tảng cho methodology. Dưới đây là bản tóm lược tiếng Việt, giữ nguyên thuật ngữ English.

> Nguồn chính cho phần này: [IBM Think — "Ten key principles of the AI-DLC"](https://www.ibm.com/think/topics/ai-dlc) (diễn giải lại whitepaper). Whitepaper gốc: [AI-DLC Method Definition Paper](https://prod.d13rzhkk8cj2z0.amplifyapp.com/) (là một web app, cần bật JavaScript để đọc).

---

### 1. Reimagine rather than retrofit (Thiết kế lại, đừng lắp ghép)
AI không nên bị "bắt vít" (bolted on) vào các phương pháp cũ. AI là **core participant**, không phải công cụ năng suất phụ trợ. Câu hỏi dẫn đường: *SDLC sẽ ra sao nếu AI đã tồn tại ngay từ đầu?* → một SDLC **AI-centric, AI-native**.

### 2. Reverse the conversation direction (Đảo chiều hội thoại)
Trước đây: developer liên tục *prompt* AI làm từng việc nhỏ rồi chờ. Giờ: developer **mô tả intent (ý định)**, còn AI dùng năng lực agentic để **tự lập kế hoạch → hỏi → thực thi → kiểm chứng → bảo trì**, đồng thời chủ động xin phê duyệt từ con người.

### 3. Integration of design techniques into the core (Tích hợp kỹ thuật thiết kế vào lõi)
Các kỹ thuật kỹ thuật phần mềm như **Domain-Driven Design (DDD)**, **Behavior-Driven Development (BDD)**, **Test-Driven Development (TDD)** trở thành **một phần bắt buộc** của workflow — chuẩn hóa chất lượng kỹ thuật, thay vì để mỗi team tự chọn.

### 4. Align with AI capability (Căn chỉnh theo đúng năng lực AI)
AI **không thể tự chủ 100%**. Nguyên tắc này đề cao **human-in-the-loop**: con người validate và giám sát quyết định của AI, để AI được hưởng lợi từ phán đoán của con người.

### 5. Cater to building complex systems (Phục vụ hệ thống phức tạp)
Phần mềm doanh nghiệp phức tạp hơn chỉ "viết code": nhiều service, nhiều kiến trúc, nhiều loại user/stakeholder, và **technical debt** tích tụ qua năm tháng. AI-DLC **giữ lại (preserve) toàn bộ context** xuyên suốt dự án để duy trì hiểu biết tổng thể (holistic understanding).

### 6. Retain what enhances human symbiosis (Giữ lại cái tăng cường cộng sinh người–máy)
AI-DLC cách mạng hóa nhưng vẫn **giữ vai trò con người ở nơi cần thiết**. Văn hóa **continuous feedback** được duy trì; các touchpoint này được tự động hóa & ghi lại (documented) để con người tập trung ra quyết định tốt nhất.

### 7. Facilitate transition through familiarity (Chuyển đổi mượt nhờ sự quen thuộc)
Tổ chức không thể thay methodology trong một đêm. AI-DLC tích hợp dần với các khái niệm/workflow sẵn có → **giảm thiểu gián đoạn** khi áp dụng.

### 8. Streamline responsibilities for efficiency (Tinh gọn trách nhiệm)
Vì AI làm việc & giữ context xuyên nhiều lĩnh vực, các tác vụ từng cần nhiều team chuyên biệt nay có thể do **team tích hợp** đảm nhận → **ít handoff hơn**.

### 9. Minimize stages, maximize flow (Giảm giai đoạn, tối đa hóa dòng chảy)
SDLC truyền thống chia việc thành các phase rời rạc (plan → design → implement → test → deploy) với handoff ở cuối mỗi phase. AI-DLC **làm mờ ranh giới** này, coi chúng là **dòng chảy liên tục**, các tác vụ diễn ra **song song & phi tuyến** → feedback loop ngắn, tiến độ nhanh.

### 10. No hard-wired, opinionated SDLC workflows (Không áp đặt workflow cứng nhắc)
AI-DLC **không quy định một workflow cứng** cho mọi dự án — nó **adaptive**. AI phân tích mục tiêu & ràng buộc rồi **sinh ra workflow phù hợp riêng** cho từng dự án.

> Đây là nguyên tắc được AWS nhấn mạnh nhất trong bài "Open-Sourcing Adaptive Workflows":
> *"AI-DLC avoids prescribing opinionated workflows for different development pathways (such as new system development, refactoring, defect fixes, or microservice scaling). Instead, it adopts a truly AI-First approach where AI recommends the Level 1 Plan based on the given pathway intention."*
> — [AWS DevOps Blog — Open-Sourcing Adaptive Workflows](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)

---

## 3 thách thức thực tế mà nguyên tắc 10 giải quyết

Trong bài open-source, AWS nêu 3 vấn đề tái diễn khi áp dụng AI vào dev, và cách AI-DLC xử lý:

| # | Thách thức | Cách AI-DLC xử lý |
|---|---|---|
| 1 | **One-size-fits-all workflow** — ép mọi dự án qua cùng một chuỗi bước cứng | Workflow **adaptive**: AI chọn stage thông minh theo intent (bug fix thì bỏ qua phân tích requirement đồ sộ) |
| 2 | **Thiếu độ sâu linh hoạt (flexible depth)** — gây over-engineering hoặc thiếu chặt chẽ | Điều chỉnh cả **breadth** (chọn stage nào) lẫn **depth** (sâu đến đâu) theo độ phức tạp |
| 3 | **Công cụ over-automate** — khiến con người mất vai trò validate/giám sát (*process atrophy*) | Bắt buộc **human-in-the-loop cycle ở mọi stage**, qua nghi thức **Mob Elaboration / Mob Construction** |

Nguồn: [AWS DevOps Blog — Open-Sourcing Adaptive Workflows](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)

---

## Đọc tiếp
- Vòng lặp cộng tác Human–AI → [`02-vong-lap-cong-tac.md`](02-vong-lap-cong-tac.md)
- Thuật ngữ (Bolt, Unit, Mob...) → [`03-thuat-ngu.md`](03-thuat-ngu.md)
