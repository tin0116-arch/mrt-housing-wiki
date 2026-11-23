# 捷運與房價知識庫首頁 (LLM Wiki: Index & MOC)

歡迎查閱「**為什麼捷運站附近的房子比較貴？**」LLM Wiki 知識庫。

本專案實踐 Andrej Karpathy 提出的 **LLM Wiki** 理念，以結構化、純 Markdown 檔案維護具備持續更新、透明可稽核與可溯源的知識庫，深入解析臺灣不動產經濟學與地政學中關於大眾捷運系統（MRT）對住宅價格影響的實證研究。

---

## 知識地圖 (Map of Content, MOC)

### 1. 核心理論概念 (Concepts)
- [特徵價格理論 (Hedonic Price Theory)](./concepts/hedonic-price-theory.md)：解析房屋價格如何由實體結構、鄰里環境與交通區位特徵共同構成。
- [交通可及性與溢價 (Accessibility Premium)](./concepts/accessibility-premium.md)：剖析通勤時間節省、出行便利性如何被資本化折現至房價中。
- [距離衰減效應 (Distance Decay)](./concepts/distance-decay.md)：探討捷運站周邊「水面漣漪狀」的溢價衰減規律與影響門檻（250m、500m、1,000m）。
- [空間異質性與區位差異 (Spatial Heterogeneity)](./concepts/spatial-heterogeneity.md)：檢驗捷運效益在不同地理區位、行政區與車站類型中的非均質性。
- [交通成本與政策資本化效果 (Transit Cost Capitalization)](./concepts/transit-cost-capitalization.md)：探討公共運輸票價補貼（如 1280 定期票）如何改變邊際通勤成本並牽動住宅市場。

### 2. 實證研究彙整 (Empirical Findings)
- [捷運距離與實質溢價幅度](./empirical-findings/mrt-distance-effects.md)：比對林祖嘉與洪得洋 (1999) 早期全域路網與温弘裕 (2015) 信義線圈層之量化實證。
- [路寬、鄰里生活設施與多維度影響](./empirical-findings/road-width-and-urban-factors.md)：探討林祖嘉 (1999) 道路寬度貢獻與黃麟雅 (2017) 公園開放空間、生活設施及次市場分化。
- [車站類型、區位差異與資本化再檢視](./empirical-findings/station-types-and-heterogeneity.md)：探討戴國正 (2011) 對捷運效益全域均質迷思的空間計量再檢視。
- [1280 定期票對住宅價格結構與空間分布之影響](./empirical-findings/fare-policy-and-spatial-distribution.md)：彙整陳品睿 (2025) 針對雙北 1280 定期票對通勤成本與住宅市場重塑之實證方向。

### 3. 綜合論述核心頁面 (Synthesis)
- [綜合論述：為什麼捷運站附近的房子比較貴？](./synthesis/why-houses-near-mrt-are-expensive.md)：貫穿五篇研究的核心全景問答與理論總成。

---

## 原始文獻庫 (Raw Literature Repository)
本專案五篇研究均取自國立政治大學學術集成（NCCU Academic Hub），遵循嚴格學術誠信原則，全數標註實際讀取範圍：
1. [Paper 1: 林祖嘉、洪得洋 (1999)](../raw/paper_1_39107.md) - 臺北市捷運系統與道路寬度對房屋價格影響之研究
2. [Paper 2: 温弘裕 (2015)](../raw/paper_2_88427.md) - 大眾運輸系統對房價的影響-以台北捷運信義線為例
3. [Paper 3: 戴國正 (2011)](../raw/paper_3_62426.md) - 大眾捷運系統對房價影響效果之再檢視
4. [Paper 4: 黃麟雅 (2017)](../raw/paper_4_127669.md) - 臺北市生活設施水準對住宅價格之影響
5. [Paper 5: 陳品睿 (2025)](../raw/paper_5_178543.md) - 檢驗雙北「1280公共運輸定期票」上路後，透過降低交通成本是否改變住宅市場價格結構與空間分布

---

## 專案與流程治理文件
- [Agent 作業規範 (AGENTS.md)](../AGENTS.md)：定義 Ingest、Query、Lint 與更新規則。
- [工作流程與回饋迴圈 (workflow.md)](../workflow.md)：包含完整節點回退機制之 Mermaid 流程圖。
- [溯源追蹤矩陣 (source-matrix.md)](../source-matrix.md)：文獻來源、Wiki 頁面與未來簡報之全景對照表。
- [執行日誌庫 (logs/)](../logs/)：
  - [Ingest 執行日誌](../logs/ingest.log.md)
  - [Lint 審查與修正日誌](../logs/lint.log.md)
  - [Query 查詢測試日誌](../logs/query.log.md)
