# Ticket Monitor (Release Distribution)

Ticket Monitor 的公開發行版本發布庫。

## 下載方式 (Downloads)

請至 [Releases 頁面](../../releases) 下載最新編譯好的 Windows 執行檔：

- **`ticket_monitor.exe`**：Windows 獨立執行檔（免安裝直接執行）
- **`ticket_monitor_windows_x64.zip`**：完整壓縮包（內含執行檔、設定範本與快速啟動腳本）

---

## 功能簡介

- **單一程式・一體化網頁操作**：啟動後自動開啟瀏覽器控制台，所有參數配置、即時監控狀態皆在網頁中完成。
- **高頻低負載背景輪詢**：免登入會員、CPU 與記憶體佔用極低。
- **釋票多重通知**：
  - Discord Webhook 即時卡片通知（附帶直達購票連結）
  - 本機音效與瀏覽器音效雙重提醒
  - 網頁頂部即時醒目橫幅
- **熱載入支援**：監控中修改設定即時生效，不需重啟程式。
- **連動搶票**：支援與搶票工具自動喚醒連動。

---

## 快速使用

1. 至 [Releases](../../releases) 下載 `ticket_monitor_windows_x64.zip` 並解壓縮。
2. 執行 `ticket_monitor.exe`。
3. 程式啟動後會自動開啟瀏覽器（預設為 `http://127.0.0.1:5000`）。
4. 在網頁控制台中填入目標活動代碼或網址，點擊「儲存設定」後「開始監控」即可。
