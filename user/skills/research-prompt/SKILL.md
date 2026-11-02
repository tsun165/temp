---
name: research-prompt
description: Soạn prompt research cho Gemini thay vì tự web search. Dùng khi xuất hiện task research (thị trường, số liệu, khuôn dạng dữ liệu thực tế, so sánh sản phẩm…) hoặc khi chuẩn hoá kết quả research vào docs/research/.
---

# Research

- Khi xuất hiện task research: mặc định không tự web search mà tự động soạn prompt
  cho Gemini để tôi chạy.
- Prompt tự đủ ngữ cảnh, có câu hỏi cụ thể, luật chống bịa (nguồn URL cụ thể, nhãn
  [Có nguồn] / [Suy luận]) và cấu trúc kết quả. Lưu ở `docs/research/YYYY-MM-DD-<chu-de>-prompt.md`
  trong repo đang mở; kết quả tôi chạy xong lưu cạnh đó (`…-result.md`), Claude chuẩn hoá vào repo.
- Chỉ tự research khi tôi bảo rõ.
