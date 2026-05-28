# 菲律賓 PAGCOR 法規政策監測工具 — 規格書 v1.0

> 版本：v1.0（已對齊，準備建置）
> 日期：2026-05-22
> 對象：業務拓展 / 市場觀察使用者；個人使用，必要時可轉給法務或主管
> 與「菲律賓話題週報工具 v1.1」關係：架構平行（單檔 HTML、Claude 自動更新、Cowork 對話通知），但內容性質與卡片設計完全不同

---

## 0. 在規格之前的共識

> **「我在做菲律賓博彩產業的業務拓展與市場觀察。我需要每天早上知道 PAGCOR 及相關主管機關有沒有新的政策、合規名單變動、執法行動、或業界風聲；其中已證實的官方公告要與未證實的傳聞視覺上明顯分開。每天的更新要極簡（三行內知道要不要點進去），週一給我一份完整彙整。原文是英文沒問題，但卡片標題與摘要要中文化，原文段落要能直接引用並一鍵跳到來源網址。資料要按月歸檔、能全文搜尋，還要有一頁專門列『目前仍生效的法規』隨時可查現況。」**

---

## 1. 已對齊的需求清單

| 編號 | 項目 | 對齊內容 |
|---|---|---|
| R1 | 主題範圍 | 菲律賓 PAGCOR 及周邊主管機關的法規政策、合規名單、執法行動、政府風聲 |
| R2 | 使用者定位 | 業務拓展 / 市場觀察；非法務專業使用者，但卡片需支援轉給法務同事 |
| R3 | 主管機關涵蓋（A+B+C 三層） | A：PAGCOR、AMLC、BIR、BI、SEC；B：DOF、DOJ、DICT、NPC、DOLE；C：CEZA / APECO / AFAB 經濟特區、BSP、PNP、NBI、MMDA / LGU |
| R4 | 業態焦點 | **PIGO（Philippine Inland Gaming Operators，現行框架）為主**；IGL 已於 2024-12-31 廢除；實體賭場與經濟特區發牌業者為次要關注 |
| R5 | 更新頻率 | **雙軌**：每日 09:00 PHT 輕量掃描 + 週一 11:00 PHT 完整彙整 |
| R6 | 預算 | 全程使用免費工具與資源，不訂閱付費服務 |
| R7 | 形式 | 單一 HTML 檔，瀏覽器打開即用 |
| R8 | 視覺呈現 | **B 風格：現代業務說明化（類 Notion / Linear）**；卡片化、藥丸式標籤、scannable |
| R9 | 檔案架構 | **單檔多頁籤**：今日新增 / 月度檢視 / 全文搜尋 / 現行法規索引 |
| R10 | 排序規則 | 影響等級（高/中/低）× 急迫性（距生效或截止天數）雙維度；命中關鍵字提權 |
| R11 | 卡片互動 | 預設只顯示徽章、標題、副標、摘要；點擊展開原文引用區塊與所有 metadata |
| R12 | 語言 | **中文摘要 + 英文原文引用區塊 + 來源網址可一鍵跳轉**；條文編號、機關名、人名保留英文原文 |
| R13 | 內容份量 | 每日掃描 0–5 張新增卡片（無事則不刷）；週一彙整把過去 7 天歸整為 8–15 張重點卡 |
| R14 | 歷史保留 | **無限期保留**；按月分頁；全文搜尋可跨所有歷史 |
| R15 | 「現行法規索引頁」 | 獨立頁籤，常駐索引所有目前生效的法規（不按時間，按主題分類） |
| R16 | 風聲處理 | **同頁但明顯視覺區隔**：未證實傳聞用橘色邊框 + 浮水印「UNVERIFIED」+ 可信度標籤 |
| R17 | 徽章類型 | 影響等級【高/中/低】、狀態【草案/即將生效/已生效/廢止】、性質【執法/風聲】、來源【官方/媒體/業界】 |
| R18 | 合規名單追蹤 | 三類名單變動：DEGL/PIGO 持牌業者、Gaming Affiliates 認證名單、Support Providers 認證名單 |
| R19 | 關鍵字監控清單 | 預設 20 個關鍵字（見附錄 §10），使用者可在 HTML 頂部即時增刪；命中時提權 |
| R20 | 每日推播 | Cowork 對話訊息**三行以內極簡**：「今日 X 條新增、重點是 Y、點此查看」 |

