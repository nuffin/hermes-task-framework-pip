# Changelog

## v1.4.0 (2026-09-06 10:56:36 CST)

> task-framework `b04fb4a` → `7758cb5`

### Release contents

- Add verified task synchronization safeguards, including task-scoped symlink
  validation, write locks, checkpoint synchronization, and corresponding tests.
- Isolate the on-demand interactive-window reference as a task-specific overlay.
- Refresh package documentation to use the canonical MEMORY.md and CHANGELOG.md
  task artifacts and the current wrapper/source repository paths.

## v1.1.0 (2026-08-06)

> task-framework `f9fc5b9` → `e046cdc`

### manage_task.py — 6 new lifecycle commands

- `create` — directory + hash + meta + templates + optional inbox move
- `accept` — create task from inbox file/dir (auto-derives name)
- `decline` — move inbox item to declined/ with DECLINED.md
- `status` — update ## Status line + auto index update
- `view` — print README.md + TASK.md (hash/dir/name resolution)
- `reset` — clear output/ + reset checkboxes + set status active (--no-hard for soft reset)
- All commands use cp+verify+rm for file moves (never raw mv)
- All commands auto-run update-index.py after changes

### Code quality fixes

- A1: replace 4 stale hardcoded paths with relative scripts/ paths
- A2: cmd_init .hermes-task.json schema 5→12 fields
- A3: unify index systems (reindex→update-index.py, list→direct scan)
- A4: task-runner.sh log path logs/→output/logs/
- B1: secrets.token_hex(3) replaces md5(random) across all 3 scripts
- B4: _safe_move rollback on failure
- B6: cmd_decline basename() prevents path injection
- C6: shared _resolve_tasks_root() in all 3 scripts (HERMES_TASKS_ROOT | DIR → config → fallback)

### Docs

- D1-D5: SKILL.md updates — trigger signal→script, inline python→task_ref.py refs

## v1.0.4 (2026-08-06)

> Unreleased bump (version gap)

## v1.0.1 (2026-07-18)

> task-framework `da9609f` → `dc6d900`

### extra_references_dir 支持

`task_create --skill <name>` 时，如果 skill 的 SKILL.md frontmatter 声明了 `extra_references_dir`，自动将该目录下所有文件复制到新任务目录。不覆盖已存在的同名文件。

使用方式：skill 在 `references/task-template/` 放置模板文件（搭配清单、pick 脚本、TASK 骨架），创建任务时自动部署。

### README 补全

完整 README 覆盖安装、目录结构、配置文件、skill 图集成。

## v1.0.0 (2026-06-05)

- 三层任务系统：methodology + container + tooling
- 任务目录结构（TASK.md / TASK_MEMORY.md / input/ / output/）
- 组合任务模式（software-dev / research / code-review）
- 跨 skill 组合任务 + phase 隔离目录
- 自动化执行器（run.py）
- `.hermes-task.json` 身份文件（named outputs + 依赖追踪）
- `manage_task.py` 生命周期管理
- 收件箱工作流（accept/decline）
- 根索引文件自动重建
