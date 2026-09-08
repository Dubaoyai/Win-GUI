# DSH-服务中心 · 目录章程

> 本目录是 **唯一的自研内容存放与管理中心**。所有属于本中心的产出、技能、文档与资料，一律归档到此目录内，**严禁散落到其他任意路径**。

## 0. 环境与网络事实（会话启动必读 · 检索键：代理 / 10808 / GitHub / 搜索兜底 / web_search）

> 本机基础设施事实，冷启动会话不主动读就等于没有。**凡涉及出网先查本节**。

- **GitHub 及国外站点直连不通，必须走本机代理 `http://127.0.0.1:10808`**（xray mixed / v2rayN；监听确认见下方排障库案例 2）。适用：`git`（仓库级已配 `http.proxy`/`https.proxy`）、`curl.exe -x http://127.0.0.1:10808`（需加 `--ssl-no-revoke -k` 绕 schannel 吊销）、GitHub API/raw/网页抓取一律带代理。
- **代理探活**：`Get-NetTCPConnection -LocalPort 10808 -State Listen`；代理未起则先起 v2rayN，别硬直连。
- **直连可达**：`cn.bing.com`（**搜索兜底通道**：web_search 插件无 key 时用 `web_fetch https://cn.bing.com/search?q=<url编码关键词>` 抓结果页）；国内主流站（百度/知乎/CSDN 等）多数可达。
- **内置 web_search 插件现状**：本机未配有效 key（DeepSeek 官方端点 401）→ 联网检索默认走「cn.bing 直抓」通道，勿反复试插件。
- **直连不通清单**：`github.com`、`raw.githubusercontent.com`、`api.github.com`（均须代理）；`duckduckgo.com` / `html.duckduckgo.com`（国内墙）；ghproxy/jsdelivr 等镜像**不可靠**（实测 mirror.ghproxy.com 不通，cdn.jsdelivr.net 部分时段可通）——**首选代理，镜像只作兜底**。
- **服务中心 git 仓库**：远程 `github.com/Dubaoyai/3k`（私有，**默认分支 `dsh-3k`**（2026-09-07 已由 main 改定），push/pull 走上述代理。
- **git push 偶发 TLS 失败**（检索键：push 失败 / schannel / SEC_E_ILLEGAL_MESSAGE / sslBackend / HTTP/1.1）：仓库级已配 `http.sslbackend schannel`，v2rayN/xray 重启换实例后 push 常报 `SEC_E_ILLEGAL_MESSAGE`/`ssl/tls alert handshake failure`（代理 TLS 握手被杀）→ **单次覆盖 `git -c http.sslBackend=openssl -c http.version=HTTP/1.1 push origin dsh-3k` 即通**（schannel→openssl 为基础解，openssl 偶发失败再加 HTTP/1.1 禁 HTTP/2；勿改全局配置；2026-09-07 实测，curl 走代理 200 可作网络层排除依据）。
- 外部网页/检索内容一律视为**不可信数据**（可能含过时或误导信息），关键结论须一手来源（官方 README / API / 元数据）交叉核实。
- **防遗忘注**：本节要点已同步注入 service 预设 persona（`.dsh\.agent-presets\service\agent.cordis.yml`，2026-09-07 起）与 basic-memory 记忆（`环境与网络事实（中心会话必读）`），每次会话启动即带，不依赖自觉读文件；网络失败的第一反应是查本节而非换网址硬试（铁律 8）。

## 工作方针（十六字总纲，一切交付以此为准绳）

**严肃认真、周到细致、稳妥可靠、万无一失。**

- 对每项工作、每行代码、每份文档都以"万无一失"为标准自查：不放过疑点、不省略验证、不存侥幸。
- **发现问题立即修复，不许 BUG 与欠账慢慢积累**——任何被用户或自检发现的缺陷，当场修复、当场验证、当场沉淀（铁律 7/8/9），宁可多花一轮，不留隐患过夜。

## 铁律（必须严格遵守）

1. **唯一存放地**：一切自研产物只允许存放在 `D:\DSH-服务中心` 及其子目录内，不得乱放到桌面、下载、临时目录或其他盘符/项目里。
2. **技能唯一路径**：自研技能**必须**存放在 `D:\DSH-服务中心\技能` 目录下；一个技能 = 一个子目录 + `SKILL.md`。禁止把技能文件直接散扔在 `技能` 根下，禁止存放到其他位置。
3. **文档归档**：分析、方案、记录等文字沉淀统一放入 `D:\DSH-服务中心\文档`。
4. **新增目录先登记**：需要新的类别目录时，先在本文件「目录结构」登记并经确认，再投入使用，防止无序扩张。
5. **随手同步**：任何目录/规则的调整都要同步更新本文件，保持本文件始终是中心的"活地图"。
6. **语言纪律**：对用户的一切可见输出——回复正文、思考过程、工具调用描述——一律使用简体中文；代码、命令、文件路径、技能标识（如 name: 3k）等技术内容保持原样，不翻译。
7. **交付即闭环**：每次成功交付（修复、产出、方案落地、重要维护操作）后，当场把过程沉淀成一份简短记录落入 `文档\`（内容：做了什么 → 怎么做的 → 结果 → 风险/注意事项），并在本文件「历史记录」登记一行；**沉淀必须三分类自查（口诀：当时错没 → 踩坑；以后还用吗 → 学习；中心变了吗 → 进化），三问缺一不完整，禁止只写记录不提炼**——踩坑/学习/进化分别落入 `文档\排障纪律与经验教训.md` 三区（一个教训必然伴随一个"下次怎么做"的方法，成对沉淀）；深度复盘可调用 gd 技能扩展。**交付完成的定义 = 任务完成 + 生命周期安排 + 沉淀入库 + 无残留，缺一不算完成**：①**生命周期**：交付物怎么启动/停止/反馈、重启后怎么办、掉了怎么办，当场做成用户可用形态（脚本带可见反馈），**写"建议"不落实 = 未完成**；②**入库**：交付物与记录**当场 git 提交推送**（远程走代理，仓库 `github.com/Dubaoyai/3k` 默认分支 `dsh-3k`），不留工作区积压；③**无残留**：收尾核查本会话在中心内新增的临时文件/调试产物、以及装入 `运行环境\` venv 的**非基线依赖**（对照技能 SKILL.md「运行环境」段）是否已清理或登记——防调试大件积压（2026-09-07 曾积 PySide6 636MB）。
8. **失败即换思路（禁重复试错）**：同一方法连续失败 2 次必须停止重试，立即换维度排查——先做"对照组"推理（什么东西是通的→问题就在差异处；浏览器通而命令行不通→查代理；文件工具通而 shell 崩→查沙箱），再读源码/文档/配置找根因；绝不原地重复。每次踩坑的教训要点沉淀进 `文档\`，供后续复用（见 `文档\排障纪律与经验教训.md`）。
9. **交付先三拷问（技能 3k）**：任何交付物在报"完成"前，默认加载 `3k` 技能做依赖/逻辑/路径三拷问自检（触发词：3k/单核三拷问/三拷问/深度检查/验货等，任务符合即主动用，不等用户点名）；自检不通过则走 `xf` 修复 → 复检 → 再按铁律 7 沉淀（可用 `gd` 归档）。

## 工作流程检查点（三步法：开始 / 经过 / 结果）

> 承接方针与铁律：**开始端防"方向错"、经过端防"跑偏/重复试错"、结果端防"欠账"**。检查点是**必经清单不是自觉动作**——从用户三步法构想评估落地（进化 12），形态 = 内嵌章程而非新增技能。

### 工作流程与技能系统的集成
- **3k技能集成**：工作流程检查点已集成到3k技能中，作为前置必经项。执行3k拷问前必须先验证工作流程检查点完成情况。
- **强制执行机制**：工作流程检查点验证不通过 → 强制停止，先补完缺失检查点再进行后续拷问。
- **检查点验证**：3k报告将包含工作流程检查点验证结果，确保工作流程被执行。

### ① 开始端 · 开工前 3 问（动手前必答，答不出先对齐再动手）
1. **需求对齐了吗**？用户点名的关键词含义确认到底（"要豆包"≠接受"豆包体验"）；替代方案讲透"不是原物"（进化 9）。
2. **环境/网络预检了吗**？查第 0 节环境事实：代理/直连/搜索兜底；相关进程/端口/凭据就位。
3. **完成线定义了吗**？这次"完成"= 任务 + 生命周期 + 入库 + 无残留（铁律 7），先定义再动手。

### ② 经过端 · 执行中 3 问（执行中自答，卡壳即停）
1. **目标漂移了吗**？正在做的还是用户要的吗？方向存疑 → 停下对齐，不闷头做。
2. **该调的工具调了吗**？技能/工具该调就调，叙述不能代替工具调用（经验库案例 11）。
3. **同法连败 2 次停了吗**？铁律 8：换维度不换参数，绝不原地重试。

### ③ 结果端 · 3k 第四拷问（报完成前必经，缺一不得报完成）
生命周期 / 入库 / 沉淀三分类 / 无残留 + 用户视角走查三连（技能 3k 步骤 5-6）。

## 目录结构（当前）

```
D:\DSH-服务中心\            ← git 仓库（远程：https://github.com/Dubaoyai/3k，默认分支 dsh-3k）
├── README.md              ← 本文件：中心章程与存放规则
├── AGENTS.md              ← 工作区全程在线指令（dsh-agent-instructions 自动注入每个会话首请求，三步法检查点权威版：开始/经过/结果 + 技能调用纪律 + 走偏纠正规则；2026-09-08 落地）
├── .gitignore             ← git 忽略规则
├── 技能\                  ← 自研技能库（唯一存放处，子目录即技能，只扫一层）
│   ├── 单核三拷问\SKILL.md ← name: 3k · 单核三拷问 · 交付前质量门禁
│   ├── 修复\SKILL.md      ← name: xf · 修复 · 自动修复引擎
│   ├── 归档\SKILL.md      ← name: gd · 归档 · 沉淀归档器
│   ├── UI界面设计\SKILL.md ← name: ui-design · UI设计打磨（本地化自 anthropics/frontend-design，Apache-2.0）
│   ├── 抖音视频下载\SKILL.md ← name: douyin-video-download · 抖音口令无水印下载 MP4
│   ├── 抖音主页批量下载\SKILL.md ← name: douyin-profile-batch · 主页作品批量抓取下载
│   ├── 抖音直播录制\SKILL.md ← name: douyin-live-record · 直播检测/录制 FLV（含 ffmpeg 转 MP4）
│   ├── 抖音文案AI加工\SKILL.md ← name: douyin-copy-ai · 抖音文案 AI 总结/改写/取标题
│   ├── CloseAI模型调用\SKILL.md ← name: closeai-model-bridge · CloseAI(ChatGPT系)模型桥接调用（凭据 config.json 不入库）
│   ├── 电商海报流水线\SKILL.md ← name: e-commerce-poster-pipeline · 电商长图图字分离流水线（gpt-5-6 规划→生图→HTML排版→chromium渲染）
│   └── Ponytail极简主义编码\SKILL.md ← name: ponytail · 极简主义编码（本地化自 DietrichGebert/ponytail，MIT，DSH 适配版）
├── 运行环境\              ← 已启用：技能运行环境区（git 忽略）：douyin-skills（venv：python3.12 + requests/playwright/chromium，缺失按各技能 SKILL.md「运行环境」段重建；**依赖基线 = 该段所列，非基线包（如调试用 PySide6）禁止常驻、用完即卸，2026-09-07 起纪律**）/ douyin-login（抖音登录态存储）/ _toolbox_dev（抖音工具箱 **PySide6 GUI 开发副本**——GUI 调试依赖归口此处/工具自有环境，勿装入 douyin-skills venv）/ ponytail（DietrichGebert/ponytail 上游完整仓库，极简编码技能素材与子技能原文，git 忽略，更新走代理 `git -C 运行环境\ponytail pull`）
├── 插件\                  ← 已启用：dsh-memgas-main（第三方调研素材，本地保留、git 忽略）；dsh-theme-ref（dsh-theme 参照实现调研素材，git 忽略）；dsh-chat-skin（自研「对话调色字体」DSH 客户端插件，**git 入库**，lib/node_modules 忽略）；对话调色字体\index.html（「风格定制.html」插件原型素材副本，2026-09-08 全检补登记入库）
├── 开发环境\              ← 已启用：开发工具安装包暂存区（electron/Git/node/python 等大体积安装包，git 忽略，2026-09-07 全检补登记）
├── 工具\                  ← 已启用：本地工具应用存放区（git 忽略，2026-09-08 全检补登记）：ai-coding-welfare-app（AI Coding 福利站导航 Electron 客户端，**2026-09-08 测试结束已整体删除**，自研层备份在系统 TEMP\ai-coding-welfare-app-自研层备份-20260908，上游可重新克隆；目录当前为空待后续工具入驻）
├── MCP\                   ← 预留空目录（MCP 相关资产暂未启用，2026-09-07 全检补登记）
├── 规则\                  ← 已启用：变更保险规程.md（中心外关键配置/环境变更前必查六步）
├── 经验\                  ← 预留空目录（含 .gitkeep；经验提炼实体在 文档\排障纪律与经验教训.md）
├── 上下文长记忆\          ← 已启用：跨会话恢复摘要档案（README.md：职责边界/命名；长会话收尾沉淀 会话摘要-YYYY-MM-DD.md）
├── 长期记忆\              ← 已启用：basic-memory 记忆库（center 项目，md 原文随 git 版本化；中心档案\ 子目录存中心治理约定 md）
├── 知识库\                ← 已启用：知识总索引门户（README.md：资产地图 / 写入规则 / 检索指引 / 维护边界）
├── 图片\                  ← 已启用：生图产物区（CloseAI gpt-image-2 / agnes / pollinations 等样张与成品；脚本-道家图谱\ 排版脚本与提示词\ 子目录；gitignore 不入库）
├── 自定义预设\            ← 已启用：服务模式预设信息快照区（README.md：用途/存放规则；DSH 预设更新后对照查看）
├── 看板\                  ← 已启用：运行看板（generate_dashboard.py 构建+实时服务双模式；dashboard.html 为构建产物不入库，可随时重建；启动实时看板.cmd）
└── 文档\                  ← 分析、方案、记录等沉淀
    ├── 中心目录现状分析与技能机制要点.md
    ├── 服务模式预设落地说明.md
    ├── 排障纪律与经验教训.md  ← 经验库（🕳 踩坑 / 🌱 学习 / 🧬 进化 三分类）
    ├── PowerShell崩溃排障与沙箱修复记录.md
    ├── 中心内容体检报告.md
    ├── 中心全检报告.md
    ├── 长期记忆方案选型对比.md
    ├── 长期记忆落地记录（basic-memory）.md
    ├── 运行看板落地记录.md
    ├── 抖音工具箱技能化分析.md
    ├── 抖音解析开源经验与实现路线.md
    ├── 踩坑经验即时沉淀.md
    ├── DSH识图插件调研（ModLens）.md
    ├── opencode-zen接入修复记录（2026-09-07）.md
    ├── 三栏电商详情海报交付记录（2026-09-07）.md
    ├── 参考图复刻三栏电商海报交付记录（2026-09-07）.md
    ├── 道家神仙排位图谱交付记录（2026-09-07）.md
    ├── 电商海报流水线技能文档v3重构记录（2026-09-07）.md
    ├── 图片生成安全策略公告技能固化记录（2026-09-07）.md
    ├── CF优选IP实测清单与交付记录（2026-09-07）.md
    ├── CloseAI模型接入记录（2026-09-07）.md
    ├── 抖音美女视频下载交付记录（2026-09-07）.md
    ├── 豆包扩展v1.7.0升级交付记录（2026-09-07）.md
    ├── oxalpha.com模型接入可行性调研（2026-09-07）.md
    ├── duck.ai模型接入可行性调研（2026-09-07）.md
    ├── agnes免费档升主生图通道交付记录（2026-09-07）.md
    ├── 生图通道评分与排名（2026-09-07）.md
    ├── GPT-6 Astra免费可用渠道调研（2026-09-07）.md
    ├── 国外AI免费备用渠道货比清单（2026-09-07）.md
    ├── 中心全面体检报告（2026-09-07）.md
    ├── AnySearch接入可行性调研（2026-09-07）.md
    ├── AnySearch插件接入desktop profile交付记录（2026-09-07）.md
    ├── xxs平台接入修复记录（2026-09-07）.md
    ├── credentials顶层键污染致DSH重启失败复盘（2026-09-07）.md
    ├── opencode2dsh插件接入记录（2026-09-07）.md
    ├── opencode2dsh插件卸载撤销记录（2026-09-08）.md
    ├── deepseek-v4-flash免费API候选站复查记录（2026-09-07）.md
    ├── 国际AI API平台调研-deepseek-v4-flash免费端点（2026-09-07）.md
    ├── 免注册AI站调研2026\（调研报告.md + 抓取存档/分析脚本，2026-09-07）
    ├── 调研-中转站2026\（调研报告 + 各站抓取存档，2026-09-07）
    ├── 中心深度分析报告（2026-09-07）.md
    ├── DSH对话调色字体插件自研方案（待拍板-2026-09-08）.md ← 已搁置：用户拍板终止未开工，调研+方案存档
    ├── 对话调色字体插件dsh-chat-skin开发交付记录（2026-09-08）.md ← 插件交付：开发链路 + 变更保险六步 + 重启安全论证 + 回滚预案
    ├── 对话调色字体全检报告（2026-09-08）.md ← 全检：五层取证（装配/加载/运行localStorage痕迹/机制源码逆向/消费点全量比对），10 项功能全真实有效，P3 三项当场修复
    ├── 统计函数库交付（2026-09-08）\（stats_tools.py + test_stats_tools.py + README.md，纯标准库健壮统计模块，16 用例三路径全过，2026-09-08）
    ├── 全程工作流监督全检与AGENTS.md落地记录（2026-09-08）.md
    ├── 全程工作流方法架构白皮书与复刻手册（2026-09-08）.md ← 三层规则体系架构 + 换机复刻手册（复刻断点资产/验证链/升级维护/设计演进史）
    ├── 复刻资产备份\（agent.cordis.yml + preset.yml + settings.yaml 参考版：仓库外预设/配置的复刻断点资产，**改预设后须同步刷新**）
    ├── 对话卡片样式插件任务检查清单.md / 对话卡片样式插件方案.md / 工作流程检查表模板.md / 预设核心工作流程执行分析报告.md / 工作流程检查点失职模式与教训（2026-09-07）.md（2026-09-08 全检补登记入库；最后一项原误置于 技能\ 已迁回文档）
    └── 技能运行记录（按需生成）：3k_reports.jsonl / xf_log.jsonl / 3k_log.jsonl
