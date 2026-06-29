# Resume Skill — 简历生成与美化

A Claude / Copilot **skill** that turns "I need a good-looking resume" into a stable, repeatable workflow:

> All inputs (existing resume, LinkedIn export, chat-style interview) flow into one **standardized structured data schema**, then render through a swappable template. Switching templates is just a skin change — content never gets lost.

把"我需要一份好看的简历"变成一条稳定流程：**所有素材先汇入一份标准化的结构化数据，再套模板渲染**。换模板只是换皮，内容不丢；美化和从零创建走的是同一条后半段。

---

## 三条第一原则

1. **绝不杜撰。** 所有经历、职责、数字必须来自用户真实提供的内容。可以引导、追问、把模糊说清楚、把弱 bullet 改强，但绝不编造公司、职位、成果或量化数字。任何数字都向用户求证，不确定就标 `[待确认]`。
2. **一次只问一个问题。** 对话式建简历是访谈不是问卷。问一个 → 等回答 → 顺着追问。
3. **先结构化，再渲染。** 不管入口是哪条，都先把内容整理成 `schema/resume-data.md` 定义的字段，确认无误后才套模板出 HTML。

---

## 三条入口

| 用户说的话 | 流程 | 脚本 |
|---|---|---|
| "帮我美化简历" / 上传了 PDF/docx/txt | **A. 美化已有简历** | [`prompts/beautify.md`](prompts/beautify.md) |
| "这是我的 LinkedIn" / 贴 linkedin.com 链接 | **B. LinkedIn 导入** | [`prompts/linkedin-import.md`](prompts/linkedin-import.md) |
| "帮我从零做一份" / "咱们聊一聊" | **C. 对话式建简历** | [`prompts/interview.md`](prompts/interview.md) |

三条入口最终都把数据汇入 [`schema/resume-data.md`](schema/resume-data.md)，再套模板渲染。

---

## 7 套模板

| 模板 | 文件 | 适合 | ATS |
|---|---|---|---|
| **Classic / ATS** | [`templates/classic-ats.html`](templates/classic-ats.html) | 单栏无花哨，机器可解析，大公司海投最稳 | ✅ 友好 |
| **Ledger 学术工程** | [`templates/ledger.html`](templates/ledger.html) | LaTeX 风衬线，两端对齐，嵌套子弹，软件/数据/工程岗 | ✅ 友好 |
| **Tech 紧凑** | [`templates/tech-compact.html`](templates/tech-compact.html) | 高信息密度+等宽点缀，多项目塞一页 | 🟡 尚可 |
| **Modern 侧栏** | [`templates/modern-sidebar.html`](templates/modern-sidebar.html) | 双栏+深色侧边栏，现代感强 | 🟡 一般 |
| **Pillar 信息卡** | [`templates/pillar.html`](templates/pillar.html) | Enhancv 风，蓝点缀+技能胶囊+图标成就，产品/市场/PM | 🟡 一般 |
| **Elegant 衬线** | [`templates/elegant-serif.html`](templates/elegant-serif.html) | 衬线居中编辑风，设计/咨询/市场 | 🟡 一般 |
| **Atelier 极简** | [`templates/atelier.html`](templates/atelier.html) | 大量留白+细字大写名+竖线分栏，设计/创意/审美岗 | 🟡 一般 |

**选模板提示**：海投/过机器筛 → Classic/ATS 或 Ledger；人直接看/内推/作品集向 → 其余几套更出彩。

---

## 用法

### 在 Claude Code / Claude.ai 里

把整个 `resume-skill/` 目录放到你的 skills 文件夹（如 `~/.claude/skills/resume-skill/`），然后直接说：

- "帮我美化这份简历"（附上 PDF）
- "我没有简历，咱们聊聊帮我做一份"
- "这是我的 LinkedIn，帮我建一份"

Claude 会读 `SKILL.md` 走对应流程。

### 在 VS Code / GitHub Copilot 里

把 `SKILL.md` 内容贴进 Copilot 的自定义指令，或者让 agent 读取这个仓库的 `SKILL.md` 作为流程指引。

### 输出

最终生成一个自包含的单文件 HTML（`<姓名>-resume-<模板>.html`），浏览器打开 → `Cmd+P` → 另存为 PDF → 边距 None/Default、勾选背景图形 → 保存。

---

## 目录结构

```
resume-skill/
├── SKILL.md                       # 流程总入口（必读）
├── schema/
│   └── resume-data.md             # 标准结构化字段（所有入口的中转格式）
├── prompts/
│   ├── beautify.md                # 入口 A：美化已有简历
│   ├── linkedin-import.md         # 入口 B：LinkedIn 导入与降级方案
│   └── interview.md               # 入口 C：对话式采集脚本
├── guides/
│   └── writing-tips.md            # bullet 写法、量化、ATS 关键词、常见错误
└── templates/                     # 7 套打印优化 HTML 模板
    ├── classic-ats.html
    ├── ledger.html
    ├── tech-compact.html
    ├── modern-sidebar.html
    ├── pillar.html
    ├── elegant-serif.html
    └── atelier.html
```

---

## 渲染时的硬规则

- **一页优先**：经验 <10 年控制在 1 页；资深可 2 页。
- **不动模板 CSS**：模板的版式/配色是设计好的，只替换内容文本。
- **空板块整块删**：没有的板块连同 `<section>` 一起删，不要留空标题。
- **真实数据**：placeholder 数字必须换成用户真实数据或 `[待确认]`，绝不留模板示例数字。
- **联系信息脱敏提醒**：要公开分享时，提醒电话/地址是否需要打码。

---

## License

MIT
