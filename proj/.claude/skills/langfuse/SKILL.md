---
name: langfuse
description: >-
  Interact with Langfuse and access its documentation: tracing, monitoring, creating datasets, running experiments, and evaluating AI applications. Use only when the task involves Langfuse itself: (1) query or modify Langfuse data (traces, costs, datasets, scores), (2) look up Langfuse documentation, concepts, integration guides, a feature or SDK usage, or (3) change how this repo sends traces or costs to Langfuse (LLM gateway callback, LANGFUSE_* settings). Do not use for general eval or prompt work that does not touch Langfuse.
allowed-tools:
  - WebFetch(domain:langfuse.com)
  - Bash(curl *langfuse.com/*)
  - Bash(npx langfuse-cli api __schema *)
  - Bash(npx langfuse-cli api * --help *)
  - Bash(npx langfuse-cli api * list *)
  - Bash(npx langfuse-cli api * get *)
  - Bash(bunx langfuse-cli api __schema *)
  - Bash(bunx langfuse-cli api * --help *)
  - Bash(bunx langfuse-cli api * list *)
  - Bash(bunx langfuse-cli api * get *)
---

Bản trỏ cho Claude Code. Nội dung thật (dùng chung với Codex, Gemini) ở
`.agents/skills/langfuse/SKILL.md` — đọc file đó và làm theo; đường dẫn `references/…`
trong đó tính từ `.agents/skills/langfuse/`.
