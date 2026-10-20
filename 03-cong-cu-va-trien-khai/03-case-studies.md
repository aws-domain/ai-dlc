# Case studies & số liệu thực tế (real-world)

> **File MỚI** — tổng hợp các nghiên cứu tình huống & số liệu định lượng từ báo cáo Gemini Deep Research. **Đọc kèm cảnh báo** ở [`../06-so-sanh-va-phan-bien/02-goc-nhin-phan-bien.md`](../06-so-sanh-va-phan-bien/02-goc-nhin-phan-bien.md): phần lớn là **số liệu tự công bố của AWS (vendor-reported)**, chưa kiểm chứng độc lập.

---

## Bảng case studies

| Tổ chức / Dự án | Lĩnh vực & bối cảnh | Cách triển khai | Kết quả ghi nhận | Độ tin cậy |
|---|---|---|---|---|
| **Wipro** | IT services & phát triển phần mềm doanh nghiệp | Mob Elaboration + Mob Construction theo chu kỳ Bolt | Nén công việc **~3 tháng → ~20 giờ** (5 ngày × 4 giờ/ngày họp Mob) | Vendor-reported |
| **Tổng hợp >100 khách hàng AWS** | Đa ngành (tài chính, bán lẻ, công nghiệp), nhiều khu vực | Dưới hướng dẫn trực tiếp của Developer Transformation Programs (Raja SP) | **10–15x** năng suất; **+40–60%** velocity; **−40–60%** defects; **ROI 300–500%**/12 tháng | Vendor-reported |
| **SAP ABAP trên S/4HANA** | ERP (đặt/hoàn/hủy vé máy bay, xuất e-ticket) | Kiro + ABAP Accelerator: Answer: tags ở Inception → sinh ABAP OO, REST API, CDS views ở Construction → kích hoạt SICF ở Operations | Giảm mạnh learning curve khi chuyển sang RAP/S4HANA; bảo toàn context từ requirement→service chạy thật | single source |
| **Financial Services** | Thanh toán & ngân hàng, quản lý rủi ro nghiêm ngặt | Scrum Teams → 1-Pizza AI Pods; risk-based change categorisation; left-shifted QA; AWS Security Agent + Amazon DevOps Agent | Đáp ứng operational risk; tự động pentest liên tục; tự động điều tra root cause sự cố | single source |
| **BigData-AIDLC (E-commerce)** | Data engineering (phân bổ GMV real-time <1 phút, 5 kênh, CDC/Kafka/API) | Đưa chuẩn phân tầng + data dictionary + Data Quality contracts vào Steering Files từ Inception | Loại lỗi lệch GMV ở tuần nghiệm thu thứ 3; ước tính **5–10x** so với nền tảng dữ liệu truyền thống | single source |
| **River Crossing Puzzle** (walkthrough) | Web UI minh họa, trên AWS DevOps Blog | VS Code + Amazon Q Developer (hoặc Kiro CLI) + Mermaid viewer | Trình diễn đầy đủ: AI sinh Mermaid, hỏi làm rõ, lưu audit qua từng gate | Chính thức AWS |

> **Lưu ý chống hallucination:** con số **"cycle time compression 44%–90%"** (AWS Builder — Units of Work) và các số liệu 5–10x cũng là **single source — uncorroborated**.

Nguồn: [AWS re:Invent DVT214 recap (Wipro, 10–15x)](https://dev.to/kazuya_dev/aws-reinvent-2025-introducing-ai-driven-development-lifecycle-ai-dlc-dvt214-32b) · [AWS for SAP Blog](https://aws.amazon.com/blogs/awsforsap/sap-abap-application-development-with-ai-dlc-ai-driven-development-lifecycle/) · [AWS Industries — Financial Services](https://aws.amazon.com/blogs/industries/ai-driven-development-lifecycle-for-financial-services/) · [AWS Builder — Units of Work](https://builder.aws.com/content/3HAB4twQ38WEKqLK7gfEIfOzHbc/accelerating-software-delivery-with-units-of-work-in-the-ai-dlc)

---

## Đọc tiếp
- Walkthrough chi tiết River Crossing → [`02-vi-du-thuc-te.md`](02-vi-du-thuc-te.md)
- Phản biện về số liệu năng suất → [`../06-so-sanh-va-phan-bien/02-goc-nhin-phan-bien.md`](../06-so-sanh-va-phan-bien/02-goc-nhin-phan-bien.md)
