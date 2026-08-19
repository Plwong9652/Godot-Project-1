# assets/

## 來源說明

**這批素材不是本人製作的。**

它們提取自一個從網上下載的免費魔塔 Flash 遊戲（SWF，Flash Player 6）。原檔內未附任何版權聲明或作者署名。從遊戲內的訊息文字可見，原作者當年曾公開徵求他人設計新地圖並留下聯絡電郵，程式亦寫成全參數化的形式，顯示原作本身即以開放分享為前提發布。

這套 32×32 的魔塔素材在中文魔塔社群屬長期公開流通的共用資源，並非單一來源獨佔：

- **WDMOTA** — 魔塔愛好者建立的網站，設有「素材專區」，站方聲明下載不收費、不含商業廣告。
- **scratch5.com** — 提供「2D 像素風格魔塔冒險遊戲素材」下載頁。
- **h5mota.com（HTML5 魔塔廣場）** — 收錄超過 2000 座玩家自製的塔，其編輯器支援使用者直接拖入素材圖片自動註冊，反映此類素材在該社群作為共用底材的使用方式。
- **愛給網（aigei.com）** — 亦有「魔塔門」素材庫。

此外，連 RPG Maker 平台上的重製版本也公開說明其設計架構參考自三原塔（原始魔塔／胖老鼠魔塔／新新魔塔），可見這個類型本身建立在長期互相參考的傳統之上。

---

## 本專案的用途

本專案（Godot 重製）以此 SWF 版本作為基底，做法是 reuse + renew：沿用其規則、系統結構與素材作為起點，再在其上做自己的版本。這批素材放在此處是為了讓開發過程可被檢視，不主張任何權利。

## 檔案說明

### 圖

| 路徑 | 內容 |
|---|---|
| `tileset_32.png` | 133 張 32×32 合成的單一 atlas，12×12 排列，384×384。tile 之間不加 margin 與 spacing |
| `misc/` | 23 個非 32×32 的圖：四張 96×96 大型敵人、UI 零件與字元、一張 JPEG |
| `floor_previews/` | 依原作地圖資料渲染的 50 層樓預覽圖，供人眼確認用 |
| `reference_contact_sheet.png` | 放大兩倍加間隔的對照圖，方便肉眼查找 |

### 對照表

| 路徑 | 內容 |
|---|---|
| `tileset_32_index.json` | 每個 tile 的 atlas 座標 ↔ 原 SWF 內的 character ID |
| `icon_animation_map.json` | 每個 Icon 使用哪幾張圖、各圖尺寸、是否在 atlas 內、atlas 座標 |

### 音效

`audio/` — 7 個 MP3（11025Hz、mono、16kbps）。原作沒有背景音樂，只有音效。

已確認用途：獲得道具、開門／拆牆、打怪、第 3 層 boss 事件及其中的怪物攻擊音。另有兩段較長的（6.00s、9.25s）對應特定敵人登場演出。

### 資料

| 路徑 | 內容 |
|---|---|
| `data/maps.json` | 50 層，每層兩個 11×11 grid：第一個是 icon 層（地形、敵人、道具），第二個是 event 層（事件編號）。索引 = row×11 + col |
| `data/enemies.json` | 70 筆敵人資料：Name、Life、Offense、Defense、Money、Magic、Cross、Dragon |
| `data/shop_exchanges.json` | 15 筆商店交易 |
| `data/messages.json` | 82 段文字 |
| `data/game_config.json` | 51 組樓梯連接、玩家初始值 |

---

## 提取方式

以自行撰寫的 SWF 解析器與 AVM1 disassembler 處理，未使用商業反編譯工具。圖片來自 DefineBitsLossless／DefineBitsJPEG3 tag，音效來自 DefineSound tag，遊戲資料來自主程式 DoAction 區塊的 bytecode。

註：原檔字串為混合編碼——constant pool 為 UTF-8，inline string 為 GBK。

## 在 Godot 使用時的注意事項

- Project Settings → Rendering → Textures → **Default Texture Filter 設為 Nearest**，否則 pixel art 會模糊。
- TileSet atlas 的 **Use Texture Padding** 保持開啟，Godot 會自動處理接縫，因此本 atlas 不需自行加 margin。
- 原作的敵人多為兩張圖交替的動畫，atlas 中看似重複的圖其實是同一物件的不同幀，並非重複素材。詳見 `icon_animation_map.json`。
