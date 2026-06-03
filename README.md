# TIK — 導師後台（Phase 1 MVP）

補習社導師 AI 一體化管理平台：個人化對話、批量備課、拍照批改、進度追蹤。

## 快速開始

### 本地預覽

```bash
cd "/Users/yanicek/Desktop/2026 Project/STP_TIK"
python3 -m http.server 8765
```

瀏覽器開啟：

- http://localhost:8765/
- http://localhost:8765/tik-app.html

### 手機（同一 Wi‑Fi）

```bash
ipconfig getifaddr en0   # 例如 192.168.1.145
```

手機瀏覽器：`http://<你的IP>:8765/`

## Vercel 部署

本 repo 已含 [vercel.json](vercel.json)，根路徑會導向應用。連接 GitHub 後 push `main` 即自動部署。

## API Key（BYOK）

1. 首次開啟可 **跳過（Demo 模式）** 或輸入 Anthropic API Key
2. Key 僅存於瀏覽器 `localStorage`，不會上傳至 TIK 伺服器
3. **安全提醒：** 公開部署時，任何能開啟網頁的人都能在 DevTools 看到 Key。正式上線請改用 Phase 2 後端代理。

## 資料儲存（Phase 1）

| Key | 內容 |
|-----|------|
| `tik_api_key` | API Key |
| `tik_mem_{id}` | 學生 AI 記憶 |
| `tik_chat_{id}` | 對話紀錄 |
| `tik_practice_{id}` | 批改／備課紀錄 |

側邊欄 **匯出資料 / 匯入資料** 可備份 JSON，避免瀏覽器清除資料。

## 功能模組

- **班級總覽** — 10 位樣本學生、功能捷徑卡片
- **個人對話** — AI 對話、**學生檔案（Memory + Soul）**、批改、**Demo PDF 下載**
- **批量備課** — 並行生成 + **Demo PDF 下載**
- **進度追蹤** — 趨勢、批改紀錄、家長月報
- **功能導覽** — Demo 說明與 5 分鐘腳本
- **底部固定列** — 全裝置五個 Tab 切換模組

詳見 [DEMO-GUIDE.md](DEMO-GUIDE.md)（Memory / Soul / Skills 教學）。

## Demo 試卷 PDF

將你的示範 PDF 放到：

```
assets/demo-worksheet.pdf
```

App 內 **⬇ PDF** / **Demo PDF** 會下載此檔（檔名含學生姓名）。說明見 [assets/README.md](assets/README.md)。

## 資料三層

| 層級 | 說明 | 儲存 |
|------|------|------|
| **Memory** | 學科：課本、弱點、答對率 | `tik_mem_{id}` |
| **Soul** | 整人：興趣、目標、導師備註 | `tik_soul_{id}` |
| **Skills** | 全站 AI 規則（出題/安全） | 內嵌 `TIK_SKILLS` |

## 技術棧

- 單檔 HTML + CSS + Vanilla JS
- Claude API `claude-sonnet-4-20250514`
- 部署：Vercel 靜態託管

## Phase 2（規劃中）

React + Vite + Supabase + 導師登入 + API 後端代理。

## 授權

專案演示用途 — 詳見團隊內部協議。
