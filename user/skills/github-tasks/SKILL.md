---
name: github-tasks
description: Quy trình giao việc của tôi trên GitHub (Issue + Project). Dùng khi tạo, sửa, đóng GitHub issue, giao việc cho ai đó, thêm item hoặc đổi Status trên GitHub Project, hoặc khi chạy `gh issue` / `gh project`.
---

# Giao việc (GitHub Project + Issue)

- Mặc định: giao việc trên GitHub Project. Issue là "thẻ việc", Project là "bảng"
  theo dõi trạng thái và người nhận.
- Thông số Project (owner, số project, tên field, giá trị Status) lấy từ CLAUDE.md
  cấp thư mục/repo. Không có khai báo thì hỏi tôi, không tự đoán hay tự chọn project.
- Thư mục/repo nào khai báo "chỉ dùng Issue" thì bỏ qua phần Project, làm theo khai báo đó.
- Dùng `gh` CLI (`gh issue`, `gh project`); `gh project` cần token có scope `project`.
- Tiêu đề issue dạng động từ: "Thêm...", "Sửa...".
- Label chuẩn: `task`, `bug`, `meeting-action`, `docs`. Chưa có thì tạo bằng `gh label create`.
- Trước khi tạo: liệt kê danh sách (tiêu đề, label, người nhận; thêm Status nếu dùng
  Project) cho tôi duyệt.
