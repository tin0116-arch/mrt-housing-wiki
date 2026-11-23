# LLM Wiki 工作流程與回饋修正機制 (workflow.md)

本文件定義「為什麼捷運站附近的房子比較貴？」專案之資料處理、知識建構、審計回饋與生成發布工作流。本流程強調「閉環回饋（Closed-loop Feedback）」，任何節點發現資訊不足或推論瑕疵，必須循指定回退路徑修正。

---

## 一、 工作流程圖 (Mermaid Closed-Loop Graph)

```mermaid
flowchart TD
    %% 主要工作流節點
    Start([啟動專案]) --> Node1[1. 來源檢索與資料取得<br>政大學術集成 5 篇文獻]
    Node1 --> Node2{2. 來源檢查與邊界評估}
    
    %% 邊界檢查
    Node2 -- 僅能取得摘要 --> Node2A[標記 reading_scope: 僅依據摘要<br>設定推論邊界禁令]
    Node2 -- 取得完整全文 --> Node2B[標記 reading_scope: 全文]
    Node2A --> Node3[3. Ingest 結構化萃取]
    Node2B --> Node3
    
    %% Ingest 到 Wiki
    Node3 --> Node3Log[寫入 logs/ingest.log.md]
    Node3 --> Node4[4. Wiki 整理與雙向連結<br>concepts / empirical / synthesis]
    
    %% Lint 審計環節
    Node4 --> Node5[5. Wiki Lint 知識庫質量審查]
    Node5 --> Node5Check{審查是否通過?}
    
    %% 回饋路徑 1 (Lint 失敗回退)
    Node5Check -- 發現違規/過度推論/斷鏈 --> Node5Fail[記錄至 logs/lint.log.md<br>標記問題等級與具體錯誤]
    Node5Fail --> LoopPathA[【回饋路徑 A】<br>修訂 Wiki 論述或限縮推論邊界]
    LoopPathA --> Node4
    
    %% Lint 通過進入 Query
    Node5Check -- 審核完全 PASS --> Node5Pass[記錄 PASS 於 logs/lint.log.md]
    Node5Pass --> Node6[6. Query 閉環檢索與壓力測試<br>Q1, Q2, Q3 實測]
    Node6 --> Node6Check{查詢測試是否完整?}
    
    %% 回饋路徑 2 (Query 發現盲點回退)
    Node6Check -- 存在盲點/無法以文獻解答 --> Node6Fail[【回饋路徑 B】<br>補充 concepts 交叉連結或標註研究限制]
    Node6Fail --> Node4
    
    %% Query 通過進入簡報製作 (後續階段)
    Node6Check -- 回答嚴謹可溯源 --> Node6Log[寫入 logs/query.log.md]
    Node6Log --> Node7[7. HTML 教學簡報製作<br>大學生與公眾科普導向]
    
    %% 最終驗證與回饋路徑 3
    Node7 --> Node8[8. 簡報與 Wiki 內容一致性終驗]
    Node8 --> Node8Check{簡報內容是否超譯?}
    Node8Check -- 出現未經證實之數據 --> LoopPathC[【回饋路徑 C】<br>回退修改 HTML，刪除未經證實內容]
    LoopPathC --> Node7
    Node8Check -- 終驗完全一致 --> End([專案發布與展示])

    %% 樣式設定
    classDef process fill:#f8fafc,stroke:#334155,stroke-width:2px;
    classDef decision fill:#eff6ff,stroke:#1d4ed8,stroke-width:2px;
    classDef feedback fill:#fff1f2,stroke:#e11d48,stroke-width:2px,stroke-dasharray: 5 5;
    classDef success fill:#ecfdf5,stroke:#059669,stroke-width:2px;
    
    class Node1,Node3,Node4,Node6,Node7 process;
    class Node2,Node5Check,Node6Check,Node8Check decision;
    class LoopPathA,Node6Fail,LoopPathC feedback;
    class End,Node5Pass success;
```

---

## 二、 具體回饋路徑說明 (Feedback Mechanisms)

### 1. 【回饋路徑 A】：Lint 審核未通過之回退機制
- **觸發條件**：
  - 出現未引證來源之孤立數值。
  - 將僅取得摘要之論文誤判為全文推論。
  - 踩中專案禁令（如：將溫弘裕 (2015) 誤寫為三期比較、將戴國正 (2011) 誤植噪音實證、將黃麟雅 (2017) 誤稱為環狀線、將陳品睿 (2025) 誤改為 TPASS）。
  - 出現 Wiki 頁面無效連結或斷鏈。
- **處理流程**：
  1. 在 `logs/lint.log.md` 記錄錯誤檔案、違規項目與問題嚴重性。
  2. 暫停下游工作，立即回到 `wiki/` 對應 Markdown 頁面修正敘述或移除不實數據。
  3. 修正後重新執行 Lint，直至完全通過（PASS）為止。

### 2. 【回饋路徑 B】：Query 壓力測試未通過之回退機制
- **觸發條件**：
  - 針對使用者常見的捷運房價提問（如「距離越近一定越貴嗎？」），發現 Wiki 無法給出有實證支持的完整回答，或無法清楚指出空間異質性。
- **處理流程**：
  1. 檢視是否遺漏了 `raw/` 中的重要觀點。
  2. 回退至 `wiki/concepts/` 或 `wiki/empirical-findings/`，深化概念間的交叉連結（Cross-link），或在論述中明確指出該問題在現有文獻中的實證限制。
  3. 重新進行 Query 測試並記錄於 `logs/query.log.md`。

### 3. 【回饋路徑 C】：HTML 簡報終驗一致性之回退機制
- **觸發條件**：
  - 簡報為了視覺效果或通俗化，出現未在 Wiki 中建立基礎的誇大文案或虛構圖表數據。
- **處理流程**：
  1. 對照 `source-matrix.md` 逐頁比對簡報內容。
  2. 發現超譯之處，強制回退修改簡報檔案，嚴格維持與知識庫一致的學術嚴謹度。
