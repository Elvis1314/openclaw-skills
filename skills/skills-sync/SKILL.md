---
name: skills-sync
description: |
  OpenClaw 技能 Git 同步工具。在多个 OpenClaw 实例之间通过 GitHub 仓库同步技能包。
  触发场景：用户提到"同步技能"、"skills sync"、"同步到另一台机器"、"拉取技能"、"推送技能"、"Git 同步技能"、"技能同步"时使用此技能。
  覆盖操作：首次拉取、增量更新、推送本地变更、查看同步状态。
metadata:
  {
    "openclaw": {
      "emoji": "🔄",
      "requires": { "bins": ["git"] },
      "always": true
    }
  }
---

# 技能同步 (skills-sync)

通过 GitHub 私有仓库在多个 OpenClaw 实例间同步技能包。

## 仓库信息

- **仓库**：`https://github.com/Elvis1314/openclaw-skills.git`
- **分支**：`main`
- **同步内容**：`skills/` 目录下的所有技能包

## 工作区路径

- Windows 默认工作区：`~\.qclaw\workspace`
- macOS/Linux 默认工作区：`~/.openclaw/workspace`

判断方法：查找存在 `skills/` 目录的路径即可。

## 操作流程

### 1. 首次拉取（目标机器）

在目标机器上执行：

```powershell
# 进入工作区
cd ~/.qclaw/workspace

# 克隆仓库到临时目录
git clone https://github.com/Elvis1314/openclaw-skills.git _skills_sync

# 复制 skills 到工作区（跳过已存在的文件，避免覆盖）
Copy-Item -Path "_skills_sync\skills\*" -Destination "skills\" -Recurse -Force

# 清理
Remove-Item -Recurse -Force "_skills_sync"

# 初始化 Git（如果工作区还没有 .git）
git init; git checkout -b main
git remote add origin https://github.com/Elvis1314/openclaw-skills.git
```

### 2. 推送本地变更（源机器）

当本地新增或修改了技能后：

```powershell
cd ~/.qclaw/workspace
git add skills/
git commit -m "sync skills"
git push origin main
```

如果推送被拒绝（远程有更新）：

```powershell
git pull --rebase origin main
git push origin main
```

### 3. 拉取更新（目标机器）

```powershell
cd ~/.qclaw/workspace
git pull origin main
```

如果有冲突（本地修改了与远程相同的技能）：

```powershell
# 查看冲突文件
git diff --name-only --diff-filter=U

# 用远程版本覆盖本地（推荐，以最新推送的为准）
git checkout --theirs skills/<冲突技能>/
git add skills/<冲突技能>/
git commit -m "resolve conflict: use remote"
```

### 4. 查看同步状态

```powershell
cd ~/.qclaw/workspace

# 查看本地有哪些技能
Get-ChildItem skills\ -Directory | Select-Object Name

# 查看未提交的变更
git status --short skills/

# 查看与远程的差异
git fetch origin
git log HEAD..origin/main --oneline
```

## 注意事项

- **不要**同步 `~/.openclaw/skills/`（内置技能覆盖目录），只同步工作区的 `skills/`
- 推送前确认不含敏感信息（API Key 等应放在 `openclaw.json` 的 `skills.entries.*.env` 中，不会被 Git 追踪）
- `.gitignore` 已配置忽略非 skills 目录的文件