---

## 2. 資料來源與蒐集策略

工具背後的「內容整理人」是 Claude。每日 09:00 PHT 與每週一 11:00 PHT 我自動執行以下流程。

### 2.1 每日輕量掃描（每日 09:00 PHT）

從以下來源掃描**過去 24 小時**有沒有新動態：

**A 層 — 必查（核心主管機關）**

1. **PAGCOR 官網**（最高優先）
   - 首頁公告：`www.pagcor.ph`
   - 法規區：`www.pagcor.ph/regulatory/`
   - 牌照名單：`www.pagcor.ph/regulatory/pdf/`（DEGL/PIGO、Affiliates、Support Providers）
2. **AMLC** — `www.amlc.gov.ph`（規則、Advisory、凍結名單）
3. **BIR** — `www.bir.gov.ph`（Revenue Regulations / Revenue Memorandum Circulars）
4. **BI（Bureau of Immigration）** — `immigration.gov.ph`（9G 工作簽證、SWP、外籍勞工政策）
5. **SEC** — `www.sec.gov.ph`（外資、合資、實質受益人揭露）

**B 層 — 建議查（業務拓展密切相關）**

6. **DOF（Department of Finance）** — `www.dof.gov.ph`
7. **DOJ** — `www.doj.gov.ph`（起訴、引渡、刑事行動）
8. **DICT / NPC** — `www.dict.gov.ph` / `www.privacy.gov.ph`
9. **DOLE** — `www.dole.gov.ph`（本地勞工配額、勞動條件）

**C 層 — 廣度查（政策訊號）**

10. **經濟特區管理局** — CEZA / APECO / AFAB（如各別有官網更新）
11. **BSP** — `www.bsp.gov.ph`（支付通路、加密貨幣、e-wallet）
12. **PNP / NBI** — 透過新聞而非官網
13. **Senate / House Bills 進度** — `legacy.senate.gov.ph` / `www.congress.gov.ph`
14. **Supreme Court rulings** — `sc.judiciary.gov.ph`

**新聞與業界媒體（每日掃，過濾關鍵字）**

15. Inquirer Business、Rappler、BusinessWorld、Manila Bulletin、PNA（Philippine News Agency）
16. **產業專業媒體**：AGB（Asia Gaming Brief）、GGRAsia、Inside Asian Gaming（IAG）
17. **業界社群 / 風聲來源**（僅限 Signal 類）：X（Twitter）搜尋 `PAGCOR`、`PIGO`、`POGO ban`；LinkedIn 業界圈

### 2.2 週一深度彙整（每週一 11:00 PHT）

- 把過去 7 天所有「Daily Add」重整：去重、合併同主題、補充背景
- 重點卡 8–15 張，按影響等級與急迫性排序
- 對「即將生效」「已生效不到 7 天」的條目重新評估並可能拉高優先級
- 對「風聲」做事實核查，若仍未證實則保留橘色徽章，若已被官方證實則升級為政策／執法卡

### 2.3 篩選與優先排序邏輯

**過濾規則**（先過濾再評分）

- 與菲律賓博彩 / 線上遊戲產業**直接相關**才收
- 純地方治安、純自然災害不收（除非影響特定 PIGO 業者運作）
- 純政治新聞不收（除非有具體政策提案）
- 重複報導同事件：只保留最權威來源（官方 > 主流媒體 > 業界媒體 > 社群）

**評分公式（用於排序）**

```
最終分數 = 影響等級分（1-100） × 急迫性係數 × 關鍵字命中加成

影響等級分：
  高 = 80-100（牌照、稅務、營運模式變動、AML 重大規則）
  中 = 50-79（廣告、人力、支付通路、認證流程）
  低 = 1-49（一般公告、技術細節）

急迫性係數：
  已生效 < 7 天 = 1.5
  即將生效 ≤ 30 天 = 1.3
  即將生效 31-90 天 = 1.1
  草案 / 提案中 = 1.0
  歷史背景 = 0.8

關鍵字命中加成：
  命中使用者關鍵字清單中 1 個 = ×1.1
  命中 2+ 個 = ×1.2
```

