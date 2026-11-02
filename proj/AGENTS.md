# AGENTS.md

Luật chung cho mọi coding agent (Claude Code, Codex, Gemini CLI/Antigravity) và mọi thành viên —
không giả định ai có sẵn skill hay rule ở máy riêng. Nội dung chỉ viết **một bản**; mỗi tool chỉ có
lớp vỏ mỏng để nạp nó:

| Loại | Bản dùng chung | Vỏ theo tool |
|---|---|---|
| Luật cứng (luôn nạp, giữ ngắn) | file này | Codex đọc thẳng; `CLAUDE.md`, `GEMINI.md` chỉ nhúng file này |
| Skill (nạp khi cần, bảng dưới) | `.agents/skills/<tên>/SKILL.md` | Codex, Gemini/Antigravity đọc thẳng; Claude qua bản trỏ `.claude/skills/<tên>/SKILL.md` |
| Rule riêng Antigravity | `.agents/rules/` (frontmatter `trigger`) | — |
| Hook ghi AI log, quyền | — | `.claude/settings.json`, `.codex/`, `.gemini/settings.json`, `.agents/hooks.json` |

Thêm hay sửa skill: sửa ở `.agents/skills/`, chép frontmatter y hệt sang bản trỏ của Claude, thêm dòng vào
bảng dưới — `tests/test_agent_skills.py` báo lỗi khi hai bản lệch nhau.

| Skill | Dùng khi |
|---|---|
| `code-style` | Viết, sửa, review code; trước khi báo xong / mở PR có code (nguyên tắc làm việc, chuẩn BTC, môi trường) |
| `meeting-notes` | Viết biên bản họp, "chốt biên bản" (đưa việc vào `docs/plan.md`) |
| `research-prompt` | Việc cần research: soạn prompt cho Gemini, chuẩn hoá kết quả vào `docs/research/` |
| `design-taste-frontend` | Làm landing / trang public (tasteskill v2, Leonxlnx/taste-skill, MIT); màn ứng dụng theo wireframe |
| `langfuse` | Việc đụng tới Langfuse: trace, cost, dataset, docs Langfuse |

## Dự án

- Sản phẩm: **AutoLead** — chấm điểm lead có giải thích cho tư vấn viên đại lý ô tô
  (đề VFO2O-02) — xem `docs/spec/`.
