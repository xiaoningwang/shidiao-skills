# 市调大赛 Skills · Shidiao Skills

面向全国大学生市场调查与分析大赛的四个中文 Codex 技能，覆盖选题、报告撰写、分析方法与质量审查。

以《市场调查与数据分析实战》书稿为方法基础，结合中国商业统计学会第十七届赛事总通知，将“问题—研究设计—数据质量—适切分析—证据—行动”转化为可复用工作流程。

## 包含哪些技能

| 技能 | 适用任务 | 主要成果 |
|---|---|---|
| [`shidiao-topic-selection`](skills/shidiao-topic-selection/SKILL.md) | 选题筛选、题目收敛、开题论证、企业命题拆解 | 候选比较、选题论证、问题与变量对应矩阵、预调查任务 |
| [`shidiao-report-writing`](skills/shidiao-report-writing/SKILL.md) | 报告撰写与修改、结果表达、图表摘要、答辩准备 | 报告结构、结果索引、发现到建议对应表、修改清单与答辩题库 |
| [`shidiao-analysis-methods`](skills/shidiao-analysis-methods/SKILL.md) | 分析预案、方法选择、统计与质性分析、模型解释 | 问题与方法矩阵、质量诊断、结果解释、验证和降级方案 |
| [`shidiao-quality-review`](skills/shidiao-quality-review/SKILL.md) | 阶段验收、规则核对、数据真实性、AI与隐私、提交检查 | 规则适用表、证据缺口、修复清单、阶段验收结论 |

这些技能是给 AI 助手读取的工作指引，不是独立运行的软件，也不自带调查数据或自动统计服务。实际分析与文档生成取决于所用环境的工具和用户提供的材料。

## 安装

### 通过 Codex 安装

在能够访问本仓库的 Codex 对话中输入：

```text
请使用 skill-installer，从 xiaoningwang/shidiao-skills 安装以下四个技能：
skills/shidiao-topic-selection
skills/shidiao-report-writing
skills/shidiao-analysis-methods
skills/shidiao-quality-review
```

私有仓库需要当前环境具备仓库读取权限。安装后在下一轮对话中使用。

### 手动安装

先克隆仓库，再将需要的技能文件夹复制到 Codex 用户技能目录。以下命令在 macOS/Linux 下运行，遇到同名技能会跳过，避免覆盖已有修改：

```bash
gh repo clone xiaoningwang/shidiao-skills
cd shidiao-skills
skill_dest="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skill_dest"
for skill in skills/shidiao-*; do
  name="$(basename "$skill")"
  if [ -e "$skill_dest/$name" ]; then
    echo "已存在，跳过：$name"
  else
    cp -R "$skill" "$skill_dest/$name"
  fi
done
```

更新已有安装时，先备份个人修改，再比较仓库新版与本地版本。

## 调用示例

### 选题与开题

```text
请使用 $shidiao-topic-selection。我们是本科组，计划研究某市社区养老服务，
可接触三个社区，周期六周。请比较可行方向，并给出开题论证和问题—变量—方法矩阵。
```

### 报告撰写

```text
请使用 $shidiao-report-writing，根据我提供的调查方案、真实结果和现有报告，
重组结果章节，检查结论与建议的证据链，并列出需要补充的材料。
```

### 分析方法

```text
请使用 $shidiao-analysis-methods。我的结果变量是是否复购，资料为横截面问卷。
请根据数据字典制定分析预案，说明变量编码、方法条件、诊断和解释边界。
```

### 提交前审查

```text
请使用 $shidiao-quality-review，按我提供的当届组别通知和项目材料，
检查报告、PPT与附件，按影响程度给出问题、证据、修复动作和验收标准。
```

也可以自然表达任务，由 Codex 根据技能描述选择适用技能。局部修改不必运行整个项目流程。

## 建议准备的材料

- 赛事届次、组别、赛区、自由或企业命题、目标阶段与截止时间。
- 已有选题、资源约束、调查方案、抽样过程、问卷与访谈提纲。
- 数据字典、脱敏数据、清理记录、分析输出、现有报告与PPT。
- 当届正式通知及附件，尤其是评分、格式、匿名、AI披露与提交要求。

材料不齐时，技能会区分可完成内容、工作假设和待补证据。没有真实数据时只生成方案或明确标识的模板，不编造调查结果。

## 方法与质量原则

1. 选题必须对应明确的决策主体、研究对象和可获得的证据。
2. 方法服从研究问题、变量类型和抽样设计，不以模型数量证明水平。
3. 保留原始数据、清理日志和版本记录，避免只凭单一异常阈值删样本。
4. 横截面关联、模型拟合和特征重要度不能单独证明因果。
5. 结论回溯到结果，建议对应行动主体、实施条件和评价指标。
6. AI辅助须人工核验，不能伪造问卷、访谈、引用或过程证明。

## 来源与规则时效

规则快照核验日期为 **2026-10-18（北京时间）**。每个技能均附独立的 `references/sources-and-rules.md`

## 仓库结构

```text
.
├── README.md
├── .gitignore
└── skills/
    ├── shidiao-topic-selection/
    ├── shidiao-report-writing/
    ├── shidiao-analysis-methods/
    └── shidiao-quality-review/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/sources-and-rules.md
```

四个技能目录均采用相同的三文件结构。`SKILL.md` 是技能入口，`agents/openai.yaml` 提供界面名称与默认提示，`references/` 保存来源和规则边界。

## 维护

更新竞赛要求时，同时记录届次、组别、阶段、发布日期、核验日和原文位置。若更新四个技能共有的规则快照，应同步四份来源说明，避免独立安装时出现版本差异。

本仓库不代表赛事主办方发布正式规则。仓库尚未指定开源许可证；书稿和第三方资料的权利归相应权利人所有。
