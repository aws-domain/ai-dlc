# Độ tin cậy, khoảng trống dữ liệu & References mở rộng

> **File MỚI** — chắt lọc mục "Confidence & Gaps" và danh mục References (gồm các paper arXiv) từ báo cáo Gemini Deep Research.

---

## 1. Bảng đánh giá độ tin cậy (Confidence & Gaps)

| Mảng nội dung | Mức tin cậy | Cơ sở chứng thực & khoảng trống |
|---|---|---|
| Định nghĩa, 10 principles, Human-AI Loop, thuật ngữ (Bolt/Unit/Mob) | **Rất cao** | Chứng thực chéo đồng nhất: AWS DevOps Blog, AWS Industries, re:Invent DVT214, IBM Think, ThoughtWorks |
| Kiến trúc engine `aidlc-workflows` (5 phases/33 stages/14 agents/11 profiles/7 harnesses) | **Rất cao** | Trích trực tiếp repo chính thức awslabs + đặc tả bản 2.x (2.11.0) |
| 4 Values / 7 Practices; biến thể (AI-DLC Lite, SAP ABAP, BigData-AIDLC) | **Trung bình–cao** | Có nguồn chính thức AWS, nhưng mỗi chủ đề **chủ yếu dựa 1 nguồn chuyên biệt** (single source — uncorroborated) |
| Số liệu năng suất ("10–15x", "40–60%", Wipro 20 giờ) | **Trung bình – cần thận trọng** | **Vendor-reported, chưa có RCT peer-reviewed độc lập** kiểm chứng. RCT độc lập (arXiv:2507.09089) lại cho kết quả **−19%** khi thiếu cấu trúc quy trình |
| Chi phí vận hành dài hạn (token cost, maintainability 2–3 năm) | **Thấp – khoảng trống nghiên cứu** | **Không tìm thấy nguồn đáng tin cậy** đo định lượng chi phí token (14 agents × 33 stages trên model đắt như Claude Opus 4.8) và maintainability dài hạn |

> **Nguyên tắc đọc:** mọi claim gắn nhãn *(single source — uncorroborated)* hoặc *(vendor-reported)* cần xác minh thêm trước khi đưa vào quyết định đầu tư.

---

## 2. References mở rộng (bổ sung so với tài liệu gốc)

### Nguồn học thuật (arXiv / journal) — MỚI
- **Becker, J. et al. (2025)** — *Measuring the Impact of AI on Experienced Open-Source Developer Productivity* — [arXiv:2507.09089](https://arxiv.org/abs/2507.09089) — academic (RCT, kết quả −19%)
- **Qiao, Y. et al. (2025)** — Comprehension-Performance Gap trong brownfield + GenAI — [arXiv:2510.17894](https://arxiv.org/abs/2510.17894), [arXiv:2511.02922](https://arxiv.org/abs/2511.02922) — academic
- **AI-DLC: Reimagining Software Engineering for the AI Era** — International Journal of AI, Data Science and ML (01/2026) — [ResearchGate](https://www.researchgate.net/publication/402813699_AI-Driven_Development_Lifecycle_AI-DLC_Reimagining_Software_Engineering_for_the_AI_Era) — academic
- **Spec-Driven Development as the Governance Backbone of AI-DLC** — IJSREM — [ijsrem.com](https://ijsrem.com/download/spec-driven-development-as-the-governance-backbone-of-the-ai-driven-development-lifecycle-ai-dlc) — academic

### Nguồn AWS chính thức — bổ sung
- **The Answer to AI Development Chaos: Systematic AI-DLC Practices** (4 Values / 7 Practices) — AWS Builder — [builder.aws.com](https://builder.aws.com/content/35b5OaMGqCxMm3y3yOTjUSnMaj3/the-answer-to-ai-development-chaos-systematic-ai-dlc-practices)
- **Accelerating Software Delivery with Units of Work in the AI-DLC** — AWS Builder — [builder.aws.com](https://builder.aws.com/content/3HAB4twQ38WEKqLK7gfEIfOzHbc/accelerating-software-delivery-with-units-of-work-in-the-ai-dlc)
- **DVT214 session video** — AWS Events YouTube — [youtube.com/watch?v=H3d3abjxWAw](https://www.youtube.com/watch?v=H3d3abjxWAw)

### Nguồn độc lập (phản biện) — MỚI
- **Felipe Fontoura — What is AI-DLC?** (mổ xẻ bản 2.11.0, 4 anti-patterns) — [felipefontoura.com](https://felipefontoura.com/articles/what-is-ai-dlc/)
- **Daoqi Zhang / ExploreAgentic — AI-DLC Explained** (accountability gap) — [exploreagentic.ai](https://www.exploreagentic.ai/insights/ai-dlc/)
- **Orchestrator.dev — AI-DLC in Practice** — [orchestrator.dev](https://orchestrator.dev/blog/2026-10-03-ai-dlc-in-practice/)
- **Desk2Mob — AI-DLC Philosophy & Methodology** — [desk2mob.com](https://www.desk2mob.com/posts/364-ai-driven-development-lifecycle-ai-dlc-philosophy-methodology)

---

## 3. Mâu thuẫn giữa các nguồn (ghi nhận khách quan)

| Chủ đề | Mâu thuẫn | Ghi chú |
|---|---|---|
| **Ngày công bố** | 2024 (Zenn) vs "Jan 2025" (journal) vs **31/07/2025** (AWS blog) | Phản ánh lộ trình 2 giai đoạn: whitepaper thử nghiệm nội bộ 2024→đầu 2025, công bố rộng rãi 31/07/2025. Xem [`../00-tong-quan/02-lich-su-hinh-thanh.md`](../00-tong-quan/02-lich-su-hinh-thanh.md) |
| **Số stages** | "32 stages" (desk2mob) vs **33 stages** (repo chính thức 2.11.0) | Repo chính thức là nguồn chuẩn; chênh 1 do thêm bước kiểm soát trong bản 2.x |
| **Audit event types** | "118" (tài liệu gốc của bộ này) vs **"119"** (báo cáo Gemini, bản 2.11.0) | Version drift — repo tiến hóa; con số tăng theo bản phát hành |

---

## Đọc tiếp
- Danh mục tài nguyên AWS gốc → [`../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md`](../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md)
