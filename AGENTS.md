# 專案規範與 AI 協作手冊 (AGENTS.md)

## 1. 專案目的 (Project Purpose)
本專案為一個「口袋美食與咖啡廳探索地圖網站」。
旨在建立一套自動化工作流：使用者只需輸入店家簡短名稱、地址草稿或 Google Maps 連結（存放於 `raw/` 或直接對話輸入），AI 即自動補全詳細資訊（行政區、捷運站、特色標籤、推薦點心/飲品、營業時間等），生成標準 Markdown 條目（存放於 `stores/`），並自動同步更新公開瀏覽的首頁 `index.html` 卡片列表。

## 2. 視覺風格與元件規範 (Design & UI Style)
- **整體風格**：日系溫暖喫茶店風 / 溫柔大地色調 (Warm Wood & Cream Ivory)。
- **色調規範**：主色調為深咖啡色 (`#4A3525`)、米白色背景 (`#FAF6F0`)、暖木黃點綴 (`#D9A05B`)。
- **排版與卡片**：
  - 卡片需包含：店家名稱、行政區標籤 (如：`#大安區`)、風格標籤 (如：`#有插座` `#不限時`)、一句話推薦、Google Maps 導航按鈕。
  - 支援按「行政區」與「風格主題」進行動態選單篩選展示。

## 3. 檔案與目錄結構 (File Structure & Naming Rules)
本專案目錄結構如下：
├── AGENTS.md               # AI 協作與規範手冊（本文件）
├── raw/                    # 原始店家推薦草稿或連結檔 (.md / .txt)
├── stores/                 # 整理後的標準店家 Markdown 條目檔
│   ├── zhongshan-fika-fika.md   # 檔案命名格式：行政區英文小寫-店家名.md
│   └── daan-quiet-corner.md
├── assets/                 # 靜態圖片、地圖圖示與 CSS 樣式
│   ├── css/style.css
│   └── images/
├── index.html              # 網站公開首頁 (包含搜尋、動態篩選與店家卡片清單)
└── README.md               # GitHub 專案說明文件

## 4. 新增店家內容之格式規範 (Data & Content Specs)

### 條目檔格式 (`stores/*.md`)
所有位於 `stores/` 的店家檔案，開頭必須包含 YAML Frontmatter 格式：

---
name: "Fika Fika Cafe"
district: "中山區"
mrt: "松江南京站"
category: "咖啡廳"
tags: ["有插座", "北歐風", "適合辦公"]
address: "台北市中山區伊通街33號"
google_map_url: "[suspicious link removed]..."
rating: 4.5
updated: "2026-11-16"
summary: "北歐簡約風名店，烘焙冠軍咖啡豆，環境明亮安靜。"
---

# Fika Fika Cafe

## 📍 店家資訊
- **地址**：台北市中山區伊通街33號
- **鄰近捷運**：松江南京站 5 號出口（步行約 3 分鐘）
- **特色標籤**：`#有插座` `#北歐風` `#適合辦公`

## 💡 探店亮點與心得
採光明亮，空間充滿簡約木質氛圍。Flat White 奶泡細緻，平日午後非常適合帶筆電工作。

## ☕ 推薦必點
- 招牌單品手沖咖啡
- 拿鐵咖啡 / Flat White

---

## 5. AI 操作流程與工作 SOP (AI Operating Workflow)
當使用者提供新的店家名稱或連結並指示「新增店家」時，AI 必須嚴格執行以下 5 個步驟：

1. **資訊查詢與補全**：依據使用者提供的店家名稱，查詢並補齊完整地址、行政區、鄰近捷運站、特色標籤與 Google Maps 導航連結。
2. **建立條目檔案**：
   - 檔名規則：`行政區英文小寫-店家名稱.md`（置於 `stores/` 資料夾）。
   - 格式要求：嚴格遵循 YAML Frontmatter 與正文標題結構。
3. **更新首頁 `index.html`**：
   - 在 `index.html` 的卡片列表中，於最上方插入最新店家的 HTML 卡片元件。
   - 正確設定 `data-district` 與 `data-tags` 屬性，確保篩選器能正確運作。
4. **驗收與檢查**：檢查 Markdown 連結有效性，確認首頁無破版或樣式遺失。
5. **回報變更**：向使用者回報新增的檔案名稱與改動清單。

## 6. 限制與原則 (Constraints)
- **保護既有資料**：未經允許，禁止刪除或修改既有的店家條目。
- **維持視覺一致性**：更新 `index.html` 時僅能調整卡片區塊，不得替換 CSS 全域樣式或改變日系大地色調。