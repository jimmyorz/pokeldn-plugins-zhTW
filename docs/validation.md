# 語言包驗證紀錄

## 本次版本與基準

| 項目 | 結果 |
| --- | --- |
| 檢查日期 | 2026-11-01 |
| 語言包 | 1.1.4 → 1.1.5 |
| pokeldn | 0.49.0 → 0.50.0 |
| 原上游基準 | `ae685dc07ee705b24c02ebe254504fe261c89c34` |
| 本次上游基準／檢查時最新 main | `7902844ac33a415945d2f1b7867ad76d73306dc1` |
| 正式 Release | [v0.50.0](https://github.com/Decryptu/pokeldn/releases/tag/v0.50.0)，commit `809aa82c47b3765e2517075ac9e06146812bc0d5` |
| Plugins API | 1.12，與上次相同 |
| 最低支援版本 | pokeldn 0.44.0，與上次相同 |
| 簽章指紋 | `ZP2X-THRM-26HS-XL2C` |

本次先以語言包遠端 `61025ef4251c0b07a398e469da3e81a85a80bd77` 核對全部 36 個檔案，再確認原基準英文 Git blob、SHA-256、中英文參照、字串數與已發布封裝的 SHA-256 均一致，沒有自行修正基準紀錄。

0.50.0 正式版已包含初訓家替換與極巨團體戰頭目檢查。其後 main 尚有 ROM 傳輸、LZMA 傳輸及存檔還原批次處理等更新，並非只有 AltStore 清單；本次採最新 main 為基準，補上尚未包含於 0.50.0 正式版的 ROM 傳輸選項說明。主英文表與 0.50.0 正式版相同。下次同步須確認這些 main 功能是否已納入正式版本。

## 增量檢查範圍

依 `docs/maintenance.md`，以原基準至本次採用 commit 的差異為主：共 32 筆提交、51 個變更檔案，排除 AltStore 清單後檢查其餘 50 個檔案的差異與必要相依內容。未重新掃描未變更的遊戲模組。遠端 tree 與比較結果的變更清單一致；沿用的快取及下載的變更檔案均核對 Git blob SHA。

- 主字串新增 4 項；另有 1 項極巨團體戰頭目說明改寫並更換鍵值。就鍵值計算為新增 5 個、移除 1 個；沒有原鍵值保留但原文或格式變數改變的項目。
- `gui/views/pokemon.py`：補上「將我設為初訓家」、不合法原因及狀態提示外層，保留 `{value0}`。
- `pokeldn/app/catalog.py`、`pokeldn/app/command.py`：更新頭目種類、型態與超極巨化狀態的說明，補上沒有符合巢穴時的拒絕提示；一般與 LAN 開房工具均使用此檢查。工具 ID 與既有選項名稱未更改。
- `bin/frlg_mg_host.py`：新增 `--rom-transfer`、`--rom-live`、`--rom-base`、`--rom-no-boot` 四個選項。實際 parser 比對確認沒有既有說明移除或改寫；`frlg-gift` 與 `rse-gift` 共用此入口，故 `help.toml` 新增 8 筆對照。
- `pokeldn/frlg/gift/host_mg_app.py`、`rom_transfer.py`、`rom_lzma.py`、`save_transfer.py` 及相關神秘禮物模組：檢查新增動態輸出、傳輸狀態、拒絕原因與遊戲端訊息。這些文字透過紀錄、終端機或主機端訊息輸出，沒有進入語言包顯示邊界；沒有為無法生效的內容新增對照。既有 `messages.toml`、`templates.toml`、`terms.toml` 保持不變。
- 變更 Python 檔案中 771 個具固定字串的 `tr()` 呼叫，其鍵值與英文 fallback 均與新版主字串表一致。
- `docs/frlg_gift.md`、`docs/gui.md`、`docs/rse_switch_build.md`、`docs/swsh_protocol.md`、`docs/swsh_raid.md` 只更新內文，front matter 未變。遊戲文件側邊欄標題不需調整。
- Plugins API 仍為 1.12；外掛格式、載入與替換機制、簽章與 Sources 解析、打包工具均未變。`services/pkhex/Program.cs` 新增初訓家替換邏輯，但 `zh-TW` → `zh-Hant` 對應未變，PKHeX.Core 仍為 26.8.26。
- 其它更新包含 0.49.1 的零加密常數寶可夢判斷、團體戰異色保留、載入動畫與視窗關閉修正、底層傳輸與測試調整，沒有額外可由語言包替換的文字。

## 字串與執行時檢查

已執行上游 `scripts/check_language_pack.py`，啟用 `POKELDN_PREVIEW=1`，並另外驗證格式規格、轉換方式與實際格式化結果。

| 項目 | 結果 |
| --- | --- |
| 主字串 | 1,873 筆 |
| 主字串缺漏／多餘／變數不符 | 0/0/0 |
| 訊息對照 | 1,673 筆 |
| 工具專用說明 | 792 筆；多餘鍵值 0 |
| 動態範本 | 49 筆；格式變數全部一致 |
| 術語 | 114 筆 |
| 英文、縮寫或純變數刻意保留 | 35 筆 |
| 上游工具說明總數 | 2,885 筆 |
| 未另設工具專用對照 | 2,093 筆；可依既有規則回退至訊息對照或英文 |

1,873 筆主字串均已檢查格式變數、轉換方式、格式規格及執行時格式化。既有 GTS 複數字尾例外 `{value2:.0}` 保持不變，另測試 0、1、2、100 筆；沒有放寬其它格式要求。努力值總和仍顯示「，共 510 點」。新增中文沒有數字或英文字母兩側使用全形斜線的情況；`--rom-live` 說明中的 `{game code: [block, ...]}` 是原文 JSON 格式範例，保持字面內容。

新增 8 筆選項說明皆以實際 parser 內容及 `i18n.help_text()` 驗證。一般與 LAN 團體戰開房工具的頭目說明、巢穴拒絕提示、有效巢穴與活動頭目的略過條件均已檢查；巢穴查詢回傳值使用替身，不代表實際 PKHeX 或硬體團體戰測試。

以模擬 PKHeX 傳輸回覆執行實際 `DisplayService.import_file()`，確認初訓家欄位與 `display_language=zh-TW` 正確傳入。另獨立執行實際 `PokemonPicker.load()` 方法，以模擬控制項驗證初訓家提示、不合法原因及開關復原；未啟動 Flet GUI。

## 封裝、簽章與圖示

| 項目 | 結果 |
| --- | --- |
| 正式封裝 | `packages/pokeldn-zh-TW-1.1.5.pokeplugin` |
| 大小 | 151,905 位元組 |
| SHA-256 | `91f5b8d7a90b0fc0666a6f4fc2ed6298a131e8454e0bb5da1901cd78778c8684` |
| Ed25519 簽章 | 通過；與 1.1.4 使用相同公鑰及指紋 |
| 檔案數 | 9；八個來源檔案加 `plugin.sig` |
| 圖示 | `icon.png`，96×96 PNG，與已發布的 1.1.4 相同 |
| 圖示 SHA-256 | `289967738e4ecdc0d4481da262101a1a1033b93e5ccca6c06b10217e20fc856b` |

封裝內只有 `plugin.toml`、五個翻譯 TOML、`LICENSE`、`icon.png` 與 `plugin.sig`；八個來源檔案皆逐一與 `language-pack/` 核對一致。使用既有私鑰前已檢查檔案存在、Ed25519 類型及公開指紋，並強制禁止自動建立新金鑰。沒有加入 README、測試報告、Python 程式碼或私鑰。

上游封裝讀取器與簽章驗證均通過，竄改翻譯、圖示或版本號時均拒絕驗證。已發布的所有舊版封裝保留原始位元組。

`plugin.toml` 的 `icon = "icon.png"` 與 Sources 圖示 URL 均正確。實際取得 [icon.png](https://raw.githubusercontent.com/jimmyorz/pokeldn-plugins-zhTW/main/language-pack/icon.png)，HTTP 200、Content-Type `image/png`，內容與本地及封裝完全一致。Sources 解析器接受新版本、下載 URL、大小與 SHA-256；`reference/upstream.json` 的中英文及封裝雜湊均重新計算並核對。

## 安裝與新程序載入

- 在全新隔離資料目錄安裝 1.1.5，啟用語言包並儲存繁體中文選擇，通過。
- 在另一隔離目錄先安裝 1.1.4，再升級至 1.1.5，確認判定為更新、簽章公鑰相同，並保留啟用狀態與語言設定，通過。
- 兩種安裝均另開新 Python 程序，確認版本、Plugins API、`zh-TW` 語系、圖示路徑、八個來源檔案及補充翻譯資源均正確載入；抽查初訓家選項、ROM 傳輸說明與努力值單位，通過。

## 限制與待確認事項

- 本次未執行完整 GUI、Switch/開發板硬體、實際 PKHeX 服務或 ROM 傳輸功能測試，未宣稱通過完整上游測試套件。實際畫面的換行、欄位寬度與新功能操作仍可由維護者確認。
- 新的初訓家替換提示將 PKHeX 回傳的 `note` 直接代入 `{value0}`；`DisplayService` 沒有翻譯此頂層欄位，`i18n.t()` 也不會再次翻譯變數內容。已用實際方法確認「不再是異色」與「對你而言成為異色」兩種原因仍顯示英文；單純新增 `messages.toml` 或 `templates.toml` 對照無法修正。
- 遭遇選單版本名稱、遭遇地點語系與配信卡標題的既有顯示限制所涉及程式碼未變，本次未重做該功能測試；既有說明保留於 `docs/translation.md`。
- ROM 傳輸尚未包含於 0.50.0 正式版。本次只驗證其工具選項翻譯，不表示傳輸、續傳、啟動或 LZMA 路徑已通過實機測試。
