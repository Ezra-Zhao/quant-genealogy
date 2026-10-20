# 量化交易与金融工程 · 立项说明与总纲

立项日期：2026-10-20。本类是「领域学习谱系」五类中的第一类，由 Ezra 亲点开工：他在短视频里看到有人安利一个叫 QuantDinger 的开源 AI 量化交易系统，让把量化交易在 GitHub 上单开一类、把里面的东西做成中文教育内容。本文件先把 QuantDinger 核实清楚，再定本类的总纲：收什么、按什么顺序学、经典材料有哪些。

## 一、QuantDinger 核实结果（2026-10-20 GitHub API + 仓库 README 实查）

- **仓库**：[OpenByteInc/QuantDinger](https://github.com/OpenByteInc/QuantDinger)，是真仓，不是同名山寨（搜索结果里另有几个 fork 与仿仓，star 只有个位数到两位数，已剔除）。
- **硬数据**：Star 12,947（Forks 2,865）；建仓 2025-12-28；主要语言 Python；许可证 Apache-2.0（指后端代码，前端与移动端是另仓、走 source-available 口径，见下）。
- **它是什么**：一家叫 Open Byte Inc. 的公司做的开源「AI 交易操作系统」（AI Trading OS）。一条链打通：AI 市场研究 → 用 Python 写策略（Strategy API V2）→ 服务器端回测 → 模拟盘/实盘执行 → 运行监控。本地优先、自托管，行情数据、策略代码、券商凭据都留在使用者自己手里。
- **覆盖市场**：加密货币交易所（Binance、OKX、Bitget、Bybit、Gate、HTX 等）+ 传统券商（IBKR、Alpaca）两条腿；AI 侧接多家模型（OpenAI 兼容接口、Google、DeepSeek 等），并提供 Agent Gateway 与 MCP 服务，让 AI agent 能直接调用它做研究与交易操作。
- **值得注意的两个细节**（读 README 与仓库说明核实）：
  1. 它内置了一套防过拟合的回测体检工具：参数寻优带 walk-forward 验证和盲测保留集，结果用 PBO（回测过拟合概率）、Deflated Sharpe、块自助 Monte Carlo 检验——这正是量化研究里最容易自欺的地方，工具把丑话写进了流程。README 明说这些结果「用来比较参数稳健性，不预测未来收益」，口径诚实。
  2. 版本迭代极快：建仓不到一年，后端已经演进到 v5（进程拆分、独立 worker、可观测性、安全模型全套）。这既是活跃的信号，也是 API 还会变的信号，学习时以它仓库内文档为准。
- **要保留的判断**（编者分析）：不到一年 1.3 万 star，增速在量化类仓库里属于快的。它有公司主体、有赞助商（README 列了 Atlas Cloud、AWS 支持）、有产品与多端配套，增长有真实产品势能打底；但「AI 交易 OS」正踩在 agent 热潮的风口上，star 里有多少是热度、多少是留存，还要时间验证。本谱系收录它是当「新物种样本」研究，不是背书——更不构成任何使用或投资建议。

## 二、本类总纲

### 收录范围

按量化研究的全链条分层收，每层攒够一批就出一批导读：

1. **数据层**：行情与基本面数据接口、数据存储与处理（akshare、ArcticDB 等）。
2. **研究与回测层**：回测引擎、因子分析、组合分析与绩效报告（backtrader、zipline、quantstats 等）。
3. **平台与框架层**：研究到实盘一体的平台（qlib、vnpy、Lean 等）。
4. **方法层**：金融机器学习、强化学习、统计套利与做市的经典实现（FinRL、mlfinlab 等）。
5. **执行与 bot 层**：实盘交易机器人与高频/做市框架（freqtrade、hummingbot、hftbacktest 等）。
6. **AI 原生层（新）**：LLM/Agent 驱动的研究与交易系统（QuantDinger 为第一号样本，后续跟踪同类）。
7. **资源索引层**：awesome-quant 这类总目录，作为整个领域的地图册。

### 学习路线（草案，随批次细化为正式路线图）

- 阶段 0 准备：Python + pandas/NumPy 基础，统计直觉（分布、相关性、为什么金融数据爱骗人）。
- 阶段 1 数据：用数据层工具把行情拿下来、清洗好、存好——先解决「数据从哪来」。
- 阶段 2 回测：用一个回测引擎完整跑通「提出想法→写策略→回测→看绩效报告」，并学会识别回测的常见陷阱（未来函数、幸存者偏差、过拟合）。
- 阶段 3 因子与组合：因子是什么、怎么检验一个因子是否有效、组合怎么优化与控风险。
- 阶段 4 方法进阶：金融机器学习与强化学习的经典工作，理解它们解决什么问题、又带来什么新坑。
- 阶段 5 实盘与系统：模拟盘先行，理解执行、滑点、延迟与风控；AI agent 类工具放在这一阶段之后再碰。

### 纪律（写在最前面，长期有效）

- 本类是**教育内容**：只讲知识、工具与方法，不推荐任何标的与策略，不承诺任何收益。
- 涉及回测结果的表述，必须同时交代回测的局限；展示第三方项目的收益数字时，注明是项目自述、未经独立验证。
- 与 Ezra 的股票投资线严格分工：那边是实盘陪跑、每笔他本人点头；这边不产出买卖指令。

## 三、经典学习材料清单（只列名目与出处，本批不展开导读）

### 书籍

- Ernest P. Chan, *Quantitative Trading*（Wiley, 2009）与 *Algorithmic Trading*（Wiley, 2013）——散户/独立量化入门的事实起点，两本都不厚。
- Robert Carver, *Systematic Trading*（Harriman House, 2015）——系统化交易的完整框架，组合构建与风险平价讲得最清楚的一本。
- Marcos López de Prado, *Advances in Financial Machine Learning*（Wiley, 2018）——金融 ML 的方法论圣经：标签、三重屏障、回测过拟合检验都出自这里；进阶可续 *Machine Learning for Asset Managers*（Cambridge, 2020）。
- Stefan Jansen, *Machine Learning for Trading*（Packt，第 3 版）——配套代码仓已收入第一批导读（第 8 条），书与代码互为表里。
- Yves Hilpisch, *Python for Finance*（O'Reilly）——Python 金融数据分析与衍生品定价的工具书。
- John C. Hull, *Options, Futures, and Other Derivatives*（Pearson）——金融工程定价的通行教材，理解衍生品绕不开。
- Larry Harris, *Trading and Exchanges: Market Microstructure for Practitioners*（Oxford, 2003）——市场微观结构，做市与高频话题的理论底座。

### 论文（arXiv 与期刊，逐字精译只对开放传播的版本做）

- Gu, Kelly & Xiu, "Empirical Asset Pricing via Machine Learning", *Review of Financial Studies* 33(5), 2020——ML 资产定价的标杆实证，工作论文版见 NBER WP 25398。
- Chen, Pelger & Zhu, "Deep Learning in Asset Pricing", arXiv:1904.00745——生成对抗网络做资产定价的代表作。
- Bailey & López de Prado, "The Deflated Sharpe Ratio", *Journal of Portfolio Management* 40(5), 2014；及 Bailey 等, "The Probability of Backtest Overfitting"（2014/2017）——QuantDinger 内置的 PBO 与 Deflated Sharpe 检验就源于这条线，是学回测诚实度的必读。
- Fama & French, "Common Risk Factors in the Returns on Stocks and Bonds", *Journal of Financial Economics* 33, 1993——因子投资的源头。
- Jegadeesh & Titman, "Returns to Buying Winners and Selling Losers", *Journal of Finance* 48(1), 1993——动量效应的经典证据。

### 开放课程

- MIT OpenCourseWare 18.S096 *Topics in Mathematics with Applications in Finance*——麻省理工的金融数学课，免费全开放。
- Georgia Tech CS 7646 *Machine Learning for Trading*（OMSCS 公开材料）——从数据到策略的完整一门课，与 Jansen 的书互补。
- WorldQuant University, MSc in Financial Engineering——免费、带学位的在线金融工程硕士项目，适合想系统补数学的人先了解其课程表。
- QuantInsti EPAT——业界口碑的算法交易职业课程（付费），只列名目，供需要职业转向的人参考。

## 四、批次规划

- 第一批（已完成）：全领域头部 12 仓导读，见 `第一批-导读.md`——覆盖数据、回测、平台、方法、bot、AI 原生、索引七个层位。选品口径说明：按 star 排序时排在最前的 ZhuLinsen/daily_stock_analysis（66,770 star）未收——它是一个 LLM 股票分析看板，不属于量化研究/交易框架的谱系范围，且其 forks 数与 star 数几乎相等（55,464 / 66,770），数据形态异常（编者判断，特此留痕）；HKUDS/Vibe-Trading 等 2026 年新仓先入观察名单，待存活验证后再议收录。
- 第二批（候）：执行与高频专题——hummingbot、hftbacktest、vectorbt、backtesting.py、jesse 等。
- 第三批（候）：方法专题——mlfinlab、PyPortfolioOpt、alphalens 及 FinRL 生态的续作（FinRL-X）。
- 经典材料导读与学习路线图正式版，在项目导读攒到两批后开工，与 AI 谱系的节奏一致。
