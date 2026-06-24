# AI 基礎設施筆記:功率半導體、CPO 光互連、GitHub AI 專案

> 來源:網路資訊圖(股海小英雄系列 7 張 + GitHub 週榜)+ 個人查證補充
> 整理日期:2026-06-24
> 註:股票/專案部分為產業鏈梳理與技術觀察,**非投資建議**。

---

## 一、功率半導體(MOSFET):為什麼從「成熟零件」變成搶貨賽道?

**核心邏輯一句話:電越猛 ≠ MOSFET 越多,而是「MOSFET 越搶」。**

### 1. 起點:AI 一代比一代吃電
- 單顆 GPU 功耗:B200 **1000W** → GB200 **2700W**
- 單一機櫃功率(3 年約 25 倍):Hopper 40kW → Blackwell 120kW → Kyber '27 **1MW**
- 真正卡關的不是算力,而是 **「怎麼把電送進晶片」**
- 電壓低(12V / 54V)→ 電流就得拉大 → 銅排上 I²R 損耗暴增、發熱嚴重
- 一座 1MW 機櫃,光 54V 銅排就吃掉 **≈ 200 公斤銅**
- 結論:不是銅比較差,是銅撐不住 → **只能把電壓往上拉**

### 2. 解法:把電壓一路往上拉(12V → 48V → 800V)
- **MOSFET = 電源電路裡的「精密開關」**,靠閘極(Gate)電壓控制電流通斷,
  負責升降壓、交直流轉換、過壓保護。屬於**主動元件(電力的調度者)**。
- 結構:源極 Source、閘極 Gate(+V)、汲極 Drain,閘極加電壓 → 通道 Channel 導通 → 電流通過。
- 階梯效益:
  - **12V → 48V(主流升級中):** 電壓×4、電流÷4 → 傳輸損耗降約 **16 倍**,單台伺服器 MOSFET 數量 ×2~3
  - **54V → 800V(2027 起):** 機櫃上看 MW,48V 也不夠;英飛凌 54V 已面臨容量瓶頸;NVIDIA「Kyber」2027 導入 800V,銅省 ~45%
- 結論:**每往上一階,就要塞進「更多顆」MOSFET**

### 3. 為什麼電越猛,MOSFET 反而越缺?
1. **數量↑**:48V 要更多級降壓,單台伺服器 MOSFET ×2~3
2. **單顆面積↑**:電壓拉到 800V / 1200V,高壓裸晶尺寸放大
- 結論:**電越猛 ≠ MOSFET 越多;電越猛 = MOSFET 越搶**

### 4. 製造卡在最老的 8 吋晶圓
- 物理事實:**耐壓越高,一片切得越少**(600V ≈ 上千顆/片 → 1200V ≈ 數百顆/片)
- 供給在縮 + 磁吸效應:
  - 台積電、三星削減成熟製程(2027 部分廠全停)
  - 全球 8 吋 2026 估 **−2.4%**、利用率衝 **90%+**、代工調漲 **5~20%**
  - 產能優先給高利潤 AI PMIC → **排擠其他功率元件,連車規一起被擠**
- 結論:功率元件從「平淡零件」**變成供需結構的根本翻轉**

### 5. 技術怎麼演化?兩條路
- **路線一|矽基「換結構」(這波主力):**
  平面 Planar(電流繞遠路,電阻高)→ 溝槽 Trench(挖溝直線,電阻更低)→ 超接面 SJ(P/N 柱,高壓也低電阻)
  → 導通電阻一路壓低
- **路線二|直接「換材料」(第三代半導體):**
  - **SiC 碳化矽**:高壓高功率(EV 800V、電網)
  - **GaN 氮化鎵**:高頻(二次側 DC-DC)
  - **Si 矽**:成本敏感的主力
- 為什麼難?① 吃 8 吋產能(高壓裸晶大,1200V 一片數百顆)② 認證週期長(車規/雲端,動輒以年計)③ 材料門檻高(SiC 生長慢、晶圓薄又脆)
- 結論:**不是 SiC/GaN 取代矽,是三者「各守生態位」、共存分工**

### 6. 相關台股(功率半導體供應鏈,非投資建議)

| 環節 | 定位 | 公司(代號) |
|------|------|------|
| **核心 IDM** | 自製晶圓=成本緩衝 | 強茂 2481、台半 5425 |
| **鄰段 Fabless / 設計** | 設計為主 | 廣閎科 6693、富鼎 8261、大中 6435、博盛 7712 |
| **賣鏟人** | 上游材料 / 8 吋代工 | 嘉晶 3016、世界先進 5347、漢磊 3707 |

