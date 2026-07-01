# job-hunt-copilot · 求职全流程助手（可开源 / 可托管 / 可随时改）

一个把求职自动化的项目：一个 **Claude Skill**（求职标准与流程）+ 一个**数据驱动的网页看板**（岗位追踪）。可放到 GitHub 开源、用 GitHub Pages 托管成固定网址、随时编辑优化。

## 目录结构
```
job-hunt-copilot/
├── SKILL.md              # 求职标准(候选人配置/五阶段/预筛规则/关键词/每日循环) —— 给 Claude 用
├── references/           # 各阶段详细方法
├── scripts/parse_resume.py
└── web/                  # 网页看板
    ├── index.html        # 指挥台(按行业分区/筛选/漏斗/状态追踪/复制打招呼语)
    └── jobs.js           # 岗位数据(window.JOBS_DATA) —— 编辑这个增删岗位
```

## 三种用法

### A. 直接本地用（最简单）
双击 `web/index.html` 用浏览器打开即可。状态存在本机浏览器(localStorage)。

### B. 托管成固定网页（GitHub Pages，免费、永久、可随时改）
1. 注册/登录 GitHub → New repository → 命名如 `job-hunt-copilot` → Create。
2. 上传本项目全部文件（网页版:Add file → Upload files → 拖入 → Commit；或用 git push）。
3. 仓库 → Settings → Pages → Build and deployment → Source 选 "Deploy from a branch" → Branch 选 `main` / 目录 `/ (root)` → Save。
4. 等 1-2 分钟，页面会给出网址：`https://<你的用户名>.github.io/job-hunt-copilot/web/`。这就是你的**固定网址**,手机电脑随时打开。
> 想要更短的根网址，可把 `web/` 里的文件移到仓库根目录。

### C. 作为 Claude Skill 用
把整个文件夹放进 Claude Code 的 skills 目录(如 `~/.claude/skills/job-hunt-copilot/`)，重启后说"帮我找工作/评估这个岗位/写打招呼语"即自动触发，按 `SKILL.md` 的标准跑。

## 随时修改优化
- **改岗位**：编辑 `web/jobs.js`（每个岗位一行，字段见文件注释）。托管版改完 commit 即更新。
- **改标准/赛道/薪资**：编辑 `SKILL.md` 顶部"候选人配置"块 + 预筛规则。
- **改界面**：编辑 `web/index.html`。
- 开源：仓库设为 Public 即可分享;别人改"候选人配置"就能复用。

## 每日自动收集（Claude in Chrome 定时任务）
让浏览器每早自动跑搜索、收集新岗位（**只收集不投递**）：
1. 装好 Claude in Chrome 扩展并登录 Boss。
2. 在扩展侧边栏跑一次 `references/browser-workflow.md` 里的收集 prompt，确认结果正确。
3. 点聊天顶部三个点 → **Convert to task**（字段自动填好）→ 打开 **Schedule** → 选 每天 + 时间 + 模型 → **Create shortcut**。（也可点扩展面板右上角**时钟图标**排程。）
4. 编辑/管理：扩展 → Settings → Shortcuts。
> 注意：定时任务仅在电脑唤醒且 Chrome 打开时运行；每次运行消耗套餐额度；先手动验证 prompt 再排程。

**每日循环**：定时任务收集新岗位 → 交给 Claude 打分+预筛 → 更新 `jobs.js` → 你在看板投一批、点状态、复制进展 → HR 回复发 Claude 精修应答。

## 边界（重要）
- 网页看板不会、也无法自动抓取 Boss（反爬 + 违反协议 + 浏览器跨域）。它是**持久的追踪 UI**;岗位数据经 `jobs.js` 每轮喂入。
- 不代填账号密码、不自动群发申请;投递/发送由本人确认。
- 详情页反爬会卡死,不硬刷(账号风控风险)。

## 借鉴
看板状态流、漏斗统计、跟进提醒、持久去重、逐岗定制思路，参考自 GitHub 上 JobApplicationWizard / jobtriage / VibeHired / AIHawk 等；**不采用**其自动群发投递（反爬封号风险）。
