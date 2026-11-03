# 語言包驗證紀錄

## 本次版本與基準

| 項目 | 結果 |
| --- | --- |
| 檢查日期 | 2026-11-04 |
| 語言包 | 1.1.7 → 1.1.8 |
| pokeldn | 0.54.0 → 0.56.1 |
| 原上游基準 | `df43d96f07dfbc94959830c894a6dd592efd9429` |
| 本次上游基準／檢查時最新 main | `70dfee44644808eb61932e75b4e02d9f7669e0c9` |
| 正式 Release | [v0.56.0](https://github.com/Decryptu/pokeldn/releases/tag/v0.56.0)，commit `3707414f81cdcdb2b056a4421c24e01e4bb80461` |
| Plugins API | 1.12，與上次相同 |
| 最低支援版本 | pokeldn 0.44.0，與上次相同 |
| 簽章指紋 | `ZP2X-THRM-26HS-XL2C` |

先以語言包遠端 `25f85f13cf3536abc5c2c33e69dd674ddf26ad22` 核對全部 39 個檔案的 Git blob SHA，再確認原基準英文 Git blob、SHA-256、中英文參照及已發布 1.1.7 封裝的 SHA-256 均一致，沒有修正既有基準紀錄。

檢查時正式 Release 仍為 0.56.0；main 已標為 0.56.1，且在 `bf05fb6fda09433b72760e5dbce524c83e443628` 的 0.56.1 版本提交之後，另有無線通訊測試及測試網路 beacon 修正。本次採最新 main 為翻譯基準，包含這些尚未納入正式 Release 的內容。AltStore 清單排除於語言包檢查範圍之外；本次 main 並非只有 AltStore 更新。下次同步時須再確認上述功能是否已正式發布。

## 增量檢查範圍

原基準至最新 main 共 12 筆提交、28 個變更檔案；排除 AltStore 清單後，依其餘 27 個檔案的差異檢查翻譯來源與必要相依內容。遠端 tree 與提交差異清單一致，沒有遺漏新增、刪除或改名。沿用 551 個雜湊一致的快取檔案，下載的 27 個變更檔案也均核對 Git blob SHA；沒有重新掃描未變更的遊戲模組。

- 主英文表新增 11 個鍵值，沒有刪除、改名或同鍵值原文變更，格式變數也沒有變更。新增內容為發射功率標題、自動與全功率選項、功率說明，以及無線通訊測試按鈕、確認視窗與操作步驟。變更 Python 檔案中的 239 個固定字串 `tr()` 呼叫，其鍵值與英文 fallback 均符合新版主字串表。
- `gui/views/boards.py` 新增 `[app] Radio test on {device}; the board may restart.`，顯示時經 `gui.localization.app_log()` 呼叫訊息替換；`templates.toml` 補入 1 筆範本並保留 `{device}`。原始紀錄仍保留英文。
- `pokeldn/ldn/esp32_radio_test.py` 的頻道、訊號強度、網路數量與判斷結果，以及 `boards.py` 的其它測試進度，均使用 `[radio test]` 紀錄。`app_log()` 不翻譯此類紀錄，單純新增訊息或範本無法生效，因此未加入無效對照。
- `bin/swsh_connect.py` 新增 `--ladder-refresh`：交換確認流程等待主機時，定期重送成對的 40040 訊息並推進時脈。實際 parser 預設為 1.0 秒，0 為停用。`swsh-join`、`swsh-lan`、`swsh-raid-join`、`swsh-lair-raid-join`、`swsh-lan-raid-join`、`swsh-lan-lair-join` 六個工具共用此入口，`help.toml` 補入 6 筆相同說明。
- 增量比對四個變更入口所對應的 12 個工具 parser，沒有其它選項原文、名稱、工具 ID 的刪除、更名或改寫。工具清單本身沒有變更。`messages.toml` 與 `terms.toml` 無需修改；神秘禮物來源沒有變更。
- `docs/hardware_esp32.md`、`docs/swsh_raid.md`、`docs/swsh_trade.md` 的 front matter 均未變，沒有新增、更名或調整父子分類的側邊欄標題。文件內文依既有範圍保留英文。
- Plugins API 仍為 1.12。外掛格式、載入、替換、簽章、Sources 解析及封裝工具均未變更；PKHeX 服務程式與依賴版本也未變更，因此未重做 PKHeX 語系與名稱資料檢查。
- 其餘更新為 ESP32 發射功率與連線重試、韌體 1.9.3、極巨大冒險場景匹配、傳說寶可夢交換等待、解密 PK8 匯入、錯誤紀錄、模擬器及相關測試；除上述文字外，不需調整語言包。

`docs/maintenance.md` 保持不變。README 與 `docs/translation.md` 僅同步版本、涵蓋數量、來源與顯示限制，不記錄本地測試過程。

## 字串與執行時檢查

已執行上游 `scripts/check_language_pack.py`，啟用 `POKELDN_PREVIEW=1`，另核對格式規格、轉換方式與執行時替換。

| 項目 | 結果 |
| --- | --- |
| 主字串 | 1,896 筆 |
| 主字串缺漏／多餘／變數不符 | 0/0/0 |
| 訊息對照 | 1,704 筆 |
| 工具專用說明 | 809 筆；多餘鍵值 0 |
| 動態範本 | 52 筆；格式變數全部一致 |
| 術語 | 114 筆 |
| 刻意保留英文、縮寫或純變數 | 35 筆 |
| 上游工具說明總數 | 2,902 筆 |
| 未另設工具專用對照 | 2,093 筆；可依既有規則回退至訊息對照或英文 |

- 1,896 筆主字串均通過格式變數、轉換方式、格式規格與執行時格式化檢查。既有 GTS 複數字尾例外 `{value2:.0}` 保持不變，另驗證 0、1、2、100 筆。
- 本次只有新增翻譯；既有主字串、工具說明及範本逐筆比對均未改寫。努力值維持「，共 510 點」，初訓家與持有紀錄用語不變，「紀念球捕捉 Bug／幻之寶可夢」保留全形斜線。
- 抽取上游實際 `BoardView._radio_test_confirm()`，以輕量 UI 替身執行，確認中文標題、四個步驟、取消與開始按鈕，及開始按鈕關閉視窗後觸發測試的回呼。未啟動 Flet GUI 或實際無線通訊測試。
- 執行實際發射功率下拉選單定義，確認「自動（預設）」「全功率（20 dBm）」及 15、11、8.5 dBm 選項，選取值與儲存的數值一一對應。
- 執行實際 `app_log()`，以 Windows、Linux、macOS 常見連接埠字串確認開始提示可翻譯，`{device}` 完整保留；`[radio test]` 訊息維持原文。
- 六筆新工具說明均與實際工具 ID、parser 原文、1.0 秒預設值及 `i18n.help_text()` 核對。

## 封裝、簽章與圖示

| 項目 | 結果 |
| --- | --- |
| 正式封裝 | `packages/pokeldn-zh-TW-1.1.8.pokeplugin` |
| 大小 | 154,018 位元組 |
| SHA-256 | `339d33da29fa106af0c5c9965242c14ddd8119e2bec304211fb6ee0012dac7b0` |
| Ed25519 簽章 | 通過；與 1.1.7 使用相同公鑰及指紋 |
| 檔案數 | 9；八個來源檔案加 `plugin.sig` |
| 圖示 | `icon.png`，96×96 PNG，與已發布的 1.1.7 相同 |
| 圖示 SHA-256 | `289967738e4ecdc0d4481da262101a1a1033b93e5ccca6c06b10217e20fc856b` |

使用原有 Ed25519 私鑰搭配本次上游 `scripts/pack_plugin.py` 封裝；打包前檢查原私鑰存在、類型與指紋，強制禁止自動建立新金鑰。封裝內只有 `plugin.toml`、五個翻譯 TOML、`LICENSE`、`icon.png` 與 `plugin.sig`；八個來源檔案均逐一比對一致。沒有 README、驗證報告、Python 程式碼或私鑰。

上游封裝讀取器與簽章驗證通過，竄改翻譯、圖示或版本號時均拒絕驗證。所有舊版封裝保留原始位元組。

`plugin.toml` 的 `icon = "icon.png"` 與 Sources 圖示設定正確；實際取得 [icon.png](https://raw.githubusercontent.com/jimmyorz/pokeldn-plugins-zhTW/main/language-pack/icon.png)，HTTP 200、Content-Type `image/png`，位元組與本地及封裝一致。Sources 解析器接受新版本、下載 URL、大小與 SHA-256；中英文參照及封裝雜湊均重新計算並核對。

## 安裝與新程序載入

- 在全新隔離資料目錄安裝 1.1.8，啟用語言包並儲存繁體中文選擇，通過。
- 在另一隔離目錄先安裝 1.1.7，再升級至 1.1.8，確認判定為更新、公鑰相同，保留啟用狀態與語言設定，通過。
- 兩種安裝均另開新 Python 程序，確認版本、Plugins API、`zh-TW` 語系、圖示與八個來源檔案一致；核對新增主字串及開始提示範本，通過。

## 限制與待確認事項

- 本次未執行完整 GUI、實際 PKHeX 服務、Switch／開發板硬體或手機 Wi-Fi 掃描。環境未安裝 .NET、Flet 與 esptool，Python 檢查使用現有依賴（PyCryptodome 4.1.0、Trio 0.34.0），未以全套上游鎖定版本啟動 App。
- 上游關於發射功率、ESP32-C3 連線及測試網路可見性的實機說明，不列為本語言包的測試成果。測試確認視窗與功率選單使用 UI 替身，只驗證翻譯與操作值，不代表已檢查畫面排版或實際無線通訊行為。
- `[radio test]` 結果與其他原始無線通訊紀錄仍為英文；需上游開放替換路徑後，語言包才能翻譯。
- 既有配信卡片標題、部分遭遇類型細節及原始紀錄等限制，仍依 `docs/translation.md` 所列範圍。
