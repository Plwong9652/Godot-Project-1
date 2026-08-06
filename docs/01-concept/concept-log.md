# 01 Concept

本階段目標：由零到定出 Game Concept、Core Pillars、Systems 骨架。
結束條件：可以在 Godot 開 project、落第一個 prototype。

本文件記錄的是思考過程，不只是結論。曾經考慮而否決的方向會保留，並寫明否決理由。

---

## 已確認前提

### 開發

- Engine：Godot
- 2D
- Single Player
- Solo Development
- Initial Target：第一個完整版本。時間無限期，三個月只作 scope 量度參考，做不完不停。

> 註：此項原記錄為「約 3 個月 Scope」。原意是無限期進行，三個月僅作為衡量 scope 的尺度，並非死線。此處更正。

### 設計方向

- Gameplay 為核心
- 非操作導向
- 小型 Project
- 故事不作核心設計。如需要，只在開場及結尾簡單交代（各一張圖、兩句字為上限）

### 美術方向

- 主要使用現成 assets
- 設計需盡量重用 assets
- 避免不停新增美術內容
- 內容變化優先來自 gameplay / system，而非美術

### Gameplay 方向（意向，未成為 design decision）

希望達到：

- Replayability
- 高配搭性
- 系統之間互相組合

可能的載體（全部未定）：mod、perk、trait、upgrade、rule combination

### 技術目標

本 project 同時作為熟習 Godot 的載體。希望自然涵蓋：

- UI
- Scene Management
- Save / Load
- Data Persistence
- 其他常見 Godot workflow

### 參考方向

Flash game 年代的設計模式作主要參考。取其「一句講得完的核心」與小規模、規則簡單的特性。不做任何既有作品的 clone。

---

## 專案外部條件

- Repo 為 public。目的是公開開發過程本身，而非只展示成品。
- 是否商業化未定。
- Licence：repo 根目錄的 MIT 只涵蓋自己擁有版權的內容。第三方 assets 各自保留其原有授權，不會因為放進本 repo 而變成 MIT。需另備一份第三方清單，逐項記錄：檔案在 project 中的位置、來源連結、作者、licence、取得日期。此清單需在加入 asset 當下即時補寫，事後補回會找不到出處。
- Asset licence 取態：MIT / CC0 一類寬鬆授權優先。遇到 GPL / LGPL 或不明的自訂授權先停下逐項查清。

---

## 過程記錄

### 關於文件與紀錄方式

- 決定以「階段」而非日期劃分文件。理由：commit 本身已帶日期，檔名再寫日期是重複；外部讀者關心的是進行到哪一步，而非哪一天。
- 決定不預先定義全部階段名稱。理由：階段的形狀要走完才看得清，先定死名稱會為了遷就名稱而扭曲內容。只定眼前這個階段，並為它寫明結束條件。
- 決定一個階段一份長文件，逐步向下增補，而非一個議題一份。理由：要呈現的是演化過程，分拆成獨立議題會失去這條線。
- 暫不設 README。等 repo 內開始有 code 等其他內容時再補。

### 關於引擎選擇（早前已決定，此處保留脈絡）

先前曾在 UE5、Unity、Godot 之間比較。最終選 Godot：2D 支援直接、體積小、開箱即用、MIT 授權無 royalty。UE5 雖然最熟悉，但對 2D 小型 project 是過度配置。

---

## 進行中

### #1 Game Concept

未決，待答：

1. 玩家在遊戲中主要在做什麼類型的決定？（例如：選組合看結果、分配有限資源、排列次序、以風險換回報）
2. 一個 run 大約多長、有沒有明確結束？（例如：一局十五分鐘有結算，或無限期經營）

這兩點決定 replayability 從何而來，也決定 save 系統是存進度還是存局面。

### 待處理的實作議題

「高配搭性、系統互相組合」若要成立，真正的成本不在寫效果本身，而在架構：效果以什麼形態存在（獨立 Resource、dictionary、其他）、何時計算（觸發時查一次或持續 recalculate）、如何疊加與處理衝突。此決定若錯，效果數量增長到一定程度會崩。此議題與技術目標中的 data persistence 對口，需在 concept 成形時一併決定，不宜留到後期。
