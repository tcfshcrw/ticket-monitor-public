# Ticket Monitor (TicketPlus 統一監票控制中心)

TicketPlus 高頻、免登入、低資源消耗的背景票況輪詢與即時通知工具，並支援與 [Tickets Hunter](https://github.com/bouob/tickets_hunter) 連動自動喚醒搶票。

---

## 📥 下載方式 (Downloads)

請至本專案的 [**Releases 釋出頁面**](../../releases) 下載最新編譯好的 Windows 檔案：

- **`ticket_monitor.exe`**：單一獨立執行檔（免安裝 Python、免設定環境，直接雙擊執行）
- **`ticket_monitor_windows_x64.zip`**：完整壓縮包（內含主程式、設定檔範本與說明文件）

---

## 🌟 功能特色

- **一體化網頁控制台 (Web Dashboard)**：啟動後自動開啟瀏覽器 (`http://127.0.0.1:16899`)，所有監控開關、活動解析、關鍵字篩選、輪詢間隔設定皆在網頁視覺化操作。
- **免登入高頻輪詢**：直接讀取售票系統 API / S3 狀態，不開瀏覽器模擬、CPU 與記憶體佔用極低。
- **多重釋票通知**：
  - **Discord Webhook**：即時發送帶有場次資訊、票區票價與直達購票連結的卡片通知。
  - **雙重音效提醒**：本機喇叭（Windows Ding-Dong）與瀏覽器音效同步警示。
  - **即時橫幅與 Log**：黑窗命令列與網頁端同步即時顯示釋票資訊。
- **動態熱載入 (Hot-Reload)**：監票運作中隨時修改設定並儲存，立即套用，無須重啟。
- **自動喚醒 Tickets Hunter**：釋票瞬間自動解除搶票程式暫停，實現「平時低負載監票、釋票瞬間極速搶票」！

---

## 🚀 快速上手使用步驟

### 步驟 1：下載並啟動
1. 至 [Releases](../../releases) 下載 `ticket_monitor_windows_x64.zip` 並解壓縮（或直接下載 `ticket_monitor.exe`）。
2. 雙擊執行 `ticket_monitor.exe`。
3. 程式啟動後會開啟命令列黑窗輸出日誌，並自動在瀏覽器開啟控制台：`http://127.0.0.1:16899`。

### 步驟 2：設定監控目標
1. **活動網址**：在網頁控制台中貼上 TicketPlus 的活動網址（例如 `https://ticketplus.com.tw/activity/...`），可點擊「解析並預覽活動資料」確認場次與票區。
2. **關鍵字篩選 (可選)**：
   - **場次關鍵字**：如 `2026/05/20`。
   - **票區關鍵字**：如 `特A區`, `2800`。
   - **排除關鍵字**：如 `身障`, `視線遮蔽`。
3. **通知設定**：填入 Discord Webhook 網址（可點擊「發送測試訊息」測試）。
4. 點擊「**儲存並套用設定**」，並確認上方狀態為「**監控中**」。

---

## ⚡ 與 Tickets Hunter 連動機制與最佳實戰設定

本工具能與主流搶票輔助程式 [Tickets Hunter](https://github.com/bouob/tickets_hunter) 深度整合，達成**平時無損監聽、釋票瞬間無縫接軌搶票**的最高效益。

### 1. 連動運作機制原理
- **Tickets Hunter 的待命機制**：Tickets Hunter 啟動後，當目錄下存在暫停標記檔 `MAXBOT_INT28_IDLE.txt`（或在搶票介面按下暫停）時，程式會暫停頁面刷新動作，處於待機狀態。
- **Ticket Monitor 的自動喚醒**：平時由 Ticket Monitor 以極低消耗在背景高速輪詢。一旦偵測到符合條件的票券釋出，Ticket Monitor 會在毫秒級瞬間**自動刪除暫停標記檔**，Tickets Hunter 即可立即解除暫停，直接展開自動搶票流程！

---

### 2. 實戰推薦設定步驟

#### 第一步：設定 Tickets Hunter（搶票端）
1. 開啟 Tickets Hunter，先登入好售票系統會員帳號。
2. 設定好預計搶購的日期、票區偏好順序、張數與驗證碼選項。
3. **將重新整理頻率／秒數調整為最低**（極限刷新速度）。
4. 進入待命狀態並**按下「暫停」**（Pause），此時 Tickets Hunter 目錄下會產生 `MAXBOT_INT28_IDLE.txt` 檔案，搶票程式停止請求並待命。

#### 第二步：設定 Ticket Monitor（監票端）
1. 在 Ticket Monitor 控制台網頁中，找到「**Tickets Hunter 連動設定**」區域：
   - 勾選 **「啟用自動喚醒 Tickets Hunter」**。
   - **程式路徑**：
     - 若 Ticket Monitor 與 Tickets Hunter 放在同一資料夾或鄰近目錄，系統會**自動偵測**並顯示綠色「已就緒」徽章。
     - 若放在其他自訂目錄，請手動填入 Tickets Hunter 所在資料夾路徑（包含 `settings.exe` 或 `nodriver_tixcraft.exe` 的目錄）。
2. 確認路徑下方顯示為綠色「已就緒 / 已偵測到實例」。
3. 點擊「**儲存並套用設定**」。

#### 第三步：坐等釋票
- 平時電腦保持安靜運行，不會因為瀏覽器頻繁狂刷而導致帳號被鎖、驗證碼跳出或記憶體飆高。
- 只要有人退票或主辦單位釋票：
  1. Ticket Monitor 立即觸發本機與網頁音效，並發送 Discord Webhook 通知。
  2. 同步在 0.1 秒內喚醒 Tickets Hunter。
  3. Tickets Hunter 立即以最快刷新率開始填表送單，搶先搶下釋出的門票！

---

## ⚙️ 進階命令列參數

若從命令提示字元 (CMD / PowerShell) 啟動 `ticket_monitor.exe`，支援以下參數：

```bash
ticket_monitor.exe --port 16899 --no-browser --no-autostart
```

| 參數 | 說明 |
| :--- | :--- |
| `--port <埠號>` | 指定 Web 控制台的 HTTP 埠號（預設為 `16899`） |
| `--no-browser` | 啟動後不要自動開啟瀏覽器視窗 |
| `--no-autostart` | 啟動後維持待機狀態，不自動展開背景監票（需手動至網頁按開始） |
| `--config <路徑>` | 指定自訂設定檔路徑（預設為同目錄之 `config_monitor.json`） |

---

## ⚠️ 免責聲明 (Disclaimer)

1. 本專案僅供程式開發、個人自動化技術交流與系統測試使用。
2. 請勿使用本工具進行任何侵犯售票系統服務條款、惡意高頻濫發請求或不當圖利之行為。
3. 使用者應自行承擔因使用本軟體所產生之任何責任與風險。
