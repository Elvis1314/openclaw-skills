# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## Directory Notes

- **桌面（Public）**: `C:\Users\Public\Desktop`
  - 公共桌面文件夹，存放快捷方式等
  - **默认保存路径**：截图、文件等统一保存到此目录

## Browser

- **agent-browser**: 默认使用 `--headed` 模式（显示真实浏览器窗口），不再使用无头模式
  - 截图保存路径：`C:\Users\GDZT\Desktop`（`C:\Users\Public\Desktop` 无写入权限）

## Application Paths

- **众图通IBSD**: `D:\Program File\zhongtu\众图通IBSD.exe`
  - Electron 应用，启动后需从系统托盘访问

## ESP32 开发环境

- **Python**: `C:\Program Files\Python311\python.exe`
- **esptool**: `python -m esptool` (v5.2.0)
- **WebView2**: 已安装 (v14.40.33810.00)