### 2.4 寫卡片內容

每張卡片寫：

- **中文標題**（25 字內，內含關鍵詞英文括號）
- **英文副標**（原文標題或文件正式名稱）
- **一行摘要**（40–60 字）
- **Key Changes**：相對於現狀的變更點（條列 2–4 條）
- **Impact**：對業者 / 投資人 / 合作夥伴的具體影響
- **Suggested Action**：建議行動（評估什麼、告知誰、留意什麼）
- **原文引用區塊**：1–3 段英文原文 + 條號 + 來源連結
- **Metadata**：發布機關、文件編號、生效日、影響領域標籤
- **可信度標籤**：官方 / 主流媒體 / 業界專業媒體 / 業界風聲

---

## 3. 卡片資料結構

```json
{
  "id": "20260522-001",
  "date_added": "2026-05-22",
  "month": "2026-05",
  "category": "policy",
  "title_zh": "PAGCOR 修訂 Gaming Affiliates 認證框架，強化 KYC 與廣告合規",
  "title_en": "Revised Accreditation Rules for Gaming Affiliates and Support Providers under PIGO Regime",
  "doc_number": "MC No. 2026-04",
  "issuing_authority": "PAGCOR",
  "doc_type": "Memorandum Circular",
  "summary": "PAGCOR 公告新版聯盟商 / 服務商認證規則，新增實質受益人揭露、廣告合規 60 天緩衝期，影響所有持牌業者推廣鏈。",
  "key_changes": [
    "所有 Affiliates 須申請正式認證，未認證者不得與持牌業者合作",
    "新增 beneficial ownership disclosure 要求",
    "廣告合規 60 天緩衝，逾期罰款 + 暫停合作關係",
    "Support Providers 同步適用新標準"
  ],
  "impact": "短期內所有 PIGO 持牌業者的廣告與聯盟通路需重新盤點；對未認證的聯盟商可能立即終止合作；廣告創意需重新審核以符合新標準。",
  "suggested_action": "1. 盤點現有 Affiliates 與 Support Providers 認證狀態  2. 法務評估 KYC 流程是否符合新規  3. 行銷團隊預備新版廣告審核 SOP",
  "impact_areas": ["licensing", "advertising", "aml", "kyc"],
  "impact_level": "high",
  "urgency": "effective_soon",
  "effective_date": "2026-06-15",
  "days_to_effective": 24,
  "badges": ["high_impact", "effective_soon"],
  "confidence": "official",
  "sources": [
    {
      "name": "PAGCOR 官網公告",
      "url": "https://www.pagcor.ph/regulatory/...",
      "type": "primary",
      "fetched_at": "2026-05-22T06:00:00+08:00"
    },
    {
      "name": "Chambers and Partners 解讀",
      "url": "https://chambers.com/articles/...",
      "type": "analysis",
      "fetched_at": "2026-05-22T06:05:00+08:00"
    }
  ],
  "original_quote": {
    "text": "All affiliates engaged by PAGCOR-licensed operators shall undergo accreditation, submit beneficial ownership disclosures, and comply with the revised advertising standards within sixty (60) days of effectivity.",
    "section": "§3(a)",
    "lang": "en"
  },
  "keywords_hit": ["PIGO", "Affiliates", "AML"],
  "heat_score": 92,
  "captured_at": "2026-05-22T06:00:00+08:00"
}
```

**欄位列舉值**

- `category`：`policy`（政策法規）/ `compliance_list`（合規名單）/ `enforcement`（執法動態）/ `signal`（政府風聲）
- `impact_level`：`high` / `medium` / `low`
- `urgency`：`in_force_new`（生效 < 7 天）/ `effective_soon`（即將生效 ≤ 30 天）/ `effective_later`（31–90 天）/ `draft` / `historical`
- `badges`：`high_impact`、`medium_impact`、`low_impact`、`draft`、`effective_soon`、`in_force`、`revoked`、`enforcement`、`unverified`
- `confidence`：`official`（官方原文）/ `mainstream_media`（主流媒體）/ `industry_media`（產業專業媒體）/ `industry_signal`（業界風聲，需明顯區隔）
- `impact_areas`：`licensing` / `taxation` / `aml` / `kyc` / `advertising` / `payments` / `foreign_workers` / `data_privacy` / `cross_border` / `enforcement` / `corporate_structure`
- `sources[].type`：`primary`（官方文件）/ `analysis`（解讀分析）/ `news`（新聞報導）/ `signal`（社群風聲）

