---
paths:
  - "**/*.{py,ipynb,js,jsx,mjs,cjs,ts,tsx,vue,svelte,go,java,kt,rs,c,cc,cpp,h,hpp,cs,rb,php,swift,sh,ps1,sql,html,css,scss}"
---

# Nguyên tắc làm việc

Các nguyên tắc giúp tránh những lỗi thường gặp của LLM khi viết code. Kết hợp với hướng dẫn riêng của từng dự án khi cần.

**Đánh đổi:** Các nguyên tắc này ưu tiên cẩn thận hơn tốc độ. Với việc đơn giản, tự cân nhắc.

## 1. Nghĩ trước khi code

**Không tự giả định. Không giấu chỗ chưa hiểu. Nêu rõ các đánh đổi.**

Trước khi làm:
- Nêu rõ các giả định. Nếu không chắc, hãy hỏi.
- Nếu có nhiều cách hiểu, trình bày tất cả, đừng âm thầm chọn một.
- Nếu có cách đơn giản hơn, hãy nói ra. Phản biện khi cần.
- Nếu có gì chưa rõ, dừng lại. Chỉ ra chỗ chưa rõ. Hỏi.

## 2. Đơn giản trước tiên

**Code tối thiểu đủ giải quyết vấn đề. Không làm thừa "phòng khi cần".**

- Không thêm tính năng ngoài yêu cầu.
- Không tạo abstraction cho code chỉ dùng một lần.
- Không thêm "tính linh hoạt" hay "khả năng cấu hình" khi không được yêu cầu.
- Không xử lý lỗi cho những tình huống không thể xảy ra.
- Nếu viết 200 dòng mà có thể chỉ cần 50, hãy viết lại.

Tự hỏi: "Một senior engineer có thấy cái này phức tạp quá không?" Nếu có, đơn giản hóa.

## 3. Sửa đúng chỗ cần sửa

**Chỉ động vào những gì bắt buộc. Chỉ dọn phần do mình gây ra.**

Khi sửa code có sẵn:
- Không "cải thiện" code, comment hay format ở xung quanh.
- Không refactor thứ đang chạy tốt.
- Giữ đúng style hiện có, kể cả khi bạn thích cách khác.
- Nếu thấy dead code không liên quan, hãy báo ra, đừng xóa.

Khi thay đổi của bạn tạo ra phần thừa:
- Xóa import/biến/hàm mà chính thay đổi của BẠN làm cho không còn dùng.
- Không xóa dead code có từ trước, trừ khi được yêu cầu.

Phép thử: mỗi dòng thay đổi phải truy ngược được về yêu cầu của người dùng.

## 4. Làm việc theo mục tiêu

**Xác định tiêu chí thành công. Lặp lại cho đến khi kiểm chứng xong.**

Biến việc cần làm thành mục tiêu kiểm chứng được:
- "Thêm validation" → "Viết test cho input không hợp lệ, rồi làm cho test qua"
- "Sửa bug" → "Viết test tái hiện bug, rồi làm cho test qua"
- "Refactor X" → "Đảm bảo test qua cả trước và sau"

Với việc nhiều bước, nêu kế hoạch ngắn:
1. [Bước] → kiểm tra: [cách kiểm tra]
2. [Bước] → kiểm tra: [cách kiểm tra]
3. [Bước] → kiểm tra: [cách kiểm tra]

Tiêu chí rõ ràng giúp tự làm tiếp mà không cần hỏi liên tục. Tiêu chí mơ hồ ("làm cho chạy được") thì phải hỏi lại liên tục.
