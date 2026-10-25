# AI安全学习路线图 · 红队转型版 V1.0

> 12周冲刺 · 每周6天 · 起始 2026/10/20 · 目标：Agent安全评测 / AI攻防实习
> 用法：此为 `AI安全学习路线图.html` 的文字源。把本文件内容贴到 markmap.js.org / 支持 markmap 的编辑器，即可渲染为同款思维导图。

---

## 🟢 阶段1 · 地基：Python工程化 + LLM应用基础 ｜ 第1-2周 ｜ 10/20–11/01

- **Python 工程化**
  - 基础巩固
    - 数据结构：list / dict / set / 推导式
    - 函数、模块、面向对象
    - 文件 / JSON / 正则处理
  - 网络请求
    - requests 同步请求
    - httpx 异步客户端
    - asyncio 并发（async/await / gather）
  - Web 框架入门
    - FastAPI 路由与请求体
    - 用 FastAPI 封装 HTTP 服务
    - Uvicorn 本地启动
  - 环境与工具
    - uv 包管理 / 虚拟环境
    - Docker Desktop 基础
    - Git 与 GitHub 仓库管理
- **LLM API 调用**
  - OpenAI 兼容接口
    - DeepSeek / 通义 / Kimi 接入
    - messages 结构（system / user / assistant）
    - 流式输出 stream
  - Prompt 基础
    - System Prompt 设计
    - Few-shot 示例
    - 温度 / top_p 参数
  - Function Calling
    - 工具定义（JSON Schema）
    - 工具调用解析
    - 多轮工具结果回填
- **Agent 核心原理**
  - Agent 工作流：感知-规划-行动-记忆 / ReAct / Planner-Executor-Tool-Memory
  - Hello-Agents 教程 1-6 章：手写最小 ReAct Agent、接入 1 个工具跑通循环、标出每步"模型可控"数据点
- **📦 项目 AgentProbe 启动**：搭 AgentAdapter 标准接口 / 产出靶 Agent
- **✍️ 博客 × 自测**
  - W1《红队眼里的 LLM Agent：它凭什么自己调工具》
  - W2《60行Python写个会被我骗的AI助手》
  - 自测：独立写异步API脚本 / 讲清工具调用数据流 / ReAct 能跑通

---

## 🟢 阶段2 · 攻击入门：Prompt注入与越狱 ｜ 第3-4周 ｜ 11/03–11/15

- **风险框架（必背）**
  - OWASP LLM Top 10：中文解读 / LLM01 Prompt Injection / 数据泄露 / 不安全输出
  - OWASP Agentic Top 10（2025.12 发布）：ASI01 Agent Goal Hijack / ASI02–ASI10 / EchoLeak、Replit 案例
- **直接提示词注入**
  - 手法：忽略上文指令 / 角色扮演（DAN）/ 分隔符逃逸 / 编码绕过（Base64、Unicode）
  - 靶场：Gandalf（Lakera）7 关 / 自建靶 Agent 打点 / 10+ payload 成功率记录
- **间接提示词注入（重点）**
  - 原理：指令藏进外部内容（网页/文档/工具返回值），模型把数据当指令
  - 实验：给 Agent 加"读网页"工具 → 网页藏恶意指令 → 劫持行为 → 数据外发 PoC
- **越狱 Jailbreak**
  - 手法综述：情景构造 / 前缀注入 / 后缀对抗 / 多轮诱导
  - 越权实验：绕过"禁止读文件"规则
- **防御基础**：输入过滤与指令隔离 / 输出检测 / 为什么没有银弹
- **📦 项目推进**：W3 攻击引擎+YAML载荷库 ｜ W4 间接注入+工具越权检测模块
- **✍️ 博客 × 自测**
  - W3《对照OWASP把AI助手打穿-上：直接注入》
  - W4《藏在网页里的一句话-间接注入实战-下》
  - 自测：背 OWASP Agentic Top10 / 复现一次间接注入

---

## 🟢 阶段3 · 深度攻击面 + 自动化评测 ｜ 第5-6周 ｜ 11/17–11/29

