# Công cụ & triển khai: aidlc-workflows

## Repo open-source chính thức

**`awslabs/aidlc-workflows`** — bộ **adaptive workflow steering rules** cho AI coding agent, hiện thực hóa methodology AI-DLC.

🔗 [https://github.com/awslabs/aidlc-workflows](https://github.com/awslabs/aidlc-workflows)

> *"AI-DLC is an intelligent software development workflow that adapts to your needs, maintains quality standards, and keeps you in control of the process."*
> — [README của repo](https://github.com/awslabs/aidlc-workflows/blob/main/README.md)

AWS open-source bộ này vào **tháng 11/2025**, triển khai dưới dạng **Amazon Q Rules** và **Kiro Steering Files**.

---

## Các harness (môi trường chạy) được hỗ trợ

Repo chạy từ **một core trung lập (harness-neutral)**, hỗ trợ nhiều coding agent:

- **Claude Code**
- **Kiro CLI** và **Kiro IDE**
- **Amazon Q Developer** (qua Project Rules)
- **Codex CLI**
- **Cursor**
- **opencode**
- **GitHub Copilot**

Gọi bằng một lệnh duy nhất (ví dụ trên Claude Code):
```
/aidlc Build a REST API for inventory management
```

Nguồn: [AI-DLC Workflows docs — Introduction](https://awslabs.github.io/aidlc-workflows/guide/00-introduction/)

---

## Cách orchestrator hoạt động

Lõi là một vòng lặp đơn giản: một **engine** deterministic quyết định bước tiếp theo; **conductor** (session `/aidlc`, `SKILL.md`) thực thi rồi hỏi engine bước kế. Trong vòng lặp, framework:

1. **Đọc stage files** — 33 định nghĩa stage trên 5 phase (mỗi stage nêu input, step, output, lead agent).
2. **Nạp agent personas** — kích hoạt góc nhìn chuyên gia (architect, developer, PM...).
3. **Quản lý state & audit** — theo dõi tiến độ trong `aidlc-state.md`, ghi mọi quyết định vào shard `audit/`.
4. **Phân phối theo stage topology** — dispatch subagent dạng hub-and-spoke, pipeline, hoặc mob.
5. **Trình approval gate** — sau mỗi stage, người dùng review & phê duyệt trước khi đi tiếp.

Nguồn: [AI-DLC Workflows docs — "How the Orchestrator Works"](https://awslabs.github.io/aidlc-workflows/guide/00-introduction/)

---

## Cấu trúc rules trong Amazon Q Developer

Khi dùng với Amazon Q, cấu trúc rules được tổ chức để tối ưu token:

- `aws-aidlc-rules/core-workflow.md` → đặt trong thư mục chỉ định `.amazonq/rules` (luôn trong context, không tốn thêm token).
- `aws-aidlc-rule-details/` → chứa rules chi tiết theo từng phase/stage, **nạp động (dynamically loaded)** khi cần → tiết kiệm context window.
  - 3 thư mục con tương ứng 3 phase.
  - 1 thư mục `common` chứa rules xuyên suốt (ví dụ "human-in-the-loop").

Nguồn: [AWS DevOps Blog — Building with AI-DLC (Step 4)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

---

## Các dự án / sản phẩm liên quan

| Tên | Mô tả | Link |
|---|---|---|
| **aidlc-workflows** | Steering rules open-source (bản chính) | [GitHub](https://github.com/awslabs/aidlc-workflows) |
| **sample-ai-driven-development-lifecycle-platform** | Platform multi-agent mẫu, dùng Bedrock AgentCore + Strands Agent SDK, tự dẫn dắt qua full SDLC | [GitHub](https://github.com/aws-samples/sample-ai-driven-development-lifecycle-platform) |
| **sample-collaborative-ai-dlc** | Tài liệu methodology cộng tác (AWS Samples) | [Docs](https://aws-samples.github.io/sample-collaborative-ai-dlc/getting-started/methodology/) |
| **AI-DLC Transformation Program** | Chương trình chuyển đổi (AWS Marketplace) | [Marketplace](https://aws.amazon.com/marketplace/pp/prodview-2dd666fx5v5hk) |
| **sample-aidlc-lite** _(mới)_ | **AI-DLC Lite** — tối ưu tốc độ: giảm gate từ 2→1/stage (chỉ duyệt output), giới hạn 1 vòng hỏi đáp rồi tự ghi giả định, hỏi đáp inline, rules mở rộng `*.opt-in.md` | [GitHub](https://github.com/aws-samples/sample-aidlc-lite) |
| **sample-aidlc-decisions-driven-skill** _(mới)_ | Kỹ năng Markdown thuần, không phụ thuộc runtime; **thực thi song song** bằng sub-agents + file ownership isolation + Unit Dashboard | [GitHub](https://github.com/aws-samples/sample-aidlc-decisions-driven-skill) |
| **sample-aidlc-toolset-with-subagents-and-custom-skills** _(mới)_ | Bộ toolset mở rộng với sub-agents & custom skills | [GitHub](https://github.com/aws-samples) |

---

## Yêu cầu để bắt đầu (prerequisites)

- Có **AWS account** hoặc **AWS Builder ID** để xác thực Amazon Q Developer.
- Cài extension Amazon Q Developer trong IDE (ví dụ VS Code), hoặc dùng **Kiro CLI** (không cần setup thêm).
- (Khuyến nghị) cài một **Mermaid viewer plugin** vì workflow sinh nhiều sơ đồ Mermaid trong file markdown.

Nguồn: [AWS DevOps Blog — Building with AI-DLC (Prerequisites)](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

---

## AI-DLC Workflows 2.0 — engine internals _(bổ sung từ nghiên cứu Gemini)_

Bản 2.x (tiêu biểu **2.11.0**, 09/2026) đã tiến hóa từ "rule scaffolds" thành **engine phần mềm hoàn chỉnh**:

- **Ngôn ngữ/runtime:** viết bằng **TypeScript**, đóng gói qua **Bun**. _(single source — uncorroborated)_
- **Triết lý kiến trúc:** *"One Core, Many Harnesses"*.
  - `core/` — định nghĩa trung lập: stages (`aidlc-common/`), agents, memory, scopes, sensors, knowledge, hooks (biến `{{HARNESS_DIR}}`).
  - `harness/<name>/` — `manifest.ts` + `emit.ts` để **biên dịch chéo** lõi sang 7 công cụ đích (`.claude`, `.kiro`, `.codex`, `.cursor`, `.aidlc`...).
- **Hệ đa tác nhân:** **14 specialized agents** = 11 domain experts + 2 reviewers + 1 adaptive composer.
- **Audit:** **119-event audit trail** (ghi mọi transition, source-bound review evidence, state, learned rules).
- **Model khuyến nghị:** AI-DLC chạy tốt nhất với reasoning model mạnh; khuyến nghị hiện tại là **Claude Opus 4.8**.
- **Kiểm thử tất định:** 4 cấp (smoke/unit/integration/e2e) + `bun scripts/package.ts --check` (biên dịch 2 lần, so khớp từng byte). _(single source — uncorroborated)_
- **Plugins:** khai báo qua `.aidlc-plugin/plugin.json`.

Nguồn: [awslabs/aidlc-workflows](https://github.com/awslabs/aidlc-workflows) · [Felipe Fontoura — What is AI-DLC? (phân tích 2.11.0)](https://felipefontoura.com/articles/what-is-ai-dlc/)

---

## 11 Workflow Profiles (scopes) — hiện thực nguyên tắc 10

Thay vì ép mọi yêu cầu qua đủ 33 stages, engine tự chọn (hoặc cho kỹ sư chỉ định) một **profile** chỉ kích hoạt tập con stages cần thiết:

| Profile | Số stages chạy | Dùng cho |
|---|---|---|
| **Feature** | 33 (full) | Tính năng mới phức tạp |
| **Classic** | 18 | Luồng phát triển tiêu chuẩn |
| **Infrastructure** | 13 | Thay đổi/chuyển đổi hạ tầng |
| **Refactor** | 10 | Tái cấu trúc mã |
| **Bugfix** | 9 (6 gates) | Sửa lỗi |
| **PoC** | 8 | Proof of Concept |

> (+ các profile khác tới tổng **11**; con số stage theo đặc tả bản 2.x.)

Nguồn: [awslabs/aidlc-workflows](https://github.com/awslabs/aidlc-workflows)

---

## Cài đặt & vận hành thực tế (install / usage) _(bổ sung)_

**Bước 1 — Install:**
```bash
# macOS / Linux / WSL
curl -fsSL https://github.com/awslabs/aidlc-workflows/releases/latest/download/install.sh | sh
```
```powershell
# Windows PowerShell (cửa sổ user thường, KHÔNG dùng Administrator)
irm https://github.com/awslabs/aidlc-workflows/releases/latest/download/install.ps1 | iex
```
> Trình cài đặt thiết lập binary `aidlc` + runtime cho harness, **không cần** cài sẵn Bun/Node.js. Môi trường bị khóa → dùng *manual-copy path* (cài Bun, tải `aidlc-copy-runtime-X.Y.Z.tar.gz`, copy `runtime/<harness>/`).
> ⚠️ **Lưu ý an toàn:** đây là lệnh *pipe-to-execute* (`irm | iex`); chỉ chạy vì nguồn là repo chính thức của AWS Labs. Với nguồn lạ, luôn tải script về đọc trước khi chạy.

**Bước 2 — Configure & Doctor:**
```bash
cd /path/to/your-project
aidlc config --harness claude   # hoặc: kiro | kiro-ide | codex | cursor | opencode | copilot
aidlc doctor                    # kiểm tra hooks & cấu hình
```
> Mở lần đầu trên Kiro IDE: chỉ chọn **Trust Folder & Continue** với dự án đã kiểm an toàn (hooks trong `.kiro` có quyền chạy lệnh trên máy trạm).

**Bước 3 — Start Workflow:**
```bash
/aidlc Build a REST API for inventory management
# Codex CLI: $aidlc ...
# Kiro IDE: chọn agent "aidlc" trong chat trước khi gõ /aidlc
```
> Doanh nghiệp dùng JIRA có thể nối qua **MCP Server Adapters** để đồng bộ Units of Work & trạng thái thực thi.

Nguồn: [awslabs/aidlc-workflows — Installation](https://github.com/awslabs/aidlc-workflows) · [AWS Builder — Units of Work (MCP/JIRA)](https://builder.aws.com/content/3HAB4twQ38WEKqLK7gfEIfOzHbc/accelerating-software-delivery-with-units-of-work-in-the-ai-dlc)

---

## Đọc tiếp
- Ví dụ thực tế từng bước (River Crossing Puzzle) → [`02-vi-du-thuc-te.md`](02-vi-du-thuc-te.md)
- Case studies & số liệu định lượng → [`03-case-studies.md`](03-case-studies.md)
