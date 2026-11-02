---
paths:
  - "**/*.{py,ipynb}"
  - "**/pyproject.toml"
  - "**/requirements*.txt"
  - "**/environment*.{yml,yaml}"
  - "**/uv.lock"
  - "**/setup.{py,cfg}"
---

# Môi trường Python (mamba)
- Mọi môi trường Python là mamba env. Không tạo venv/virtualenv/`uv venv`, không dùng
  Poetry/Pipenv. Repo có `pyproject.toml`/`uv.lock`/`requirements.txt` vẫn cài vào mamba env.
- `base` để trống (chỉ có conda/mamba): không cài package vào `base`.
- Task nhỏ lẻ không thuộc repo nào (script nhanh, thử nghiệm) → dùng env `temp`;
  thiếu thư viện thì cài thêm vào `temp`.
- Chọn env cho repo/thư mục, theo thứ tự:
  1. CLAUDE.md cấp repo/thư mục có khai báo env → dùng env đó.
  2. Không có khai báo → xem `mamba env list` rồi đề xuất cho tôi duyệt:
     - Dùng lại env có sẵn nếu cùng mục đích và không phải nâng/hạ phiên bản package
       đã có trong env (nhất là torch, numpy, transformers).
     - Ngược lại thì tạo env mới.
  3. Chốt xong thì ghi tên env vào CLAUDE.md của repo (mục "Môi trường") để lần sau dùng luôn.
- Tạo env mới:
  - Tên: tên repo/thư mục dạng snake_case, chữ thường, không dấu
    (vd. `Smart-Air-Mobile-App` → `smart_air_mobile_app`).
  - Python 3.12 trừ khi repo yêu cầu khác: `mamba create -n <ten> -c conda-forge python=3.12`.
- Cài package: ưu tiên `mamba install -n <env> -c conda-forge ...`; conda-forge không có
  thì mới dùng `mamba run -n <env> python -m pip install ...`. Package đã cài bằng pip thì
  nâng/hạ cũng bằng pip, không cài chồng bằng mamba (tránh 2 bản cùng lúc như `myenv`).
- Chạy lệnh trong env bằng `mamba run -n <env> <lệnh>` (shell của Claude không giữ `activate`).