- **自动化红队工具**
  - Promptfoo（阿里JD点名）：YAML 配置红队 / HTML 报告 / red teaming 插件
  - Garak（阿里JD点名）：pip install garak / probe 探针架构 / 扫描开源模型 API
  - AgentDojo：97 任务 + 629 安全用例 / 攻击成功率 vs 任务效用
- **MCP / Skill 安全**
  - MCP 协议原理：工具描述即上下文 / 工具投毒 tool poisoning / 元数据藏指令
  - 腾讯 AI-Infra-Guard（朱雀）：MCP-Scan / Agent-Scan / ClawScan / 14 类风险分类
  - Skill 供应链风险：恶意 skill 识别 / 哈希固定+白名单 / 沙箱隔离运行
- **RAG / 记忆攻击**
  - RAG 投毒：知识库污染攻击链 / 恶意文档被召回 / 投毒检测思路
  - 记忆污染：长期记忆篡改 / 跨会话污染
- **工具调用越权**：越权调用检测 / 最小权限原则 / 高危动作人工确认
- **📦 项目推进**：W5 评测指标ASR+中文风险报告 ｜ W6 RAG/记忆投毒模块+README+架构图
- **✍️ 博客 × 自测**
  - W5《Promptfoo+Garak 给大模型做安全体检》
  - W6《工具/记忆/知识库都能被投毒》
  - 自测：会写 Promptfoo 配置 / 讲清 Agent 评测指标

---

## 🟢 阶段4 · AI for Security + 项目收尾 ｜ 第7-8周 ｜ 12/01–12/13

- **LLM 做安全（辅线）**
  - 告警降噪：日志喂模型判定攻击流量 / 结合绿盟 2000+ 告警经历 / 漏报控制与效果评估
  - LLM 辅助代码审计：源码喂模型找漏洞 / 误报过滤
  - 安全知识沉淀：攻击技法封装成 Skill / 信息收集 Agent 工具
- **AI 自主渗透（看思路）**：Strix 开源项目 → AI 驱动渗透闭环 / 动作不可控、幻觉风险 / 对标绿盟、小鹏 JD
- **离线审计（对标阿里/360）**：Agent 执行轨迹审计 → 越权工具调用 / 异常数据外流 / 疑似注入特征 / 权限突变
- **📦 项目收尾**：README 完整可 clone 运行 / Mermaid 架构图标注 OWASP 编号 / Demo 动图 视频
- **✍️ 博客 × 自测**
  - W7《2000条告警让大模型帮我分类》
  - W8《我做了个Agent安全检测工具-开源全过程》
  - 自测：讲一个 AI 做安全完整案例 / 项目能跑通

---

## 🟣 阶段5 · 面试冲刺与投递 ｜ 第9-12周 ｜ 12/15–01/10

- **简历重塑（W9 ｜ 12/15–12/20）**：STAR 改写 AgentProbe / 三版简历（A·B·C保底）/ 博客成果包装一行 / GitHub 项目置顶
- **八股与手撕（W10 ｜ 12/22–12/27）**
  - 八股 10 题：三类注入辨析 / Agent 攻击面与防御 / 评测方案设计 / MCP 投毒检测
  - 手撕预测：Prompt 注入检测函数 / 日志攻击分类脚本 / Agent 日志找越权 / SQL 聚合统计 / 牛客华为机试前 30 题
- **投递与内推（W11 ｜ 12/29–01/03）**：绿盟带教老师内推（王牌）/ BOSS 直投 阿里·网易·启明·小鹏 / 关注 HR 附项目博客链接 / 公众号跟进
- **面试与复盘（W12 ｜ 01/05–01/10）**：面试集中期 / 当天复盘写博客 / 迭代答案 / 1 月中入职实习
- **⚠️ 避坑三忠告**：别躲学习舒适区（每周必有产出）/ 别堆关键词（每点要有踩坑故事）/ 别丢攻防优势（红队 × AI 主线）



![多模态深度学习框架](C:\Users\lenovo\Desktop\多模态深度学习框架.png)

