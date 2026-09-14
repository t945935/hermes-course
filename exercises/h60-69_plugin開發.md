# H60-H69 實作紀錄：Plugin 開發

> 完成日期：2026-09-14 ｜ 狀態：生態系與結構實測完成；撰寫自製 plugin 可續作

## 插拔介面地圖（官方「我要加什麼 → 讀哪份」）
| 想加的 | 介面 |
|---|---|
| 工具/hook/斜線指令/技能/CLI 子指令 | 本指南（plugin.yaml + register(ctx)）|
| 新模型/推理後端 | model-provider-plugin |
| 新訊息平台 | adding-platform-adapters |
| 新記憶後端（mem0 等） | memory-provider-plugin |
| 圖/影片生成、web 搜尋、雲端瀏覽器 | 各自 provider plugin |
| 金鑰管理後端 | secret-source-plugin |
| 外部工具（filesystem/github…） | 直接走 MCP（config.yaml）|

## plugin 結構（實測 spotify bundled 範例）
```text
plugins/spotify/
├── plugin.yaml      # manifest：name/version/description/author/kind/provides_tools
├── __init__.py      # register(ctx) 掛載點
├── client.py        # API 客戶端
└── tools.py         # 工具實作
```
plugin.yaml 範例：
```yaml
name: spotify
version: 1.0.0
description: "Native Spotify integration — 7 tools (playback, devices, queue…)"
author: NousResearch
kind: backend
provides_tools: [spotify_playback, spotify_devices, spotify_queue, spotify_search, …]
```
- 認證掛 `hermes auth spotify`（PKCE OAuth），tools gate 在 auth.json 的 providers 區塊

## 管理指令（hermes plugins，17 子指令）
`install / search / browse / validate / update / remove / list / enable / disable / capabilities / doctor / compat / pack / show / info`
- 安裝來源：精選目錄 / Git URL / owner/repo
- validate = 目錄放入 catalog 的 CI 門檻
- 實測精選目錄：herdr-auto-recon、hermes-plugin-chrome、hermes-plugin-netbox（5 tools, 2 env）…

## Agent Plugins v1（portable 套件）
```text
my-portable-plugin/
├── plugin.json      # v1.0.0 相容規範
├── skills/summarize/SKILL.md
└── mcp.json         # stdio / streamable-http MCP
```
- `hermes plugins install owner/repo --no-enable` → `enable` 後生效
- ⚠️ 預設安裝後 disabled；裝完需明確 enable
- 技能具 namespace：`agent-plugin-<slug>-<hash>`（防碰撞）
- ⚠️ 不要放憑證進 mcp.json（env 不是秘密儲存）

## 安全提示
- portable 套件無 sandbox/信任模型，啟用 = 全信任（與原生 plugin 同級）
- 第三方產品整合的 plugin 走「獨立 repo」發布（不併入核心樹）
- 宣傳管道：Nous Research Discord #plugins-skills-and-skins

## 驗收自評
✅ 說得出 plugin 系統的 5+ 插拔介面與對應文件
✅ 看懂 plugin.yaml + register(ctx) 結構
✅ 會用 plugins list/browse/search/install/enable/disable
✅ 知道 portable Agent Plugins v1 的組成與安全注意事項
🔶 實作一顆 plugin（tools/hooks）→ 列入期末專題選項