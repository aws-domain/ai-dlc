# Góc nhìn phản biện đa chiều: hạn chế, rủi ro & tranh luận

> **File này là nội dung MỚI**, bổ sung từ báo cáo Gemini Deep Research (10/2025). Bộ tài liệu gốc (10/2025) chủ yếu trình bày AI-DLC từ góc nhìn AWS; phần này cân bằng lại bằng 4 lăng kính: **AWS** (nhà sáng lập), **học thuật** (RCT độc lập trên arXiv), **chuyên gia thực hành** (người vận hành engine 2.0), và **hoài nghi/quản trị** (kiểm toán viên, ThoughtWorks).

---

## 1. Tranh luận về con số "10–15x" và "Heavy Evaluation Costs"

**Fact:** AWS truyền thông mức tăng năng suất **10–15x**, cải thiện velocity **40–60%**, giảm defects **40–60%**, ROI **300–500%** trong 12 tháng — tổng hợp từ 100+ thử nghiệm khách hàng.

**Cảnh báo từ giới thực hành:** các con số này là **số liệu tự công bố (vendor-reported)**, đến từ các dự án có **chính kỹ sư AWS ngồi trong phòng điều phối** ("with AWS engineers in the room"), **chưa được bên thứ ba kiểm chứng độc lập**. Phải coi đây là **mức trần lý tưởng (upper bound)**, không phải mức dự báo trung bình.

**Đối trọng học thuật (arXiv — bằng chứng độc lập):**

