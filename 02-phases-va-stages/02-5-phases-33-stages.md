# Mô hình mở rộng: 5 phases / 33 stages (open-source workflow)

Repo open-source [`awslabs/aidlc-workflows`](https://github.com/awslabs/aidlc-workflows) hiện thực hóa AI-DLC chi tiết hơn mô hình 3 phase gốc: **5 phases chứa 33 stages**.

> *"The AI-DLC lifecycle is organized into 5 phases containing 33 stages."*
> — [AI-DLC Workflows docs — Phases and Stages](https://awslabs.github.io/aidlc-workflows/guide/04-phases-and-stages/)

> **Lưu ý quan trọng:** Mô hình 5-phase này là của **bản triển khai open-source** (có thể tiến hóa theo thời gian), còn mô hình **3-phase (Inception/Construction/Operations)** là khung khái niệm gốc trong whitepaper & blog. Hai mô hình không mâu thuẫn — 5 phase là bản "nở ra" chi tiết hơn.

---

## Tổng quan dòng chảy

```
INITIALIZATION (0.1–0.3)  →  IDEATION (1.1–1.7)  →  INCEPTION (2.1–2.9)
   →  CONSTRUCTION (3.1–3.7)  →  OPERATION (4.1–4.7)
                                      │
                   (Feedback loop quay về Ideation 1.1)
```

Các phase chạy **tuần tự**. Ở mỗi ranh giới phase (trừ Initialization → Ideation) có một **Verification Gate** chạy kiểm tra traceability tự động.

---

## Các con số then chốt

| Metric | Giá trị |
|---|---|
| Phases | 5 (Initialization, Ideation, Inception, Construction, Operation) |
| Stages | 33 |
| Agents | 14 (11 domain expert, 2 reviewer, 1 composer) |
| Scopes | 11 (enterprise → express, + workshop) + plan do agent tự đề xuất |
| Depth levels | 3 (Minimal, Standard, Comprehensive) |
| Test strategy levels | 3 (Minimal, Standard, Comprehensive) |
| Audit event types | 118 |

Nguồn: [AI-DLC Workflows docs — Introduction (Key Numbers)](https://awslabs.github.io/aidlc-workflows/guide/00-introduction/)

---

## Phase 0 — Initialization (0.1–0.3)
Bootstrap workspace: scaffold thư mục docs, detect workspace (greenfield/brownfield), init state. Chạy **tự động, không có approval gate**, trong một tool call deterministic (`aidlc-utility intent-create`).

| # | Stage | Artifact chính |
|---|---|---|
| 0.1 | Workspace Scaffold | thư mục record của intent đầu tiên |
| 0.2 | Workspace Detection | `aidlc-state.md` |
| 0.3 | State Initialization | `aidlc-state.md`, các shard `audit/` |

## Phase 1 — Ideation (1.1–1.7)
Validate sáng kiến: capture intent, đánh giá khả thi, định scope, lập team, xin phê duyệt.

| # | Stage | Lead agent | Điều kiện |
|---|---|---|---|
| 1.1 | Intent Capture & Framing | product-agent | ALWAYS |
| 1.2 | Market Research | product-agent | CONDITIONAL |
| 1.3 | Feasibility & Constraints | architect-agent | CONDITIONAL |
| 1.4 | Scope Definition | product-agent | ALWAYS |
| 1.5 | Team Formation | delivery-agent | CONDITIONAL |
| 1.6 | Rough Mockups | design-agent | CONDITIONAL |
| 1.7 | Approval & Handoff | delivery-agent | ALWAYS |

## Phase 2 — Inception (2.1–2.9)
Làm chi tiết requirements: phân tích codebase, elicit requirements, thiết kế kiến trúc, phân rã thành Unit, lập kế hoạch delivery.

| # | Stage | Lead agent | Điều kiện |
|---|---|---|---|
| 2.1 | Reverse Engineering | developer-agent | Brownfield (chạy dạng *pipeline* 2 mắt xích) |
| 2.2 | Practices Discovery | pipeline-deploy-agent | CONDITIONAL (chạy dạng *subagent* hub-and-spoke) |
| 2.3 | Requirements Analysis | product-agent | ALWAYS |
| 2.4 | User Stories | product-agent | User-facing (chạy dạng *mob*) |
| 2.5 | Refined Mockups | design-agent | UI projects |
| 2.6 | Domain Design | architect-agent | Theo execution plan |
| 2.7 | Units Generation | architect-agent | ALWAYS |
| 2.8 | Contract Design | architect-agent | CONDITIONAL |
| 2.9 | Delivery Planning | delivery-agent | ALWAYS (sinh `bolt-plan.md`) |

## Phase 3 — Construction (3.1–3.7)
Xây dựng giải pháp: design, implement, test — theo từng "slice" review được. Các stage 3.1–3.5 lặp **per Unit**; 3.6–3.7 chạy một lần sau cùng.

| # | Stage | Lead agent | Khi nào chạy |
|---|---|---|---|
| 3.1 | Functional Design | architect-agent | Per Unit (điều kiện) |
| 3.2 | NFR Requirements | architect-agent | Per Unit (điều kiện) |
| 3.3 | NFR Design | architect-agent | Per Unit (điều kiện) |
| 3.4 | Infrastructure Design | aws-platform-agent | Per Unit (điều kiện) |
| 3.5 | Code Generation | developer-agent | Per Unit (ALWAYS) |
| 3.6 | Build and Test | quality-agent | ALWAYS, một lần cuối |
| 3.7 | CI Pipeline | pipeline-deploy-agent | CONDITIONAL, một lần cuối |

**Đặc điểm:** mặc định chạy **unit-major, tuần tự** với checkpoint phê duyệt từng Unit. Có khái niệm **walking skeleton** (Unit đầu tiên là slice tích hợp nhỏ nhất chạy được, phải qua kiểm tra end-to-end thật & được người duyệt trước khi làm các Unit sau). Có thể chạy **swarm** (song song các Unit độc lập) nếu chọn stage-major. **Mọi failure đều dừng và hỏi người** (halt-and-ask).

## Phase 4 — Operation (4.1–4.7)
Deploy & vận hành. Toàn bộ 7 stage đều **CONDITIONAL** (có thể bỏ qua cả phase với scope `mvp`/`poc`). Stage 4.7 là **terminal** — duyệt xong là workflow hoàn tất; hoặc quay lại Ideation 1.1 cho chu kỳ mới.

| # | Stage | Lead agent |
|---|---|---|
| 4.1 | Deployment Pipeline | pipeline-deploy-agent |
| 4.2 | Environment Provisioning | aws-platform-agent |
| 4.3 | Deployment Execution | pipeline-deploy-agent |
| 4.4 | Observability Setup | operations-agent |
| 4.5 | Incident Response | operations-agent |
| 4.6 | Performance Validation | quality-agent |
| 4.7 | Feedback & Optimization | operations-agent |

Nguồn cho toàn bộ bảng: [AI-DLC Workflows docs — Phases and Stages](https://awslabs.github.io/aidlc-workflows/guide/04-phases-and-stages/)

---

## Triết lý "Small Mob, Broad Agents"
Thay vì hàng chục chuyên gia hẹp (tái tạo chuỗi handoff kiểu waterfall), AI-DLC dùng **11 agent có năng lực rộng**, mỗi agent tham gia nhiều stage/phase và **mang context xuyên suốt** → giảm handoff & chi phí điều phối. Giống cách một "mob" 3–5 người bao trọn một feature.

Nguồn: [AI-DLC Workflows docs — "Philosophy: Small Mob, Broad Agents"](https://awslabs.github.io/aidlc-workflows/guide/00-introduction/)

---

## Đọc tiếp
- Công cụ & cách chạy → [`../03-cong-cu-va-trien-khai/01-aidlc-workflows.md`](../03-cong-cu-va-trien-khai/01-aidlc-workflows.md)
