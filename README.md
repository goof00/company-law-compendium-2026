# 公司法律法规及司法解释汇编（2026年版）· Agent Skill

一个**离线、可核验、带效力卡**的公司法领域法规全文库，封装为 Agent Skill。

收录截至 **2026年8月31日** 现行有效的公司、证券、破产领域法律、行政法规、司法解释及中国证监会现行规章
共 **37 件全文**，每件附效力状态、公布机关、文号、施行日期与官方来源链接。

> 💡 **核心价值**：断网可用、无需 API 额度、全文完整、每条引用可溯源到官方链接。
> 与传统"实时检索类"法律技能互补——本技能负责**拿权威原文**，检索类技能负责**验时效、补汇编外法规**。

---

## 收录范围（37 件，五部分）

| 部分 | 内容 | 件数 |
|------|------|------|
| 一 | 公司法及其司法解释（含解释一至五、时间效力规定、88条批复） | 8 |
| 二 | 公司登记、注册资本与财务会计 | 6 |
| 三 | 证券发行与上市（IPO、承销、再融资、外资股、创投减持、区域性市场） | 7 |
| 四 | 上市公司监管（治理、股东会、信披、重组、收购、投关、现场检查、国有股权、合规） | 9 |
| 五 | 企业破产（破产法全文、破产解释一至三、管理人规定与报酬、企业改制） | 7 |

完整清单与效力速查表见 [`references/00-index-and-status.md`](references/00-index-and-status.md)。

---

## 目录结构

```
company-law-compendium-2026/
├── SKILL.md                    # 技能主指令（路由规则、引用规范、输出模板）
├── README.md
├── LICENSE                     # MIT
└── references/                 # 知识库（786KB，11 个按需加载文件）
    ├── 00-index-and-status.md  # 总索引、37件效力速查表、立法动态、已知瑕疵
    ├── 01-company-law.md                               # 公司法全文
    ├── 02-company-law-judicial-interpretations.md      # 公司法解释一至五等
    ├── 03-registration-capital-finance.md              # 登记、注册资本、财务会计
    ├── 04-securities-issuance-underwriting.md          # 发行与承销
    ├── 05-foreign-shares-broker-regional-market.md     # 外资股、创投减持、四板
    ├── 06-listed-governance-disclosure.md              # 公司治理与信息披露
    ├── 07-restructuring-acquisition.md                 # 重组与收购
    ├── 08-investor-relation-state-owned-compliance.md  # 投关、现场检查、国有股权
    ├── 09-enterprise-bankruptcy-law.md                 # 企业破产法全文
    └── 10-bankruptcy-interpretations-restructuring.md  # 破产解释、管理人、改制
```

**按需加载设计**：`SKILL.md` 中定义了文件路由表，Agent 一次只读取与问题直接相关的 1–2 个分册，
避免把 786KB 全部塞进上下文。

---

## 安装

### 方式一：curl 逐文件下载（WorkBuddy 用户级）

```bash
mkdir -p ~/.workbuddy/skills/company-law-compendium-2026/references && cd ~/.workbuddy/skills/company-law-compendium-2026

BASE="https://raw.githubusercontent.com/goof00/company-law-compendium-2026/main"

curl -fsSL -o SKILL.md "$BASE/SKILL.md"
curl -fsSL -o LICENSE "$BASE/LICENSE"
curl -fsSL -o README.md "$BASE/README.md"

for f in 00-index-and-status 01-company-law 02-company-law-judicial-interpretations \
         03-registration-capital-finance 04-securities-issuance-underwriting \
         05-foreign-shares-broker-regional-market 06-listed-governance-disclosure \
         07-restructuring-acquisition 08-investor-relation-state-owned-compliance \
         09-enterprise-bankruptcy-law 10-bankruptcy-interpretations-restructuring; do
  curl -fsSL -o "references/$f.md" "$BASE/references/$f.md"
done
```

### 方式二：git clone

```bash
git clone https://github.com/goof00/company-law-compendium-2026.git \
  ~/.workbuddy/skills/company-law-compendium-2026
```

### 方式三：让 AI 助手代装

把本仓库地址告诉你的 AI 助手，让它按上述步骤安装到用户级 Skills 目录即可。

---

## 使用方法

安装后，直接提问即可自动激活，例如：

- "查一下新公司法第88条关于未届出资期限股权转让的规定"
- "股东知情权诉讼的司法解释依据是什么？"
- "上市公司收购达到30%触发要约收购的依据条文"
- "破产原因的认定标准，破产法怎么规定的？"
- "帮我检索注册资本认缴期限的相关规定并出一份合规清单"

### 强制规则（技能内已内置）

1. **先读索引再读分册**，禁止一次性读入全部文件
2. **逐字摘录条文原文**，汇编未收录的直说未收录，绝不凭记忆默写
3. 每条引用必须包含：**法规全称 + 文号 + 第X条 + 施行日期 + 官方来源链接**
4. 超过效力基准日（2026-08-31）的引用，**主动提示时效核验**
5. 涉及在修文件（如公司法统一司法解释、破产法修订草案）时，**主动提示立法动态**

---

## 与其他法律技能的关系

| 场景 | 推荐工具 |
|------|---------|
| 拿权威条文原文、断网环境 | **本技能** |
| 核验时效、检索汇编外法规 | 华宇元典 MCP、北大法宝 MCP、`legal-retrieval` |
| 类案检索 | `case-retrieval`、华宇元典案例库 |
| 文书起草 | `china-legal-assistant`、`draft-litigation-docs` |

---

## 已知瑕疵

源汇编存在少量提取残留，已在本仓库索引中标注并尽力修正，引用前建议复核：

- 第 11、12 件「效力状态」字段源提取有括号残留（索引已清洗）
- 第 16、19、25 件源汇编缺「施行日期」字段，索引据「沿革」推定
- 第 4、5、14 件无官方来源链接

---

## 免责声明

- 本汇编为依据公开官方来源整理的**工作参考文本**，非官方出版物。文本重排与网页提取可能存在个别标点、空格差异。
- **正式引用（起诉状、法律意见书、交易文件等）前，请务必以官方公布文本为准核对**。
- 效力状态以整理基准日 **2026年8月31日** 为准，此后如有制定、修改、废止，以官方最新发布为准。
- 本技能的 AI 输出不构成正式法律意见，具体案件处理请咨询执业律师。

---

## 许可证

MIT License — 详见 [LICENSE](LICENSE)。

法律、行政法规、司法解释及部门规章的**正文文本属于公共资料**，
依照《中华人民共和国著作权法》第五条第（一）项不适用著作权保护。
MIT 许可证仅覆盖本仓库的组织结构、检索路由设计、索引编排与效力卡整理工作。