| Nghiên cứu | Phát hiện |
|---|---|
| **Joel Becker et al.** (07/2025, [arXiv:2507.09089](https://arxiv.org/abs/2507.09089)) | RCT trên developer mã nguồn mở giàu kinh nghiệm làm trên repo **quen thuộc của họ**: dùng công cụ AI thực chất **kéo dài thời gian hoàn thành trung bình +19%** (chậm hơn, không nhanh hơn) |
| **Yunhan Qiao et al.** (10–11/2025, [arXiv:2510.17894](https://arxiv.org/abs/2510.17894), [arXiv:2511.02922](https://arxiv.org/abs/2511.02922)) | Hiện tượng **"Comprehension-Performance Gap"** trong brownfield có GenAI hỗ trợ; mã AI sinh thường chứa lỗ hổng bảo mật tiềm ẩn |

**"Heavy Evaluation Costs" — nghịch lý cốt lõi:** AI sinh mã với tốc độ & khối lượng khổng lồ, nhưng ẩn bên trong là lỗi tinh vi về **business logic**, hiểu sai **preconditions**, thiếu yêu cầu bảo mật, mã *"looks correct but is fundamentally broken"*. Khi khối lượng mã vượt quá khả năng đọc hiểu của con người, **khâu review trở thành nút thắt cổ chai**. Nếu tốc độ xuất xưởng tăng 10x nhưng **defect escape rate** tăng 3x → tổ chức không hề nhanh hơn, chỉ đang **đẩy gánh nặng QA sang production**.

Nguồn: [Orchestrator.dev — AI-DLC in Practice](https://orchestrator.dev/blog/2026-10-03-ai-dlc-in-practice/) · [AICTO/Medium — Why Isn't It Working? (dẫn các paper arXiv)](https://medium.com/@aicto/part-1-ai-driven-development-why-isnt-it-working-af02ee18bb29)

---

## 2. "Gate Fatigue" & 4 anti-patterns trong thực hành

Chuyên gia vận hành engine `awslabs/aidlc-workflows` đúc kết: *"The method lives or dies on gate quality"* — thành bại phụ thuộc hoàn toàn vào **chất lượng cổng phê duyệt**. Nhưng chính cơ chế Approval Gate dày đặc sinh ra **4 anti-pattern**:

| # | Anti-pattern | Mô tả |
|---|---|---|
| 1 | **Artifact looks complete, says nothing** | Tài liệu LLM sinh ra luôn có Markdown đẹp, văn phong trôi chảy → **đánh lừa thị giác người duyệt** dù bên trong thiếu quyết định kỹ thuật cụ thể |
| 2 | **Gate fatigue (lần duyệt thứ 10 trong ngày)** | Ngay cả bugfix profile cũng có **6 gates**; luồng lớn có hàng chục gates. Reviewer fatigue + thiếu domain knowledge → thoái hóa thành **bấm duyệt máy móc (rubber-stamping)** chỉ sau 1 tuần |
| 3 | **Self-approval bias** | Người viết Intent ban đầu cũng là người bấm Approve → **không có kiểm tra chéo độc lập** |
| 4 | **"Vibe coding between the gates"** | Dev thấy gate rườm rà → tự sửa mã ngoài luồng → **đứt gãy tính toàn vẹn** của state file & audit trail |

**Khuyến nghị khắc phục:** giới hạn mỗi phiên Mob ~1 giờ; dùng `aidlc-state.md` để tạm nghỉ giữa các gate không mất context; cử tech lead ngồi cùng các phiên Mob đầu; **quy tắc bắt buộc**: trước khi Approve, người duyệt phải phát biểu được **bằng một câu** tạo phẩm đó *làm gì* và *tại sao đúng*.

Nguồn: [Felipe Fontoura — What is AI-DLC?](https://felipefontoura.com/articles/what-is-ai-dlc/)

---

## 3. Căng thẳng nội tại: lý thuyết (1.0) vs engine thực thi (2.0)

Phân tích của Felipe Fontoura (mổ xẻ bản 2.11.0): engine **AI-DLC 2.0 đang tự mâu thuẫn với chính nguyên tắc 9 & 10** của whitepaper gốc.

- **Whitepaper (Raja SP):** *"Minimize stages, maximize flow"* (nguyên tắc 9) + *"No hard-wired workflows"* (nguyên tắc 10).
- **Engine 2.0:** một **deterministic engine** cứng với 5 phases, 33 stages, 11 profiles định sẵn → **bộ máy nghi thức khá nặng nề**.

Chính sự cồng kềnh này buộc AWS phải đẻ thêm nhánh **AI-DLC Lite** (cắt nửa số gate + giới hạn vòng hỏi đáp) để cứu tốc độ.

> **Khuyến nghị:** tiếp cận AI-DLC 2.0 như một **"kệ hàng siêu thị"** — chọn lấy cơ chế giải đúng nỗi đau của team (lưu artifact vào repo, gate giữa các bước lớn, chu kỳ tính bằng giờ, AI chủ động hỏi) và **mạnh dạn lược bỏ** thủ tục rườm rà; ghi chép rõ cái đã giữ và đã bỏ.

Nguồn: [Felipe Fontoura — What is AI-DLC?](https://felipefontoura.com/articles/what-is-ai-dlc/)

---

## 4. Khoảng trống lớp quản trị kiểm toán (Accountability Layer)

Chuyên gia AI governance **Daoqi Zhang (ExploreAgentic)**: *"The methodology is real; the governance layer is not."*

- Nghi thức **Mob Validation** là quality control tốt, **nhưng KHÔNG phải accountability structure hợp lệ** trước kiểm toán. Câu *"cả phòng họp đã đồng ý" ("the room agreed")* **không bao giờ thỏa mãn** kiểm toán viên ngân hàng/bảo hiểm.

**3 chốt kiểm soát tổ chức BẮT BUỘC tự xây trước Bolt đầu tiên:**

1. **Named approver per Unit of Work** — cá nhân cụ thể ký duyệt, lưu vết, và **tuyệt đối không phải người đã gõ lệnh tạo kế hoạch đó**.
2. **Review standard cho AI-drafted plans** — checklist rõ: phân loại dữ liệu bị chạm, **blast radius**, **rollback path**, điểm lệch so với Steering Files.
3. **Decision log gắn chặt artifact version + identity** — liên kết mỗi Unit với change ticket; lấy acceptance tests đã validate làm tiêu chuẩn thoát Inception; chạy **agent evals** trước khi nhân rộng từ 1→5 team; tách rạch ròi **3 lớp quyền AI**: đọc dữ liệu / sửa mã / phát hành production.

Nguồn: [Daoqi Zhang — ExploreAgentic](https://www.exploreagentic.ai/insights/ai-dlc/)

---

## 5. "Chiếc Ferrari trong rừng rậm" & điều kiện tiên quyết khắt khe

Ẩn dụ của **Sunit Parekh (ThoughtWorks, 02/2026):** AI giống **siêu xe Ferrari** — chỉ phát huy tốc độ trên **đường cao tốc phẳng** (PO + Architect + Dev ngồi cùng, quyết định tức thì). Đưa vào **"rừng rậm doanh nghiệp quan liêu"** — mã sinh trong vài phút nhưng chờ **hàng tuần** xin chữ ký qua email, các phòng ban đổ lỗi (blame game), release train cố định 2 tuần/lần — thì **mọi lợi thế tốc độ thượng nguồn bị triệt tiêu**.

Nghịch lý bất ngờ: AI **gặp khó nhất với kiến trúc phân tán hiện đại** (microservices, event-driven) của doanh nghiệp lớn, vì business logic **phân mảnh qua hàng chục repo**, thiếu **contracts** định nghĩa sẵn, thiếu **data dictionary** toàn diện (ý nghĩa dữ liệu chỉ tồn tại dưới dạng tribal knowledge).

**Điều kiện tiên quyết không thể thương lượng** (chính tài liệu Financial Services của AWS cảnh báo): tổ chức **bắt buộc có sẵn nền tảng DevSecOps trưởng thành** (CI/CD tự động, test tự động, security scan liên tục) + năng lực **Spec-Driven Development** trước khi áp dụng. *"AI-DLC amplifies existing capabilities. It does not compensate for foundational gaps."*

**Phân hóa lực lượng lao động:** senior engineers/architects có tư duy hệ thống + viết Steering Files/Specs chuẩn → nắm đòn bẩy; lập trình viên chỉ có kỹ năng gõ mã cơ học hoặc thiếu domain knowledge để thẩm định output AI → **nguy cơ bị đào thải**.

Nguồn: [ThoughtWorks — Sunit Parekh (dẫn qua phân tích tổng hợp)](https://www.thoughtworks.com/insights) · [AWS Industries — Financial Services](https://aws.amazon.com/blogs/industries/ai-driven-development-lifecycle-for-financial-services/)

---

## 6. Lưu ý tránh nhầm lẫn thuật ngữ

- **AI-DLC (AWS)** ≠ **Harness AI DLC Insights** — một sản phẩm phân tích năng suất của công ty Harness (xuất hiện trên Gartner Peer Insights). Trùng chữ viết tắt, khác hoàn toàn.
- **AI-DLC** ≠ **"AISDLC"** — tài liệu không chính thức lưu hành trên Scribd chia 5 pha (Analyze, Ideate, Develop, Launch, Curate) + 94 chỉ số gắn vào Scrum. Không phải của AWS.

Nguồn: [Gartner Peer Insights — Harness AI DLC Insights](https://www.gartner.com/reviews/product/harness-ai-dlc-insights)

---

## Đọc tiếp
- Bảng so sánh AI-DLC vs Waterfall/Agile/Vibe Coding → [`../06-so-sanh-va-phan-bien/01-so-sanh-phuong-phap.md`](01-so-sanh-phuong-phap.md)
- Độ tin cậy & khoảng trống dữ liệu → [`03-do-tin-cay-va-khoang-trong.md`](03-do-tin-cay-va-khoang-trong.md)
