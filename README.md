# Psychotherapist OpenClaw Agent

面向心理咨询师、心理治疗师和督导工作的 OpenClaw Agent workspace。它可根据初访记录、咨询记录、治疗逐字稿、督导材料或报告草稿，辅助生成中文个案概念化、识别既有干预、分析治疗难点并规划后续干预。

## 目录结构

```text
psychotherapist/
├── AGENTS.md                 # Agent 总入口与强制规则
├── SOUL.md                   # Agent 人格与表达规范
├── IDENTITY.md               # Agent 展示身份
├── TOOLS.md                  # PDF 工具说明
├── USER.md                   # 本地用户偏好模板
├── HEARTBEAT.md              # 禁止主动扫描个案材料
├── guides/                   # 临床工作流与知识读取指南
├── knowledge/                # 个案概念化、干预、诊断和模板知识库
└── tools/pdf-analyzer/       # PDF 提取与 OCR 工具
```

## 安装 OpenClaw

Windows PowerShell：

```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
openclaw onboard --install-daemon
openclaw gateway status
```

## 注册 Agent

克隆仓库后，将其作为独立 workspace 注册。请把示例路径替换为实际绝对路径：

```powershell
git clone https://github.com/rikosellic/psychotherapist.git `
  "$HOME\.openclaw\workspace-psychotherapist"

openclaw agents add psychotherapist `
  --workspace "$HOME\.openclaw\workspace-psychotherapist" `
  --non-interactive

openclaw agents set-identity `
  --agent psychotherapist `
  --from-identity

openclaw agents list
```

如果 Agent 已经注册，修改 workspace 文件后通常只需开始新会话；修改 `IDENTITY.md` 后可再次执行 `agents set-identity`。

## 使用方式

可向 Agent 提供心理咨询记录、初访访谈、督导材料或个案报告草稿，并指定：

- 完整版报告；
- 简版概念化；
- 督导讨论版；
- 指定流派版（CBT、心理动力学、家庭系统等）；
- 干预指导版。

Agent 会先读取 `guides/` 中的工作流，再按照 L1 索引、L2 章节、必要时 L3 原文的顺序使用 `knowledge/`。

## 隐私与临床边界

- 不要把真实来访者身份、原始咨询记录、联系方式或其他敏感资料提交到版本库。
- 输出用于临床辅助和督导讨论，不替代持证专业人员的评估、诊断、伦理判断或危机处置。
- 涉及急性风险时，应优先执行现实世界中的风险评估、机构流程和当地紧急支持安排。
