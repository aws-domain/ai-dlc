# AI-DLC — Tổng hợp nghiên cứu

> **AI-DLC** (*AI-Driven Development Life Cycle*) — phương pháp (methodology) phát triển phần mềm "AI-native" do AWS giới thiệu năm 2025, đặt AI làm **cộng tác viên trung tâm** (central collaborator) thay vì chỉ là công cụ hỗ trợ.

Thư mục này tổng hợp toàn bộ kiến thức về AI-DLC: định nghĩa, lịch sử hình thành, nguyên tắc, các phase/stage, thuật ngữ, công cụ triển khai, và các bài viết chính thức từ AWS. Mọi nội dung đều **gắn link nguồn** để bạn kiểm chứng.

Tài liệu được viết bằng **tiếng Việt**, giữ nguyên các **thuật ngữ chuyên ngành bằng English**.

---

## 🗂️ Cấu trúc thư mục

```
AI-DLC/
├── README.md                        ← bạn đang ở đây (mục lục tổng)
├── 00-tong-quan/
│   ├── 01-ai-dlc-la-gi.md           Định nghĩa, bản chất, so sánh AI-assisted vs AI-managed
│   └── 02-lich-su-hinh-thanh.md     Timeline, co-authors, đối chiếu mâu thuẫn niên đại
├── 01-nguyen-ly-va-khai-niem/
│   ├── 01-10-nguyen-tac.md          10 principles nền tảng (Method Definition Paper)
│   ├── 02-vong-lap-cong-tac.md      Vòng lặp Human–AI (plan → clarify → execute → verify)
│   ├── 03-thuat-ngu.md              Glossary: Bolt, Unit, Mob, 1-Pizza AI Pods, Harness...
│   └── 04-4-values-7-practices.md   ★ MỚI: 4 Foundational Values + 7 Practices
├── 02-phases-va-stages/
│   ├── 01-ba-phase-cot-loi.md       Inception / Construction / Operations (mô hình gốc)
│   └── 02-5-phases-33-stages.md     Mô hình mở rộng của open-source workflow
├── 03-cong-cu-va-trien-khai/
│   ├── 01-aidlc-workflows.md        Repo, engine 2.0, 11 profiles, lệnh install/usage
│   ├── 02-vi-du-thuc-te.md          Walkthrough River Crossing Puzzle (blog AWS)
│   └── 03-case-studies.md           ★ MỚI: Wipro, SAP ABAP, FinServ, số liệu 10–15x
├── 04-tai-nguyen-aws/
│   └── 01-bai-viet-chinh-thuc.md    Danh mục đầy đủ blog/paper/session AWS + link
├── 05-slides-va-tai-lieu-tai-ve/
│   └── README.md                    Trạng thái thu thập slide + hướng dẫn tải
└── 06-so-sanh-va-phan-bien/          ★ MỚI (toàn bộ thư mục)
    ├── 01-so-sanh-phuong-phap.md    So sánh AI-DLC vs Waterfall/Agile/Vibe Coding
    ├── 02-goc-nhin-phan-bien.md     Gate fatigue, anti-patterns, RCT arXiv, Ferrari
    └── 03-do-tin-cay-va-khoang-trong.md  Confidence & gaps + References (arXiv)
```

---

## 🚀 Đọc theo thứ tự nào?

| Nếu bạn muốn... | Đọc file |
|---|---|
| Hiểu nhanh AI-DLC là gì | [`00-tong-quan/01-ai-dlc-la-gi.md`](00-tong-quan/01-ai-dlc-la-gi.md) |
| Biết nó ra đời thế nào, ai làm | [`00-tong-quan/02-lich-su-hinh-thanh.md`](00-tong-quan/02-lich-su-hinh-thanh.md) |
| Nắm triết lý & 10 nguyên tắc | [`01-nguyen-ly-va-khai-niem/01-10-nguyen-tac.md`](01-nguyen-ly-va-khai-niem/01-10-nguyen-tac.md) |
| Hiểu Bolt, Mob Elaboration, Unit | [`01-nguyen-ly-va-khai-niem/03-thuat-ngu.md`](01-nguyen-ly-va-khai-niem/03-thuat-ngu.md) |
| Xem quy trình 3 phase / 33 stages | [`02-phases-va-stages/`](02-phases-va-stages/) |
| Thử tay / triển khai thực tế | [`03-cong-cu-va-trien-khai/`](03-cong-cu-va-trien-khai/) |
| So sánh với Agile/Scrum/Vibe Coding | [`06-so-sanh-va-phan-bien/01-so-sanh-phuong-phap.md`](06-so-sanh-va-phan-bien/01-so-sanh-phuong-phap.md) |
| Đọc phản biện, hạn chế, rủi ro | [`06-so-sanh-va-phan-bien/02-goc-nhin-phan-bien.md`](06-so-sanh-va-phan-bien/02-goc-nhin-phan-bien.md) |
| Lấy toàn bộ link gốc AWS | [`04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md`](04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md) |

---

## ⚡ TL;DR (tóm tắt 30 giây)

- **AI-DLC** do **Raja SP** (Principal Solutions Architect, AWS) tạo ra, công bố qua blog AWS DevOps ngày **31/07/2025**.
- Nó khắc phục 2 anti-pattern: **AI-assisted** (AI chỉ làm việc vặt) và **AI-managed/autonomous** (AI tự làm hết, không có người giám sát) — cả hai đều cho kết quả dưới mức kỳ vọng.
- Mô hình tư duy cốt lõi: **AI lập kế hoạch → hỏi để làm rõ → thực thi → con người ra quyết định quan trọng & phê duyệt**.
- 3 phase gốc: **Inception → Construction → Operations**; thuật ngữ mới: **Bolt** (thay cho sprint), **Unit of Work** (thay cho epic), **Mob Elaboration / Mob Construction** (nghi thức cộng tác nhóm).
- Tháng **11/2025**, AWS **open-source** workflow rules tại repo [`awslabs/aidlc-workflows`](https://github.com/awslabs/aidlc-workflows), chạy được trên **Amazon Q Developer, Kiro** và nhiều coding agent khác; đến **09/2026** tiến hóa thành **engine 2.0** (bản 2.11.0, native CLI, 5 phases/33 stages/14 agents/11 profiles/7 harnesses).
- ⚠️ **Góc nhìn phản biện:** số liệu "10–15x" là **vendor-reported chưa kiểm chứng độc lập**; RCT độc lập (arXiv) cho kết quả **−19%** khi thiếu cấu trúc. Rủi ro thực tế: **gate fatigue**, accountability gap, cần nền tảng **DevSecOps + Spec-Driven Development** trưởng thành. Xem [`06-so-sanh-va-phan-bien/`](06-so-sanh-va-phan-bien/).

> Nguồn gốc của mọi khẳng định trên nằm trong các file con, đều kèm URL để kiểm chứng.

---

*Tổng hợp bởi Kiro — tạo ngày 2026-10-13, **bổ sung ngày 2026-10-20** từ báo cáo Gemini Deep Research (thêm co-authors, engine 2.0, 11 profiles, 4 Values/7 Practices, case studies, và toàn bộ góc nhìn phản biện + so sánh). Toàn bộ nguồn là tài liệu công khai của AWS, IBM, arXiv và cộng đồng.*