---

## 4. 介面設計與互動

### 4.1 整體版面

```
┌──────────────────────────────────────────────────────────────────┐
│  菲律賓 PAGCOR 法規政策監測                       [🔄 重整]      │
│  2026-05-22 ｜ 今日新增 3 條，本月累計 47 條                     │
├──────────────────────────────────────────────────────────────────┤
│  [今日新增] [月度檢視 ▾] [🔍 全文搜尋] [📑 現行法規索引]          │
├──────────────────────────────────────────────────────────────────┤
│  關鍵字：[PIGO ✕] [DEGL ✕] [AMLC ✕] [+ 新增]                   │
├──────────────────────────────────────────────────────────────────┤
│  [全部] [政策] [合規名單] [執法] [風聲]                          │
│  [☐ 僅高影響] [☐ 僅即將生效] [☐ 含未證實風聲]                   │
├──────────────────────────────────────────────────────────────────┤
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ 🔴 高影響  🟠 D-24  政策法規  🟢 官方                    │  │
│  │ PAGCOR 修訂 Gaming Affiliates 認證框架⋯                  │  │
│  │ Revised Accreditation Rules · MC No. 2026-04             │  │
│  │ 新規要求認證+揭露受益人+60天合規緩衝⋯                    │  │
│  │ [PAGCOR] [2026-06-15 生效] [牌照·廣告·AML]              │  │
│  │                                          [▸ 展開]        │  │
│  └──────────────────────────────────────────────────────────┘  │
│  ⋯ 更多卡片 ⋯                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### 4.2 四個頁籤

1. **今日新增** — 今日掃描出的新卡片（時序由新到舊）
2. **月度檢視** — 下拉選擇月份，顯示該月所有卡片（按熱度分數排序）
3. **全文搜尋** — 搜尋框 + 結果列；可跨所有歷史月份；支援關鍵字、機關、文件編號、日期區間
4. **現行法規索引** — 不按時間，按主題分類列出所有「目前仍生效」的法規（牌照 / 稅務 / AML / 外籍勞工 / 廣告 / 支付 / 資料隱私）；每條一行 + 連到完整卡片

### 4.3 卡片狀態

**收合（預設）**：徽章列 + 中文標題 + 英文副標 + 一行摘要 + 三個 metadata 方塊 + 「▸ 展開」按鈕

**展開**：完整顯示所有欄位（Key Changes / Impact / Suggested Action / 原文引用區塊 / 所有 sources 連結）+「📋 複製全文」「📄 匯出 PDF」「🔼 收合」按鈕。所有 source 連結支援一鍵跳轉到原網址。

### 4.4 徽章與視覺區隔規則

**影響等級徽章（左到右閱讀優先級）**

| 徽章 | 顏色 | 意義 |
|---|---|---|
| 🔴 高影響 | 紅 #FCEBEB / #791F1F | 牌照、稅務、營運模式直接衝擊 |
| 🟡 中影響 | 黃 #FAEEDA / #633806 | 認證、廣告、人力相關 |
| ⚪ 低影響 | 灰 #F1EFE8 / #444441 | 一般公告 |

**狀態徽章**

| 徽章 | 顏色 | 意義 |
|---|---|---|
| 🟠 即將生效 D-NN | 橘 #FAEEDA / #633806 | 距生效 ≤ 30 天，顯示倒數 |
| 🟢 已生效 | 綠 #EAF3DE / #27500A | 已生效（< 90 天內標 NEW） |
| 🟡 草案 | 黃 #FAEEDA / #633806 | 提案中、草案、討論階段 |
| ⚫ 廢止 | 灰 #F1EFE8 / #444441 | 已被撤銷或取代 |

**性質徽章**

| 徽章 | 顏色 | 意義 |
|---|---|---|
| ⚖️ 執法 | 紅 #FCEBEB / #791F1F | 突襲、處分、撤照、罰款、起訴 |
| 🌬️ 風聲 | 橘 #FAEEDA / #633806 | 未證實傳聞（需特殊視覺處理，見下） |

**可信度徽章（小，置於卡片右側）**

| 徽章 | 顏色 | 意義 |
|---|---|---|
| 🟢 官方 | 綠 #EAF3DE / #27500A | PAGCOR 或其他主管機關官網 |
| 🔵 主流媒體 | 藍 #E6F1FB / #0C447C | Inquirer / Rappler / BusinessWorld 等 |
| 🟣 產業媒體 | 紫 #EEEDFE / #3C3489 | AGB / GGRAsia / IAG 等 |
| 🟠 業界風聲 | 橘 #FAEEDA / #633806 | X / LinkedIn / 業界論壇 |

**風聲（Signal）卡片的特殊視覺**

- 卡片有 **橘色 1px 左邊框 + 0.5px 全邊框**
- 卡片右上角顯示「UNVERIFIED」灰色浮水印（不影響閱讀）
- Metadata 區塊強制顯示「可信度：業界風聲」紅字
- 與官方政策卡片**完全不會視覺混淆**

### 4.5 篩選與切換

- **類別篩選**：政策 / 合規名單 / 執法 / 風聲（點「全部」回到不過濾）
- **快速篩選勾選**：「僅高影響」「僅即將生效」「含未證實風聲」（預設**不含風聲**，避免與官方混淆；勾選後才顯示）
- **關鍵字標籤**：頂部「關鍵字 chips 區」可即時增刪；命中關鍵字的卡片優先顯示，並在卡片內以底色高亮關鍵字
- **月度切換**：「月度檢視」頁籤下拉選單，按月跳轉
- **歷史月份檢視標示**：副標出現橘色「（檢視歷史月份）」字樣
- **重整按鈕禁用**：檢視歷史月份時「🔄 重整」按鈕自動變灰
- **手動重整**：點「🔄 重整」彈出小視窗：「請至 Cowork 對話對 Claude 說『請更新菲律賓 PAGCOR 法規政策』。點此複製指令到剪貼簿。」

### 4.6 視覺風格

- **整體**：B 風格（現代業務說明化），純白卡片 + 圓角藥丸標籤 + 充足留白
- **配色**：以白底 + 灰階為主，徽章使用語意色（紅/橘/綠/灰），不使用菲律賓國旗藍紅（避免與原話題工具混淆）
- **字型**：全 Sans-serif（系統默認思源黑體 / 微軟正黑體 / -apple-system）；英文原文引用區塊使用等寬字型（mono）以強調「這是引用原文」
- **響應式**：桌面 1024px+ 單欄寬卡片；手機尺寸亦可閱讀（metadata 方塊由 3 欄堆疊為 1 欄）
- **暗色模式**：v1 不做（與原工具一致），未來可加

---

## 5. 自動化排程

### 5.1 觸發時間

- **每日 09:00 PHT（UTC+8，等同 Asia/Taipei）**：輕量掃描 — `0 9 * * *`
- **每週一 11:00 PHT**：完整彙整與排序重整 — `0 11 * * 1`
- 您在台灣或新加坡時這些時間就是當地時間 09:00 / 11:00（同時區）
- Cowork App 在排程時間未開啟時，下次開啟補跑並通知

### 5.2 每日推播訊息格式（三行以內極簡）

```
📋 PAGCOR 今日 3 條新增｜🔴 1 條高影響｜重點：Gaming Affiliates 認證新規 (D-24)
👉 點此打開：菲律賓 PAGCOR 法規政策監測.html
```

若當日無新增：

```
📋 PAGCOR 今日無新增｜本月累計 47 條
```

若有【高影響】或【執法】類，自動在開頭加 🚨：

```
🚨 PAGCOR 今日 5 條新增｜🔴 3 條高影響｜重點：PIGO 牌照費調漲提案 (草案)
👉 點此打開：菲律賓 PAGCOR 法規政策監測.html
```

### 5.3 週一彙整訊息格式

```
✅ 本週菲律賓 PAGCOR 法規政策週報已更新

