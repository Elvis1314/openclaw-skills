# OpenClaw Skills 同步

此仓库用于在多个 OpenClaw 实例之间同步技能包。

## 使用方法

### 在新机器上拉取

```bash
cd ~/.qclaw/workspace
git clone https://github.com/Elvis1314/openclaw-skills.git skills-temp
xcopy /E /I skills-temp\* skills\
rmdir /s /q skills-temp
```

### 同步更新

```bash
cd ~/.qclaw/workspace
git add skills/
git commit -m "sync skills"
git push
```
