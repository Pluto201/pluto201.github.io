# TODO：需要你确认或补充的信息

> 本文件不会发布到网站（已在 `_config.yml` 的 `exclude` 中）。
> 网站内容的事实来源优先级：`interview-handbook/00-fact-conflicts.md`（你亲自确认过的）＞ `forphd/HANDOVER.md`、`forphd/CV_change_report_and_checklist.md` ＞ `interview-handbook/*/01-mainline.md` ＞ `prompt.md` ＞ `resume.md`。
> 有疑问的内容一律没有写上网站，只在这里登记。

## 一、上线前必须处理

| # | 事项 | 现状 | 改哪里 |
|---|---|---|---|
| 1 | **GitHub 用户名** | ✅ 已填 `pluto201`（`url`、`repository`、`author.github` 三处），仓库名 `pluto201.github.io`，`baseurl` 保持 `""` | — |
| 2 | **公开邮箱** | ✅ 已决定**不公开**，保持空，Contact 页显示 "to be added"。仓库内的提交身份已改用 GitHub noreply 地址，原邮箱不出现在任何提交元数据或文件中 | `_config.yml` → `author.email` |
| 3 | **项目公开授权** | ✅ 已确认**允许公开**（2026-10-28）。两个项目页已去掉内部代码、配置、IP、截图、业务系统名称 | `_portfolio/*.md` |
| 4 | **雇主名称** | ✅ 已决定**暂不公开**（2026-10-28）。网站一律写 "state-owned enterprise, Beijing"。具体公司名**不记录在本文件内**，以免随仓库一并公开 | `_pages/home.md`、`about.md`、`experience.md`、`cv.md`；`_config.yml` → `author.employer` |
| 5 | **英文 PDF 简历** | 未放置。CV 页和首页的按钮会在 `files/cv.pdf` 存在时**自动**变成下载链接 | 放入 `files/cv.pdf` |

> 上线前必须处理的现在只剩第 5 项（英文 CV PDF）。第 1 项已于 2026-10-27 定为 `pluto201`；第 2、3、4 项已于 2026-10-28 确认。

关于第 5 项：`forphd/Academic_CV_TU_Delft_Game_Theory.pdf` 是针对 TU Delft 博弈论职位定制的，并且里面还有红色待确认占位符，所以**没有使用**。建议准备一份通用版英文 CV 后再放入。

## 二、个人信息（可选，有就填）

| # | 事项 | 改哪里 |
|---|---|---|
| 6 | LinkedIn（只填 `linkedin.com/in/` 后面的部分） | `_config.yml` → `author.linkedin` |
| 7 | Google Scholar / ORCID（DBLP 已有条目 `journals/isci/SongZZW24`） | `_config.yml` → `author.googlescholar` / `author.orcid` |
| 8 | 头像（没有提供就不显示） | 放 `images/profile.png`，再设置 `_config.yml` → `author.avatar: "profile.png"` |
| 9 | 社交分享图：目前用的是模板自带的 `images/og-image.png` | 换成你自己的 1200×630 图片，或保持默认 |
| 10 | 网站图标 favicon：目前是模板默认图标 | `images/favicon*` |

## 三、教育与论文

| # | 事项 | 网站目前写法 |
|---|---|---|
| 11 | 硕士学位英文全称（Master of Engineering 还是 Master of Science，学术型还是专业型） | "Master's degree in Computer Science and Technology" |
| 12 | 本科学位英文全称 | "Bachelor's degree in Mechanical Engineering" |
| 13 | 奖学金英文名称和学年 | "First-Class Academic Scholarship, 2021–2022"（来自 `forphd/HANDOVER.md` 已确认事实） |
| 14 | 硕士论文英文题目、导师 | 未写 |
| 15 | **你在论文中的具体贡献**：算法设计、实验、写作是否由你完成 | 只写了"first author"和"implemented the algorithm in MATLAB on PlatEMO"（代码实现已在 `forphd/HANDOVER.md` 确认） |
| 16 | 基准测试集名称、评价指标（如 IGD、HV） | 只写了"three benchmark test suites and four real-world CMOPs" |

论文的书目信息（作者顺序、卷 655、文章号 119906、2024 年 1 月、DOI）此前已经按 Crossref 核对过，见 `forphd/CV_change_report_and_checklist.md`。

## 四、工作经历

