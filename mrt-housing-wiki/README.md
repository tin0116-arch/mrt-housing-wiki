# 捷運與房價 LLM Wiki (mrt-housing-wiki)

> **主題：為什麼捷運站附近的房子比較貴？**  
> 一個實踐 Andrej Karpathy **LLM Wiki** 概念的持續演化知識庫與教學簡報專案。

---

## 專案緣起與核心理念

在不動產市場中，「買房跟著捷運走」幾乎是一般大眾與租屋族的口頭禪。但捷運站附近的房子究竟貴在哪裡？貴多少？距離越近就一定越貴嗎？

本專案摒棄傳統不透明向量資料庫（Vector DB）的黑盒子檢索架構，全面採用 Andrej Karpathy 提出的 **LLM Wiki** 核心架構：
1. **純 Markdown 維護**：所有文獻、理論概念、實證數據與綜合論述皆以結構化 Markdown 檔案維護，具備高度可讀性與 Git 版本控管能力。
2. **零幻覺與嚴格來源可溯性 (Zero-Hallucination & 100% Provenance)**：每一個論點皆能 100% 雙向追溯至原始文獻。
3. **讀取邊界誠實揭示 (Honesty of Scope)**：原始研究因授權限制僅取得官方摘要者，全數嚴格標註「僅依據官方摘要」，絕不編造全文細節或未經證實之數據。
4. **閉環回饋機制 (Closed-Loop Feedback)**：透過 Lint 靜態審查與 Query 壓力測試，建立完整的自動回退與錯誤校正迴路。

---

## 五篇政大學術集成核心來源

本知識庫嚴格收錄國立政治大學學術集成（NCCU Academic Hub）之五篇真實學術研究：

1. **林祖嘉、洪得洋（1999）**：《臺北市捷運系統與道路寬度對房屋價格影響之研究》，《住宅學報》第 8 期。  
   • 核心主題：捷運站實際距離（負向）與面臨道路寬度（正向）對房價之特徵價格模型估計。
2. **温弘裕（2015）**：《大眾運輸系統對房價的影響-以台北捷運信義線為例》，行政管理碩士學程碩士論文。  
   • 核心主題：信義線通車後實價登錄資料之距離圈層溢價（相較於 500m 以上基準群，250m 內增約 26.051 萬/㎡）。
3. **戴國正（2011）**：《大眾捷運系統對房價影響效果之再檢視》，地政研究所碩士論文。  
   • 核心主題：空間異質性（Spatial Heterogeneity）、行政區位與車站機能類型（轉乘站 vs 端點站）對捷運效益之調節。
4. **黃麟雅（2017）**：《臺北市生活設施水準對住宅價格之影響》，地政學系碩士論文。  
   • 核心主題：生活設施水準與交通便利性；實證捷運距離與主題公園開放空間對住宅總價之正向推動最為顯著。
5. **陳品睿（2025）**：《檢驗雙北「1280公共運輸定期票」上路後，透過降低交通成本是否改變住宅市場價格結構與空間分布》，地政學系碩士班碩士論文。  
   • 核心主題：雙北 1280 定期票降低長距離邊際通勤成本，引導不同價格層與外圍空間分布之重塑。

---

## 知識庫架構與目錄說明

```text
mrt-housing-wiki/
│
├── index.html                   # GitHub Pages 入口（直接呈現 10 頁教學簡報）
├── README.md                    # 專案中文完整說明與教學導引
├── AGENTS.md                    # LLM Wiki 維護守則與 Agent SOP（四大邊界禁令）
├── workflow.md                  # 包含回饋與修正迴圈之 Mermaid 工作流程圖
├── source-matrix.md             # 文獻來源、Wiki 概念、實證與 10 頁簡報之追溯矩陣
│
├── raw/                         # 原始文獻庫（不可竄改，完整保存中繼資料與官方摘要）
│   ├── paper_1_39107.md         # 林祖嘉、洪得洋 (1999) 原始摘要與限制
│   ├── paper_2_88427.md         # 温弘裕 (2015) 原始摘要與限制
│   ├── paper_3_62426.md         # 戴國正 (2011) 原始摘要與限制
│   ├── paper_4_127669.md        # 黃麟雅 (2017) 原始摘要與限制
│   └── paper_5_178543.md        # 陳品睿 (2025) 原始摘要與限制
│
├── wiki/                        # 結構化知識庫（純 Markdown 雙向語義鏈結）
│   ├── index.md                 # 知識庫總目錄與 MOC（Map of Content）
│   ├── concepts/                # 核心理論概念頁
│   │   ├── hedonic-price-theory.md        # 特徵價格理論
│   │   ├── accessibility-premium.md      # 交通可及性與溢價
│   │   ├── distance-decay.md             # 距離衰減效應
│   │   ├── spatial-heterogeneity.md      # 空間異質性與區位差異
│   │   └── transit-cost-capitalization.md# 交通成本與政策資本化效果
│   ├── empirical-findings/      # 實證研究彙整
│   │   ├── mrt-distance-effects.md       # 捷運距離與實質溢價幅度
│   │   ├── road-width-and-urban-factors.md# 路寬、生活設施與多維度影響
│   │   ├── station-types-and-heterogeneity.md# 車站類型、區位差異再檢視
│   │   └── fare-policy-and-spatial-distribution.md# 1280 定期票對空間結構之影響
│   └── synthesis/               # 整合論述總成
│       └── why-houses-near-mrt-are-expensive.md # 核心問題全景解答
│
├── logs/                        # 稽核、操作與測試日誌
│   ├── ingest.log.md            # 五次文獻 Ingest 歷程記錄
│   ├── lint.log.md              # 三次靜態代碼與知識品質審查紀錄
│   ├── query.log.md             # 三次閉環 QA 壓力測試紀錄
│   └── presentation-test.log.md # HTML 簡報完整功能與排版測試紀錄
│
└── presentation/                # 獨立簡報目錄
    └── index.html               # 10 頁互動教學 HTML 簡報
```

