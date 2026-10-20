# Ví dụ thực tế: xây app "River Crossing Puzzle" bằng AI-DLC

Blog hướng dẫn của AWS demo toàn bộ workflow qua một app web đơn giản — **River Crossing Puzzle** (bài toán qua sông kinh điển: nông dân, cáo, gà, túi thóc) — dùng **Amazon Q Developer** trong VS Code.

🔗 Nguồn đầy đủ: [AWS DevOps Blog — Building with AI-DLC using Amazon Q Developer](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

---

## Các bước (tóm tắt)

| Bước | Stage | Điều gì xảy ra |
|---|---|---|
| 1 | — | Clone repo `git clone https://github.com/awslabs/aidlc-workflows.git` |
| 2 | — | Copy rules files vào thư mục project (theo README) |
| 3 | — | Cài & xác thực extension Amazon Q Developer trong IDE |
| 4 | Kick-off | Nhập problem statement, **có tiền tố "Using AI-DLC..."** để kích hoạt workflow |
| 5 | Workspace Detection | AI xác định greenfield/brownfield → vì mới nên đi tới Requirements Analysis. Tạo thư mục `aidlc-docs/` + `aidlc-state.md` + `audit.md` |
| 6 | Requirements Analysis | AI hỏi **câu hỏi trắc nghiệm** (kèm "Other") trong `requirement-verification-questions.md`; người dùng trả lời inline, gõ "Done"; AI kiểm mâu thuẫn rồi sinh `requirements.md` |
| 7 | Workflow Planning | AI sinh `execution-plan.md`, đề xuất **bỏ qua** các stage không cần (vì app đơn giản) → đi thẳng tới Code Generation |
| 8 | Code Generation Planning | AI tạo plan đánh số có checkbox trong `{unit-name}-code-generation-plan.md` (8 bước: HTML → CSS → game logic → test → doc) |
| 9 | Code Generation | AI sinh code thật (một file `index.html` nhúng CSS + JS), tick checkbox khi xong |
| 10 | Build and Test | AI tạo file hướng dẫn build & test (unit, integration, performance...) + summary readiness |

Kết quả: mở `index.html` trên trình duyệt → app chạy, giải được puzzle.

---

## Những điểm minh họa rõ triết lý AI-DLC

1. **Adaptive theo độ phức tạp:** AI tự nhận ra app đơn giản → **bỏ qua** User Stories, Application Design, Units Planning... Người dùng có quyền **override** nếu muốn giữ lại.

2. **Human-in-the-loop ở mọi checkpoint:** mỗi stage kết thúc bằng lựa chọn *Request Changes / Approve & Continue*. Không có gì chạy tiếp nếu người dùng chưa duyệt.

3. **Chống "AI tự giả định":** AI buộc phải hỏi làm rõ, trình bày dạng trắc nghiệm + "Other", và phát hiện mâu thuẫn trong câu trả lời.

4. **Audit & traceability:** mọi prompt/quyết định ghi vào `audit.md`; tiến độ theo dõi qua `aidlc-state.md` và các checkbox trong plan.

5. **Tính xác suất của LLM:** AWS lưu ý rằng chạy lại cùng problem statement sẽ cho câu hỏi & artifact **khác nhau** — đó là điều bình thường & mong muốn.

---

## Có thể chạy không cần IDE

Blog dùng Amazon Q Developer IDE plug-in, nhưng cũng có thể dùng **Kiro CLI** để build với AI-DLC **không cần setup thêm** — workflow y hệt, chỉ khác là tương tác qua command line.

Nguồn: [AWS DevOps Blog — Building with AI-DLC](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/) · [Kiro CLI](https://kiro.dev/cli/)

---

## Một hướng dẫn độc lập đáng đọc thêm
"From Intent to Software: Running the AI-DLC MCP Server in Kiro" — hướng dẫn thực hành chạy AI-DLC MCP Server, nối vào Kiro (hoặc bất kỳ MCP client nào) để chạy full Inception → Construction → Operations từ một dòng intent.

🔗 [AWS Builder Center](https://builder.aws.com/content/3EcgPNd9d2MMnKuRdrlInq7TTVt)

---

## Đọc tiếp
- Danh mục đầy đủ bài viết AWS → [`../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md`](../04-tai-nguyen-aws/01-bai-viet-chinh-thuc.md)
