---
name: code-style
description: Nguyên tắc làm việc và chuẩn viết code của repo AutoLead (Python backend, React frontend, test, môi trường). Dùng khi viết, sửa, refactor hoặc review code trong src/, tests/, eval/, scripts/, frontend/, và trước khi báo xong hay mở PR có code.
---

# Viết code trong repo AutoLead

Áp dụng cho mọi người và mọi agent (Claude, Codex, Gemini/Antigravity). Luật cứng ở `AGENTS.md` luôn thắng
skill này. Nguồn chuẩn của BTC: `btc-reference/khung-chung/technical-book/` (`code-style/python.md`,
`anti-patterns/common-mistakes.md`, `testing/writing-tests.md`) — skill này tóm tắt và ghi chỗ repo làm khác.

## 1. Nguyên tắc làm việc

Ưu tiên cẩn thận hơn tốc độ; việc đơn giản thì tự cân nhắc.

1. **Nghĩ trước khi code.** Nêu rõ giả định. Có nhiều cách hiểu thì trình bày, đừng âm thầm chọn một. Có cách
   đơn giản hơn thì nói ra. Chưa rõ thì dừng lại và hỏi.
2. **Đơn giản trước tiên.** Code tối thiểu đủ giải quyết vấn đề: không thêm tính năng ngoài yêu cầu, không
   abstraction cho code dùng một lần, không "cấu hình được" khi không ai cần, không xử lý lỗi cho tình huống không
   thể xảy ra. Viết 200 dòng mà 50 dòng đủ thì viết lại.
3. **Sửa đúng chỗ cần sửa.** Không "cải thiện" code, comment, format xung quanh; không refactor thứ đang chạy;
   giữ style sẵn có. Thấy dead code không liên quan thì báo, đừng xoá. Chỉ dọn import / biến / hàm mà chính thay
   đổi của mình làm thừa. Phép thử: mỗi dòng đổi phải truy ngược được về yêu cầu.
4. **Làm theo mục tiêu kiểm chứng được.** "Sửa bug" → viết test tái hiện rồi làm cho qua; "refactor" → test qua
   cả trước và sau. Việc nhiều bước thì nêu kế hoạch ngắn, mỗi bước kèm cách kiểm.

## 2. Python (backend, eval, scripts)

- Python **3.11** (CI và `ruff.toml` `target-version = "py311"`). Lint + format bằng ruff: `ruff check src/ tests/`,
  `ruff format src/ tests/` (luật E, F, I, N, W, UP; dòng ≤ 120). CI chạy ruff, đỏ là không merge.
- Theo BTC (`code-style/python.md`), áp dụng cho code mới và code đang sửa; code cũ không tự refactor (mục 1.3):
  - Type hint đầy đủ, kể cả kiểu trả về; docstring cho hàm public.
  - Hàm ngắn (BTC: ≤ 30 dòng, ≤ 3 tham số — nhiều hơn thì gom vào Pydantic model / dataclass).
  - Tên: file, hàm `snake_case`; class `PascalCase`; hằng `UPPER_SNAKE`. Import: stdlib → thư viện → `src.` (ruff `I`).
  - Bắt exception cụ thể, không `except:` trống, không nuốt lỗi im lặng.
  - Không viết cứng secret: đọc qua `src/config.py` (không đọc, không in `.env`).
- Nghiệp vụ nằm ở backend: LLM chỉ chọn tool / trích tín hiệu; luật kiểm, ghi DB, chấm điểm là code (ADR-032).
  Barem ở `config/scoring/`, không tự đổi trọng số / ngưỡng / *k*.

## 3. Test

- `pytest tests/`, cấu trúc thư mục test theo `src/`. Sửa bug → thêm test tái hiện. Gọi LLM trong test thì dùng
  fake model (xem `tests/test_agents/`), không gọi API thật.
- Test cần DB tự skip khi không có Postgres; muốn chạy đủ: `docker compose up -d db` → `alembic upgrade head`.
- BTC tối thiểu: ≥ 3 test API, ≥ 2 test agent, mọi test pass trước khi push — repo đã vượt, giữ nguyên.
- Eval agent bằng LLM thật (`python -m eval.run`) do Sơn phụ trách (`docs/testing.md` mục 2, `AGENTS.md`).

## 4. Môi trường

- Mỗi người một môi trường riêng (conda/mamba env hoặc venv), không cài vào Python hệ thống hay env `base`.
  Cài: `pip install -r requirements.txt`. Thêm thư viện thì thêm vào `requirements.txt` trong cùng PR.
- Máy của Sơn: mamba env `VinAI`, chạy bằng `mamba run -n VinAI <lệnh>`.
- Frontend dùng **npm** (repo có `frontend/package-lock.json`, không đổi sang trình quản lý khác): `npm --prefix
  frontend install`, `npm --prefix frontend run dev`.

## 5. Frontend (`frontend/`)

- React + Vite + Tailwind. Giao diện theo `docs/diagrams/ui-wireframe.md` (căn cứ chuẩn); icon dùng `lucide-react`.
- Gọi API qua `frontend/src/api.js`; lớp mock (`mockData.js`, `VITE_USE_MOCK`) chỉ để chạy không cần backend.
- Landing / trang public có thể dùng skill `design-taste-frontend`; màn ứng dụng thì theo wireframe.

## 6. Trước khi báo xong hoặc mở PR

- `ruff check` sạch và `pytest` pass (luật cứng). Frontend đổi thì `npm --prefix frontend run build` chạy được.
- PR nhỏ, một PR một việc (mentor: < ~400 dòng nếu được), mô tả có "đã đổi gì" + "đã kiểm thế nào". Repo không
  dùng GitHub Issue nên không ghi "Closes #n"; việc theo dõi ở `docs/plan.md`.
- Đổi hành vi thì cập nhật docs liên quan (spec, API contract, wireframe, ADR) trong cùng PR — mỗi loại thông tin
  chỉ ở một file.
