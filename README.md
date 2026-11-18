# 同路 Way for All｜世新大學互動地圖

世新大學的 2.5D 互動校園地圖。掃描大樓、校門或地標上的 QR code，地圖會標出「你在這裡」，並指出最近的性別友善廁所、無障礙廁所與哺集乳室，再沿著分區色線帶你到目的地。

本專案為「校園友善空間識別與指引設計徵件」作品「同路 Way for All」的一部分。

An interactive 2.5D campus map of Shih Hsin University. Scan the QR code on a building, gate or landmark to see where you are, find the nearest all-gender restroom, accessible restroom or nursing room, and follow the zone-coloured line to get there.

## 功能

- **你在這裡**：每個 QR code 帶有位置代碼，打開就會標出目前位置，不需要 GPS，也不需要下載 App。
- **找最近的設施**：性別友善廁所、無障礙廁所、哺集乳室、AED、無障礙電梯、坡道、停車位、照護床。
- **帶我去**：任兩棟大樓、校門或地標之間都能導航，路線用目的地所在分區的顏色標示，並提示要搭電梯到幾樓。
- **樓層導覽**：每棟樓列出各樓層的教室、單位與設施。
- **搜尋**：可搜尋教室代碼（如 R503、S1204）或單位名稱（如 7-ELEVEN、郵局）。
- **中英切換**：英文名稱採學校官方譯名。
- **無障礙**：大樓可用鍵盤操作，樓層與路線也以文字清單呈現，螢幕報讀軟體可以讀到。

## 六個分區色碼

| 分區 | 顏色＋形狀 | 包含 |
| --- | --- | --- |
| 入口・新聞區 | 藍 ● | J、W |
| 行政・圖書區 | 紫 ◆ | 行政大樓、L、G、言論廣場 |
| 生活・廣電區 | 黃 ■ | 學生宿舍、廣電 B・T（改建中） |
| 舍我・廣場區 | 橘 ▲ | R、S、學校廣場、八風舞台 |
| 傳播・運動區 | 青 ⬢ | A、操場、C、V |
| 管理・媒體區 | 洋紅 ★ | M、OM |

入口一律用綠底白字的門號（門1–門4）標示。

## QR code 位置代碼

在網址後面加上 `#代碼`，例如 `https://你的網址/#bldg-r`。自行架設時也可以用 `?at=bldg-r`。

| 類型 | 代碼 |
| --- | --- |
| 校門 | `gate1` 前校門、`gate2` 後校門、`gate3` 傳院大門、`gate4` 側門 |
| 大樓 | `bldg-j`、`bldg-w`、`bldg-dorm`、`bldg-adm`、`bldg-l`、`bldg-g`、`bldg-r`、`bldg-s`、`bldg-a`、`bldg-v`、`bldg-c`、`bldg-m`、`bldg-om` |
| 地標 | `spot-fountain` 魔法噴水池、`spot-statue` 舍我爺爺 |

頁面下方的「QR code 一覽」可以直接看到並截圖每一個 QR code。

## 用 GitHub Pages 發布

1. 把 `index.html`、`README.md`、`.gitignore` 上傳到這個 repository 的根目錄。
2. 到 **Settings › Pages**，在 **Build and deployment** 選 **Deploy from a branch**，分支選 `main`、資料夾選 `/ (root)`，按 **Save**。
3. 等一兩分鐘，頁面上方會出現網址，例如 `https://你的帳號.github.io/shu-map/`。
4. **更新 QR code 網址**：打開 `index.html`，把 `DEFAULT_BASE` 改成你的新網址後重新上傳。

   ```js
   var DEFAULT_BASE = "https://你的帳號.github.io/shu-map/";
   ```

   也可以直接在頁面下方的「公開網址」欄位貼上新網址，但那只會存在你自己的瀏覽器裡，別人看到的 QR code 還是 `DEFAULT_BASE`。

## 修改資料

所有資料都在 `index.html` 的 `<script>` 開頭：

| 要改的內容 | 找這個變數 |
| --- | --- |
| 大樓名稱、樓層、設施、位置 | `BUILDINGS` |
| 步道路口與路線 | `NODES`、`EDGES` |
| 校門 | `GATES` |
| 地標 | `LANDMARKS` |
| 分區名稱與顏色 | `ZONES` |

- 大樓的 `parts` 是 `[中心 x, 中心 y, 寬, 深, 旋轉角度]`，座標以校園平面圖為準。
- `fl` 是地上樓層數，只用來決定建築畫多高。
- `f` 是設施，例如 `gender:"4F"` 代表 4 樓有性別友善廁所。
- `floors` 是樓層導覽，同一層的項目用全形分號「；」隔開。

## 注意事項

- 建築位置依校園平面圖概略繪製，並非精確測量。
- 步行時間尚未實地測量，所以「最近」是依校內步道距離估算。
- 廣電大樓 B、T 改建中，暫不提供導航。
- QR code 圖案由 [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator)（MIT 授權）產生，從 cdnjs 載入；字型使用 Google Fonts 的 Noto Sans TC。
- 本專案尚未附授權條款，如要開放他人使用或修改，請自行加上 LICENSE 檔。
