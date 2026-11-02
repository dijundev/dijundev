# 刘迪君 · AI 应用开发 / Agent 工程

深圳 · 随时到岗 · 2 年开发经验

我做的事可以概括成一句话：**业务规则不交给模型自由发挥——先固化成确定性边界，再让模型在边界里工作。**

## 在做的方向

- **Agent 工程** — LangGraph 状态机编排、工具调用白名单、会话状态持久化，把自由循环换成可重放的代码控制流
- **LLM 数据问答** — 指标语义层 + 只读 SQL 编译，模型负责理解问题、SQL 由编译器产出，模型输出永不直接进执行路径
- **Agent 安全** — 提示注入红队评测，把「我的 Agent 比较安全」变成一张有攻击成功率和误杀率的表

## 代表项目

### [agent-redteam](https://github.com/dijundev/agent-redteam) · Agent 安全靶场

给带工具的 Agent 建一套可复现的红队评测：60 条攻击用例（5 类攻击面）× 20 条正常任务，
目标 Agent 在 **5 层可独立开关的防御**下运行，用「工具调用轨迹断言 + LLM 判据」判定成败，
量化防御前后的攻击成功率与误杀率。

| 指标 | 结果 |
| --- | --- |
| ASR（防御全关 → 全开） | 100% → 1.7% |
| 正常任务误杀 | 0 / 20 |
| 560 次运行（7 种防御配置）全量耗时 | 4 秒 |
| 逐层边际贡献 | 参数校验 +21.6 pp，出站过滤 +8.3 pp |

固定 seed、温度 0、用例与判据入库，同一套集可完全复现。

### [dsl-guard](https://github.com/dijundev/dsl-guard) · 表达式与 SQL 的确定性边界

配置驱动的系统里，「表达式」和「SQL」是最容易变成执行入口的两处。

自研递归下降解析器 + **AST 白名单**，不开放 `eval`——语法里根本没有属性访问、下标、`import`，
所以 `__import__('os').system(...)` 连解析阶段都过不去；SQL 侧用 sqlglot 做只读校验、
危险函数拦截，并把权限条件下推到**最内层 WHERE**（防「总数 − 可见明细」的推断式越权）。

53 个测试，含 21 条攻击表达式全部拦截、0 误杀。

## 技术栈

`Python` · `FastAPI` · `LangGraph` · `MySQL` · `Redis` · `Qdrant` · `Elasticsearch` · `sqlglot` · `pytest`

## 找到我

- 作品集 → https://interview-cheatsheet.app.workbuddy.host/
- 邮箱 → liudijunfo@foxmail.com
- Gitee 镜像 → https://gitee.com/dijundev

工作项目代码归属公司，可面谈演示脱敏版本与实测报告。
