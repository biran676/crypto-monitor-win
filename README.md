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