📅 期間：2026-05-18 ~ 2026-05-24
📊 共 12 張重點卡片（政策 5 / 合規名單 3 / 執法 2 / 風聲 2）
🔴 高影響：3 條
🟠 即將生效（30 天內）：2 條
🚨 執法行動：2 條

📋 重點 Top 3：
   1. PAGCOR 修訂 Gaming Affiliates 認證框架 (D-24)
   2. AMLC 公告新版博彩業可疑交易申報指南 (生效中)
   3. BI 收緊 9G 工作簽證審查 (D-7)

📑 現行法規索引頁已更新 2 條
👉 點此打開：菲律賓 PAGCOR 法規政策監測.html
```

### 5.4 失敗處理

- 任何來源 WebSearch / WebFetch 失敗：先重試 1 次
- 仍失敗：在 HTML 頂部顯示橘色橫幅「今日 X 個來源未能更新（[失敗來源清單]）」；**保留昨日內容不覆蓋**
- Cowork 對話同步通知失敗

### 5.5 手動觸發

隨時在 Cowork 對話對 Claude 說「請更新菲律賓 PAGCOR 法規政策」即可立刻執行同樣流程。也可指定範圍：

- 「請更新 PAGCOR 法規政策（僅 A 層主管機關）」
- 「請補抓過去 7 天的執法動態」
- 「請更新合規名單」

---

## 6. 檔案結構

放在您的工作資料夾：

```
菲律賓法規政策小工具/
├── 菲律賓 PAGCOR 法規政策監測.html       ← 主檔（單檔多頁籤，內含所有歷史）
├── 規格書_PAGCOR法規政策工具_v1.0.md     ← 本規格書
└── data/
    ├── 2026-05.json                       ← 月度資料檔（從 HTML 自動匯出備份）
    ├── 2026-04.json
    └── ⋯
