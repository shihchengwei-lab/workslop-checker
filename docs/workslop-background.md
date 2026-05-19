# Workslop 背景

「Workslop」一詞是 BetterUp Labs 與 Stanford Social Media Lab 在 [HBR 2025 年 9 月發表的研究文章](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity) 中提出，後續延伸研究刊在 [HBR 2026 年 1 月](https://hbr.org/2026/01/why-people-create-ai-workslop-and-how-to-stop-it)。

## 定義

> "AI generated work content that masquerades as good work, but lacks the substance to meaningfully advance a given task."
>
> —— AI 產出的工作內容，看起來像好作品，但缺乏實質、無法真正推進任務。

詞源由 "AI Slop"（社群媒體上的低品質 AI 內容）延伸，但聚焦在「職場」場景。

## 研究數據

針對 1,150 名美國全職員工的調查：

- **40%** 過去一個月收過 workslop
- 每件 workslop 平均要 **2 小時**修正
- 每員工每月隱性成本 **$186**
- 10,000 人公司每年隱性成本 **$9M**

## 接手者常見遭遇

收到 workslop 文件後最常踩到的六種問題：

1. **責任不清**：沒列 owner、沒列截止時間、不知道誰要做什麼
2. **事實混在建議裡**：看不出哪些是已確認、哪些是 AI 推測
3. **缺少限制**：沒寫適用範圍、例外、不能做什麼
4. **過泛**：看起來有結構但拿掉公司名後可套用任何情境
5. **連結偽造**：引用看似專業但實際無法查證
6. **下一步空話**：寫「持續優化」「全面提升」但沒具體動作

## 為什麼「不抓 AI」？

`verify-doc` 跟 AI 偵測器（GPTZero 等）是**反方向**：

- AI 偵測器：問「這是不是 AI 寫的？」這問題難回答、且回答了也沒用
- workslop 視角：問「這份文件會不會把成本丟給接手者？」不管誰寫的、抓品質問題

人類寫的文件也可能是 workslop；AI 寫的文件也可能很好。重點是**接手者的隱性成本**。

## 相關報導

- [TechCrunch (2025-09-27): Beware co-workers who produce AI-generated 'workslop'](https://techcrunch.com/2025/09/27/beware-coworkers-who-produce-ai-generated-workslop/)
- [Axios (2025-09-24): AI "workslop" is crushing workplace efficiency, study finds](https://www.axios.com/2025/09/24/ai-workslop-workplace-efficiency-study)
- [Pivot to AI (2025-09-23): Workslop — bad 'study', but an excellent word](https://pivot-to-ai.com/2025/09/23/workslop-bad-study-but-an-excellent-word/) — 對原研究方法有質疑，但承認這個詞有用
- [Substack: Workslop and AI — Thomas Otter](https://thomasotter.substack.com/p/workslop)

## 這份 repo 為什麼基於這概念

`verify-doc / Workslop Checker` 把「workslop 接手者隱性成本」這個觀察具體化成檢查工具：

- 八類驗收（任務符合度／事實與來源／事實推測分離／完整性／可執行性／接手成本／語氣／風險邊界）對應上面六項常見問題
- 紅燈分硬／可修兩級，讓嚴重問題（敏感資料外洩、偽造引用）退回重做，但小問題（缺來源）只標 Fix 不一律 Red
- 文件類型 + 成熟度分流，避免「範本」「報告」「Action 文件」一視同仁

詳見 [design-rationale.md](design-rationale.md)。
