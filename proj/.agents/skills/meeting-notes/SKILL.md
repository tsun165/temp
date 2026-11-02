---
name: meeting-notes
description: Viết biên bản họp của đội vào docs/meetings/ và quy trình "chốt biên bản" (đưa việc cần làm vào docs/plan.md). Dùng khi ghi chú hoặc viết biên bản cuộc họp, mentor duty, góp ý khách mời, tạo file trong docs/meetings/, hoặc khi được bảo "chốt biên bản".
---

# Biên bản họp

- Định dạng (đường dẫn, mục cố định, dạng việc cần làm) ghi ở `docs/meetings/_index.md` — đọc file đó và làm
  đúng như vậy. Mỗi buổi một file `docs/meetings/YYYY/YYYY-MM-DD-<chu-de>.md`.
- Thêm biên bản mới thì thêm một dòng vào bảng trong `docs/meetings/_index.md` (mới nhất ở trên).
- Ghi đúng điều đã nói; ý của mentor / khách mời là tham khảo, gắn rõ là của ai. Không tự thêm quyết định.

## Chốt biên bản

Khi được bảo "chốt biên bản":

1. Liệt kê các dòng `- [ ]` ở mục "Việc cần làm" để Sơn duyệt từng việc (giữ, bỏ, sửa người / hạn).
2. Việc được duyệt → thêm vào `docs/plan.md`: việc của đồng đội vào "Việc giao đồng đội" (dạng
   `- [ ] **tên việc** (@Tên, hạn dd/mm). Xong khi …`), việc của Sơn vào mục "Việc". Repo **không dùng GitHub Issue**.
3. Ở biên bản, thay dòng đó bằng chỗ đã chuyển tới, vd. `→ plan.md "Việc giao đồng đội" (@Heargreaves1)`.