---

## 二、延伸主題:CPO 共封裝光學(光互連)

**主題從「電怎麼進晶片」延伸到「資料怎麼用光送出去」。**

### 封裝垂直堆疊(上 → 下)
| 層 | 內容 | 角色 |
|----|------|------|
| GPU / Switch | 主晶片,旁有 **HBM** 高頻寬記憶體 | 算力與資料核心 |
| Interposer 中介層 | 高密度互連 | 晶片間的高速公路 |
| MCM 多晶片模組 | 整合多顆 die | 封裝基座 |
| PCB | 電路板 | 對外連接 |

- **互連層級(細→粗):** Hybrid bonding pad(混合鍵合)→ µbump → Bump / BGA Ball
- **光引擎三件套:**
  - EIC(Electronic IC):電子晶片,負責驅動與訊號處理
  - PIC(Photonic IC):光子晶片,電 ↔ 光轉換核心
  - FAU(Fiber Array Unit):光纖陣列,光的進出口
  - C2C(Chip-to-Chip):晶片間電互連介面
- **收發鏈路:** C2C → OE(光電轉換)→ 光纖 → OE → C2C,共 9 條 lane(lane0~8)
- **WDM 分波多工:** 每條 lane 各有一顆調變環(ring modulator),不同顏色=不同波長,
  同一根光纖同時跑多色光 → **頻寬倍增**

### 意義
把光引擎搬到 GPU 旁一起封裝,用光取代板上的銅走線 → **更低功耗/位元、更高頻寬密度、更短延遲**。
與第一部分「銅撐不住、要拉高電壓」是同一個物理困境的另一面(電互連的速度/距離/功耗瓶頸)。

---

## 三、GitHub AI 爆紅專案週榜(已逐一查證)

> 全部 7 個專案皆經 Web 查證為**真實存在**,資料截至 2026-06 中下旬。
> 主題集中在:**Agent 基礎設施、降本(token 壓縮)、聯網、MCP、安全**。

| # | 專案 | 作者 | 語言 | 一句話定位 |
|---|------|------|------|------|
| 1 | [ponytail](https://github.com/DietrichGebert/ponytail) | DietrichGebert | JS | 讓 AI agent「像最懶的資深工程師」,優先不寫程式(YAGNI/stdlib/原生)|
| 2 | [headroom](https://github.com/chopratejas/headroom) | chopratejas | Python | 工具輸出/日誌/RAG chunks 進 LLM 前先壓縮,省 60~95% token |
| 3 | [Agent-Reach](https://github.com/Panniantong/Agent-Reach) | Panniantong | Python | 給 agent 一雙眼睛讀網路(Twitter/Reddit/YT/GitHub/B站/小紅書),零 API 費 |
| 4 | [agent-skills](https://github.com/addyosmani/agent-skills) | addyosmani | (MD/Shell) | 生產級工程技能集合,把資深工程師流程包成 skill |
| 5 | [codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) | DeusData | C/Go | 代碼庫知識圖譜 MCP,毫秒級索引,158 語言,結構查詢省 ~99% token |
| 6 | [SkillSpector](https://github.com/NVIDIA/SkillSpector) | NVIDIA | Python | agent skills 安全掃描器,64 檢查/16 類別(prompt injection、外洩等)|
| 7 | [TimesFM](https://github.com/google-research/timesfm) | google-research | Python | 時序預測基礎模型(ICML 2024,零樣本預測)|

### 本週信號
1. **Agent 基礎設施仍在霸榜**(技能、記憶、聯網、安全全是 infra 層)
2. **降本是最熱方向**:token 壓縮(headroom)、知識圖譜省 token(codebase-memory-mcp)
3. **安全與工程化開始升溫**:NVIDIA SkillSpector 把「skill 供應鏈安全」搬上檯面

### 評估重點(詳見對話)
- **最具實用價值 / 可立即用**:headroom、codebase-memory-mcp、SkillSpector(都解真實痛點,有客觀指標)
- **概念價值高、效果視情況**:ponytail、agent-skills(prompt/skill 包,效益依任務而定,易複製)
- **有真本事但有依賴風險**:Agent-Reach(靠各平台非官方 CLI + cookie,平台一改可能失效)
- **最成熟、機構背書**:TimesFM(Google Research)、SkillSpector(NVIDIA)

---

## 待補
以下圖卡尚未讀到內容,之後補入:`15850 / 15852 / 15854 / 15856 / 15858 / 15860 / 15863`
