# verify-doc / Workslop Checker

[繁體中文 | [English (TODO)](README.md)]

> 判斷 AI 寫的文件能不能被人接手、使用、送出或拿來決策。
> 重點不是抓 AI，是防止 AI 產物把修正成本丟給接手者。

---

## 直接用（推薦）

點連結就能用，不用自己建：

**👉 https://chatgpt.com/g/g-6a0c5412dca48191be1632fac7523af4-verify-doc-workslop**

支援中英雙語對話，依你最近一句的語言自動切換輸出。

---

## 這工具解決什麼問題

**Workslop** 是 BetterUp Labs 與 Stanford Social Media Lab 在 [HBR 2025 年 9 月文章](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity)提出的詞，指「AI 產出的工作內容看起來完整、但缺乏實質、無法推進任務」。研究指出：

- 40% 員工過去一個月收過 workslop
- 每件平均修兩小時
- 每員工每月成本 $186（10,000 人公司每年 $9M）

這工具**不問「這是不是 AI 寫的」**（這問題很難回答而且回答了沒用）。
它問**「這份文件會不會把修正成本丟給接手者」**——能不能直接交、需不需要回工、有沒有藏起來的缺洞。

---

## 怎麼用

### 一般使用者（最簡單）

點上面 GPT 公開連結，把文件貼進去問「能不能用」。

### 用 Claude Code 的開發者

複製 `claude-skill/zh-TW/SKILL.md` 到你的 `~/.claude/skills/verify-doc/SKILL.md`，重啟 Claude Code，下次說「驗收這份文件」即可觸發。

### 想 fork / 客製化

見各語言子資料夾下的 README：
- [Claude skill 中文版](claude-skill/zh-TW/SKILL.md)
- [ChatGPT Custom GPT 中文版（含 Description / Starters / Instructions）](chatgpt-custom-gpt/zh-TW/README.md)
- 英文版（TODO）

---

## 適合用在

- AI 寫的報告、SOP、教案、提案、簡報文字、公告、會議紀錄、交接紀錄
- 想判斷文件能不能交出去 / 接手 / 做決策

## 不適合用在

- 對話品質檢查（每輪回答的好壞）
- 程式碼 review
- 聊天紀錄、便條、隨筆等非交付內容

---

## 結構

```
workslop-checker/
├── README.md                       # 英文版（TODO）
├── README.zh-TW.md                 # 本檔
├── LICENSE                         # CC-BY-4.0
├── claude-skill/
│   ├── en/SKILL.md                 # TODO
│   └── zh-TW/SKILL.md              # Claude Code skill 完整版
├── chatgpt-custom-gpt/
│   ├── en/README.md                # TODO
│   └── zh-TW/README.md             # ChatGPT Custom GPT 設定（含 source）
└── docs/
    ├── design-rationale.md         # 設計理由
    └── workslop-background.md      # workslop 出處與背景
```

---

## 反饋

遇到誤判歡迎開 issue：

- **False positive**：好文件被判 Red / Yellow
- **False negative**：workslop 被判 Green

請描述：文件特徵（類型、規模、來源）+ 工具判斷結果 + 你預期的判斷。

---

## License

[CC-BY-4.0](LICENSE)。允許商用、要求 attribution。

---

## Credits

- **Workslop 概念**：BetterUp Labs + Stanford Social Media Lab（[HBR 2025 原文](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity)）
- **設計**：[@shihchengwei-lab](https://github.com/shihchengwei-lab) 與 Claude / Codex 協作
