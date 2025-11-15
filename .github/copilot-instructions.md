**Repository Overview**
- **Purpose:**: 该仓库名为 `YSM`，主要以资源目录组织（例如 `九夏/animations`、`九夏/avatar`、`九夏/models`、`九夏/textures` 等），看起来是一个以模型/资源为主的项目，而非典型的编译型代码库。
- **Big Picture:**: Treat the repo as a content/artifacts workspace (models, animations, textures, sounds, GUI assets) rather than an app with a build pipeline. Avoid invasive refactors to binary/resource files; prefer adding scripts or docs.

**What to look for first**
- **Key dirs:**: Reference `九夏/animations`, `九夏/avatar`, `九夏/controller`, `九夏/functions`, `九夏/lang`, `九夏/models`, `九夏/sounds`, `九夏/textures`, `九夏/gui` when reasoning about functionality or assets.
- **Top-level docs:**: Only `README.md` exists at repo root; it contains minimal info. Ask the maintainer for missing build/test commands before assuming workflows.

**Agent Goals & Constraints**
- **Non-destructive edits:**: Do not modify binary asset files (images, model binaries, audio) unless explicitly requested. Prefer adding new text files, scripts, or documentation.
- **When unsure, ask:**: If a change could affect downstream tools or user workflows (renaming assets, changing paths), prompt the maintainer rather than guessing.

**Common Tasks & How to Approach Them**
- **Adding a new model or texture:**: Place art assets under the appropriate `九夏/*` subdirectory and update any manifest or README entries. If there is no manifest, add `docs/` or `README-assets.md` explaining intended paths.
- **Implementing small automation (recommended):**: If asked to add build/test helpers, create a top-level script folder (e.g. `scripts/`) and include plain `README.md` usage examples. Do not assume a specific runtime (Node/Python) unless repository contains `package.json`, `requirements.txt` or similar.
- **Code changes in `functions/` or `controller/`:**: These directories probably contain logic (scripts or small utilities). Keep changes minimal, add unit tests only if a test harness is present or the user requests one.

**Patterns & Conventions Observed**
- **Resource-first structure:**: The repo groups by resource type (animations, models, textures, sounds). Follow that structure when adding or relocating files.
- **Naming / path sensitivity:**: Asset consumers often use relative paths; preserve filenames and directory structure to avoid breaking references.

**Search / Investigation Examples**
- **Find usage of an asset:**: Search for occurrences of the asset filename across the repo: ``grep -R "<asset-name>" .`` (or use the editor’s global search). Example targets: any file under ``九夏/textures`` or ``九夏/models``.
- **Verify docs before changing assets:**: Check `README.md` at repo root and any per-folder README before modifying assets.

**Developer Workflows (discoverable / verified)**
- **Build / Test:**: No build scripts or test harness were discovered in the repository root or in top-level folders at time of inspection. Do not invent build commands — ask the maintainer for CI/build/test steps.
- **Debugging:**: For logic inside `九夏/functions` or `controller`, run locally using the language/runtime the files target. If file types are unclear, ask which runtime is expected.

**PR / Commit Guidelines for Agents**
- **Small, focused PRs:**: Keep PRs limited to a single purpose (docs, small script, or tiny bugfix).
- **Explain asset changes:**: When committing asset modifications, include a short `README` update describing why the asset changed and how to validate it.

**Files to Reference for Examples**
- **`README.md`**: repository root (very short—use as initial context). Use it as the canonical place to add usage or workflow details.
- **`九夏/` subfolders**: Inspect folder names to infer responsibilities; reference them explicitly in suggestions and PR descriptions.

**When You Can’t Proceed**
- If a requested change affects runtime behavior (e.g., a controller script) but there is no indicated runtime or test, stop and ask:
  - Which runtime should be used? (Node/Python/other)
  - How should I validate changes locally?

**Example assistant prompts (when asking the user)**
- "这个改动会修改 `九夏/models/<name>` 下的模型文件 — 你希望我也更新使用该模型的引用或只替换文件？"
- "仓库内没有构建或测试说明。我可以：1) 添加一个 `scripts/` 目录并放入示例脚本，或 2) 先询问你偏好的运行时。你选哪种？"

**Final notes**
- Keep updates minimal and well-documented. This repository appears to be asset-centric; prioritize clarity and non-destructive edits. When in doubt, ask the maintainer for missing operational details.
