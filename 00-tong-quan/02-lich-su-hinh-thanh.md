# Lịch sử hình thành & xuất hiện của AI-DLC

## Ai tạo ra?

AI-DLC được **Raja SP** — **Principal Solutions Architect tại AWS** (lãnh đạo các *Developer Transformation Programs*) — và nhóm của ông sáng tạo ra.

> Raja đã làm việc với **hơn 100 khách hàng lớn**, giúp họ thiết kế và vận hành các hệ thống mission-critical trên kiến trúc hiện đại. Chính từ kinh nghiệm này, Raja và nhóm tạo ra AI-DLC — "an end-to-end, AI-native methodology that reimagines how large teams collaboratively build production-grade software in the AI era."

Nguồn: [Tiểu sử tác giả — AWS DevOps Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)

Xác nhận độc lập từ IBM:
> "Coined by AWS's Raja SP in 2025 and described in his 'AI-Driven Development Lifecycle (AI-DLC) Method Definition' whitepaper..."
> — [IBM Think](https://www.ibm.com/think/topics/ai-dlc)

Và từ repo mẫu của AWS:
> "Created by Raja SP at AWS, AI-DLC repositions AI from coding assistant to development orchestrator..."
> — [AWS Samples — AIDLC Collaborative Documentation](https://aws-samples.github.io/sample-collaborative-ai-dlc/getting-started/methodology/)

### Đội ngũ đồng tác giả (co-authors) — _bổ sung từ nghiên cứu Gemini_

Raja SP là người sáng lập, nhưng việc chuyển lý thuyết thành engine open-source + hướng dẫn thực chiến là công sức của cả nhóm:

| Người | Vai trò | Đóng góp |
|---|---|---|
| **Raja SP** | Principal Solutions Architect, AWS | Sáng lập methodology; tác giả whitepaper *Method Definition* |
| **Raj Jain** | Senior Solutions Architect (Developer Specialist), AWS | Đồng tác giả; nền tảng bảo mật ở Amazon, tác giả Bell Labs Technical Journal, đồng tác giả tiêu chuẩn IETF, **12 bằng sáng chế** |
| **Will Matos** | AWS | Xây dựng bộ khung adaptive workflows + hướng dẫn triển khai trên Amazon Q / Kiro |
| **Siddhesh Jog** | AWS | Xây dựng adaptive workflows + tài liệu triển khai |
| **Anupam Mishra** | Director, Developer Programmes (Ấn Độ & Nam Á), AWS | Đúc kết nghi thức cộng tác; **đồng thuyết trình** DVT214 tại re:Invent 2025 |

Nguồn: [AWS DevOps Blog — Building with AI-DLC (author bios)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/) · [Open-Sourcing Adaptive Workflows](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)

---

## Dòng thời gian (timeline)

| Thời điểm | Sự kiện | Nguồn |
|---|---|---|
| **Cuối 2024 → đầu 2025** | Bản thảo **Method Definition Paper** (Amplify) được Raja SP khởi thảo & **thử nghiệm thực địa với 100+ khách hàng** để kiểm chứng trước khi công bố rộng rãi. | Phân tích đối chiếu niên đại (xem mục bên dưới) |
| **Tháng 7/2025** | AI-DLC được **công bố công khai** lần đầu qua bài blog nền tảng "AI-Driven Development Life Cycle: Reimagining Software Engineering" (đăng **31/07/2025**, tác giả Raja SP). Đồng thời phát hành **Method Definition Paper** (whitepaper). | [AWS DevOps Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) |
| **Năm 2025** | Khái niệm được Raja SP "đặt tên" (coined) và mô tả chính thức trong whitepaper. | [IBM Think](https://www.ibm.com/think/topics/ai-dlc) |
| **Tháng 11/2025** | AWS **open-source workflow rules** của AI-DLC (triển khai dưới dạng Amazon Q Rules + Kiro Steering Files) tại repo `awslabs/aidlc-workflows`, giấy phép **MIT-0**. Repo ban đầu lưu tại `aws-samples/sample-aidlc-workflows` trước khi dời về nhà chung `awslabs/`. | [Dedicatted Guide](https://media.dedicatted.com/wp-content/uploads/2026/08/Dedicatted-AI-DLC-Guide-1.pdf) · [awslabs/aidlc-workflows](https://github.com/awslabs/aidlc-workflows) |
| **29/11/2025** | Đăng 2 blog quan trọng cùng ngày: **"Open-Sourcing Adaptive Workflows for AI-DLC"** và **"Building with AI-DLC using Amazon Q Developer"** (hướng dẫn thực hành). | [Open-sourcing blog](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/) · [Building blog](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/) |
| **re:Invent 2025** | Session **DVT214 — "Introducing AI-driven development lifecycle (AI-DLC)"** do Anupam Mishra & Raja SP trình bày (video AWS Events, **>115.000 lượt xem**). | [dev.to](https://dev.to/kazuya_dev/aws-reinvent-2025-introducing-ai-driven-development-lifecycle-ai-dlc-dvt214-32b) · [Zenn](https://zenn.dev/kiiwami/articles/45a7ac851f2aeb27?locale=en) |
| **2025 → 2026** | Mở rộng sang nhiều lĩnh vực: Financial Services, SAP ABAP, Amazon Bedrock AgentCore; cộng đồng & đối tác (Dedicatted, IBM, v.v.) viết tài liệu phân tích. | Xem [`../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md`](../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md) |
| **Tháng 9/2026** | **AI-DLC Workflows 2.0** — tiến hóa từ "rule scaffolds" thành **engine phần mềm hoàn chỉnh** (native `aidlc` CLI, deterministic engine): bản ổn định **2.11.0** + kênh preview nightly. Mở thêm nhánh `sample-aidlc-lite`, `sample-aidlc-decisions-driven-skill`. | [awslabs/aidlc-workflows](https://github.com/awslabs/aidlc-workflows) · [Felipe Fontoura](https://felipefontoura.com/articles/what-is-ai-dlc/) |

### ⚠️ Đối chiếu mâu thuẫn niên đại (discrepancy analysis) — _bổ sung từ nghiên cứu Gemini_

Các nguồn ghi **3 mốc khác nhau** cho "lần xuất hiện đầu":

- **"(2024)"** — một tài liệu Zenn trích năm xuất bản của Method Definition Paper trên Amplify.
- **"Jan 2025"** — một bài journal (*International Journal of AI, Data Science and ML*, 01/2026) ghi trong danh mục tham khảo.
- **31/07/2025** — ngày đăng/cập nhật chính thức của blog nền tảng AWS (nguồn uy tín nhất).

**Giải thích (interpretation):** không mâu thuẫn thực sự, mà phản ánh **lộ trình 2 giai đoạn** điển hình của AWS — whitepaper được khởi thảo & field-test nội bộ từ **cuối 2024→đầu 2025**, rồi mới **công bố công khai 31/07/2025**. → Dùng **31/07/2025** làm mốc công bố chính thức.

> **Lưu ý về mốc "tháng 7/2025":** Dedicatted ghi "published by AWS in July 2025, with the workflow rules open sourced that November." Blog nền tảng ghi ngày đăng 31/07/2025. Hai nguồn này nhất quán → **evidence: strong**.

---

## Bối cảnh ra đời — "vì sao lại xuất hiện lúc này?"

AI-DLC xuất hiện trong làn sóng các công cụ generative AI cho lập trình chín muồi — đặc biệt là **Amazon Q Developer** và **Kiro** của chính AWS. Khi các công cụ này đã có khả năng "agentic" (tự lập kế hoạch, tự thực thi nhiều bước), AWS nhận ra rằng **cách tổ chức quy trình** mới là nút thắt, chứ không phải năng lực sinh code.

Nói cách khác: công cụ đã đủ mạnh, nhưng **methodology** để dùng chúng đúng cách thì chưa có → AI-DLC ra đời để lấp khoảng trống đó.

Nguồn:
- [AWS DevOps Blog — mở đầu bài viết nền tảng](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- [Brights.io — "Built around Amazon Q Developer and Kiro, it integrates AI into every stage"](https://brights.io/blog/ai-driven-development-life-cycle)

---

## Vị trí trong lịch sử các phương pháp phát triển phần mềm

```
Waterfall  →  Agile / Scrum  →  (AI-assisted trong Agile)  →  AI-DLC
(tuần tự)     (lặp, human-     ("faster horse")              (AI-native,
              centric)                                        human-AI symbiosis)
```

IBM mô tả bước nhảy này: Agile/Scrum về cơ bản là **human-centric**; AI-DLC là **machine-human collaboration**. Ví von: thêm AI vào Agile chỉ tạo ra "con ngựa nhanh hơn", còn AI-DLC là "chiếc ô tô".

Nguồn: [IBM Think](https://www.ibm.com/think/topics/ai-dlc)

---

## Đọc tiếp
- Triết lý chi tiết & 10 nguyên tắc → [`../01-nguyen-ly-va-khai-niem/01-10-nguyen-tac.md`](../01-nguyen-ly-va-khai-niem/01-10-nguyen-tac.md)
- Danh mục đầy đủ tài nguyên AWS → [`../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md`](../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md)
