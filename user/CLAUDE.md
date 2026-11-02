# CLAUDE.md

## Về tôi
- Họ tên: Đỗ Thái Sơn
- Nghệ danh làm việc: tysondoforwork (chỉ dùng khi tôi chỉ đạo)
- Email làm việc: sondoforwork@gmail.com
- GitHub: tsun165
- Quan tâm: nghiên cứu AI, kiến trúc AI

## Trình độ (để giải thích đúng mức)
- Thành thạo kiến trúc ML/DL (ResNet, Transformer, attention), hiểu ý nghĩa toán học; thành thạo PyTorch.
- LLM/agent: hiểu concept và biết vibe code; không cần giải thích lại kiến thức nền ML/DL.
- Đang học Docker: khi đụng tới Docker thì giải thích kỹ hơn.

## Giao tiếp
- Trò chuyện với tôi bằng tiếng Việt; giữ nguyên thuật ngữ kỹ thuật tiếng Anh.
- Tài liệu (docs, biên bản họp) viết bằng tiếng Việt; code và tên biến bằng tiếng Anh.
- Giải thích trực quan, dễ hiểu, gần gũi; concept mới thì kèm một ví dụ đơn giản.
- Tôi sẽ tự review kỹ kết quả. Với việc liên quan giao tiếp giữa các đầu mối
  (gửi email, tin nhắn, đăng bài, trả lời thay tôi), luôn hỏi tôi trước khi gửi.

## Môi trường
- Windows, Python 3.12, có GPU và có thể dùng Colab.
- Python chỉ dùng mamba env (miniforge3): không venv/virtualenv/`uv venv`/Poetry/Pipenv,
  không cài vào `base`, task lẻ dùng env `temp`, chạy bằng `mamba run -n <env> <lệnh>`.
  Quy tắc chọn/tạo env và cài package: `~/.claude/rules/python-env.md`.
- LLM API key nằm ở C:\Users\sondo\Desktop\study\LLM_API_Key.txt.
  Chỉ để code đọc lúc chạy; không tự mở, in, hay ghi nội dung file này vào
  log, code, commit hoặc câu trả lời.

## Git
- Commit message: ngắn gọn, súc tích, ưu tiên tiếng Anh.
- Tên nhánh: feat/<ten_nhanh_snake_case>
- Sau khi PR đã merge: xóa nhánh ở remote và local (`gh pr merge --delete-branch`
  làm cả hai; nhánh local xóa bằng `git branch -d`, không dùng `-D`),
  rồi `git fetch --prune` để dọn nhánh remote đã mất.

## Quyền
- Tự làm không cần hỏi: đọc file, chạy test, git status/diff/log.
- Luôn hỏi trước: xóa file, git push, đọc .env hoặc file chứa API key.
- Luôn hỏi trước: tạo, sửa, đóng GitHub issue; thêm, sửa, xóa item hoặc đổi field
  trên GitHub Project (người khác trong repo/project sẽ thấy hoặc nhận thông báo).

## Quản lý dự án (chi tiết nằm trong skill)
- Giao việc, GitHub issue/Project → skill `github-tasks`.
- Ghi chú cuộc họp, "chốt biên bản" → skill `meeting-notes`.
- Task research (thị trường, số liệu, khuôn dạng dữ liệu thực tế, so sánh sản phẩm…):
  mặc định không tự web search, soạn prompt cho Gemini theo skill `research-prompt`.
  Chỉ tự research khi tôi bảo rõ.
- Sơ đồ: dùng Mermaid nhúng trong file .md; sơ đồ dùng lại nhiều lần lưu ở `docs/diagrams/`.

## Nguyên tắc làm việc (tóm tắt)
- Nghĩ trước khi làm: nêu giả định, có nhiều cách hiểu thì trình bày, chưa rõ thì hỏi.
- Đơn giản trước tiên; chỉ sửa đúng chỗ cần sửa; xác định tiêu chí thành công rồi kiểm chứng.
- Bản đầy đủ: `~/.claude/rules/coding-principles.md` (tự nạp khi đọc/sửa file code).
