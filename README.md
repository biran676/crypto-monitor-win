# Crypto Monitor for Windows (OKX)

Windows 桌面即時幣價監測工具（Tkinter + OKX WebSocket）。

## 主要功能

- 即時價格、漲跌顯示（可選 `OKX 24h` / `香港08:00` 算法）
- 主視窗 + 迷你視窗（可透明、可縮放、可吸附）
- 迷你 K 線（1m/5m/15m/1H，支援縮放與左右拖拉）
- 24h 與 5m 漲跌提示（視窗震動、提示、音效、靜音）
- Telegram 提醒與定時報價
- 多幣持倉與總收益（金額 + 百分比）

## 系統需求

- Windows 10/11
- Python 3.9+
- 網路可連線至 OKX 公開 API

## 快速安裝

1. 下載或解壓專案
2. 雙擊 `install.bat`
3. 雙擊 `run.bat` 啟動（不顯示黑色 console）

## 手動安裝（可選）

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

## 基本設定

可複製範例檔：

```powershell
copy .env.example .env
```

` .env ` 主要欄位：

- `OKX_WS_URL`：WebSocket URL（預設已填）
- `OKX_INST_IDS`：預設訂閱交易對（逗號分隔）
- `RECONNECT_SECONDS`：斷線重連秒數

## Telegram 接入教學

### 1) 建立 Telegram Bot

1. 在 Telegram 搜尋 `@BotFather`
2. 輸入 `/newbot`
3. 按提示設定 Bot 名稱與使用者名稱（需以 `bot` 結尾）
4. 建立後會拿到 `Bot Token`（格式像 `123456:ABC...`）

請妥善保存 token，不要公開。

### 2) 取得 Chat ID

有兩種常見方式：

- **個人聊天**
  1. 對你的 Bot 發一則訊息（例如 `hi`）
  2. 在瀏覽器打開：
     `https://api.telegram.org/bot<你的BotToken>/getUpdates`
  3. 在回傳 JSON 裡找到 `chat.id`（通常是正整數）

- **群組聊天**
  1. 把 Bot 加入目標群組，並先在群組發一則訊息
  2. 同樣打開 `getUpdates` URL
  3. 找到群組的 `chat.id`（通常是負數，例如 `-100...`）

### 3) 在程式內填入 Telegram 設定

1. 啟動程式後，打開「設置」
2. 找到 Telegram 區塊，填入：
   - `Bot Token`
   - `Chat ID`
3. 勾選 `Telegram 升跌提醒`
4. 點擊 `儲存 Telegram`
5. 點擊 `測試發送`，確認是否可收到訊息

### 4) 設定定時報價（可選）

在「設置」視窗可設定：

- `定時報價`：數值（例如 `5`）
- 單位：`sec` / `min` / `hour`
- `報價模式`：
  - `interval`：每幾秒/分/小時發一次
  - `hourly_minute`：每小時固定第幾分
  - `at_time`：每天固定時間（`HH:MM`，可多個逗號分隔）

### 5) 常見問題排查

- 收不到訊息：
  - 先確認你已對 Bot（或群組）發過訊息
  - 檢查 `Bot Token` 與 `Chat ID` 是否有多空白
  - 群組模式請確認 Bot 有發言權限
- `getUpdates` 沒資料：
  - 先手動對 Bot 發訊息，再重新整理
- 避免憑證外洩：
  - 不要把含 token 的設定檔上傳到公開倉庫

## Telegram 定時報價模式

在「設置」視窗可選：

- `interval`：每幾秒/分/小時發一次
- `hourly_minute`：每小時固定第幾分（例如 `0`=每整點、`30`=每點30分）
- `at_time`：每天固定時間（例如 `08:00,12:00,20:00`）

## 注意事項

- 請勿把 `.env`、`settings.json` 上傳到公開倉庫
- 若遷移資料夾後 `.venv` 壞掉，重新執行 `install.bat` 即可

## 打包 EXE（可選）

```powershell
.\.venv\Scripts\python.exe -m pip install pyinstaller
.\.venv\Scripts\pyinstaller --noconsole --onefile .\app.py
```

產物位於 `dist\app.exe`。