```

說明：

- 主 HTML 檔自帶所有歷史資料（內嵌 JSON），單檔可攜
- `data/` 資料夾為自動備份，每月初由 Claude 從 HTML 提取上個月資料另存（避免 HTML 過大時資料遺失）
- 若您不需要 `data/` 備份，可告訴我移除這個機制

---

## 7. 技術實作要點

### 7.1 HTML 內部結構

```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>菲律賓 PAGCOR 法規政策監測</title>
  <style>/* 內嵌 CSS — B 風格設計 */</style>
</head>
<body>
  <header>
    <h1>菲律賓 PAGCOR 法規政策監測</h1>
    <div class="meta">2026-05-22 ｜ 今日 3 條 ｜ 本月 47 條</div>
    <button>🔄 重整</button>
  </header>
  <nav class="tabs">
    <button data-tab="today">今日新增</button>
    <button data-tab="monthly">月度檢視</button>
    <button data-tab="search">全文搜尋</button>
    <button data-tab="index">現行法規索引</button>
  </nav>
  <section class="keyword-chips"><!-- 關鍵字 chips --></section>
  <section class="filters"><!-- 類別/快速篩選 --></section>
  <main id="cards"></main>
  <script>
    const KEYWORDS = [ /* 預設關鍵字清單 */ ];
    const DATA = {
      "2026-05": [ /* 卡片陣列 */ ],
      "2026-04": [ /* 卡片陣列 */ ],
      ...
    };
    const ACTIVE_LAWS = [ /* 現行法規索引資料 */ ];
    /* 渲染、篩選、搜尋、互動 */
  </script>