- Bối cảnh: AI20K Build Phase Cohort 4, repo đội P-102. Đội 4 người (Sơn, Phong, Huy, Long),
  Sơn duyệt; bản rebuild của Sơn đã thay `main` (PR #50).
- Stack: Python · FastAPI · LangGraph · Postgres · pytest · ruff. Frontend React + Vite +
  Tailwind ở `frontend/`. CI chạy Python 3.11.
- Python local: mỗi người env riêng (máy Sơn: mamba env `VinAI`) — chi tiết ở skill `code-style`.

## Lệnh

- Chạy: `uvicorn src.main:app --reload --port 8000` (Swagger: `/docs`)
- Test: `pytest tests/` · Lint: `ruff check src/ tests/` · Format: `ruff format src/ tests/`
- Eval agent (LLM thật, DB local): `python -m eval.run` → `eval/results/` — xem `docs/testing.md` mục 2.
- DB local: `docker compose up -d db` (cổng 5433) → `alembic upgrade head` → mock:
  `python -m src.db.seed` (xoá sạch rồi nạp lại). Test DB tự skip khi không có Postgres.
- Frontend: `npm --prefix frontend run dev` (cổng 5173) · build: `npm --prefix frontend run build`.
- Deploy (chỉ khi Sơn bảo): merge `develop` → `main` trước, rồi build từ `main` đã pull mới nhất. Có migration mới thì
  migrate Supabase trước backend: `python -m src.db.push_remote --migrate` (giữ dữ liệu). Backend `docker build` + `docker push tsun165/c4-app-p102-api:latest` rồi Sơn
  bấm deploy trên Render; frontend `npx vercel deploy --prod --cwd frontend`. Chi tiết: `ARCHITECTURE.md` mục Deploy.

## Bản đồ tài liệu

| Cần gì | Đọc ở |
|---|---|
| Bản đồ toàn bộ `docs/` | `docs/README.md` |
| Sản phẩm làm gì, cho ai, acceptance criteria | `docs/spec/` (bắt đầu từ `README.md`) |
| Kiến trúc, sơ đồ, data model | `ARCHITECTURE.md` |
| Giao diện (wireframe, căn cứ làm frontend) | `docs/diagrams/ui-wireframe.md` |
| API contract (danh sách endpoint) | `docs/api-contract.md` |
| Vì sao chọn như vậy | `docs/decisions/` (mục lục ở `README.md`) |
| Đang làm gì, việc tiếp theo, mốc | `docs/plan.md` |
| Lịch sử việc đã làm theo ngày (ai làm gì) | `WORKLOG.md` |
| Chiến lược test và eval | `docs/testing.md` |
| Research nền (tham khảo, không phải căn cứ chuẩn) | `docs/research/` |
| Đề xuất của đồng đội trước khi code (chờ Sơn duyệt) | `docs/proposals/` (khung + quy trình ở `README.md`) |
| Barem chấm điểm (chỉ admin; mock v0) | `config/scoring/` |
| Biên bản họp | `docs/meetings/YYYY/YYYY-MM-DD-<chu-de>.md` |
| Hồ sơ Gate của đội trước rebuild (lưu trữ, không phải căn cứ) | `gates/` |
| Lịch, deliverables, rubric, sách BTC | `btc-reference/` (bắt đầu từ `README.md`) |

## Luật cứng

- Quy trình nhánh (Git Flow rút gọn):
  - `develop` là nhánh làm việc chung. Bắt đầu việc mới (code hay docs) thì agent **chủ
    động** tạo nhánh `feat/<snake_case>` (hoặc `fix/<snake_case>`) từ `develop` đã pull
    mới nhất, không đợi Sơn nhắc; xong mở PR vào `develop`.
  - `main` luôn sát nhất với sản phẩm đang deploy: chỉ nhận PR từ `develop` ngay trước
    hoặc ngay sau khi deploy (Gate, demo). Deploy luôn từ `main`. Không commit hay mở PR
    thẳng vào `main` từ nhánh khác.
  - Merge PR bằng merge commit, không squash. Merge xong xoá nhánh (remote + local).
  - Giữ lâu dài: `main`, `develop`, `gate1`.
  - Push nhánh và mở PR thoải mái. Không đẩy tag khi Sơn chưa bảo.
- **Chỉ đọc, không sửa hay xoá:**
  - `btc-reference/` — tài liệu BTC (`.claude/settings.json` chặn cả việc thêm file). Muốn
    thêm file ghi ý mới thì hỏi Sơn, Sơn tự thêm.
  - `docs/guide/` — sách bản cũ của template, giữ nguyên. Không dùng làm nguồn
    tham khảo; sách bản mới ở `btc-reference/khung-chung/technical-book/`.
  - `.github/`, `LICENSE`, `SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`
    — file quản trị của template. Chỉ sửa khi Sơn yêu cầu rõ.
- Không đọc hay in `.env`. Secret chỉ đọc qua `src/config.py`.
- Spec trước code: việc chưa có trong `docs/spec/` hoặc `docs/plan.md` thì hỏi,
  không tự thêm.
- Việc giao dạng **đề xuất** (`docs/plan.md` ghi file ở `docs/proposals/`): chỉ viết file đề xuất
  theo `docs/proposals/README.md`, không code, không sửa spec/ADR/barem. Code chỉ sau khi Sơn chốt.
- **Eval do Sơn phụ trách** (16/10 Sơn nhận lại quyền Eval đã cấp cho Phong ngày 13/10): `eval/`, golden dataset,
  so model, `docs/testing.md` mục 2. Việc eval không cần viết đề xuất trước; các luật cứng khác vẫn áp dụng.
- Lõi chấm điểm là điểm yếu business logic đã biết (`docs/spec/open-questions.md`). Barem
  nằm ở `config/scoring/` — không tự đặt hay đổi trọng số, ngưỡng, *k* khi chưa có căn
  cứ; đề xuất kèm nguồn rồi hỏi Sơn.
- Viết hay sửa code: theo skill `code-style`. Báo xong chỉ khi `ruff check` sạch và `pytest` pass.
- Link chết đã biết: `btc-reference/README.md` trỏ tới `docs/planning/`,
  `AGENTS.md → phan-vai.md` của đội cũ — không tồn tại trên nhánh này, bỏ qua.

## Quy ước

- Commit: `type(scope): mô tả` bằng tiếng Anh, ngắn. Nhánh: xem "Quy trình
  nhánh" ở Luật cứng.
- Tài liệu viết tiếng Việt; code và tên biến tiếng Anh. Sơ đồ dùng Mermaid.
- Mỗi loại thông tin chỉ ở một file. File dài quá ~300 dòng mới tách thành thư mục.
- Mỗi thư mục trong `docs/` có `README.md` (hoặc `_index.md`, như `docs/meetings/`) làm bản
  đồ; thêm hay đổi file thì cập nhật file bản đồ đó.
- Đầu mỗi phiên làm việc: đọc mục "Trạng thái hiện tại" trong `docs/plan.md`.
- Đầu mỗi phiên: đọc mục "Việc giao đồng đội" trong `docs/plan.md`, xác định người đang làm theo
  bảng ở đó; còn việc chưa tick của người đó thì nhắc ngay ở câu trả lời đầu tiên.
- Cuối mỗi phiên làm việc: **thay** nội dung mục "Trạng thái hiện tại" trong `docs/plan.md`
  (≤ 5 dòng: đang giữa việc gì · bước tiếp · blocker), không nối thêm; lịch sử ghi ở
  `WORKLOG.md` (bảng theo ngày).

## Mức tự chủ (chỉ cho Codex và Gemini/Antigravity; Claude bỏ qua mục này)

- Lựa chọn kỹ thuật có default hợp lý (tên biến, cấu trúc file, thư viện đã có
  trong stack, cách viết test) thì tự chọn và ghi giả định vào câu trả lời, không
  hỏi. Gom mọi câu hỏi còn lại vào một lần, kèm phương án đề xuất.
- Chỉ dừng để hỏi khi: xoá file, git push/PR/tag, thao tác ngoài workspace, đụng
  barem `config/scoring/`, việc ngoài spec/plan, hoặc yêu cầu mơ hồ thực sự.
  Các luật cứng ở trên luôn được ưu tiên hơn mục này.
