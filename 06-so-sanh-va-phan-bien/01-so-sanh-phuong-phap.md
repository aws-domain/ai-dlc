# So sánh AI-DLC với Waterfall, Agile/Scrum & Vibe Coding

> **File MỚI** — bộ tài liệu gốc chưa có bảng so sánh chuyên biệt. Nội dung tổng hợp từ báo cáo Gemini Deep Research + nguồn AWS/IBM/ThoughtWorks.

---

## 1. Góc nhìn kinh tế học: nút thắt cổ chai đã dịch chuyển

Điểm mấu chốt để hiểu AI-DLC khác biệt **về chất** (không chỉ về mức độ): **hàm chi phí của kỹ thuật phần mềm đã đổi**.

- **Kỷ nguyên Waterfall & Agile/Scrum:** tài nguyên khan hiếm & đắt nhất là **thời gian con người gõ mã** + **chi phí phối hợp thông tin**. Vì thế Scrum gom việc thành **batch 2–4 tuần (Sprint)**, họp ước lượng Story Points, chia việc cá nhân + review PR bất đồng bộ.
- **Kỷ nguyên Agentic AI:** chi phí sinh mã, vẽ kiến trúc, viết test **sụt về gần 0** — AI phác thảo domain model + architecture + test suite nhanh hơn một cuộc họp Sprint Planning. Khi đó **Sprint 2 tuần biến thành "pure queueing delay"** (độ trễ xếp hàng thuần túy).
- **Nút thắt mới:** không còn là tốc độ gõ mã, mà là **tốc độ con người kiểm chứng & xác thực** những gì AI đề xuất (*human validation speed*).

AI-DLC được tái cấu trúc đúng quanh sự dịch chuyển này: **chạy ở tốc độ AI, nhưng khóa chất lượng** bằng Spec-Driven Development + DDD + lưu state vào repo + review đồng bộ tại Approval Gates.

Nguồn: [AWS re:Invent DVT214 recap](https://dev.to/kazuya_dev/aws-reinvent-2025-introducing-ai-driven-development-lifecycle-ai-dlc-dvt214-32b) · [Orchestrator.dev](https://orchestrator.dev/blog/2026-10-03-ai-dlc-in-practice/)

---

## 2. Bảng so sánh toàn diện

| Tiêu chí | **Waterfall** | **Agile / Scrum** | **Vibe Coding / AI-Assisted** | **AI-DLC** |
|---|---|---|---|---|
| **Triết lý & vai trò AI** | Tuần tự tuyến tính, thuần con người; không có AI cấu trúc | Lặp, human-centric; AI (nếu có) chỉ **retrofit** như công cụ phụ trợ cá nhân | AI là **autocomplete**/sinh mã tự phát theo cảm tính, không đổi quy trình | **AI-Native**: AI là **central collaborator + orchestrator** điều phối cả lifecycle dưới giám sát con người |
| **Chiều hội thoại** | Đặc tả tĩnh, truyền một chiều xuống | Con người viết ticket + thảo luận giữa người với người | Thuận chiều: người ra lệnh từng prompt, AI trả lời tác vụ lẻ | **Đảo ngược**: người nêu **Intent** cấp cao; AI khởi xướng plan, **chủ động hỏi làm rõ**, chờ duyệt |
| **Chu kỳ & batch** | Pha kéo dài hàng tháng/năm; bàn giao 1 khối lớn cuối dự án | **Sprint 2–4 tuần**; chia Epic/User Story; ước lượng Story Points | Ad-hoc, không chu kỳ chuẩn | **Bolt vài giờ–vài ngày** (lý tưởng <1 ngày); chia **Unit of Work**; **bỏ** Story Points |
| **Tổ chức đội & nghi thức** | Phòng ban chuyên môn tách biệt, bàn giao qua tài liệu | **2-Pizza Teams** (8–10); solo ticket + Daily Standup + async PR review | Lập trình viên **solo prompting**, tối ưu cục bộ | **1-Pizza AI Pods** (AI-Native Trailblazers); cộng tác đồng bộ qua **Mob Elaboration + Mob Construction** |
| **Nguồn sự thật & context** | Tài liệu BDUF lớn, mau lỗi thời | Phân mảnh (JIRA + Miro + Slack) + tribal knowledge | Tạm trong **chat history**; mất context nghiêm trọng khi phình to | **Versioned trong Git repo**: Steering Files, `AGENTS.md`, `aidlc-state.md`, Memory Bank, audit trail |
| **Kỷ luật thiết kế & QA** | Thiết kế cứng từ đầu; test dồn cuối → sửa lỗi đắt | Để trống "whitespace" kỹ thuật → thiếu nhất quán | Nhảy cóc ý tưởng→mã; dễ nợ kỹ thuật, lỗi logic ngầm | **Tích hợp cứng**: DDD + Logical Design + BDD/TDD + Shift-Left QA bắt buộc |
| **Quản trị & rủi ro** | CAB nặng nề cuối mỗi pha | DoD + peer review + Sprint Review (phân tán) | Rất yếu/không có gate chính thức | **Approval Gates bắt buộc** mỗi stage/Unit + **Bounded Autonomy** + phân loại thay đổi theo rủi ro |
| **Độ linh hoạt quy trình** | Tuyến tính, khó quay lui | Khung nghi thức cố định lặp đều | Tùy tiện, non-repeatable | **Adaptive**: tự chọn 1/11 Workflow Profiles (8→33 stages), điều chỉnh depth theo loại yêu cầu |

Nguồn tổng hợp: [AWS DevOps Blog (bài gốc)](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) · [IBM Think](https://www.ibm.com/think/topics/ai-dlc) · [AWS Industries — Financial Services](https://aws.amazon.com/blogs/industries/ai-driven-development-lifecycle-for-financial-services/) · [Felipe Fontoura](https://felipefontoura.com/articles/what-is-ai-dlc/)

---

## 3. Vì sao AI-DLC ≠ chỉ "thêm AI vào Agile"?

- **Agile + AI** = con ngựa chạy nhanh hơn (faster horse). **AI-DLC** = chiếc ô tô (ẩn dụ gốc của whitepaper).
- Vibe Coding tốt cho **prototype nhỏ**, nhưng khi dự án lớn: context trôi mất, kiến trúc lệch lạc, thiếu truy vết, mã không bảo trì được ở cấp enterprise.
- AI-DLC giải quyết **cả hai thái cực thất bại** (AI-assisted trần thấp 10–15%, và fully-autonomous mất kiểm soát) bằng con đường trung đạo: tốc độ AI + kỷ luật spec + human-in-the-loop.

---

## Đọc tiếp
- Góc nhìn phản biện (hạn chế, rủi ro) → [`02-goc-nhin-phan-bien.md`](02-goc-nhin-phan-bien.md)
- Định nghĩa gốc & 2 anti-pattern → [`../00-tong-quan/01-ai-dlc-la-gi.md`](../00-tong-quan/01-ai-dlc-la-gi.md)
