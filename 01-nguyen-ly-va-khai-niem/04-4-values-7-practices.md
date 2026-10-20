# 4 Foundational Values & 7 Practices (bổ trợ 10 principles)

> **File MỚI** — ngoài 10 principles trong whitepaper, một chuyên đề trên **AWS Builder** ("The Answer to AI Development Chaos: Systematic AI-DLC Practices") hệ thống hóa thêm **4 Foundational Values** và **7 Practices** để vận hành hóa các nguyên lý vào thực tế kỹ thuật.
>
> ⚠️ **(single source — uncorroborated):** phần này hiện chủ yếu dựa trên **một nguồn AWS Builder duy nhất**; chưa có nguồn độc lập thứ hai đối chứng.

---

## 4 Foundational Values (giá trị nền tảng)

Theo mô-típ "X over Y" quen thuộc của Agile Manifesto:

1. **Human-AI Collaboration over Isolated Solutions** — ưu tiên cộng tác Nhân-Máy hơn các giải pháp cô lập.
2. **Collective Intelligence over Individual Brilliance** — đề cao trí tuệ tập thể hơn sự xuất chúng cá nhân.
3. **Rapid Informed Decisions over Analysis Paralysis** — ra quyết định nhanh nhưng đủ thông tin, thay vì tê liệt vì phân tích.
4. **Business Impact over Development Velocity** — đặt tác động kinh doanh thực tế lên trên tốc độ viết mã thuần túy.

---

## 7 Practices (chia theo 3 trụ cột)

### 🟦 Trụ cột Foundation — Collaboration
| Practice | Nội dung |
|---|---|
| **Decompose** | Phân rã bài toán phức tạp thành các bước tuần tự **có giám sát** |
| **Maximize Semantics** | Giao tiếp giàu **ngữ nghĩa**, tránh mô tả mã nguồn dài dòng |
| **Refresh Context** | Quản lý context chiến lược: **giải phóng** bộ nhớ hội thoại ra tệp ngoài, rồi **nạp chọn lọc** |

### 🟨 Trụ cột Protection — Intelligence
| Practice | Nội dung |
|---|---|
| **Rein in Overreach** | Kiềm chế xu hướng AI **tự ý mở rộng phạm vi** → chống over-engineering & feature creep |
| **Handle Design Principles with Care** | Ưu tiên **plain component modelling** (phù hợp dữ liệu huấn luyện của AI) thay vì các design pattern truyền thống quá phức tạp |

### 🟥 Trụ cột Acceleration — Judgment
| Practice | Nội dung |
|---|---|
| **Tame Brownfield Beast** | Chuyển **legacy code** thành **semantic models** trước khi cho AI xử lý → vượt giới hạn context window |
| **Refactor with Surgical Precision** | So sánh **A/B hệ thống quy tắc nghiệp vụ** cũ↔mới bài bản để **bảo toàn trọn vẹn business logic** khi hiện đại hóa |

Nguồn: [AWS Builder — The Answer to AI Development Chaos: Systematic AI-DLC Practices](https://builder.aws.com/content/35b5OaMGqCxMm3y3yOTjUSnMaj3/the-answer-to-ai-development-chaos-systematic-ai-dlc-practices)

---

## Đọc tiếp
- 10 principles nền tảng → [`01-10-nguyen-tac.md`](01-10-nguyen-tac.md)
- Thuật ngữ (1-Pizza AI Pods, Bounded Autonomy...) → [`03-thuat-ngu.md`](03-thuat-ngu.md)