| # | 事项 | 网站目前写法 |
|---|---|---|
| 17 | 正式英文职位名称 | "R&D Engineer"（来自学术版简历） |
| 18 | 入职日期 | "July 2024 – present" |
| 19 | 实习经历：几份材料的日期互相矛盾（2023.12–2024.04 / 2024.12–2025.04 / 2024.12–2025.07） | **没有放到网站上** |
| 20 | "早期报表自动化"阶段：做了什么、用了什么工具 | 只有一句概括 |
| 21 | 技能栏的 Java、Hive：是否有实际项目经验 | 列在 Skills 中（来自 prompt 和 resume） |

## 五、湖仓项目：与 prompt 不一致、已按保守口径处理的地方

| # | prompt 或简历中的说法 | 网站处理方式 | 依据 |
|---|---|---|---|
| 22 | "任务成功率提升约 20%" | **改为**"调度任务实例失败率约 10% → 约 7%（上线后一个月观察期）" | `00-fact-conflicts.md` L3：20% 已放弃 |
| 23 | 新架构使用 Spark、Hive、DataX | **没有写**。新架构只写 Flink | L6：新架构全部改为 Flink，没用 Spark |
| 24 | Hive Metastore、DataXWeb、Oracle 数据源、DataHub、Atlas | **没有写**。请确认：Paimon 是否用 Hive Metastore 作为 catalog？Oracle 是否是数据源？DataHub / Atlas 用在哪个项目？ | 材料之间不一致 |
| 25 | 实时大屏延迟"5–12 秒，高峰 ≤ 20 秒" | **没有写**具体数字，只写了"near-real-time" | L8：测量方法未确认 |
| 26 | 500+ 张表、日处理近百亿条、十余 TB | **没有写** | 口径待确认（是否含临时表；入湖行数还是计算行数） |
| 27 | Checkpoint 成功率 99.9%、湖表查询耗时降低 65%、文件数降低 72% | **没有写** | 统计窗口、查询类型未确认 |
| 28 | 简历里的"独立完成" | 改为"你和组长两人，组长定方向和审批" | L2 / L2b |
| 29 | FastAPI 接口数量（近 30 个）、对接的 4 个业务系统 | 只写了"有 FastAPI 数据服务层，带鉴权、限流、超时、行数限制" | 调用量未确认 |
| 30 | 105G OOM 的原因 | 写成"working explanation（推断），未通过内存分析证实"，并注明只解决了这一个任务 | `02-key-events.md` E5 |

## 六、Light-ChatBI 项目：与 prompt 不一致、已按保守口径处理的地方

| # | prompt 或简历中的说法 | 网站处理方式 | 依据 |
|---|---|---|---|
| 31 | "本地 Qwen3 27B" | **改为** Qwen3.6 27B、4bit 量化、公司机房私有化部署 | C1 / C1b |
| 32 | "AST 确定性拼装 SQL"作为当前方案 | 写成 V1 方案；当前 V2 已迁移到 Cube Core | C2 / C2b |
| 33 | "SQL 生成准确率 58% → 100%" | 写了，并注明：同一套 200+ 道验收题；业务确认 + 标准 SQL 比对；澄清后答对也算对；100% 是在迁移 Cube **之前**测得；不代表泛化能力 | C4 / C2b |
| 34 | "执行正确率 100%" | **没有写**。和"SQL 准确率"的区别、口径不清楚 | prompt 有、材料没有口径 |
| 35 | 迁移 Cube 后是否用同一套题回归 | 网站写明"当前版本没有报告同等数字" | C2c 未回答 |
| 36 | 需要澄清的题目占比 | 网站写明"没有统计" | C4b |
| 37 | 排队 2–3 小时 → 10 分钟以内 | 明确写成 **target（目标）**，未实测 | prompt |
| 38 | 代码模块名（config.py、agent_executor.py 等） | **没有写**，属于内部代码结构 | 公开安全 |
| 39 | 项目开始时间 2026 年 3 月 | 已写 | `02-chatbi/01-mainline.md` |
| 40 | 思维链开启时单次 7–8 分钟 | 只写"开启思维链时延迟明显变高"，没写数字 | 口径未确认 |

## 七、可以以后补充的内容（目前没有放到网站上）

- 销量预测项目（MAE 降低 16.2%、RMSE 降低 13.7%，有滚动验证口径，见 `portfolio/forecast-resume-and-interview.md`）：可以作为第三个项目页。prompt 要求模型效果"缺少完整上下文时谨慎呈现"，所以暂时只在 Experience 中写了一句"forecasting-model experiments"。
- 字段级血缘、数据质量平台的具体规模和指标。
- Document AI / OCR 项目（prompt 没有提到，未放）。
- VU Amsterdam 合作课程（成绩和英文课程名确认后可以放到 Education）。
- 英语成绩（CET-6 549；雅思或托福）。