---

## 核心 SOP 與閉環回饋機制

### 1. Ingest（資料匯入）
- 檢核原始網址與典藏元資料，嚴格標記 `reading_scope: 僅依據摘要`。
- 提取概念與實證分別路由分流至 `wiki/concepts/` 與 `wiki/empirical-findings/`。

### 2. Lint（知識審計）
- 檢查項：來源覆蓋度、數據真實性（剔除未見於摘要之金額）、四大禁令防誤（不將温弘裕寫成三期比較、戴國正不捏造噪音數據、黃麟雅不混淆聯開宅、陳品睿不改稱 TPASS）、超連結有效性。

### 3. Query（閉環問答）
- 僅使用 `wiki/` 內容回答，包含核心回答、文獻依據與研究限制說明。

### 4. Loop / Graph（閉環回退）
- **回饋路徑 A**：Lint 發現斷鏈或數據無憑證時，強制回退修改 Wiki。
- **回饋路徑 B**：Query 發現知識盲點時，回退補充 Wiki 交叉連結。
- **回饋路徑 C**：簡報文案超譯時，強制回退修訂 HTML。

---

## 10 頁教學 HTML 簡報概覽

簡報位於根目錄 [`index.html`](index.html)（亦備份於 [`presentation/index.html`](presentation/index.html)），設計重點：
- **美學風格**：研究型教學風格，米白、淺咖、深棕與霧金配色，留白大器、排版精緻。
- **純原生技術**：無外部框架、無 CDN，單檔自帶 CSS 與 JavaScript。
- **互動功能**：上一頁/下一頁、鍵盤方向鍵、進度條、跳頁點位、**第 8 頁可作答即時反饋測驗**。
- **響應式**：支援桌機與手機瀏覽，不破版、不溢出。

---

## 本機預覽方式

1. **直接開啟**：在檔案總管中按兩下 `index.html`，即可在任何瀏覽器中檢視與互動。
2. **VS Code Live Server**：於 VS Code 開啟本資料夾，右鍵 `index.html` 點選 **Open with Live Server**。

---

## GitHub 上傳與 GitHub Pages 公開步驟

在全新建立的 `mrt-housing-wiki` 資料夾內開啟終端機（PowerShell 或 Bash），依序執行：

```bash
# 1. 初始化 Git 儲存庫
git init

# 2. 加入所有檔案並提交
git add .
git commit -m "feat: complete MRT Housing LLM Wiki and interactive presentation"

# 3. 設定主分支名稱
git branch -M main

# 4. 連接遠端 GitHub 儲存庫（請替換為您的 GitHub 帳號與 repo 名稱）
git remote add origin https://github.com/<您的GitHub帳號>/mrt-housing-wiki.git

# 5. 推送至 GitHub
git push -u origin main
```

### 啟用 GitHub Pages：
1. 進入 GitHub 儲存庫頁面，點選上方 **Settings**。
2. 點選左側選單的 **Pages**。
3. 在 **Build and deployment** 下方的 **Branch** 選擇 `main` 分支，資料夾選擇 `/ (root)`。
4. 點擊 **Save**。
5. 稍候約 1 分鐘，重新整理頁面即可取得專屬公開網址（例如：`https://<您的帳號>.github.io/mrt-housing-wiki/`）。