</body>
</html>
```

### 7.2 為什麼選這種架構

- **單檔自給自足**：不需伺服器、不需 API、不需 CORS、不需 VPN
- **由 Claude 端整理資料、產出 HTML**：規避瀏覽器無法跨域抓取 PAGCOR 等政府網站的限制
- **資料內嵌而非外鏈**：即使所有來源網站全部下線，您手上 HTML 還能看到歷史內容
- **「複製到任何電腦都能用」**：把 HTML 寄給法務、主管或同事看，他們不需要任何安裝

### 7.3 不做的事（v1）

- 不做帳號登入 / 個人化
- 不做使用者自行加新卡片的功能
- 不做評論 / 收藏 / 分享功能
- 不做行動 App
- 不做後端伺服器
- 不串接任何付費法規資料庫（如 Westlaw、LexisNexis）
- 不做暗色模式（保留未來）
- 不做卡片版本歷史追蹤（同一條法規從草案到生效的多次修改僅以新卡片呈現，不做版本 diff 視覺化）

---

## 8. 上線後的維運注意事項

### 8.1 您需要做的事

- 每日打開 HTML（或閱讀 Cowork 推播）確認排程有跑
- 若連續兩日「內容品質不對」或「漏抓重要新規」，告訴我
- 每月初確認「現行法規索引頁」內容仍正確（會包含 Claude 自動偵測的「應從索引下架」清單供您確認）

### 8.2 我會做的事

- 每日 09:00 PHT 自動掃描；週一 11:00 PHT 完整彙整
- 任何來源失敗時主動通知
- 您回饋後調整來源權重與篩選邏輯

### 8.3 風險與限制

- **政府網站常更新慢或當機**：發生時保留前日內容並通知
- **業界風聲難以驗證**：v1 採「同頁但明顯區隔」策略；若您發現混淆，可改為「獨立分頁」
- **法規生效日的判讀**：菲律賓法規常有「公告日 / 簽署日 / 公布日 / 生效日」四種日期，工具以「Effectivity Date / Date of Effectivity」為準，無法判斷時標記「待確認」
- **PIGO 框架仍在演化中**：2026 PAGCOR 重組正在進行（商業與監管分拆），規則可能再變；本工具會即時跟上
- **語言邊界**：菲律賓法規偶有 Tagalog 用語，將以英文翻譯版為準

---

## 9. 未來可擴充項目（v1 不做）

| 項目 | 說明 | 預估難度 |
|---|---|---|
| 暗色模式 | 配合夜間閱讀 | 低 |
| 條文版本 diff | 同一法規從草案到生效的逐版差異視覺化 | 中 |
| 法規生效日曆 | 月曆視圖顯示未來 90 天所有生效 / 截止節點 | 中 |
| Email / Slack 推播 | 把 Cowork 訊息額外推到 Email / Slack | 中 |
| 多語言切換 | 中英雙語介面（給菲律賓本地同事看） | 中 |
| 條文交叉引用網 | 視覺化呈現新規與舊規、上位法之間的引用關係 | 高 |
| AI 諮詢入口 | 點某條規時直接喚出對話框問 Claude「對 X 業務情境有什麼影響」 | 中 |
| 競品 / 業界動態頁 | 整合 Solaire / Bloomberry 等業者公告為平行頁籤 | 中 |
| 自動匯出 PDF 週報 | 把週一彙整一鍵變 PDF 寄給主管 | 中 |
| 「警報設定」 | 自訂條件（如「PAGCOR + 高影響 + 即將生效」）達標時 Cowork 立即通知 | 中 |

---

## 10. 附錄：預設關鍵字監控清單（v1 起跑用）

工具上線時內建以下 20 個關鍵字，命中時提權排序。您可在 HTML 頂部即時增刪。

**牌照與框架**

1. `PIGO` / `Philippine Inland Gaming Operator`
2. `DEGL` / `Domestic Electronic Gaming License`
3. `PAGCOR license`
4. `accreditation` / `re-accreditation`

**業者類型**

5. `Gaming Affiliates`
6. `Support Providers`
7. `Junket`
8. `Service Provider`

**AML / KYC**

9. `AMLC`
10. `STR` / `Suspicious Transaction Report`
11. `beneficial ownership`
12. `KYC`

**稅務與財務**

13. `BIR ruling` / `Revenue Memorandum Circular`
14. `gaming tax` / `GGR tax`
15. `withholding tax`

**人力與簽證**

16. `9G visa`
17. `SWP` / `Special Work Permit`
18. `foreign worker`

**執法與處分**

19. `revocation` / `cancellation` / `suspension`
20. `raid` / `padlock` / `closure order`

**保留可擴充類別**（您可自行添加）

- 特定業者名稱（如 Bloomberry, Solaire, Okada, City of Dreams）
- 特定政治人物名稱（總統、PAGCOR 董事長、相關委員會主席）
- 特定地理區（Manila, Pampanga, Clark, CEZA, Cagayan）

---

## 11. 變更紀錄

| 版本 | 日期 | 變更 |
|---|---|---|
| v1.0 | 2026-05-22 | 首版規格書，與「菲律賓話題週報工具 v1.1」平行設計 |

---

*規格書版本 v1.0｜2026-05-22｜準備建置｜對齊輪數：4 輪 16 個問題*
