# Mineradio Next Chat Handoff

更新时间：2026-07-09

## 新对话先执行

```powershell
cd E:\User Files\Study_Files\Github\Mineradio-fix_SMTC
git status --short --branch
git log --oneline -5 --decorate
Get-Content docs\PROJECT_MEMORY.md
Get-Content docs\HANDOFF_NEXT_CHAT.md
```

如涉及 3D 歌单架、安全重建、发布、安装包或旧备份取用，再读：

```powershell
Get-Content docs\3D_PLAYLIST_SHELF_MEMORY.md
Get-Content docs\SECURITY_REBUILD_2026-06-24.md
Get-Content CHANGELOG.md -TotalCount 80
Get-Content docs\RELEASE_NOTES_v1.1.4.md
```

## 当前状态

- 当前代码/Git 仓库：`E:\User Files\Study_Files\Github\Mineradio-fix_SMTC`
- 当前版本：`v1.1.4`
- GitHub 仓库：`https://github.com/Minecraftmc22/Mineradio-fix_SMTC`
- 当前发布策略：纯净安装版，从当前可信源码重新构建。
- 安装包样式继续沿用 `docs/INSTALLER_STYLE.md` 的中文极简黑白蓝格式。

## 本轮重点（v1.1.4）

### TTML 歌词与翻译支持
- 新增 Apple TTML 格式歌词解析器，支持逐词时间戳和翻译
- 歌词数据结构新增 `translation` 字段
- 支持网易云翻译歌词（tlyric）自动合并
- TTML 解析修复：空格处理（自动补全单词间缺失空格）

### 3D 歌词翻译显示
- 翻译歌词作为独立 3D mesh 渲染，带完整描边/发光效果
- 翻译位于主歌词下方，大小可调节
- 新增「翻译大小」滑块（设置 → 歌词 → 翻译）

### 桌面歌词翻译
- 桌面歌词新增翻译显示支持
- 新增「桌面歌词翻译」开关（设置 → 叠加效果）

### 歌词源设置完善
- 歌词来源信息显示（平台标签 + 时间轴类型标签）
- 新增「自动搜索歌词」开关
- 新增「优先 TTML 歌词」开关

### 自定义歌词 TTML 支持
- 自定义歌词弹窗新增格式选择：LRC / TTML / 自动检测

### 快捷键设置
- 新增「快捷键」设置区域（设置 → 快捷键）
- 支持配置：播放/暂停、上/下一首、歌词显示/隐藏、歌词放大/缩小、音量加/减、老板键

### 音量滚轮调节
- 鼠标悬停在音量按钮上时，使用滚轮调节音量

### 歌词描边修复
- 描边层现在正确跟随摄像头方向（使用 gl_FrontFacing 翻转 UV）

## 已知验证

- `git diff --check`：通过。
- `node --check server.js`：通过。
- 前端 `public/index.html` 内联脚本解析：通过。
- `public/desktop-lyrics.html` 内联脚本解析：通过。

## 发布注意

- 发布 `v1.1.4` 时上传 `dist/latest.yml` 用于软件内更新检测。
- Release 建议上传：
  - `dist/Better-Mineradio-1.1.4-Setup.exe`
  - `dist/Better-Mineradio-1.1.4-Setup.exe.blockmap`
- Release 正文使用 `docs/RELEASE_NOTES_v1.1.4.md`。
- 构建后需要更新 `dist/latest.yml` 中的 `sha512` 和 `size`。

## 不要做

- 不要使用 `git reset --hard` 或 `git checkout --` 回滚用户改动。
- 不要从旧 dist、旧 node_modules 或旧 packaged build 中恢复可执行产物。
