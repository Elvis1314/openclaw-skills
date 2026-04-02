# OpenClaw Skills 同步

此仓库用于在多个 OpenClaw 实例之间同步技能包及用户环境配置。

## 同步内容

| 路径 | 说明 |
|------|------|
| `skills/` | 所有已安装的技能包（Skill） |
| `TOOLS.md` | 本地工具配置（CLI路径、目录别名等） |
| `USER.md` | 用户偏好（桌面路径、项目路径等） |
| `SOUL.md` / `AGENTS.md` / `MEMORY.md` | Agent 行为与记忆配置 |

## 使用方法

### 在新机器上拉取

```bash
cd ~/.qclaw/workspace
git clone https://github.com/Elvis1314/openclaw-skills.git _sync_tmp
# 复制 skills 及配置文件
Copy-Item -Path "_sync_tmp\skills\*" -Destination "skills\" -Recurse -Force
Copy-Item -Path "_sync_tmp\TOOLS.md" -Destination "." -Force
Copy-Item -Path "_sync_tmp\USER.md" -Destination "." -Force
# 清理
Remove-Item -Recurse -Force "_sync_tmp"
```

### 同步更新（当前机器 → 云端）

```bash
cd ~/.qclaw/workspace
git add skills/ TOOLS.md USER.md
git commit -m "描述本次变更"
git push origin main
```

### 拉取更新（云端 → 当前机器）

```bash
cd ~/.qclaw/workspace
git pull origin main
```

## 注意事项

- `openclaw.json` 不纳入 Git（包含 API Key 等敏感信息），存储在本地
- 技能配置中的凭据通过 `skills.entries.*.env` 管理，不随仓库同步
- 同步前请确认 `skills/` 不含大型二进制文件（建议每个 Skill 不超过 5MB）
