# 語言包驗證紀錄

## 本次版本與基準

| 項目 | 結果 |
| --- | --- |
| 檢查日期 | 2026-11-06 |
| 語言包 | 1.1.8 → 1.1.9 |
| pokeldn | 0.56.1 → 0.57.0 |
| 原上游基準 | `70dfee44644808eb61932e75b4e02d9f7669e0c9` |
| 本次上游基準／檢查時最新 main | `77eb90d392736ca506e3c95183786a6c5f551b5b` |
| 正式 Release | [v0.57.0](https://github.com/Decryptu/pokeldn/releases/tag/v0.57.0)，與本次基準相同 |
| Plugins API | 1.12 → 1.13 |
| 最低支援版本 | pokeldn 0.44.0 → 0.57.0 |
| 簽章指紋 | `ZP2X-THRM-26HS-XL2C` |

先以語言包遠端 `6dce169d73750235582ba7a0502b0cb9a5648712` 核對全部 40 個檔案的 Git blob SHA，再確認原基準英文 Git blob、SHA-256、中英文參照、字串數及已發布 1.1.8 封裝的 SHA-256 均一致，沒有修正既有基準紀錄。

上一版已翻譯的無線通訊測試功能，已於上游 0.56.2 正式發布。本次正式 Release 與 main 相同，沒有尚未正式發布的翻譯差異。AltStore 清單仍排除於語言包檢查範圍之外。

## 增量檢查範圍

原基準至最新 main 共 22 筆提交、92 個變更檔案；遠端 tree 與提交差異清單一致。排除 AltStore 清單後，依變更檔案定位翻譯來源及必要相依內容。沿用 527 個雜湊一致的快取檔案，另外取得 41 個必要的變更檔案並核對 Git blob SHA，其餘依差異判斷是否涉及翻譯；沒有重新掃描未變更的遊戲模組。

- 主英文表位元組與原基準相同，沒有新增、刪除、改名、原文或格式變數變更。變更 Python 檔案中的 564 個固定字串 `tr()` 呼叫，其鍵值與英文 fallback 均符合主字串表。
- `pokeldn/app/catalog.py` 將無線模式「極巨大冒險（開房）」的步驟改為先在主機選擇邀請，再啟動 pokeldn 開房；鍵值與原文未變，既有中文會依新順序顯示。LAN 模式仍有自己的操作步驟。
- 增量比對六個變更入口所對應的 21 個工具 parser：新增 9 筆說明、改寫 10 筆，沒有選項或工具 ID 的刪除、更名。`--save-restore-emerald` 新增於兩個工具；`--lair-scene` 新增於七個工具；兩筆 `--rom-base` 增加 `none` 模式；八筆朱紫 `--record-set` 移除過時的 scratchpad 路徑。
- `help.toml` 新增 17 筆、更新 2 筆：包含新增選項的 9 筆，以及此次改寫、原先未收錄的 `--record-set` 8 筆；原有兩筆 `--rom-base` 補上新模式。其餘工具說明保持不變。
- `host_mg_app.py` 新增 `Writing the ROM` 進度標題。已追查 `progress.show()` → `SessionPanel.show_progress()` → `show_bar()` → `theme.section()`；標題直接顯示，沒有訊息替換路徑，因此未新增無效對照。
- 綠寶石存檔完成訊息經 `save_transfer.EMERALD_WRITTEN` 編碼後送往遊戲主機；新存檔／ROM 錯誤與結果也主要寫入原始執行紀錄，並未接入語言包替換。`messages.toml`、`templates.toml`、`terms.toml` 無需調整。
- 十份變更文件的 front matter 均未變，沒有新增或更名的遊戲側邊欄標題；`docs/rse_switch_build.md` 仍排除於 App 文件顯示範圍。文件內文依既有範圍保留英文。
- `services/pkhex/Program.cs` 調整提升等級、進化及團體戰首領的招式選擇與合法性處理。差異沒有新增介面原文或改動顯示語系／名稱查詢；`zh-TW` → `zh-Hant` 對應不變，PKHeX.Core 仍為 26.10.18。
- 其它更新包含 Intel Mac 發行檔、ROM 傳輸與綠寶石時鐘、存檔寫入、訓練家選取記憶、無線通訊測試的頻道切換、開發工具、範例路徑與測試資料清理。Android 的 esp-pylib 升至 1.2.1，未涉及語言包或 PKHeX 語系處理。

## Plugins API 相容性

1.13 新增 `run_launcher()`、`pokeldn.switch.cartridge.read()` 與正式列入支援範圍的 ROM 工具選項；沒有變更語言包 manifest 欄位、資源格式、載入、訊息／範本替換、簽章或 Sources 解析規則。`runner._execute()` 改名為 `execute()` 供新介面使用，本語言包不含執行程式碼，不依賴此私有名稱。

新封裝宣告 Plugins API 1.13，於 0.57.0 的讀取、相容性判斷及安裝驗證通過。另以 0.56.1 的實際 Plugins API 1.12 程式碼讀取新封裝，確認判定為需要更新 pokeldn 並拒絕載入。因此同步將 manifest、Sources、README 與參照紀錄更新為 API 1.13，最低支援版本提高至 0.57.0。

## 字串與執行時檢查

已執行上游 `scripts/check_language_pack.py`，啟用 `POKELDN_PREVIEW=1`，另核對格式規格、轉換方式與執行時替換。

| 項目 | 結果 |
| --- | --- |
| 主字串 | 1,896 筆 |
| 主字串缺漏／多餘／變數不符 | 0/0/0 |
| 訊息對照 | 1,704 筆 |
| 工具專用說明 | 826 筆；多餘鍵值 0 |
| 動態範本 | 52 筆；格式變數全部一致 |
| 術語 | 114 筆 |
| 刻意保留英文、縮寫或純變數 | 35 筆 |
| 上游工具說明總數 | 2,911 筆 |
| 未另設工具專用對照 | 2,085 筆；可依既有規則回退至訊息對照或英文 |

- 1,896 筆主字串均通過格式變數、轉換方式、格式規格與執行時格式化檢查。GTS 複數字尾例外 `{value2:.0}` 另驗證 0、1、2、100 筆。
- 本次 19 筆新增或更新的工具說明，均與實際工具 ID、parser 原文及 `i18n.help_text()` 核對；`--rom-base none` 可由新版 parser 正確解析。
- 重新載入實際工具清單，確認無線模式極巨大冒險的中文步驟順序與上游一致；LAN 模式的前置設定步驟及原順序保留。
- 抽取實際 ROM 進度回呼與畫面處理方法，以輕量替身執行，確認進度資料為 `items`、數值完整，標題仍原樣顯示 `Writing the ROM`。此檢查沒有傳輸 ROM 或啟動完整 GUI。
- 主字串、訊息、範本、術語及中英文快照均與 1.1.8 完全相同。努力值「510 點」、初訓家「設為」、持有紀錄用語及全形斜線規則均保留。

## 封裝、簽章與圖示

| 項目 | 結果 |
| --- | --- |
| 正式封裝 | `packages/pokeldn-zh-TW-1.1.9.pokeplugin` |
| 大小 | 154,629 位元組 |
| SHA-256 | `502a2140b8e1497b69e93ca3b736a54e04f14a7e2facba500832c356b8258856` |
| Ed25519 簽章 | 通過；與 1.1.8 使用相同公鑰及指紋 |
| 檔案數 | 9；八個來源檔案加 `plugin.sig` |
| 圖示 | `icon.png`，96×96 PNG，與 1.1.8 相同 |
| 圖示 SHA-256 | `289967738e4ecdc0d4481da262101a1a1033b93e5ccca6c06b10217e20fc856b` |

使用原有 Ed25519 私鑰搭配本次上游 `scripts/pack_plugin.py` 封裝；打包前確認原私鑰存在、類型與指紋，強制禁止自動建立新金鑰。封裝內只有 `plugin.toml`、五個翻譯 TOML、`LICENSE`、`icon.png` 與 `plugin.sig`；八個來源檔案均逐一比對一致。沒有 README、驗證報告、Python 程式碼或私鑰。

上游封裝讀取器與簽章驗證通過，竄改翻譯、圖示或版本號時均拒絕驗證。所有舊版封裝保留原始位元組。

`plugin.toml` 的 `icon = "icon.png"` 與 Sources 圖示設定正確；實際取得 [icon.png](https://raw.githubusercontent.com/jimmyorz/pokeldn-plugins-zhTW/main/language-pack/icon.png)，HTTP 200、Content-Type `image/png`，位元組與本地及封裝一致。Sources 解析器接受新版本、API、下載 URL、大小與 SHA-256；中英文參照及封裝雜湊均重新計算並核對。

## 安裝與新程序載入

- 在全新隔離資料目錄安裝 1.1.9，啟用語言包並儲存繁體中文選擇，通過。
- 在另一隔離目錄先安裝 1.1.8，再升級至 1.1.9，確認判定為更新、公鑰相同，保留啟用狀態與語言設定，通過。
- 兩種安裝均另開新 Python 程序，確認版本、Plugins API 1.13、`zh-TW` 語系、圖示與八個來源檔案一致；19 筆工具說明均正確替換，通過。

## 限制與待確認事項

- 本次未執行完整 GUI、實際 PKHeX 服務、Switch／開發板硬體、遊戲封裝讀取或 ROM／存檔傳輸。環境未安裝 .NET、Flet 與 esptool，Python 檢查使用現有依賴（PyCryptodome 4.1.0、Trio 0.34.0），未以全套上游鎖定版本啟動 App。
- PKHeX 的招式與合法性變更僅依來源差異檢查，未實際執行 .NET 合法性分析；上游的實機或模擬器結果不列為本語言包的測試成果。
- ROM 寫入進度標題、遊戲內綠寶石存檔完成訊息及原始執行紀錄仍有英文，需上游開放替換路徑後才能翻譯。其它既有限制見 `docs/translation.md`。

`docs/maintenance.md` 保持不變；README 與 `docs/translation.md` 不記錄本地測試過程。