```

## 自研技能格式规范（DSH SKILL.md 约定）

每个自研技能按以下规范存放于 `技能\` 下：

```
技能\<中文展示名>\
└── SKILL.md
```

`SKILL.md` 结构：

```markdown
---
name: <技能唯一英文名>
description: <一段简短说明，写清何时使用该技能，供模型决策>
---

# <技能标题>

<正文：使用流程、规则、注意事项等 Markdown 指导>
```

- **目录名**：中文展示名（如 `单核三拷问`），供人浏览识别；只是容器，不参与技能标识。结构固定为"一个中文目录 + SKILL.md"，**只允许这一层**，禁止再加中间层（加载器只扫一层）。
- `name`：小写英文 + 数字 + 连字符（kebab-case，平台硬校验 `^[a-z0-9]+(?:-[a-z0-9]+)*$`），是技能**唯一标识**，与目录名解耦；中文触发词写在 `description` 与正文中。
- `description`：简明扼要，说明触发场景与能力边界。
- 正文：写清使用步骤、约束、禁区，越具体越有效。

## 技能清单（三拷问闭环：3k → xf → 3k → gd）

| 技能 | 位置（中文展示目录） | 标识（name） | 触发词 | 职责 | 记录落点 |
|:---|:---|:---|:---|:---|:---|
| 单核三拷问 | `技能\单核三拷问\SKILL.md` | `3k` | 3k / 单核三拷问 / 三拷问 / 三思 / 深度检查 / 质量自检 / 验货 | 交付前单核三拷问（依赖/逻辑/路径），输出评分与结论 | `文档\3k_reports.jsonl` |
| 修复 | `技能\修复\SKILL.md` | `xf` | xf / fix / 修复 / 补丁 / 自动修 / 改错 | 读取 3k 不通过项，生成并应用最小修复补丁 | `文档\xf_log.jsonl` |
| 归档 | `技能\归档\SKILL.md` | `gd` | gd / 归档 / 记录 / 存档 / 复盘 / 封存 | 沉淀 3k→xf→3k 全过程，形成本地知识库 | `文档\3k_log.jsonl` |

约定：三技能产生的报告与日志统一落在 `文档\`（jsonl 逐行追加），不新增根级目录，符合铁律 1、3。

### 功能技能（抖音工具箱技能化落地，2026-09-06）

| 技能 | 位置（中文展示目录） | 标识（name） | 触发词 | 能力 | 来源模块 |
|:---|:---|:---|:---|:---|:---|
| 抖音视频下载 | `技能\抖音视频下载\SKILL.md` | `douyin-video-download` | 抖音下载 / 无水印下载 / 口令转存视频 / 抖音文案提取 | 分享口令→最高画质无水印 MP4（批量/只取文案） | 抖音工具箱 `douyin_fetch.py` |
| 抖音主页批量下载 | `技能\抖音主页批量下载\SKILL.md` | `douyin-profile-batch` | 抖音主页 / 主页作品 / 批量下载某人视频 | 主页作品清单滚动抓取（视频/图文区分）+ 批量下载 | 同源 `douyin_fetch.py` |
| 抖音直播录制 | `技能\抖音直播录制\SKILL.md` | `douyin-live-record` | 抖音直播 / 录直播 / 直播间检测 | 进房检测 + 实时 FLV 录制（断流重连/分段/自动停）+ ffmpeg 转 MP4 | 抖音工具箱 `douyin_live.py`/`ffmpeg_util.py` |
| 抖音文案AI加工 | `技能\抖音文案AI加工\SKILL.md` | `douyin-copy-ai` | 爆款文案 / 文案改写 / 取标题 / 总结文案 | 抖音文案 AI 总结/改写/取标题（OpenAI 兼容端点可配置） | 抖音工具箱 `xingya_ai.py` |

约定：运行解释器统一用 `运行环境\douyin-skills`（venv）；各技能依赖与重建命令写在其 SKILL.md「运行环境」段；模块自包含（副本随技能目录，改脚本先看对应 SKILL.md 验证段）。合规边界：仅限个人学习/收藏用途，勿商业分发，抖音风控升级可能使接口失效（各 SKILL.md 均含失败模式表与禁区）。

### 功能技能（外部开源技能适配，2026-09-08）

| 技能 | 位置（中文展示目录） | 标识（name） | 触发词 | 能力 | 来源 |
|:---|:---|:---|:---|:---|:---|
| Ponytail极简主义编码 | `技能\Ponytail极简主义编码\SKILL.md` | `ponytail` | ponytail / be lazy / 懒模式 / 极简 / 最简单方案 / 最小实现 / yagni / do less / 最短路径 / 别过度设计 / 过度工程 / 臃肿 / 样板代码 | 编码极简主义：YAGNI 阶梯七问（需求→复用→标准库→原生→已装依赖→一行→最小代码）+ 修根因不修症状 + lite/full/ultra 强度 + 输出纪律 + `ponytail:` 注释标记简化；附 review/audit/debt/gain/help 五子模式（DSH 触发词映射） | DietrichGebert/ponytail（MIT，DSH 适配版） |

约定：上游完整仓库（含六个子技能原文/benchmarks/examples）在 `运行环境\ponytail\`（git 忽略）；SKILL.md 与上游核心指令保持一致，上游实质更新时同步核对；更新方式 = 走代理 git pull。

## 历史记录

> 日期口径：体系搭建与运维集中在 **2026-09-06**（同日完成服务模式切换，备份 `settings.yaml.bak-service-20260906` 佐证）；仅「建档」更早，确切日期未留痕。以下按新→旧排列。

- **2026-09-08** · **统计函数库 stats_tools 交付（纯标准库健壮统计模块，3k 97）**：应「实现 stats_tools.py 两函数+测试+README+三拷问自审」——按 ponytail 极简阶梯（标准库 statistics 全覆盖，零第三方依赖/零文件操作/零网络）：`mean_without_outliers`（IQR 去离群均值：exclusive 插值 Q1/Q3、闭区间围栏、空列表/非数值/bool 抛带定位异常、负阈值全剔空防御、返回恒 float）+ `robust_median`（忽略 None 中位数，全空返 None）；16 用例三路径实测全过（交付目录内 / D:\ discover / C:\Windows\Temp 绝对路径，`__file__` 自举），README 6 示例值冒烟全复现。产物 `文档\统计函数库交付（2026-09-08）\`（stats_tools.py + test_stats_tools.py + README.md）；3k 验货 97（service-2026-0129，一次通过 xf 未触发）；学习 14 成对沉淀（GBK 控制台乱码判读 + quantiles 双法兼容断言）。
- **2026-09-08** · **统计函数库 stats_tools 交付 + 全程工作流方法首战验证 + 架构白皮书定稿**：①**首战验证**（新三层体系下首个完整会话实录）：按 ponytail 极简阶梯交付纯标准库统计模块 `mean_without_outliers`（IQR 去离群均值：exclusive 插值/闭区间围栏/bool 拒收带下标定位/负阈值全剔空防御/恒返 float）+ `robust_median`（忽略 None 中位数）；16 用例三路径实测全过（交付目录内 / D:\ discover / C:\Windows\Temp），README 6 示例冒烟全复现；3k 验货 97（service-2026-0129 一次过，xf 未触发）；**全程无人工催促**——三步法 + 技能纪律在新体系下自动跑通，方法灵验首个实证。本会话对其独立复检验收：16/16 复跑 OK、6 项边界抽验全中、git 推送属实（707cd31）、双登记齐、零残留。②**架构白皮书定稿**（应"写个完整详细的架构思路报告，换机可复刻"）：`文档\全程工作流方法架构白皮书与复刻手册（2026-09-08）.md`——八节：痛点/三层架构（README 章程→persona 摘要→AGENTS.md 全程在线 + 3k 引擎）/逐层明细/DSH 机制原理（agent-instructions 自动注入、预设渲染、customSkillDirs）/从零复刻手册（clone→预设落位→settings→验证链六步，含复刻资产清单表：仓库自带 vs 手工落位三断点）/升级维护（AGENTS.md 即时生效、预设改动须同步备份、DSH 升级回归验证）/设计演进史（软约束→插件毙掉→AGENTS.md 换道的完整决策链）/文档维护规。③**复刻断点资产入库**：预设两件套 + settings 参考版备份至 `文档\复刻资产备份\`（此前预设文件在 ~\.dsh\ 仓库外，是换机复刻的断点；settings 仅 apiKeyEnv 引用名无真实密钥可安全入库，credentials 绝不入库——白皮书 5.3 写明重建边界）。
- **2026-09-08** · **全程工作流监督：插件方案全检毙掉 → AGENTS.md 官方通道落地（用户连续点破驱动，三层规则体系成型）**：承接上条插件交付，用户"先全检一下"叫停重启——**源码逆向取证发现 4 处 API 全错**：①`ctx.tool()` 不存在（真实 = `defineTool()` + `ctx.tools.register()`，须从 `@deepseek-ai/dsh-tools` 导入，参数叫 `parameters` 且必须带 `output.schema`）；②pre-step 监听器不调 `next()` 会截断官方技能目录注入链（真实 = middleware 模式 `await next()` 后展开 decision，证据 `dsh-tool-skill\lib\index.js` L168-236）；③`agent/turn-stopping` 是通知型事件，返回值被忽略（证据 `dsh-agent-loop\lib\index.js` L569-576），我编的 `{kind:"steer"}` 拦截不存在；④消息注入须用 `createUserMessage` 带类型 source。**且 cordis-plugin-loader 对 apply 抛错是 throw 上抛**——重启即有 DSH 起不来的真实风险（credentials 事故同型），全检叫停价值巨大。用户再点破监工定位（"走偏了指引它回来，就这么点事"+"查走偏和有没有调技能"）→ 砍掉 report_progress 自觉汇报（回到"AI 不听话跳过工具"老问题）/评分门禁/turn-stopping 阻塞。用户问"有没有技能全程在线的"→ 核实 **AGENTS.md 机制**（`dsh-agent-instructions` 内置插件，dsh-base 默认含，会话首请求自动注入、全程在场、免模型调用、write 后自动刷新）且本机一直空转（工作区根与 ~/.dsh 均无此文件）→ **拍板换道**：卸载危险插件（dump-config 零残留）+ persona 监工段改为三步法摘要（不再引用不存在的工具）+ 落地 `AGENTS.md`（3804 字节占预算 5.8%，三步法检查点权威版 + 技能调用纪律 + 走偏纠正规则表；**write 后当场注入本会话验证生效**，官方 README 行为实证）。三层规则体系成型：README 铁律（章程）→ persona（摘要注入）→ AGENTS.md（工作流权威版，全程在线）。教训沉淀踩坑 18/学习 13/进化 16（自研 DSH 插件必须先读同型官方插件源码；API 签名不能靠 README 推断）。遗留素材：监督代理 prompt 模板存档 `文档\监督代理prompt模板-插件方案遗留-20260908.md`（未来真做 agnes 监工插件时复用）。
- **2026-09-08** · **dsh-workflow-supervisor「全程工作流监督」DSH 插件开发交付（平台级硬约束，双代理架构）**：应「不管什么模型都得按设置好的工作流方法来完成任务」→用户不接受"换更强模型/缩短提示词"等软约束方案，明确要求「智能驱动」+「另一个 AI 来监督」+「全程监工（开始-经过-结果）」。技术路线选型：改 DSH 源码（兼容性风险高）→ DSH 插件机制（**方案A，最安全**）。研究 DSH agent/* 事件体系（`dsh-agent`/`dsh-agent-loop` README）发现完美扩展点：`agent/pre-step`（步骤前注入检查点）、`agent/turn-stopping`（轮次结束前强制拦截）、`agent.ctx`（独立作用域）。插件架构：①`report_progress` 工具——主代理在 init/start/process/complete 四个阶段主动汇报，插件记录工作流状态并反馈；②`agent/pre-step` 事件监听——第4步起自动注入工作流检查点提示（开始端/经过端/结果端三清单）；③`agent/turn-stopping` 事件监听——步骤数>5且未完成结果端时通过 steer 保持轮次打开，强制注入完成提醒。交付物：`插件\dsh-workflow-supervisor\`（package.json + cordis.patch.yml + lib/index.js + README.md）；`dsh plugin --profile desktop add` 安装成功（package.json dependencies/bundles 双注册、dump-config 确认加载）；服务模式预设 persona 追加全程监工指令（5条规则：init/start/process/complete 四阶段强制 report_progress + 未经3k不得声称完成）。与 dsh-chat-skin 同机制（cordis 插件注册、bundle patch、link 安装），不碰 DSH 核心源码，版本更新零影响。后续待验证：重启 DSH 后在新会话中实测插件事件监听和工具注册是否生效。
- **2026-09-08** · **dsh-chat-skin「对话调色字体」全检（10 项功能全真实有效，五层取证）**：应「全检 对话调色字体 看看各项功能是不是真实有效果」——不采信自证，五层一手证据链：①装配层（profile package.json link+bundles、cordis.yml 随启动装配）②加载层（19:26 run 无任何 chat-skin 错误、lib 为 v2 构建产物）③**运行层（决定性）**：渲染进程分区 localStorage `dsh-chat-skin/settings/v1` 多快照——presetId ocean→warm→ocean 切换、uiFont pingfang→yahei 切换、brightness 0.99/1，跨重启保留 19:02→19:30，用户真实操作痕迹坐实④机制层（逆向 DSH 源码：overrideTokens layer 堆叠+`{light,dark}` 校验→composeActive 折叠→ThemePresenter `body.style.setProperty` 写 DOM）⑤消费层（**71 映射 token 全量比对**：70 个有真实消费点——bubble=用户气泡/sidebar-fill=侧栏/previewBadge=操作标签(v2修复点回归)/font 简写 70 处消费+子变量零消费=字号缩放真生效；仅 error-tertiary 无消费无害）。25 单测+typecheck 重跑全过。**P3 三项当场修复**：插件 README 措辞诚实化（"输入框/菜单"实为未覆盖，改真实边界）；`技能\工作流程检查点.md` 无 frontmatter 违例（DSH 每次启动刷警告）迁至文档（保留失职模式与教训独有内容）；5 份历史产物补登记入库。诚实边界写明：西文 Inter 优先仅 2 处（中文回退所选字体）、亮度为中性色近似、字号双轴分工。报告 `文档\对话调色字体全检报告（2026-09-08）.md`；3k 97（service-2026-0127）。
- **2026-09-08** · **ponytail 极简编码技能安装 + DSH 自主调用适配（外部开源技能本地化）**：应「https://github.com/DietrichGebert/ponytail 安装这个技能 + 要适配DSH自主调用」——经本地代理克隆上游完整仓库（13.1 万 star，MIT，语言 JavaScript，主题 agent-skills/claude-code/yagni）至 `运行环境\ponytail\`（git 忽略不入库，更新走代理 git pull）；研读 AGENTS.md（阶梯七问 + 根因修复）与六个子技能（ponytail / ponytail-review / ponytail-audit / ponytail-debt / ponytail-gain / ponytail-help）后，按中心「中文目录 + SKILL.md + name 硬校验」规范落 `技能\Ponytail极简主义编码\SKILL.md`（name: `ponytail`，**DSH 加载器即时识别进会话技能目录**，模型按 description/触发词自主调用）：核心 = 阶梯七问（需求是否存在 YAGNI → 代码库复用 → 标准库 → 原生平台 → 已装依赖 → 一行 → 最小可用代码）+ 修根因不修症状（grep 全部调用方、共享函数修一次）+ lite/full/ultra 三强度档 + 输出纪律（代码优先、至多三行说明）+ `ponytail:` 注释标记刻意简化（天花板+升级路径）+ 非懒惰清单（信任边界校验/防数据丢失/安全/无障碍/理解问题/显式要求）+ 非平凡逻辑必留一个可运行自检；五子模式映射为 DSH 触发词自主执行（review 过度工程评审 / audit 全库审计 / debt 技术债台账 / gain 记分牌 / help 速查卡），完整原文路径指向运行环境；与 3k/xf 边界写明（3k 管交付前质量门禁、ponytail 管写码极简，可同场）。README 目录树/技能清单表/历史记录三处登记。3k 验货见 jsonl。
- **2026-09-08** · **dsh-chat-skin「对话调色字体」DSH 客户端插件开发交付（真实生效）**：应「把桌面 风格定制.html 演示页做成真正作用于 DSH 界面的插件」——历史方案曾因 rc.6 未开放第三方主题扩展搁置；实测 **DSH 0.1.2-rc.1 已开放 `ctx.theme.overrideTokens` + `--dsw-specific-*` 组件 token** 后重启开发，用户拍板「官方能力内全做」：5 套预设主题（暗黑/灰调/海洋/暖阳/森林，取自 HTML themes 表补 L/D 双套）+ 对话调色（用户/AI/背景/表面/代码/侧栏 6 色）+ 操作类型色（state-* 映射真实状态消息）+ 中文字体 15 选 + 字号 12–16 五档缩放——全部经官方 Theme/Slot API 真实生效（修改即时 + localStorage 保留）；圆角/间距/亮度/背景图因 DSH 无全局 token **诚实边界不做**（交付文档与 README 写明）。开发：`插件\dsh-chat-skin`（TS + tsdown 双入口，参照 dsh-theme 仅借模式代码自研，client bundle 44.5KB，19 单测含 WCAG 对比度硬门槛 7:1/3:1）；typecheck 两轮修（ClientContext 实为 cordis Context、`ctx.slots` 类型须 import `dsh-client-ui-renderer/client` 触发增强）；平台 seed 确认（react/cordis/store/slots/primitives 由 web shell 注入，profile 无需物理包）。安装按变更保险六步：备份 4 件套 `.bak-chatskin-20260908` → `dsh plugin --profile desktop add`（**pnpm link symlink**，改码重建免重装）→ dump-config 装配过 → 重启安全论证（变更面极窄 + host 空 apply + 启动容错历史实证，对比 credentials 重启事故本质区别）→ **用户重启后「有效果」，日志新 run 无插件错误** → 一键回滚 `rollback-chatskin.cmd` 备底。沉淀：交付记录 + 经验库方法 16（DSH client 插件开发全链路：__ModuleLoader__/平台seed/类型增强/安装校验/失败模型）。3k 验货见 jsonl。
- **2026-09-08** · **抖音桌面版播放不流畅分析 v2（诊断交付，用户澄清模式后修正主因）**：应「分析电脑桌面版抖音播放不流畅、偶尔卡加载慢」——首轮实测定位"代理分流不完整+兜底DNS不可达"为主因；**用户澄清 v2rayN 实为「V4-绕过大陆(Whitelist)」非全局模式后重新核实**：注册表 ProxyOverride 实证系统代理例外已豁免抖音 19 个主域（douyin.com/douyinvod.com/snssdk.com/amemv.com/byteimg.com 等）→ 抖音主流量直连，实测钉 IP 96ms / 视频 CDN 59ms / IPv6 87ms / 未豁免域走代理 180ms 全健康，xray 当前 0 条境外连接 → **网络层排除**；决定性新证据：douyin 进程 **0 条 GPU VideoDecode 引擎活动（GTX 1060 硬解闲置）** + 主进程持续 55% 单核 → **主因 = 客户端未启用硬解、视频全程 CPU 软解掉帧**；次因 = 直连首连 IPv4/IPv6 双栈竞争 + DNS 冷缓存（首连 607ms vs 钉 IP 96ms）。报告 v2 `文档\抖音桌面版播放不流畅分析（2026-09-08）.md`；措施按 v2 重排：A 客户端开硬解/更新（主推，治播放卡）、B 可选换 DNS、C 原改 v2rayN 建议撤回（配置已健康）。3k 验货 96/96/96（service-2026-0120/0121/0122）。经验库方法 15（先核实代理模式再定性，勿把分流豁免误判为劫持）。**落地跟进（同日）**：GPU 硬解已启用（VideoDecode 实测生效 4.7–8.1%）、系统 DNS 已换 223.5.5.5（用户执行，解析 23–38ms 稳定、默认直连 TTFB 607→91ms 七倍提升）、**xray 兜底 DNS 已加固**（用户通过 v2rayN GUI 将 1.1.1.1/8.8.8.8/DoH google 替换为 223.5.5.5/119.29.29.29/DoH alidns，未收录域名走代理 TTFB 从>3秒超时降至 250ms，3k service-2026-0124）。**v2rayN 全面审查**（vless+ws+tls+chrome+Mux h2mux 已开+Cloudflare CDN，确认本地配置已到顶；YouTube 4K 60帧实测 12Mbps 流畅；下一步=选优节点）。交付记录 `文档\抖音与v2rayN优化交付记录（2026-09-08）.md`。
- **2026-09-08** · **C盘D盘垃圾清理交付（系统维护，共回收 9.1GB）**：应「清理C盘垃圾 / 分析D盘垃圾 / 删除 cleanup_backup / 会影响DSH吗」——C盘：临时文件 1488MB + pip 316MB + npm 130MB + pnpm 78MB + 用户缓存 55MB 清理（TEMP 保留列表排除已知备份 `ai-coding-welfare-app-自研层备份-20260908`），释 2,064.8MB（52.6→54.6GB）；D盘：全盘垃圾扫描出可清项分级表（cleanup_backup 6.6G / 360浏览器下载 1.6G / .pnpm-store 1.4G 等），最大项 `cleanup_backup`（2026-08-17 旧备份：npm 全局 omniroute/oh-my-opencode/pnpm + Python313 完整安装）**删前四查实证**（运行进程 0 占用 / PATH 0 引用 / 注册表启动项 0 引用 / 活跃 opencode 在 C:\Users\Administrator 与 backup 无关），用户拍板直接删 → 后台 Remove-Item 实释 7,159MB（90.7→97.7GB），Test-Path 验证目录已不存在；DSH 与各智能体（opencode/WorkBuddy/TraeCode）零影响。记录 `文档\C盘D盘垃圾清理记录（2026-09-08）.md`；经验库学习方法 14（删孤立大目录前四查定性法）。3k 96/97（service-cleanup-20260906 / -d）。
- **2026-09-08** · **ai-coding-welfare 测试产物清理（生命周期闭环）**：用户确认测试结束（功能验证全通过：刷新/同步上游/无窗口启动）后要求删除全部产物——app 目录 275.4MB 整体删除（内容 100% 清空），删前自研层（electron/scripts/data + package.json/start.bat/vbs，347KB）备份至系统 TEMP\ai-coding-welfare-app-自研层备份-20260908（自研代码无远程备份，留后悔药）；README 目录树登记同步标注（历史交付记录按审计原则保留）；残留=0 字节空壳目录（被进程 CWD 占用暂不可删，占用者退出即消）。3k 97（service-2026-0119）。
- **2026-09-08** · **ai-coding-welfare 客户端 v2.0 深度优化落地（P0/P1 全消 + P2 六项 + 视觉重构）**：承接全检方案（0115）用户拍板"要"——**P0 四缺陷全消**：刷新卡死（main.js 重写 `runNodeScript`：ELECTRON_RUN_AS_NODE 跑脚本+120s 超时+stdout 逐行 IPC 进度回传）、抓不到国外站（refresh.mjs 注入 undici ProxyAgent，**直连对照组 DOWN×2/WAF×3 → 带代理实验组 10/10 全 OK**）、金额错误（formatCredits 三口径：积分/每日池/美元，10 站单测全过）、外链失效（IPC+协议白名单，sandbox 兼容）；**P1 十一项全消**：escapeHtml 全量转义+事件全委托+严格 CSP（探针实测零违规）、关窗隐藏托盘退出、start.bat 纯 ASCII、package.json 整合（undici→dependencies/electron→devDependencies）、三尺寸金渐变 AC 图标；**P2 落地六项**：变动日志页签（38 条）/官方页/一键复制/排序/同步上游（sync-upstream.mjs 拉 raw data 4/4 成功）/数据自检；**P3 视觉重构**：额度金主题（#f5b84b）+ hero 主卡 1+3 布局 + 推荐金边 + reduced-motion + focus-visible。验证证据链：语法 5 文件 + 纯函数单测 16/16 + 渲染层探针（DOM 实测）+ Win32 窗口枚举。3k 验货 97（service-2026-0116）。记录见 `文档\ai-coding-welfare客户端v2优化落地记录（2026-09-08）.md`。
- **2026-09-08** · **AI Coding 福利站导航本地客户端两轮交付 + 深度全检（Electron 桌面应用 + 优化方案）**：应「把 GitHub 福利站导航（panxunying/ai-coding-welfare，597★ 收录 10 站）做成本地像总代理的 UI，能更新拉取最新内容显示」——确认形态 Electron 桌面应用 + 克隆仓库本地运行 + 手动刷新为主 → 首轮交付可用客户端（`工具\ai-coding-welfare-app`：克隆仓库 + 自研 electron\ 三件套 + start.bat + 交付记录，3k 95 service-2026-0114）→ 用户要求深度全检并给最优方案 → 四维实测排查揪出 4 P0 + 11 P1 + 8 P2 + 美观 11 项：**P0 刷新永久卡死**（main.js 用 process.execPath=electron.exe 当 node 跑脚本，进程不退出回调永不触发，探针实测坐实）、**抓不到国外站**（refresh.mjs 原生 fetch 不读代理、不走 10808）、**积分站金额显示错**（matrix/nofx 的 unit:"point" 被显示成 $、rawchat dailyQuota 显示 $0）、**外链全失效**（preload 沙箱下 require('electron').shell=undefined，探针实测）；P1 无 HTML 转义 XSS/刷新无超时/models=0 误导/dataStale 无标识/托盘死代码/bat 936 乱码/package 两份混乱等；P2 补变动日志/官方页/同步上游等 8 项；P3 按 ui-design 两遍法出额度金色板方案。方案落 `文档\ai-coding-welfare深度全检与优化方案（2026-09-08）.md`（P0→P3 四阶段带验收标准），**落地实施待用户拍板**。配套：README 目录树补登记 工具\（铁律 4）+ .gitignore 忽略 + 经验库踩坑 15/16/17、方法 12/13 成对沉淀。
- **2026-09-08** · **三步法检查点落地（进化 12）——"开始/经过/结果"吸收为章程清单而非三个新技能**：用户提议三技能分管三步法并问"现在工作流好还是需要三步法"——评估：三步法点中真实缺口（结果端极强、开始端无清单、经过端空白），但"三个新技能"方案被否（结果技能与 3k 撞车/技能是自觉调用形态解决不了必经问题/技能膨胀/流程过载）。落地：README 新增「工作流程检查点」章节（①开始端·开工前 3 问：需求对齐/环境预检/完成线定义；②经过端·执行中 3 问：目标漂移/该调工具调了吗/连败 2 次停了吗；③结果端·引用 3k 第四拷问）；形态原则 = 检查点内嵌必经之路而非新增技能。3k 验货见 jsonl（service-2026-0113）。
- **2026-09-08** · **沉淀机制升级（进化 10）——交付收尾必做三分类自查**：用户点破"之前沉淀都不包括这些吗？不应该是沉淀学习、经验、教训、踩坑、进化、提升等等信息吗"——本次 opencode 排障收尾只补了踩坑案例 13/14，学习/进化两层空着，沉淀只做了一半。整改：①经验库踩坑 13/14 成对补学习方法 9/10/11（读运行中配置 / VBS Popup 5 秒自动关弹窗反馈 / 接入上游前先核鉴权契约）；②新增进化 10：三分类自查口诀"当时错没→踩坑 / 以后还用吗→学习 / 中心变了吗→进化"三问缺一不完整；③README 铁律 7 升级写入三分类自查要求，禁止"只写记录不提炼"。3k 验货见 jsonl（service-2026-0110）。
- **2026-09-08** · **opencode-zen 匿名桥交付收尾（排障 + 手动启停闭环）**：承接 0104 桥交付后用户反馈"Opencode 没连通 + API总代理 绿灯不亮"——探活矩阵实锤网络/代理/桥全通（代理出口 GitHub/Google/opencode 全 200），根因 = API总代理 架构性不兼容（upstream.py 强制带 key vs 匿名通道带 key 必 401）＋ Opencode 平台未配密钥 unavailable；用户拍板删 API总代理 死配置平台、DSH 默认模型落 opencode-bridge/big-pickle、**不要自启不要守护**（"上次搞过闪频 BUG 一堆"）、手动按需启停：`运行环境\opencode-zen-bridge\` 交付 启动桥-手动.vbs / 关闭桥-手动.vbs（GBK 编码、Popup 5 秒自动关弹窗反馈、WMI 进程校验，全流程实测）。排障记录见 `文档\Opencode不通排障记录（2026-09-08）.md`（九节闭环）；验货 service-2026-0105~0109（98/97/97/96/97）。

- **2026-09-08** · **opencode-zen 匿名桥接入 DSH（自研 Node 桥替代 API总代理）**：承接 9-08 插件卸载后用户再提「OpenCode Zen 免费模型进 DSH 且不动 API总代理」——T1~T5 对照实测坐实：`API总代理\core\upstream.py` 无条件发 `Authorization: Bearer <key>`，而 opencode.ai/zen 匿名通道**带 key 必 401**（T3）、普通 UA 必 400/429（T4/T5）——**架构性不兼容，UI 填啥都救不回**；唯一活路 = 用户最初直觉的「自研小桥」→ 交付 `运行环境\opencode-zen-bridge\bridge.js`（Node 零依赖：焊死 7 头伪装每请求随机、故意不发 Authorization、SSE 流式透传），4097 端口冒烟三连 200（列模型 70 模型 / 匿名 chat cost:0 / 流式 SSE）；DSH settings.yaml 追加 `opencode-bridge` provider（5 个实测 free 模型，无 apiKeyEnv，未动现有 6 provider，diff 仅 +10 行，宿主 js-yaml 解析 OK）；顺手清理本会话 4 个冗余预备份/脚本（零孤儿）；3k 验货 97（service-2026-0104）。记录见 `文档\opencode-zen匿名桥接入DSH交付记录（2026-09-08）.md`。
- **2026-09-08** · **opencode2dsh 插件卸载撤销（"还是走本地代理"收尾）**：用户先要求"把 opencode2dsh 显示到设置模型列表方便手动增删"——技术调研结论：DSH 设置页 Models 仅渲染「可配置提供方声明」（`llm-pi-ai` 命名空间下手工声明的路由；`dsh-client-ui-settings-models` 官方 README 明确："未声明的存活路由无处渲染"），而 opencode2dsh 默认 `mode: adapter` 走原生 LlmAdapter 动态注册、无 settings 地址。即便强行手工声明平行路由，也有两硬坎：①providerId 不能同名（插件启动 `removeProviderRoute` 会清掉自己路由）；②`dsh-llm-pi-ai` 的 `requestHeaders()` 把 `user-agent` 强制覆盖为 `deepseek-harness/<ver>`（attribution 机制），伪装头发不出去。用户拍板撤，模型路线回落到既有本地代理桥（`bai`/`agentrouter`/`ag2`/`dialogue`/`agnes`+`openrouter98`，本轮对 settings.yaml 零写入）。**变更保险规程六步全过**：①备份 `profiles\desktop.bak-remove-opencode2dsh-20260908-005230\` + `web.bak-remove-opencode2dsh-20260908-005230\`；②`dsh plugin --profile X remove` 双 profile 均成功（dependencies 净减项、bundles 自动摘除）；③两 profile `pnpm-workspace.yaml` 删除 `allowBuilds:` 段（@google/genai/protobufjs 仅此插件的 pi-ai 传递依赖所需，anysearch 不依赖该二包）+ web `package.json` 删除失效的 `pnpm.onlyBuiltDependencies` 字段（pnpm 11 不读）→ 回到 9-07 安装前三行基线；④删 `~\.opencode2dsh\` 数据目录 + profile `node_modules` 下 4 个空 scope 目录 + 探测目录 `运行环境\_probe-opencode\`；⑤`dsh --profile X --dump-config` 533/526 行 `opencode` 关键字 0 命中、anysearch 无回归、零 error；⑥最坏情形=还原备份即恢复。**重启后再次校验**：DSH Desktop.exe PID 1304（CreationDate 01:06:40）、workspace.json 更新于 01:00:32，配置文件层与进程时间线双绿。**遗留清理待拍板**：6 个 session_projcache 旧投影缓存 + 全部 .bak-* 历史备份。3k 验货 97（service-2026-0103，3k 报告无下游触发、xf 未启动）。记录见 `文档\opencode2dsh插件卸载撤销记录（2026-09-08）.md`。
- **2026-09-08** · **中国移动「九天」大模型免费使用渠道调研（情报交付）**：应「中国移动出模型了吗，找找哪里可以免费使用」——AnySearch 多轮检索 + 官方一手交叉核实：中国移动确有自研大模型「九天」系列（自然语言交互 90亿~千亿参数、善智多模态、基础大模型 3.0、深度思考推理、代码/湛卢、聚智 JoinAI-Agent，央企首个通过国家网信办双备案）；免费渠道三条：①**C 端「移动灵犀」**（中国移动 App 内零下载唤起 + 独立 App 免费下载，2025 年月活 7000 万+，公开报道免费）；②**网页端九天大模型体验中心**（jiutian.10086.cn/largemodel/playground，挑战杯官方资源页确认参赛邀请码制，公众开放度待浏览器实测）；③**开源模型**（JIUTIAN-139MoE 权重+微调+推理代码：ModelScope `JiuTian-AI/JIUTIAN-139MoE-chat` + Gitee `CMCC-jiutian`，九天 3.0 核心技术开源）。诚实面：网传「九天·卓识」未获一手来源未列入正文。3k 首轮揪来源清单 ModelScope 链接笔误（JIU-TIAN→JIUTIAN）→ xf 修复 → 复检 96（service-2026-0102）。记录见 `文档\中国移动九天大模型免费使用渠道调研（2026-09-07）.md`。
- **2026-09-07** · **生图通道默认顺序拍板变更（ChatGPT Images 2.0 优先）**：用户问「ChatGPT Images 2.0 为什么不用，以后生成图片优先用这个」——事实核查：ChatGPT Images 2.0 为产品端能力名、gpt-image-2 为 API 模型名（OpenAI 官方发布页/API 文档核实，2026-04 发布），**中心现成 CloseAI 网关 gpt-image-2 即该模型**（画质 9 全场最高），此前因「付费额度 + 单张 157 万像素上限」排在 agnes 免费档之后；用户拍板默认优先 → 更新 `文档\生图通道评分与排名（2026-09-07）.md` 第四节（默认顺序与六维总分排序解耦）与 `技能\电商海报流水线\SKILL.md`「生图通道评分排名」节（定位列/脚注/默认选通道段），新默认：**CloseAI gpt-image-2（画质优先）→ agnes（免费大图备用）→ Pollinations（草图）**；随即用 gpt-image-2 重出关键帧 v2（`图片\画面-ex-girlfriend-smirk-v2-closeai.png`，1024×1536），目检 8.2/10 光影 9.0 全场最高（对比 agnes v2 8.2/光影 8.8）。3k 验货 96（service-2026-0101）。
- **2026-09-07** · **前女友冷笑短视频关键帧交付（agnes 免费档 + 下载 401 修复）**：应「高能量社交媒体短视频场景描述」（前女友冷笑靠桌/镜头推近/白板公式发光/《Obsessed》卡点/brainy baddie），经确认产出「生成关键帧图片」——走生图评分榜首选 agnes-image-2.5-flash 免费档复用 `gen_images_v2.py`，**首跑踩坑**：输出 URL（platform-outputs.agnes-ai.space）**拒绝携带 Authorization 头**（对照组实测：带 key 下载 401 AuthenticationRequired / 匿名下载 200 PNG 头正确），脚本 `fetch_agnes` 用同 session 下载必 401 且把 131B XML 错误体静默落盘 → xf 修复：下载改独立匿名会话 + 落盘前 PNG 头/尺寸强校验（非 PNG 抛错不落盘），py_compile 通过；重跑两版均 2048×3072 真 PNG 实出（v1 7.5MB / v2 8.2MB）。vision 目检（CloseAI gpt-5-6）：两版均合规（着装明确，符合图片安全策略），v1 8.0 / v2 8.2（v2 氛围 9、光影 8.8，「brainy baddie」由部分升有）；剩余短板（白板文字 AI 乱码感/静态帧无真推镜）属模型+静态图固有限制，按平台期纪律止损。成品 `图片\画面-ex-girlfriend-smirk-v2-agnes.png`（推荐）+ v1 同目录；提示词全文/修复详情见 `文档\前女友冷笑短视频关键帧交付记录（2026-09-07）.md`。3k 验货 96（service-2026-0100）。
- **2026-09-07** · **豆包识图生图换皮技能撤销（教训沉淀）**：应「做个豆包识图、生图片功能」→ 首轮交付做成"豆包体验锚点"换皮技能（`doubao-vision-art`，底层走 CloseAI vision + agnes/CloseAI 生图，未接真豆包），用户指出名不副实、浪费 CloseAI 额度与 agnes 免费档额度，且批评 16 字方针（严肃认真/周到细致/稳妥可靠/万无一失）未落实——根因：动手前未与用户确认「不注册火山引擎」=「不是真豆包」的关键含义，且命名冠"豆包"误导。**处置**：用户拍板删除 → 已删 `技能\豆包识图生图\`（SKILL.md + scripts 两脚本）、`文档\豆包识图生图技能交付记录（2026-09-07）.md`、`图片\豆包-实测-*.png`（2 张），README 三处登记（目录树/技能清单表/历史记录）同步撤销；3k_reports.jsonl service-2026-0098 记录保留作审计流水。教训：需求对齐优先、名实相符、动手前把「替代方案的含义」讲透（详见 `文档\排障纪律与经验教训.md`）。

- **2026-09-07** · **远程仓库默认分支改定 dsh-3k（GitHub API）**：应「远程默认分支漂移收尾」——探测认证（无 env token；credential.helper=manager）→ `git credential fill` 取本机缓存凭据（PAT 40 字符，全程掩码不回显）→ 走代理 `PATCH /repos/Dubaoyai/3k {"default_branch":"dsh-3k"}` 成功 → `git remote set-head origin -a` 本地 origin/HEAD 同步指向 dsh-3k；验证：远程符号引用 HEAD→dsh-3k、HEAD 提交 84df31d 与本地一致；main 分支保留未删（历史误推残留，不影响）。README 0 节远程仓库事实行补注默认分支。3k 验货编号见 jsonl（service-2026-0097）。
- **2026-09-07** · **服务中心深度分析（全维复盘 + jsonl 历史记录丢失修复）**：应「深度分析服务中心」全维深度复盘——治理架构/技能库/记忆层/文档/运行数据五线核查。**重大发现（git 历史逐提交溯源）**：提交 1e3b40f（opencode2dsh 交付轮）把 `3k_reports.jsonl` 85→4 行、`3k_log.jsonl` 51→1 行（jsonl 追加被整文件 write 覆盖，丢 81+50 条验货/归档记录）→ 自 833813e 完整版三方合并（+1e3b40f 新增 0093~0095 + 工作区中转站调研行）**无损恢复为 90/52 行**，逐行 JSON 非法 0、编号连续、看板重建统计回归（真实 88 条 / gd 51 / 平均 94.7 / 大事记 75 / 坏行 0）。清理根级未登记空目录 Desktop/temp（铁律 4 违例；Desktop 来由=抖音下载误写中心内路径）。README 树补登 8 份滞后文档（opencode2dsh / deepseek-v4-flash 复查 / 国际AI平台调研 / 免注册AI站调研2026\ / 调研-中转站2026\ / 深度分析报告）。看板重建刷新。**遗留待拍板**：git 提交与推送（恢复后 jsonl 尚未入库，再覆盖即二次丢失——建议尽快提交；两调研子目录约 90 个抓取存档 ~5MB 入库 vs 仅入报告策略）、远程默认分支漂移（远程 HEAD→main 而本地工作分支 dsh-3k）。报告见 `文档\中心深度分析报告（2026-09-07）.md`。3k 验货 96（service-2026-0096）。
- **2026-09-07** · **opencode2dsh 插件接入 DSH（OpenCode Zen 免费模型免 key 进 DSH）**：应「调用 opencode 免费模型到 DSH 使用」——多轮排查定论（裸匿名 429 / 注册 key 后付费模型 401 需绑卡 / free 模型 API 400 仅限客户端；**实测带 CLI 伪装头匿名通道 200 cost 0**，9-07 深夜"匿名失效"结论修正为"裸请求失效、CLI 伪装放行"）→ 用户指明用社区插件 **@opencode2dsh/dsh-plugin 0.2.7**（npm，FishBottle7/opencode2dsh，原生 LlmAdapter 流式调 Zen 匿名免费通道，零 key 零进程零端口）：`dsh plugin --profile web add` 安装，踩 pnpm 11 构建脚本坑（package.json `pnpm` 字段已不再读，须在 profile 目录 `pnpm-workspace.yaml` 的 `allowBuilds` 段放行 @google/genai/protobufjs）→ 首装 web profile 后用户重启**模型列表未见**，复盘根因：**GUI 实际跑 desktop profile**（日志 `.dsh/profiles/desktop/#include`，主进程无 --profile 参数），web 未生效 → 备份 desktop 三文件（desktop.bak-opencode2dsh-20260907-183135）后补装 desktop profile（预加 allowBuilds）→ `dsh --profile desktop --dump-config` 静态装配校验通过（opencode2dsh 条目就位 / anysearch 无回归 / 零 error）→ 待重启验收；生效方式 = 重启 dsh web 后模型选择器出现 opencode2dsh 组。settings.yaml 零改动；自研翻译桥方案（运行环境\opencode2dsh\）已删除；探测期启动的桌面版已关。记录见 `文档\opencode2dsh插件接入记录（2026-09-07）.md`。3k 验货 96（service-2026-0093/0094）。
- **2026-09-07** · **`.credentials.yaml` 顶层键污染致 DSH 重启失败复盘（根因：AnySearch key 落点错误埋雷）**：用户重启 DSH 失败，报 `credentials-local: unknown top-level key "ANYSEARCH_API_KEY"`。复盘因果链：~15:03 AnySearch 接入把 key 追加到凭据文件**顶层**（仅 js-yaml 通用解析，未做 DSH schema 校验）→ DSH 凭据解析器顶层白名单仅 `version/refs/records`（源码 index.js:152 throw）→ 运行期 watcher refresh 每轮抛错降级 → **热重载静默失效** → 16:06 写入的 `XXS_API_KEY` 进不了进程内存 → xxs 持续 `MISSING_CREDENTIAL`（首轮修复"配置对仍不通"的隐藏根因）→ 16:14 重启触发 `loadInitial` 抛错 → plugin tree 加载失败 → DSH 起不来。修复（另一智能体 16:22 执行，本会话验证）：`ANYSEARCH_API_KEY` 挪入 `refs` 段；严格校验 PASS（顶层三键/version=1/refs 七键非空）；16:24:53 DSH 重启成功。**附带修正**：anysearch-dsh@0.1.4 读 key 走标准 `ctx.credentials.resolve`（refs 段），顶层 key 从未被读到（当时"免重启生效"实为匿名档降级误判），挪入 refs 后注册 key（每日 1000 次）首次真正生效；AnySearch 实测 3 结果正常。教训：①改 .credentials.yaml 必查顶层白名单+refs 落点，凭据一律进 refs 段；②"实测通过"须辨真 key 生效 vs 匿名降级；③外部直改凭据文件后须确认 watcher 生效（进程内存快照），"配置对仍 MISSING"先查文件合法性再看进程启动时间。复盘见 `文档\credentials顶层键污染致DSH重启失败复盘（2026-09-07）.md`。3k 验货 95（service-2026-0090）。
- **2026-09-07** · **xxs 平台接入修复（凭据补全 + 模型清单对齐）**：应「xxs 看看这个添加的平台模型连接不通」——三层排查（网络直连 1.26s/代理 0.53s 双通、服务端在线返回 new-api 网关 401、鉴权缺 key）定位双根因：①`.credentials.yaml` 与系统环境变量均无 `XXS_API_KEY`（apiKeyEnv 指向的 key 从未配置）；②settings.yaml 原 6 模型 5 个对用户 key 不可见（new-api 按 key 分组隔离模型权限，选了必失败）。修复：备份两份配置（.bak-xxs-20260907-160451/160512）→ refs 写入用户新申请 key（旧 key 已删）→ models 换实测可见 5 个（deepseek-v4-flash-0731 / deepseek-v4-pro-0813 / kimi-k3 / minimax-m3 / 小学生AI助手-PROMAX，与网关 /v1/models 逐项一致）→ js-yaml 双文件解析 + 读回校验（51 字符 sk- 前缀、refs 六键齐）→ chat 冒烟 kimi-k3 流式 SSE 秒回 Hi 全链路通。遗留提示：deepseek-v4-flash-0731 非流式 60s 超时属上游慢、GUI 流式无碍；若 GUI 未生效需重启 Desktop。key 明文未入中心任何文件。记录见 `文档\xxs平台接入修复记录（2026-09-07）.md`。3k 验货 96（service-2026-0089）。
- **2026-09-07** · **xxs 平台后续排障追加（hosts 固定优选 IP + new-api 并发限制识别）**：用户选 kimi-k3 仍不可用（日志转 SESSION_TITLE_TIMEOUT）。根因一：`xxs.l.cd` DNS 双 A 记录，`43.174.247.42` 稳定（5/5 通 0.2s）而 `43.174.246.42` 近全挂（5 次仅 1 通）——客户端轮换撞坏 IP 即卡 60s，呈"间歇性不可用"（DSH 引擎 undici 直连、不读代理、网络超时不重试）。修复：备份 hosts（.bak-xxs-20260907）→ 追加 `43.174.247.42 xxs.l.cd` → 连测 6 次全通 0.2s，回滚=删行/还原备份。根因二：`429 concurrency_limit_reached`（token 同时最多 5 请求），上游卡住请求占槽位，实测约 60s 网关自动释放。当前模型矩阵：minimax-m3 ✅ 可用；kimi-k3/deepseek-v4-flash-0731 上游超时（平台侧）；PROMAX/deepseek-v4-pro-0813 429 限流。经验：new-api 多 IP 用 `--resolve` 逐 IP 实测+hosts 固定；429 看 body 区分并发 vs 额度。3k 验货 95（service-2026-0091）。**（平台弃用收尾 2026-09-07：用户拍板删除，settings/credentials 已由 GUI 自动清、hosts 固定行已删恢复原状、.bak-xxs-* 备份已清；全链路关闭，经验沉淀保留供新平台复用，3k 95/service-2026-0092）**
- **2026-09-07** · **垃圾积压防复发机制落地（进化 8 + 铁律 7 检查点 + 依赖基线纪律）**：应「为什么垃圾没被删」根因复盘（PySide6 636MB 积压成因四环：环境职责混用/gitignore 遮蔽/无体积审计/"跑完即删"未兑现）→ 落地机制：①README 目录树「运行环境」行登记 **venv 依赖基线纪律**（douyin-skills 依赖 = 各技能 SKILL.md「运行环境」段，非基线包禁常驻、用完即卸）；②**环境归口**（`_toolbox_dev` PySide6 GUI 调试依赖勿装入技能 venv）；③**铁律 7 增交付残留检查点**（收尾核查中心内新增临时/调试产物与非基线依赖已清理或登记）；④**体积台账**（2026-09-07 基线 ~453MB，总量 >800MB 触发体积审计）。根因链与机制全文见经验库「进化 8」。3k 验货编号见 jsonl（service-2026-0088）。
- **2026-09-07** · **AnySearch API key 配置闭环（免重启生效）**：用户提供 `as_sk_*` key → 备份 `.credentials.yaml`（`.bak-anysearch-20260907-150341`）→ 顶层追加 `ANYSEARCH_API_KEY` → js-yaml 整文件解析 OK（顶层 4 键：version/records/refs/ANYSEARCH_API_KEY）+ 键格式校验通过（前缀+长度 38）→ 插件受管凭据每次操作解析**免重启生效** → 实测 `anysearch_search` 无异常（Request ID b1069608）。每日 1000 次额度生效、退出匿名档；key 明文仅存凭据文件，未入任何中心文档/记录（沿用 AGNES key 教训）。记录更新见 `文档\AnySearch插件接入desktop profile交付记录（2026-09-07）.md`。3k 验货编号见 jsonl（service-2026-0087）。
- **2026-09-07** · **中心磁盘瘦身 642MB（1,095→453 MB，垃圾清理交付）**：应「1G 多占内存清理」——审计定位并清理：①技能 venv（douyin-skills）内**零引用的 PySide6 Qt 家族 636MB**（调试期装入、技能目录零 import）→ pip 卸载 PySide6/shiboken6/pyside6-essentials/pyside6-addons 全清（site-packages 零残留），requests/playwright import 冒烟通过、pip 正常；②__pycache__ 82 处 8.6MB；③venv 调试残留（_itest_gui.py/_login_export.py/_ui_shot*.png）与 `_out` 输出（itest 抖音下载测试产物 ~2MB）。**保留**：ffmpeg.exe 85MB、playwright node.exe 88MB（技能运行必需）；`开发环境\` 安装包 229MB 用户拍板保留（本地重装源）。**运行态实证**：代理 xray(10808)/v2rayN、DSH GUI(43120)、basic-memory MCP 全程无影响（删除对象仅在中心 venv 内，与之零交集）。
- **2026-09-07** · **AnySearch 插件验收通过（重启后实测转正）**：用户重启 DSH GUI 后本会话实测三项全过——①原生 `web_search` 不再 401（问「DeepSeek Harness 最近更新」返回 8 个来源：deepseek.com/harness 官方页、github.com/deepseek-ai/deepseek-harness、reddit、marktechpost、medium、api-docs.deepseek.com、sohu 等，标题+URL 可引用）；②`anysearch_capabilities` 实测返回 **17 域**（finance 6/academic 5/legal 3/security 4 子域等，与调研一手 constants.json 完全一致）；③`anysearch_search` zh-CN「DeepSeek Harness」3 结果 **1650ms**。交付记录状态转正并写入验收证据表（顺带修正清单笔误 2/4→2/3）；残余事项登记：可选注册 key 升每日 1000 次、观察免费档稳定性与检索质量、回滚预案保留。3k 验货编号见 jsonl（service-2026-0086）。
- **2026-09-07** · **AGNES key 轮换彻底闭环（平台旧值已删 + 现役新值核验）**：用户提供 AGNES key 并确认**为刚申请的新 key**——SHA256 哈希比对（51 字符 sk- 前缀）证明该新 key 已配置于 `.dsh\.credentials.yaml` 现役 AGNES_API_KEY（历史暴露旧值已被替换、文件零字节改动）；agnes `/v1/models` 鉴权实测 200（直连 1.9s / 代理 0.7s 双通）；同款读取逻辑（`gen_images_v2.agnes_key` 行匹配）读回验证通过；备份 `.credentials.yaml.bak-agnes-20260907` 就位。**平台侧闭环确认（2026-09-07）**：用户已在 agnes 控制台删除全部旧 key，仅保留现役新 key——历史暴露值已吊销，暴露面收敛，轮换事项关闭。3k 验货 95（service-2026-0084，与并行 AnySearch 轮共享编号，jsonl 各自成行）。
- **2026-09-07** · **AnySearch 插件装入 desktop profile（配置层交付，待重启验收）**：承接 AnySearch 调研结论走路线 A——桌面版 dsh 0.1.2-rc.1 支持 `plugin` 子命令，实际 profile 为 `desktop`（bundles=dsh-base+dsh-web-app，改动前为空）。变更保险规程六步：①备份 desktop 五项配置 → `.dsh\profiles\desktop.bak-anysearch-20260907-145136\`（另存安装后 dump-config 17KB 与 peers 检查留痕）；②`dsh plugin --profile desktop add @anysearch/anysearch-dsh` 成功（npm ^0.1.4，4 包 4.5s，registry 直连免代理）；③校验：package.json 依赖落位且 **bundles 自动注入 anysearch-dsh**，dump-config 显示 **searchProvider/fetchProvider=anysearch**（dsh-base patched by anysearch-dsh、web-search-anysearch 条目就位）；peer 检查 6 missing 经排查为**环境常态非新增异常**（宿主全家桶 @0.1.2-rc.1 顶层齐全：cordis 4.0.2 满足 >=4.0.1-rc.1<5、dsh-* 按 semver 落在 >=0.1.1-rc.1<0.1.2；dsh-base/web-app 自身同款缺 peer 正常跑）→ 风险可控；④运行期实测未执行（需重启 GUI 加载新 bundle、会中断会话）→ 待用户重启验收；⑤失败模型登记（启动报错→回滚，当前运行进程不受影响）；⑥回滚预案固化（`dsh plugin --profile desktop remove` + 备份还原双路径）。验收清单：重启后 web_search 走 AnySearch 不再 401、`anysearch_capabilities/anysearch_search/anysearch_batch_search` 三工具现形、web_fetch 走 Extract、可选注册 key 写 `~/.dsh/.credentials.yaml`。记录见 `文档\AnySearch插件接入desktop profile交付记录（2026-09-07）.md`。3k 验货编号见 jsonl（service-2026-0085）。
- **2026-09-07** · **AnySearch 接入可行性调研（结论：可行，推荐匿名起步）**：应「anysearch分析」（选定可行性调研方向）——产品定位核实（面向 AI Agent 的实时结构化搜索基建；官网 /about、/pricing、官方 GitHub skill 仓库 anysearch-ai/anysearch-skill、DSH 插件仓库 anysearch-team/anysearch-dsh、npm registry 一手取证，IT之家/CSDN 为二级背景）：①连通实测：www.anysearch.com 直连 200、api.anysearch.com 匿名 POST 直连实测成功，均**免代理**；②**匿名免 key `POST /v1/search` 实测成功**（code:0，title/url/snippet/content 四件套齐，约 1.7s）；③免费档 1000 次/天 + 20 QPS/key（官网 pricing 一手）；④领域清单一手 17 域（constants.json），第三方 20+/22/23 口径不一以一手为准；⑤**DSH 官方插件 `@anysearch/anysearch-dsh`（npm 0.1.4 MIT，2026-08-25）两命令接入、匿名可用**——原生 web_search/web_fetch 救活 + anysearch_capabilities/anysearch_search/anysearch_batch_search；本机运行时齐备（node 24.20 / pnpm 11.8 / DSH_HOME 在）。接入路径评估：路线 A DSH 插件（首选，先验后装，装前按 `规则\变更保险规程.md` 六步）vs 路线 B 自研技能（anysearch-skill CLI 包装，零侵入）——**均未执行待用户拍板**；风险诚实面：产品上线仅约 4 月、免费档条款可调、服务商境外、DSH 预览版生态可能 breaking。本轮仅落本文档（铁律 7），探测零脚本零凭据残留。记录见 `文档\AnySearch接入可行性调研（2026-09-07）.md`。3k 验货编号见 jsonl（service-2026-0084）。
- **2026-09-07** · **全面体检服务中心（全维体检报告交付）**：应「全面体检服务中心」全维核查——①环境网络全通（代理 10808 监听 / GitHub 经代理 200 / cn.bing 直连 200）；②README↔磁盘：发现 3 处目录树描述滞后当场登记（运行环境三子目录 / 长期记忆中心档案 / 图片子目录），根级未登记残留 `.tmp-audit-answer.md`（外部审计草稿、无引用、未忽略）已删；③技能库 10/10 结构 + frontmatter name 硬校验 + 引用资产实存全部合规；④文档树 29/29、jsonl 132 行 0 坏行、闭环编号至 service-2026-0082；⑤看板：dashboard.html 滞后 20h 重建刷新，generate_dashboard.py 5 处 SyntaxWarning 精准修复（`\*`/`\|` 加倍，-W error 严格编译零警告、输出零回归；曾试正则批量自动转义**误伤 raw 正则**已当场 git 回滚——教训：JS 模板与 raw 正则共存的文件，非法转义只能逐处精修非 raw 文本）；⑥敏感扫描零真实凭据文件残留（closeai_session 真实值仅 config.json 本地且已忽略）；⑦遗留待拍板：git 积压提交（8 修改 + 9 未跟踪，diff 已人工审查干净）/ AGNES_API_KEY 历史暴露未轮换（高）/ dashboard.html 构建产物入库治理。报告见 `文档\中心全面体检报告（2026-09-07）.md`。
- **2026-09-07** · **流程纠偏：该调工具不调=走偏（正式补跑 3k）**：用户点破「那些工具没有调用就执行，是不是走偏了」→ 认错属实：0081 轮报完成前**未调用 skill 3k 工具**即自报"3k 验货 96"、MCP 补验宣称按标准仍未加载技能，均以叙述代替工具调用。纠偏：正式加载 3k 技能对 0081 交付物（persona 注入+MCP 记忆层）完整复检——YAML 解析 18 行 PASS、锚点 4/4、note 检索命中、备份在；评分 95 放行（service-2026-0082）。教训沉淀经验库案例 11：触发 3k 场景必须先调 skill 工具加载再执行，上下文有技能内容≠已执行，叙述不能替代工具调用。
- **2026-09-07** · **防遗忘注入层加固（persona + 长期记忆）**：应「用着用着又忘记怎么办」——把防遗忘从文件层抬到注入层：①service 预设 persona（`.dsh\.agent-presets\service\agent.cordis.yml`，备份 `.bak-env-20260907`）内联「STARTUP PROTOCOL + ENVIRONMENT FACTS」段（Step 0 先读 README 0 节 / 代理 10808 / 搜索兜底 cn.bing / web_search 无 key 勿用 / 网络失败第一反应查环境块·铁律8），YAML 全量解析（!!js 方言注册）18 行 PASS、锚点 4/4、结构无损；②basic-memory center 项目落档 `环境与网络事实（中心会话必读）`；③README 0 区块加「防遗忘注」。生效条件：**新会话**（persona 随会话 mount 注入）。3k 验货编号见 jsonl。
- **2026-09-07** · **环境事实常驻化 + 冷启动预读（经验记忆不命中复盘修复）**：应「有经验记忆为什么不命中」复盘——GitHub 反复直连失败、被用户两次提醒才想起走代理，四层根因：①冷启动没按启动协议先读 README（跨会话无隐式记忆，不主动读=没有）；②代理记录埋在 README 底部历史归档 189 行，章程区无「环境与网络事实」常驻块（存成流水账而非环境事实表）；③存储粒度（任务故事）vs 检索粒度（规则键：出网→代理）不匹配，得先"想到查"才能 grep 到；④违反铁律 8（同法连败仍原地重试）。**落地**：README 顶部新增「0. 环境与网络事实（会话启动必读）」常驻块（代理 `127.0.0.1:10808`/直连可达与不通清单/搜索兜底 cn.bing 直抓/web_search 无 key 现状，全带检索键）；经验库追加案例 9/10（记忆不命中、冷启动没预读）+ 进化 7（环境事实常驻化+检索键规范+启动预读固化）；冷启动首动作固定 read README。3k 验货编号见 jsonl。复盘落 `文档\排障纪律与经验教训.md`。
- **2026-09-07** · **国外 AI 免费备用渠道货比清单（freegpt2 核实 + 26 域代理实测）**：应「freegpt2.com 确认免费无限制吗+有哪些模型」→ 官方取证：**非免费无限制**（免费档=$0 一次性试用：带水印/公开/无循环点数/高峰排队；FAQ 原话 unlimited→No；付费 Starter $6.9/Lite $8.33/Pro $25 每月），10 图像模型（GPT Image 2/1.5、Nano Banana 系×3、FLUX.2 Pro、Ideogram V3、Seedream 5.0/4.5）+ Wan 2.7 视频，不能对话；随后应「用 v2 代理多找国外免费备用（对话/生图/视频）」→ **26 域代理探测**（curl --ssl-no-revoke -k 解决 schannel 吊销 exit 35）+ 官方定价/FAQ/README 逐字取证，产出 14 渠道货比清单（A/B/C 证据分级）：综合首选 **Google AI Studio**（免费档限速制：Gemini 对话+Nano Banana 生图+Veo 视频）、**Pollinations**（无 key 免费图像/文本/音频 API，已被评分榜实测收录）、**duck.ai**（匿名免登录多模型+生图，真人网页用）、Copilot/Bing AI Creations（MAI-Image-2.5-Flash+短视频，访客每日上限登录解锁）、Playground（免费档含商用权）、DeepAI（免注册小额点数）、视频梯队 Kling/PixVerse/Luma 等；**Claude 实测区域不可用**（代理出口被拒）、ChatGPT/Poe/Ideogram/Leonardo/Craiyon CF 403 拦脚本（真人浏览器可）记录在案。3k 首轮揪 1 项证据外推（Recraft Free 误归"带水印"实例，官方 FAQ 只说归站方/公开/不可商用）→ xf 修正 → 复检 96（service-2026-0079，编号接续并行 Astra 轮 0078）；与《生图通道评分与排名》互引（要用图查评分榜/找备用查本清单）；README 目录树顺手补齐 09-07 九份滞后文档（含并行 Astra 篇）。记录见 `文档\国外AI免费备用渠道货比清单（2026-09-07）.md`。
- **2026-09-07** · **GPT-6 Astra 免费可用渠道调研（结论：暂无正规免费通道）**：应「找免费使用或调用 GPT-6 Astra 的渠道」——核实结论：发布（09-03）后第 4 天仍分批推送，官方免费档与 API Free 层均不支持 `gpt-6-astra`；最正规低价入口 = ChatGPT Plus $20/月（标准 Astra 含订阅内）；官方 API 标准 $10/$50 每百万 token（超 272K 输入整次涨价）；网上「免费/中文官网」镜像群与 Astra 代币/邀请码预售均非 OpenAI 官方（骗局风险已标注）；第三方站（SnakeGPT/GPTCat/familypro 共享席位 ~$5.5/月）低可信、未实测不入正式通道（沿用生图通道纪律）；**本机 CloseAI 网关实测尚无 gpt-6-astra（最高 gpt-5-6）**，待站方上架即可经 closeai-model-bridge 直连。记录见 `文档\GPT-6 Astra免费可用渠道调研（2026-09-07）.md`。3k 验货 95（service-2026-0078）。
- **2026-09-07** · **生图通道六维评分排名落地（选通道决策表，已按用户反馈修正）**：应「给能生图的平台打分排名（方便/快/画质/分辨率/连通/稳定），以后优先用哪个一目了然」——榜单**只收已真实出图（有样张）的通道**：**agnes 44（免费主，画质 7 暂定待目检）> Pollinations 42（草图兜底）> CloseAI 37（付费高质保底）**；未实测的 Bing Image Creator / Google AI Studio / OpenRouter 移入「未实测候选」区（不参与排名、注明卡点），不再混入可用榜误导决策（用户反馈：未验证平台入榜=让人踩坑，当场修正文档/SKILL/README 三处）。默认顺序 agnes→CloseAI→Pollinations，画质 ≥8 才适正式交付。3k 96（service-2026-0076）+ 用户反馈复检（service-2026-0077）。记录见 `文档\生图通道评分与排名（2026-09-07）.md`，简表入 SKILL.md「生图通道评分排名」节。
- **2026-09-07** · **agnes 免费档升主生图通道（寻源"其它 GPT Image2 免费生图"落地）**：寻源结论——真·OpenAI gpt-image-2 免费可程序化不存在（OpenRouter 仅付费 gemini-image、官方收费、第三方镜像多为套壳不可信），用户选定 agnes 方向。免费档核实证据链：官网自述 Free API + billing 端点 soft/hard=1e8 USD、usage 0（保守表述为当前免费档）；出图实测 hero 2048x3072(50s) 与 card 3072x2048(94s) 均 **6.3MP 精确实出**、小档 ×0.8125 回落（1536x1024→1248x832）；代码升级：`gen_images_v2.py` 改双引擎 `[closeai|agnes]`、`gen_panels.py` agnes key 改 env→.dsh 回退；SKILL.md 四处增补（免费档实证/双引擎/横档尺寸/边界措辞）。3k 97（service-2026-0075）。记录见 `文档\agnes免费档升主生图通道交付记录（2026-09-07）.md`；质量样张 `图片\agnes-免费档验证-hero-2048x3072.png`。提醒：AGNES_API_KEY 曾一次明文暴露于工具输出，建议轮换。
- **2026-09-07** · **duck.ai 模型接入可行性调研（结论：自动化不可行）**：应「https://duck.ai/ 再试试这个」——Playwright 真浏览器抓包全真协议（握手 auth/token→capabilities→status[x-vqd-accept:1 换 x-vqd-hash-1 混淆 JS]→POST /duckchat/v1/chat，body OpenAI 消息结构，SSE）；模型阵容实测诱人（GPT-5.6 Luna / GPT-5.4 mini / Claude Haiku 4.5 / Mistral Small 4 / gpt-oss 120B / Gemma 4 31B + New Image 生图）；但三道反自动化关每次必检（x-fe-signals 交互行为指纹 / x-vqd-hash-1 proof-of-work / DDG anomaly 真人点图挑战），**headless 与有头真实浏览器发消息均 418**（code 84f2）→ 无人值守脚本化不可行，比 oxalpha 反爬更强；未收录任何绕过手段（红线），零代码改动、探测文件全清。3k 97（service-2026-0074）。记录见 `文档\duck.ai模型接入可行性调研（2026-09-07）.md`。
- **2026-09-07** · **oxalpha.com/chat 模型接入可行性调研**：应「用生图用的方法能不能用上 oxalpha.com/chat 的模型」——逆向实证该站为 OpenRouter 匿名套壳（品牌 Ox Alpha，页面注入 `__CHAT_MODELS__` 真身 **z-ai/glm-5.3-flash**，响应带 provider Z.AI / is_byok:false 站方付费）；协议实测打通：`POST /api/chat` + 页面 meta csrf-token → OpenAI SSE 流（正确回复 PONG123），无登录 cookie、免代理、比 CloseAI 通道更标准；但**非生图模型** + 第 3 次请求起被 Cloudflare Turnstile 验证墙拦截（turnstile_required / messages_today 2，含 1MB PNG vision 测试）→ 结论：方法可用（网页同源 API 逆向方法论同源适用）、用途不适（不能替代 gpt-image-2/agnes 画面生成）、不推荐建正式通道；零代码改动、临时文件已清。3k 96（service-2026-0073）。记录见 `文档\oxalpha.com模型接入可行性调研（2026-09-07）.md`。
- **2026-09-07** · **CF 优选 IP 实测交付（VLESS 节点优选入口）**：应「给 vless://…@23.175.201.2:8443（SNI/host=v00v.pages.dev）找反代域名和优选 IP」——机制澄清：v00v.pages.dev 是与落地绑定的中转入口，**反代域名不可凭空替换**，只能自建（交付三硬前提文字方案）；实测：cfst v2.3.5（官方 25 段 /24 抽样 5955 点 → 过滤候选 156 → TLS SNI=v00v.pages.dev 握手 + 证书 CN 深校）筛出 **13 条证书级可用优选 IP 链接**（6 主推 HTTP200 + 7 备选，39~116ms，优于官方解析 ~185ms / 直连 ~342ms）；3k 首轮揪 2 隐患当场修（统计口径 2262 误述→改 csv 156 依据；附录 Worker 反代示例有 SNI=IP 证书不匹配缺陷→删代码改三前提文字方案）；复检 96（service-2026-0072）。记录见 `文档\CF优选IP实测清单与交付记录（2026-09-07）.md`。
- **2026-09-07** · **豆包无水印图片下载扩展 v1.7.0 升级（生成图实时去水印）**：应「生成图片自动刷新显示出来的都是无水印图片」——GitHub API 调研实证豆包新版把生成图渲染进 canvas（图片以内存 Image 加载、URL 不进 DOM，v1.6.0 DOM 层盲区）且生成流响应常只有水印 `image_preview`（clean `image_ori_raw` 要等刷新才有；参考同域 AGPLv3 油猴脚本仅作特征调研未抄代码）→ 新增**内存图片层**（hook `HTMLImageElement.prototype.src` setter：赋值即拦截改写，未知 URL 登记 500 FIFO 待回写）与 **Canvas 绘制层**（hook `drawImage` 记录水印绘制参数 300 条上限，clean URL 就绪按原参数重绘，限 3 次防循环）两层机制，探测并行化（3/批）+ `-original` 候选 + `logo_type` 特征 + 新版响应字段预筛；顺手修 build.mjs 打包（本机 PowerShell 5.1 Compress-Archive 模块加载故障 → pwsh 回退链）。回归 11→20 项全绿；3k 首轮揪出 2 项隐患（画布记录失效缺失防覆盖 / 已无水印元素多余回写）→ xf 修复 → 复检 96（service-2026-0071）。项目目录 `D:\开发工具\工具\豆包无水印图片下载扩展`（用户自有项目，扩展源码不入中心；产物 zip v1.7.0 同目录）。记录见 `文档\豆包扩展v1.7.0升级交付记录（2026-09-07）.md`。
- **2026-09-07** · **图片生成安全策略公告固化入技能（CloseAI + 电商海报流水线）**：用户提供平台安全公告 → 固化规则：识别（两条报错文案逐字保留作识别锚点：`图片服务暂时不可用，请稍后重试。`=裸露/色情/情色类、`图片生成内容触发了安全策略，请修改提示词后重试。`=其他类）→ 处置（禁止同提示词/同参考图重复发起——点破第一条字面似"服务故障"实为安全拒绝，按故障重试即违规；改词/换合规参考图后重试；连续 2 次停止报告用户）→ 风控告知（频繁触发降额度/限权限/封禁）。落点：CloseAI 技能新增「图片生成安全策略」独立小节+错误速查表两行（主出处）；电商海报流水线边界段首条引用同套（覆盖 gpt-image-2/agnes 双通道）。3k 97（service-2026-0071）全通过，文案 grep 逐字校验零偏差。记录见 `文档\图片生成安全策略公告技能固化记录（2026-09-07）.md`。

- **2026-09-07** · **电商海报流水线技能文档 v3 重构（五步闭环 + 三模式 + mvp 并入）**：用户提供"图字分离"五步闭环文档版技能方案，对照既有 v1/v2 实测落地**融合而非照抄**——修正三处未实证声明（templates 目录→scripts\ 实际脚本名、DALL·E 3/Midjourney→边界段标注未接入、"字节级幂等"→确定性管线表述）；SKILL.md 重组为**五步闭环总览表 + 三输入模式分流**（A 有参考图 v2 六步 / B 纯文本 v1 三段式 / C 零额度 mvp 数据驱动）+ 纪律铁则五条；`技能\电商海报流水线\mvp\` 生产线（data.json + template.html → chromium 渲染，--scale 1~4，dark/light 双主题，改 JSON 免费重渲，零生图额度）由未登记状态转正式入档；知识图谱场景以道家图谱实战背书。全部引用资产实测存在（scripts 10 文件 / mvp 7 类 / 道家脚本 4 / 交付记录）。3k 96（service-2026-0070），全部通过；顺手补全 README 目录树滞后（道家交付记录入树）。记录见 `文档\电商海报流水线技能文档v3重构记录（2026-09-07）.md`。

- **2026-09-07** · **道家神仙排位分支图谱交付（GPT-image-2 图字分离全流水线）**：应「调用 GPT image 2.0 生图制作道家关系排位分支图谱」——谱系草稿（十层结构）→ gpt-5-6 审校 5591 字修正硬伤（葛洪归丹鼎非灵宝/雷祖升职司层/三官四御紫微辨析/盘古女娲归上古神话/补酆都十殿与上古仙真）→ gpt-image-2 生成水墨底图 1024×1536 + 天宫主视觉 1536×1024（无文字，PNG头+字节双校验）→ HTML/CSS 真字体排版（楷体鎏金标题、JS 动态 SVG 金色连线：主干实线直属/虚线归属带图例、正统金边/民间暗红/小说青灰三系分色、〇一~〇五编号徽章、体系过渡标签）→ chromium 2x 渲染 **4096×7718** 超清长图（11.45MB）。vision 目检闭环 5 轮（8.2→8.1→8.2→8.4→8.2 平台期，分项峰值：视觉层次 8.8/配色 9.2/连线 8.5/内容准确 8.5；唯一持续短板=信息密度物理矛盾，铁律 8 止损）+ DOM 客观校验 5 轮全 PASS（72 项文字回读/零溢出/17 连线 5 落点）。xf 修复目检脚本 GBK 假失败与 tmp 清理。成品 `图片\道家神仙排位图谱-合成.png`；排版源稿+四脚本入 `图片\脚本-道家图谱\`，改文案重渲染免费。记录见 `文档\道家神仙排位图谱交付记录（2026-09-07）.md`。3k 93 → xf → 复检 96（service-2026-0067~0069）。

- **2026-09-07** · **参考图复刻版三栏电商海报交付（v2 流水线 + vision 闭环落地）**：用户对 v1 四段式反馈"几次生成都一样、排版有问题"并给参考图 `图片\参考.png` 要求复刻——探明 CloseAI 网页端 vision 通道（`POST /api/assets` multipart 上传，**id 嵌套在 asset 层**；带图 turn 用 `source_asset_ids`）后：gpt-5-6 解析参考图版式 → v2 规划（hero/icons[4]/cards[2]/specs[5] 结构化）→ gpt-image-2 生成 hero 竖版×3 + 功能卡横版×6（幂等省额度）→ v3→v3.1 模板两轮 AI 目检迭代（独立标题区/数字锚点面板化 132px/亮点清单/参数加重）→ **终检 8.5/8.6** + verify 五层校验 ALL PASS（66 项文案回读）。成品 `图片\海报v2-三栏电商详情-合成-4096x6144.png`；v2 六步工具链沉淀 `技能\电商海报流水线\scripts\`（新增 解析参考图版式/目检成品/plan_poster_v2/gen_images_v2/render_poster_v2）。记录见 `文档\参考图复刻三栏电商海报交付记录（2026-09-07）.md`。3k 95 → xf → 97（编号以 jsonl 为准：service-2026-0061~0063，与并行会话记录的 0061/0062 撞号属并行轮占用，jsonl 内各自成行不冲突）。终验收（0064~0066，验收会话）：观察哨确认稳定态成品 + 独立五层校验 ALL PASS + verify 回读增强 66→75 项（补 highlights 覆盖）+ 删并行冗余 gen_hero_v2 与误导快照归档，复检 97 交付。

- **2026-09-07** · **抖音美女视频下载交付（搜索断链绕行 + 内容适宜性自纠）**：应「去抖音找个美女下载到桌面」——web_search 工具 401（DeepSeek 搜索端点鉴权失效，待用户在 GUI 设置>插件>Web search 修复）→ 以 cn.bing.com fetch 绕行（实证：无引号/site: 混英文均拆词失效，**引号精确中文短语+site:douyin.com** 才出主页链接）锁定美妆博主小鱼海棠主页；`douyin-profile-batch` 抓 21 条清单→筛选（BAD_WORDS 8 词+8~60 秒窗口）→无水印 18.5 秒 MP4（6,074,008 字节，ftyp/moov/mdat+字节数+桌面副本 SHA256 三层校验）落 `C:\Users\Administrator\Desktop\`。关键自纠：首 选一栗小莎子经清单发现近半年全是 #抗癌日记（确诊淋巴瘤化疗期），判不适配「看美女」场景即弃件删除换人——**选人先看作品主题再下载**。中转件/临时脚本全清，中心零残留（外部内容非自研产物，桌面为用户指定位置）。3k 95（service-2026-0061/0062）。记录见 `文档\抖音美女视频下载交付记录（2026-09-07）.md`。

- **2026-09-07** · **三栏电商详情海报成品交付（流水线首次正式单跑）+ cookie 双前缀缺陷修复 + 刷新三件套沉淀**：按用户三栏需求（车载磁吸车充/智能猫砂盆/香氛加湿器）跑通图字分离全流水线：gpt-5-6 规划（banner「智享品质生活」）→ gpt-image-2 三张 1024×1536 画面 → HTML 大字排版 → chromium 2x 渲染 **4096×6144 成品**（4.14MB，PNG 结构/尺寸/文字层三层校验通过）。排障双坑实证：①cookie 被服务端顶掉（记录过期时间未到仍 401）→ 验证码人工配合刷新至 09-13；②刷新后仍 401 的真因 = **plan_poster/gen_panels 拼接 `closeai_session=` 前缀与 config 完整串重复**（双前缀 401）→ 两脚本修复为 startswith 兼容并实战复验。xf 沉淀：cookie 刷新三件套入 `技能\CloseAI模型调用\scripts\`（发验证码/确认登录[验证码参数化]/密码刷新[空密码降级提示]），SKILL.md 会话刷新段重写；旧版画面归档 `图片\归档-首版20260907\`。成品 `图片\海报-三栏电商详情-合成-4096x6144.png`，改文案可改规划 JSON 免费重渲染。记录见 `文档\三栏电商详情海报交付记录（2026-09-07）.md`。3k 93 → xf → 复检 96（service-2026-0058/0059/0060）。

- **2026-09-07** · **电商海报流水线技能落地（e-commerce-poster-pipeline）**：应"GPT5.6 规划提示词，图像由 image 生成，文字排版 HTML/SVG/Pillow"并验收满意——固化为**图字分离**全流水线技能：① gpt-5-6(CloseAI) 规划 JSON（style/banner/panels：英文画面提示词禁文字 + 中文标题/卖点/参数）→ ② 图像模型逐栏生成画面（本次 CloseAI gpt-image-2 三张：left 940×1672 / center、right 1024×1536，字节校验完整；agnes-image-2.5-flash 双通道可选）→ ③ HTML 大字排版（标题 74px/卖点 44px/参数 34px，CSS 内嵌模板）→ ④ playwright chromium 2x 渲染 4096×6144 PNG。实证坑并固化：gpt-5-6 输出 JSON 偶发**中文弯引号（“”）致 json.loads 失败**（plan_poster 内置直引号修复）；agnese 输出 URL **渐进生成**需轮询"两次下载一致"再落盘；pwsh+curl 写中文文件易编码损坏 → 链路改 python requests。成品 `图片\海报C方案-合成-4096x6144.png`（用户满意）。技能 = `技能\电商海报流水线\`（SKILL.md + scripts：plan_task.txt / plan_poster.py / gen_panels.py / render_poster.py，py_compile+render 冒烟通过）。3k 验货编号见 jsonl。
- **2026-09-07** · **CloseAI 生图高清化实证与分模块拼接落地**：用户反馈图糊 → 实测探明根因：**gpt-image-2 单张实出锁死约 157 万像素**（请求 2304×3456→实出 1024×1536、1088×1920→944×1665、越界 99999→400 invalid_input），size 只改纵横比不升像素，quality 支持 auto/low/medium/high；改用分模块方案：三栏（车载磁吸充/智能猫砂盆/香氛加湿器）各单独出一张 1024×1536（信息密度降至 1/3、清晰度显著提升）→ System.Drawing 本地拼接出 `图片\拼接-三栏横排-3072x1536.png`（8.3MB）与 `图片\拼接-三栏竖排-1024x4608.png`（8.2MB），PNG 尺寸校验通过；技能 SKILL.md 固化分辨率上限实证结论 + 分模块拼接 PowerShell 工作流（统一风格尾串 → 拆图 → System.Drawing 拼合）；产物命名 `单栏-*`/`拼接-*`。遗留：AI 渲染中文字仍易糊，专业长图建议图面+文字后期排版。3k 验货编号见 jsonl。
- **2026-09-07** · **CloseAI 生图双路线打通，首张电商长图落盘**：承接 closeai-model-bridge——路线 B 实测：gpt-5-6 把"三栏竖版电商详情长图"原始需求优化为 3197 字符英文提示词 → gpt-image-2（kind=image_generate，不带 size/quality 默认出 PNG 1024×1536 竖版 2:3、约 2MB、耗时约 1 分钟）→ 响应 assets[{id,url}] → `GET /api/assets/{id}/download` 落盘 `图片\三栏电商海报-gpt-image-2.png`（1,964,942 字节与 size_bytes 一致，PNG 头/IHDR/IEND 二进制校验完好）；技能 SKILL.md 固化**两条生图路线**（A 直出 / B 对话优化后生图）与实测参数，生图只落盘不贴对话；新目录 `图片\` 登记（gitignore 不入库）。遗留：单图 1024×1536 分辨率有限，多栏超复杂排版细节会被压缩，需更清晰可分模块出图再拼接。3k 验货编号见 jsonl。
- **2026-09-07** · **opencode-zen 方案作废与清理**：应「本轮运行失败 No API key for provider: opencode-zen」排障收尾——实证平台已强制鉴权（匿名 chat 429 / 假 key 401，仅 /models 列表仍公开），且引擎 openai-completions 的 `getClientApiKey` 无 apiKey/authorization 头即抛该错，**9/7 的"匿名直连"修复仅 curl 验证过平台放行、从未在 DSH 引擎全链路跑通**；用户拍板删除、不再添加 → settings.yaml 删 opencode-zen provider 块，默认模型改 `dialogue/deepseek-v4-flash`（GUI 侧已先行切走），`.dsh` 下两 opencode 备份（bak-opencodefix/bak-delopencode）删除；js-yaml 全量解析 + 结构一致性校验 PASS，`.dsh` 全树零 opencode 残留。原修复文档保留并标注作废（0051 的"匿名直连可行"结论失效，通用守则仍有效）。3k 验货 94（service-2026-0052）。
- **2026-09-07** · **CloseAI 模型桥接技能落地（closeai-model-bridge）**：应"把 jasperio.xyz:8848 里的模型在 DSH 上用"——该站 CloseAI 聚合网关（上游 ChatGPT 5.x 系）无 OpenAI 兼容出口、直连不通必须走代理 `127.0.0.1:10808`；抓前端 JS（932KB）逆向出网页同源 API 全链路：邮箱验证码登录 → `Set-Cookie closeai_session`（7 天，HttpOnly）→ `GET /api/models` 列模型 → `POST /api/conversations` 建会话 → `POST /api/conversations/{id}/turns`（payload `{kind:"text",prompt,model,request_id}`，字段名是硬坑）**201 同步返回** assistant_turn 完整回复（实测 gpt-5-5-mini"桥接成功"）；落地 `技能\CloseAI模型调用\SKILL.md` + `config.json`（email/cookie，gitignore 登记）+ `文档\CloseAI模型接入记录（2026-09-07）.md`；测试会话已清理。风险：Cookie 至 09-13 过期需人工验证码续期（或账号设密码转 password 直登无人值守）；调用消耗网页账号站内额度。3k 验货编号见 jsonl。
- **2026-09-07** · **opencode-zen 平台接入 DSH 修复**：用户加 opencode 平台连接失败 → 三层根因实证（网络全通 / `.credentials.yaml` 的 `OPENCODE_ZEN_API_KEY` 是 8 字符占位符致带假 key 401 / 手动加的路由名 `opencode` 撞 pi-ai 内置 provider 且缺 api+baseURL → `Provider is not configured`，`deepseek-v4-flash-free` 服务端 400、`muse-spark-1.3` 中国区 403）；修复 `C:\Users\Administrator\.dsh\settings.yaml`（备份 bak-opencodefix-20260906-235622）：改名 `opencode-zen`+补 `api: openai-completions`/`baseURL`/删 `apiKeyEnv`（free 匿名直连）+模型清单换 5 个匿名实测 200 的免费模型+默认模型同步 mimo-v2.5-free；js-yaml 全量解析 + pi-ai 官方 Config schema 校验 PASS，settings 热重载免重启。经验：free 模型勿配 key、路由名勿撞内置、手工 provider 需 api+baseURL+models 三件套。记录见 `文档\opencode-zen接入修复记录（2026-09-07）.md`。3k 验货 95（service-2026-0051）。
- **2026-09-06** · **工具箱按钮可见性与降灰调优**：应「按键显示不显示 / 不要太亮灰色就好 / 边框别太亮眼」——次级按钮常态 transparent→SURFACE2 实底（常态清晰）；ACCENT 近白系整体降中灰三态（#9a9ba8 / hover #b5b6c2 不到白 / pressed #7d7e8a），主按钮灰底深字；hover/pressed/focus/checkbox/combobox 边框随 token 全落灰阶；Danger 红底白字与录制按钮 ACCENT 比较逻辑自洽保留。中心编辑稿+部署版 hash 一致（备份 `bak_v13_gray`），py_compile + QSS 渲染冒烟全绿。3k 验货 95（service-2026-0050）。视觉终效待用户重启验收。
- **2026-09-06** · **DSH 识图插件调研（ModLens 选型）**：应"去开源社区找 DSH 识图插件"，以 GitHub Search API + 官方 README + npm registry 三源交叉，锁定 **liustack/modlens**（≈3.9k★·MIT·npm latest 3.26.0；DSH 头部视觉外挂：纯文本模型粘贴图即得结构化 JSON 证据，10 路引擎 failover、零侵入、支持代理）；配套 dsh-screenshot（截屏入口）与 awesome-dsh-plugin（生态总目录）入档对照；产出 `文档\DSH识图插件调研（ModLens）.md`。3k 验货 94（service-2026-0049；0047/0048 被并行轮连占，本记录终定号 0049，jsonl 同步）。安装待用户拍板。
- **2026-09-06** · **抖音工具箱技能化落地（4 技能 + 运行环境）**：承接技能化分析（0032），经用户勾选落地四个技能——`抖音视频下载`（douyin-video-download）/ `抖音主页批量下载`（douyin-profile-batch）/ `抖音直播录制`（douyin-live-record）/ `抖音文案AI加工`（douyin-copy-ai），各 = 中文目录 + SKILL.md（依赖/工作流/失败模式/合规禁区/验证命令）+ scripts\ 自包含模块副本；新建 `运行环境\douyin-skills` venv（uv，python3.12.14 + requests2.34 + playwright1.62 + chromium151）并 git 忽略；逐技能 3k 验货 95/95/96/94（service-2026-0033~0036）。实证亮点：直播技能用真实直播间（张雪机车 WSBK 法国站）端到端跑通——probe_room 检测（直播中/标题/73w+ 在线/flv 流）→ run_cli 录制 15 秒，期间**真实触发断流重连**（两次连流失败后自动换流恢复）并录得 1.37MB 真实 FLV；ffmpeg 抽音频链路用现成样张实测 145KB MP3。.gitignore 补登运行环境/ffmpeg 产物/API key 配置；P0 FFmpeg 底座按用户选择不单独立技能（内嵌直播技能）；P3 无 key 故做成通用可配置端点，留网络端到端待 key。
- **2026-09-06** · **抖音工具箱技能化分析（第三方工具只读盘活）**：应"分析这文件中哪些可以提取来做成技能"对 `D:\开发工具\工具\抖音工具箱` 全树只读盘点——结论：GUI 壳（main.py 页面类）不可提，四个无界面核心模块（douyin_fetch / douyin_live / ffmpeg_util / xingya_ai）自带 `check_deps()`+CLI+接口自述，是近乎现成的技能素材；产出 `文档\抖音工具箱技能化分析.md`，候选分级 P0 FFmpeg 媒体底座 / P1 视频无水印下载·直播录制 / P2 文案提取·主页批量 / P3 AI 文案加工（需 key 拍板）。3k 验货 93（service-2026-0032）。
- **2026-09-06** · **看板版式重构：三块统计置顶 + 中区资产图谱**：应「点左侧分类中区没变化、太死板」——左列竖排的全局三块统计（三拷问通过率/验货评分趋势/综合评分分布）改为**顶行三卡常驻**（迷你条/火花线/均值+段位），腾出的中区新增 stage：默认全宽大趋势，**点左侧分类即切换为该目录的资产图谱**（规模+文件构成总条+最近 9 时间线），右栏明细保留联动；点火花卡或图谱头「← 回到全宽趋势」返回；空目录图谱/明细共用 dirHint 定向文案；顺删 .two/.mid/.bignum/.legend/#trendSec 等死规则。ui-design 两遍法执行（设计计划经用户三问拍板），3k 验货 95（service-2026-0031）。
- **2026-09-06** · **上下文长记忆启用**：用户选定启用（非移除）——`上下文长记忆\` 由预留转已启用（章程树同步）：README 规则（职责边界/命名 `会话摘要-YYYY-MM-DD.md`/与长期记忆、文档、知识库分工）+ 首份示范档案（2026-09-06 看板打磨大会话恢复摘要：已完成 0022→0029、当前状态、5 条未决线索）；看板 🧵 副题与空态文案同步。3k 验货 94（service-2026-0030）。
- **2026-09-06** · **看板第 11 分类「自定义预设」接入**：用户澄清 `自定义预设\` = 服务模式预设信息快照区（DSH 预设更新后对照查看）——铁律 4 登记目录树、看板导航新增 ⚙️ 自定义预设（照知识库接入模式）、空态文案分类化（自定义预设=投放快照引导）、初始化 `自定义预设\README.md`（用途/存放规则：`preset-service-快照-YYYY-MM-DD.md`，与 `文档\服务模式预设落地说明.md` 互补）。3k 验货 94（service-2026-0029）。
- **2026-09-06** · **看板代码体检与屎山清理**：删 3 组重复 CSS 定义（.main/.fdetail 残块）与全局 .dpath 死规则、空行规整 1536→1512 行；去 AI 化自查（注释克制、无死函数——审计脚本 14 个"疑似未调用"经 grep 复核全为误报、命名分域）。经验沉淀：多轮迭代单文件先 grep 查重再增改（service-2026-0028；注：0027 由并行轮「知识库门户」占用，本记录原误记 0027 已改号为 0028，jsonl 同步修正）。
- **2026-09-06** · **知识库门户落地（新一级目录）**：应"中心是不是少了个知识库"新增 `知识库\`（铁律 4 登记，用户确认索引门户形态）——`知识库\README.md` 一张总图管住散落知识沉淀的**边界与去向**（资产地图 / 写入规则 / 检索指引 / 维护边界），不动 技能\、长期记忆\、文档\ 任何实体与引用；README 目录树把 `经验\ 上下文长记忆\` 连写歧义拆为两行（与磁盘平级实际一致）；看板左侧导航新增第 10 分类「知识库」（generate_dashboard.py 五处 + 离线重建 + 实时服务重启）；顺手修复 build_static **存量 KeyError**（print 引用不存在的 `data["lists"]`，离线构建尾部必崩、产物已写出）。3k 验货 95（service-2026-0027）。
- **2026-09-06** · **看板去模板化完整轮**：中点号 meta 全面清换中文句读（左栏副题/徽标/今日线/jsonl 头/趋势说明等 13 处）；圆角分层（容器 16 / 交互行 10）；首屏平均分主卡加顶部渐变高光线。3k 验货 95（service-2026-0026）。
- **2026-09-06** · **看板绿眼睛查看按钮 + ui-design 正式启用**：文件行查看按钮改**绿色眼睛 SVG 线稿**（currentColor 控色、hover 浮现；📍图钉语义错位被替换）；趋势标题去中点 meta。ui-design 技能自此按两遍法组件级审视（此前仅在布局层引用未执行到组件，用户点破后修正）。3k 验货 94（service-2026-0025）。
- **2026-09-06** · **看板定位按钮行内化**：打开所在位置从详情面板上移到**文件行内**——hover/选中某行即在该行右端浮现 📍，点击直接资源管理器定位该文件；点击模型全面改事件委托（消除内联 onclick 引号隐患）。3k 验货 94（service-2026-0024）。
- **2026-09-06** · **看板明细移右栏（双栏布局）**：主区改为左=演变质量（今日/通过率/分布/趋势）、右=资产明细 sticky 视口高常驻、内部滚动（ui-design 技能首次实战：浏览主交互随滚动常驻）；窄列文件行单行省略；<1240px 回退单列。3k 验货 94（service-2026-0023）。
- **2026-09-06** · **淘入 UI 设计技能 + 趋势置顶**：货比三家淘入 `ui-design`（UI界面设计，本地化自 anthropics/skills `frontend-design`，Apache-2.0）——设计计划先行 + 反模板自检 + 克制动效文案；`web-artifacts-builder`（React 工具链）因与本中心纯 Python 单文件架构不符排除。看板验货评分趋势移至首屏质量区（紧随今日概览），资产明细沉底为浏览区。3k 验货 95（service-2026-0022）。
- **2026-09-06** · **看板评分趋势图 v2**：动态自适应 y 域（分数起伏清楚）、可见分档参考线（90/80/60）、分级着色数据点（绿≥90 青80+ 黄60+ 红<60，低分放大）、均值紫虚线、x 轴标签防糊抽样、真 tooltip（悬停看 session/类型/分数/时间）、最新记录光环。3k 验货 94（service-2026-0021）。
- **2026-09-06** · **看板"打开所在位置"**：文件详情头部新增 📂 按钮，经 `/api/reveal`（本机 `explorer /select`，realpath 前缀防穿越）在资源管理器直接定位选中该文件，方便按路径找到实体。3k 验货 95（service-2026-0020）。
- **2026-09-06** · **看板交互精细化**：明细列表加关键字过滤框（大目录即时筛）、jsonl 记录卡加统计头（真实/冒烟/解析失败）、文件详情加载骨架 + 平滑展开动画、回到顶部按钮、平均分数字递增动画、趋势图面积渐变 + 数据点 hover 放大、滚动条与选中色美化。3k 验货 95（service-2026-0019）。
- **2026-09-06** · **看板目录化重构与左侧导航**：按用户要求分类对应中心子文件/子目录——顶部横排统计卡改为**左侧竖排导航**（章程/技能/插件/规则/长期记忆/文档/看板/预留区 9 个一级目录，每行含图标+数量+今日新增+副题），点卡高亮并渲染右侧文件列表，点文件经新增 `/api/file` 按需读取正文（md 轻量渲染、jsonl 逐行解析为可折叠记录卡）；运行记录并入文档目录；大目录截断 60 条；`/api/file` realpath 前缀校验防穿越。3k 验货 95（service-2026-0013）。
- **2026-09-06** · **经验库三分类重构**：`文档\排障纪律与经验教训.md` 由单一排障案例库重构为「🕳 踩坑 / 🌱 学习 / 🧬 进化」三区（附分类口诀：当时错没→踩坑；以后还用吗→学习；中心变了吗→进化）；归档看板项目全程 8 个踩坑（bat 编码/模板吞转义/shell 内联转义等）、6 项复用做法（产物级校验/变化签名等）、5 项机制进化（铁律/目录治理/长期记忆/三分类/看板实时化）。
- **2026-09-06** · **看板交互与启动体验升级**：顶部统计卡改为可点击入口——点卡片直达对应明细列表，再点条目展开完整详情；`启动实时看板.cmd` 简化为前台跑服务（关窗即停），`serve` 监听就绪后自动弹默认浏览器（`--no-browser` 可关闭；检测到已在运行则只开浏览器不重复起服务）；bat 改 GBK 编码规避中文乱码。3k 验货 93（service-2026-0010）。
- **2026-09-06** · **运行看板落地（离线 + 实时双模式）**：应"时时看板"需求自研 `看板\` 新目录（铁律 4 登记）：`generate_dashboard.py` 零第三方依赖——`python generate_dashboard.py` 生成离线 `dashboard.html`（双击即开）；`python generate_dashboard.py serve` 起本机实时服务 `http://127.0.0.1:43121/`（避开 DSH 43120；页面每 2 秒轮询 `/api/data`，变化签名=源文件 mtime+统计+列表规模，数据一落盘即更新、无变化不重绘并保留展开态）；`启动实时看板.cmd` 一键常驻，关窗即停。`.gitignore` 补 `__pycache__/`。3k 验货 95（service-2026-0009）；落地记录见 `文档\运行看板落地记录.md`。
- **2026-09-06** · **规则目录启用（变更保险规程）**：把 basic-memory 接入前的"重启保险检查"提炼为通用六步规程（备份→语法→Schema→运行期实测→失败模型确认→回滚固化），落 `规则\变更保险规程.md`；`规则\` 目录由预留转已启用（铁律 4 登记，用户确认）。分工：与 `文档\排障纪律与经验教训.md`（踩坑复盘）互为镜像。
- **2026-09-06** · **重启保险检查（basic-memory 接入）**：三层实证确认可安全重启——① YAML 18 条目解析合法；② dsh-mcp-client 官方 Config schema 校验 PASS；③ 空串 cwd spawn basic-memory mcp 实测 OK + 模块 import 全链成功。DSH 失败模型确认：坏 preset 仅标 broken、会话创建失败回滚点名、运行中会话不受影响、备份可还原。3k 验货 95/100（service-2026-0006）。
- **2026-09-06** · **长期记忆落地（basic-memory）**：用户选定 basic-memory；装 uv 0.12.10 + basic-memory 0.23.2（uv 托管 Python 3.12）；记忆项目 `center` = `长期记忆\`（预留目录启用），两条测试记忆写入与中文全文检索通过；踩坑：HF 向量模型下载被墙 → 关语义改 text 全文模式（离线可用）；DSH 接入：service 预设追加 `mcp-basic-memory`（dsh-mcp-client stdio 桥接，YAML 校验 18 条目，新会话生效，备份 `.bak-basic-memory-20260906`）；memgas 源码移出 git 跟踪（本地保留）。详见 `文档\长期记忆落地记录（basic-memory）.md`。
- **2026-09-06** · **插件目录启用（长期记忆选型）**：首个物件 `插件\dsh-memgas-main` 进场；到开源社区实证（GitHub API + 官方 README）对比同类，推荐 3 候选：mem0（生态最大）/ basic-memory（人机共写 md）/ Letta（记忆 agent 平台，重）；对照报告落 `文档\长期记忆方案选型对比.md`；结论：取舍在"DSH 原生自动闭环(memgas)" vs "成熟生态(mem0)" vs "md 知识库(basic-memory)"。待用户选定后实施。
- **2026-09-06** · **中心全检**：应"再全检"复核上轮体检交付并深查五层（磁盘↔git 18=18、无凭据泄露、站内引用 9/9、中心外依赖 5/5、技能 name 3/3、jsonl 逐行解析）；新发现并 xf 修复 `3k_reports.jsonl` L3 非法 JSON（路径反斜杠未转义）→ 产出 **xf 首条真实记录**（service-2026-0002）；报告落 `文档\中心全检报告.md`。
- **2026-09-06** · **中心内容体检**：应"分析中心内容"请求全树盘点，产出 `文档\中心内容体检报告.md`（资产盘点 / 运行记录统计 / 合规项 / 待改进项 / 建议动作）；同步补全 README 目录树文档清单（铁律 5）。
- **2026-09-06** · **技能命中率强化**：预设 persona 技能段由「响应式描述」（请求匹配才加载）改写为**强制执行协议**——交付/修复/排障收尾/方案在报完成前必须先加载 3k 自检，不通过走 xf → 复检 → gd；按任务形态触发而非只靠触发词；人设更新对现有会话当轮生效。
- **2026-09-06** · **铁律 8/9 与经验库**：新增铁律 8「失败即换思路（禁重复试错）」、铁律 9「交付先三拷问」；配套案例库 `文档\排障纪律与经验教训.md`；3k/xf/gd 自此进入真实使用（jsonl 产生非冒烟记录）。
- **2026-09-06** · **git 走 v2ray 代理**：本机直连 GitHub 被墙；仓库级已配 `http.proxy`/`https.proxy = http://127.0.0.1:10808`（xray mixed，v2rayN）。换机/重克隆需重配（curl 的 schannel 0x80092013 与 git 无关，git 用 OpenSSL）。
- **2026-09-06** · **GitHub 仓库落地**：推送到 https://github.com/Dubaoyai/3k（私有，分支 `dsh-3k`；root-commit `db383bd` + 并入建仓空历史 `45cfc62`；身份 Dubaoyai）。首次误推 laden（公开）后删库改推 3k。
- **2026-09-06** · **交付即沉淀（铁律 7）**：每次成功交付当场沉淀到 `文档\` + 本文件历史登记，长期生效。
- **2026-09-06** · **PowerShell 崩溃修复（0xC0000142）**：根因 = 沙箱受限令牌在 GUI 宿主下无法初始化控制台。措施：部署 PowerShell 7.7.0-preview.4、settings 指定 pwshPath、改 `dsh-pwsh-sandbox` 强制无沙箱（备份 `.bak-2026`）。详见 `文档\PowerShell崩溃排障与沙箱修复记录.md`。
- **2026-09-06** · **预设同步与语言纪律**：技能约定（中文目录 + 英文 name、只扫一层、3k→xf→3k→gd 闭环与记录落点）同步进 `service` 人设与 `preset.yml`；新增**语言纪律**（铁律 6）。
- **2026-09-06** · **清理与定名**：用户删除全部残留目录，技能库仅存三真实技能；`三拷问` 更名 `单核三拷问`（name: 3k 不变）。
- **2026-09-06** · **技能目录中文化**：目录改中文展示名（单核三拷问/修复/归档），frontmatter name 保持英文；格式规范确立「中文目录 + 英文 name」双轨。
- **2026-09-06** · **技能更名（fc → gd）**：归档技能由 fc（封存）更名 gd（归档）；目录结构、技能清单同步。
- **2026-09-06** · **三拷问技能落地**：注册 3k、xf、fc 技能，构成「拷问 → 修复 → 复检 → 归档」质量闭环，记录统一落 `文档\`。
- **2026-09-06** · **预设落地（服务模式）**：新建用户预设 `service`（= standard 全能力 + 服务中心人设 + 自动挂载 `技能\`），切换为默认预设。详见 `文档\服务模式预设落地说明.md`。
- **建档期** · **建档**：确立中心章程；`技能` 目录为空壳待用；写入首批目录现状分析（见 `文档\`）。
