# 🎢 樂園即時看板 Disney & Universal Live

全球迪士尼樂園與環球影城即時資訊看板。單一 HTML 檔案、純前端、免後端伺服器，可直接部署在 GitHub Pages 等靜態網站空間。

**🔗 使用網址：[https://vincent981010.github.io/theme-park-dashboard/](https://vincent981010.github.io/theme-park-dashboard/)**

手機瀏覽器打開後，可點選 Safari/Chrome 的「加入主畫面」，以全螢幕 App 方式使用。

---

## ✨ 功能

- **樂園選擇**：涵蓋全球迪士尼度假區（加州、奧蘭多、東京、巴黎、香港、上海）與環球影城度假區（好萊塢、奧蘭多、日本、新加坡、北京、Epic Universe），可搜尋樂園／度假區名稱快速跳轉
- **開關園時間**：顯示當日開園／閉園時間
- **即時營運狀態**：每項設施的營運中／暫停／整修／休園狀態
- **遊樂設施等待時間**：即時排隊等待分鐘數，每 2 分鐘自動刷新，數字更新有翻牌動畫
- **演出時間**：各表演節目的今日場次時間
- **中英文名稱切換**：設施名稱可切換「中文／English／中英對照」，內建約 230+ 筆人工校對的官方中文譯名，未收錄的設施會自動呼叫機器翻譯並標示「機器翻譯」以示區別
- **真實地圖**：使用 OpenStreetMap 圖資的可縮放、拖曳地圖，標示各設施位置與目前狀態
  - 📍 定位我的位置（使用裝置 GPS）
  - 🧭 一鍵規劃從目前位置到指定設施的步行路線，顯示預估時間與距離
- **PWA 支援**：可加入主畫面、有獨立圖示與啟動畫面，接近原生 App 體驗

---

## ⚙️ 原理 / 技術架構

這是一個**純前端網頁**（單一 `index.html`），沒有自己的後端或資料庫，所有資料都即時向第三方公開 API 請求：

| 功能 | 資料來源 | 說明 |
|---|---|---|
| 樂園清單、開關園時間、即時排隊/營運狀態、演出時間 | [themeparks.wiki](https://themeparks.wiki) API | 社群維運的免費公開 API，整合全球樂園官方即時資料 |
| 地圖圖資 | [OpenStreetMap](https://www.openstreetmap.org) | 免費開源地圖，顯示實際道路與步道 |
| 步行路線規劃 | [OSRM](http://project-osrm.org/)（公開示範伺服器） | 依 OpenStreetMap 步道資料計算步行路線，僅供參考 |
| 中文名稱自動翻譯（字典未收錄的設施） | [MyMemory Translation API](https://mymemory.translated.net/) | 免費機器翻譯，結果會標示「機器翻譯」以區別人工校對譯名 |

**CORS 備援機制**：由於部分 API 未開放瀏覽器端直接請求（CORS 限制），前端會先嘗試直連，失敗時自動改用公開 CORS 代理（allorigins.win / corsproxy.io）重試。

**技術棧**：純 HTML / CSS / JavaScript（無框架、無建置流程），地圖使用 [Leaflet.js](https://leafletjs.com/)，字型使用 Google Fonts。所有程式碼都在單一 `index.html` 內，方便直接部署與修改。

---

## ⚠️ 已知限制

- 設施資料完整度取決於 themeparks.wiki 的社群維運進度，較新開幕或非美國地區的樂園（如日本、海外新設施）資料可能不完整或缺漏
- 部分設施採用官方 App 專屬的「指定入場」或「虛擬排隊」機制（例如需搶票的新設施），這類即時資料通常無法透過公開 API 取得
- 步行路線僅依據 OpenStreetMap 標記的步道資料計算，可能與園區實際動線有落差，僅供參考
- 中文設施名稱为自建對照表，涵蓋主要熱門設施，未收錄者會顯示機器翻譯結果，可能與官方正式譯名有出入

---

## 📁 檔案結構

```
theme-park-dashboard/
├── index.html         # 主程式（唯一必要檔案）
├── manifest.json       # PWA 設定檔
├── icon-192.png         # App 圖示 (192x192)
└── icon-512.png         # App 圖示 (512x512)
```
