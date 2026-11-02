---
name: research-prompt
description: Soạn prompt research tự đủ ngữ cảnh để người chạy bằng Gemini (Deep Research) thay vì agent tự web search, rồi chuẩn hoá kết quả vào docs/research/. Dùng khi xuất hiện việc research (thị trường, số liệu, khuôn dạng dữ liệu thực tế, so sánh sản phẩm, pháp lý…) hoặc khi đưa kết quả research vào repo.
---

# Research

- Mặc định **không tự web search**: soạn prompt để người dùng chạy bằng Gemini. Chỉ tự research khi người dùng
  bảo rõ.
- Prompt tự đủ ngữ cảnh (dán nguyên file là chạy được): bối cảnh AutoLead, câu hỏi cụ thể, luật chống bịa (mỗi ý
  có URL cụ thể, không chỉ trang chủ; gắn nhãn **[Có nguồn]** / **[Suy luận]**), cấu trúc kết quả mong muốn.
- Lưu prompt ở `docs/research/YYYY-MM-DD-<chu-de>-prompt.md`; kết quả người dùng chạy xong lưu cạnh đó
  `…-result.md` (hoặc `.json`). Thêm dòng vào bảng `docs/research/README.md`: nội dung, nguồn sinh, **độ tin cậy**
  (đánh giá thật: link có mở được không, số có căn cứ không).
- Research là tham khảo, không phải căn cứ chuẩn: điều được chốt từ research ghi thành ADR ở `docs/decisions/`.
