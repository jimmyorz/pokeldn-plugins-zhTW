# pokeldn 繁體中文（台灣）語言包

[pokeldn](https://github.com/Decryptu/pokeldn) 是一款開源工具，可透過 ESP32 開發板與 Nintendo Switch/Switch 2 上的寶可夢遊戲進行本地無線通訊，支援寶可夢交換、團體戰等功能。

本儲存庫為 pokeldn 提供符合台灣用語與寶可夢中文社群習慣的繁體中文介面，專門維護語言包、翻譯來源及更新參照。

如果發現翻譯錯誤、用語不自然，或有更合適的譯法，歡迎提出 [Issue](https://github.com/jimmyorz/pokeldn-plugins-zhTW/issues) 或 [PR](https://github.com/jimmyorz/pokeldn-plugins-zhTW/pulls)，協助改進翻譯。回報時請盡量附上相關畫面或原文字串，方便確認與調整。

## 下載與安裝

可加入 Sources，在 pokeldn 內取得後續更新，也可選擇手動安裝。

### 透過 Sources 安裝（推薦）

加入來源後，可直接在 pokeldn 內安裝與更新語言包，不必每次回到本頁下載檔案。

來源網址（可按程式碼區塊右上角的複製按鈕）：

```text
https://raw.githubusercontent.com/jimmyorz/pokeldn-plugins-zhTW/refs/heads/main/pokeldn-source.json
```

1. 開啟 **Plugins → Sources**，加入上述來源網址。
2. 前往 **Browse**，找到 **繁體中文（台灣）語言包**，按下 **Install**，依畫面提示完成安裝。

開啟 **Settings → Updates** 後，pokeldn 會在啟動時**自動檢查更新**；有新版時，在 **Plugins** 頁面按下更新按鈕並確認安裝即可。已手動安裝的使用者也可加入來源，取得後續更新，無須重新安裝。

### 手動安裝

無須設定來源，直接下載套件即可安裝；後續更新可自行下載新版套件再安裝。

**[下載最新 pokeldn 繁體中文（台灣）語言包](https://raw.githubusercontent.com/jimmyorz/pokeldn-plugins-zhTW/main/packages/pokeldn-zh-TW-1.1.16.pokeplugin)**

下載後，開啟 **Plugins → Add a plugin**，選擇下載的 `.pokeplugin`，依畫面提示完成安裝。

### 安裝後切換語言

兩種安裝方式完成後，都需要執行以下步驟：

1. **完整退出 pokeldn，再重新開啟**，讓語言包出現在語言選單中。
2. 前往 **Settings → App language**，選擇 **繁體中文（台灣）**。
3. **再次完整退出 pokeldn，再重新開啟**，套用介面語言。

> **安裝或啟用外掛不會自動切換語言。** 如果介面仍是英文，請確認已完成上述步驟。「App language」控制介面語言，與訓練家／寶可夢的語言設定不同。

本包已加入數位簽章，簽章指紋見下方版本資訊。

## 版本資訊

| 項目 | 內容 |
| --- | --- |
| 目前翻譯對應版本 | pokeldn **0.63.1** |
| 語言包版本 | `1.1.16` |
| 語系 | `zh-TW` |
| Plugins ID | `community-zh-tw` |
| Plugins API | `1.13` |
| Plugins 簽章指紋 | `ZP2X-THRM-26HS-XL2C` |
| 更新日期 | **2026-11-12** |

本版需使用 pokeldn **0.57.0 或以上**（支援 Plugins API 1.13）。

此語言包以表列的 pokeldn 版本與 Plugins API 為製作及檢查基準，屬於社群翻譯，非 pokeldn 或寶可夢官方發布。

## 檔案配置

| 路徑 | 用途 |
| --- | --- |
| [`packages/`](packages/) | 可安裝的 `.pokeplugin` 檔 |
| [`language-pack/`](language-pack/) | 主字串及所有補充翻譯的 TOML 原始檔 |
| [`docs/translation.md`](docs/translation.md) | 翻譯涵蓋範圍、用語原則與已知限制 |
| [`reference/strings.en.toml`](reference/strings.en.toml) | 製作時的上游英文基準 |
| [`reference/strings.zh-TW.toml`](reference/strings.zh-TW.toml) | 同一基準的完整中文對照，內容與 `language-pack/strings.toml` 相同 |
| [`reference/upstream.json`](reference/upstream.json) | 上游版本與檔案比對資料 |
| [`docs/maintenance.md`](docs/maintenance.md) | 後續更新與檢查方式 |
| [`docs/validation.md`](docs/validation.md) | 驗證紀錄與來源 |
| [`CHANGELOG.md`](CHANGELOG.md) | 版本更新紀錄 |

`language-pack/messages.toml`、`help.toml`、`terms.toml`、`templates.toml` 即為額外補充翻譯，均以可編輯文字保存。對照檔中的中文檔名為 `strings.zh-TW.toml`；安裝包使用 `strings.toml`，由 `plugin.toml` 指定，兩者內容相同。

## 授權 / License

翻譯內容衍生自 pokeldn，依 **AGPL-3.0-or-later** 提供，完整條款見 [LICENSE](LICENSE)。

pokeldn 與本語言包皆為非官方同好專案，與任天堂、The Pokemon Company、Game Freak 或 Creatures 無關，亦未獲上述公司的認可或贊助。寶可夢、Nintendo Switch 及相關名稱與角色的商標權屬於各權利人。依據 AGPL 第 7(e) 條，本授權不授予使用上述商標或任何其他寶可夢智慧財產的權利。

作者不支持將 pokeldn 用於商業、宣傳或品牌活動，包括神秘禮物配信。任何人若將其用於上述用途，均須自行負責取得所需的權利授權。

The translations are derived from pokeldn and provided under **AGPL-3.0-or-later**; see [LICENSE](LICENSE).

pokeldn and this language pack are unofficial fan projects. They are not affiliated with, endorsed by or sponsored by Nintendo, The Pokemon Company, Game Freak or Creatures. Pokemon, Nintendo Switch and the related names and characters are trademarks of their owners. Under section 7(e) of the AGPL, no right to use those trademarks or any other Pokemon intellectual property is granted.

The authors do not endorse using pokeldn for commercial, promotional or branded events, including Mystery Gift distributions. Anyone who does so is responsible for obtaining the rights it requires.
