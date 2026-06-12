# CCF Rank 2026 数据集

本仓库提供中国计算机学会（CCF）两份关键名录的结构化 JSON 数据，便于检索、统计与二次开发：

1. **《CCF 推荐国际学术会议和期刊目录（第七版，2026 年 3 月正式版）》**：A/B/C 三级国际目录（681 条）
2. **《CCF 计算领域高质量科技期刊分级目录（2025）》**：T1/T2/T3 三级中文期刊目录（68 条）

## 数据来源与三重校对方式

数据通过三次独立来源比对完成：

1. **官方 PDF 主源**：`第七版中国计算机学会推荐国际学术会议和期刊目录（正式版）.pdf`
2. **CCF 中文官网分类页**：<https://www.ccf.org.cn/Academic_Evaluation/By_category/>（含 10 个学科方向子页 `ARCH_DCP_SS / CN / NIS / TCSE_SS_PDL / DM_CS / TCS / CGAndMT / AI / HCIAndPC / Cross_Compre_Emerging`）
3. **CCF 计算领域高质量科技期刊分级目录页**：<https://www.ccf.org.cn/ccftjgjxskwml/>（2025 年发布的中文 T1/T2/T3 目录，已并入 `chinese_journal_catalog` 字段）

> 第七版 PDF 为最新权威版本，部分新增条目（如 JCC、ICXR、ACMDLT、APNet、HotStorage、ACMSIGOPSATC 等）尚未同步至官网静态页面。当 PDF 与官网出现差异时以 PDF 为准；官网用于交叉核验条目缩写、英文全称、出版社字段。

## 文件说明

- `ccf_rank_2026.json`：主数据文件（JSON，UTF-8）
- `第七版中国计算机学会推荐国际学术会议和期刊目录（正式版）.pdf`：原始 PDF 参考
- `README.md`：本说明文件

## 数据概览

### 国际目录（list）

| 指标 | 数量 |
|---|---|
| 年份 | 2026 |
| 版本 | 第七版（2026 年 3 月正式版） |
| 机构 | 中国计算机学会（CCF） |
| 学科方向（category）数量 | 10 |
| 期刊（Journal）条目 | 295 |
| 会议（Conference）条目 | 386 |
| **条目总计（list）** | **681** |

### 中文期刊目录（chinese_journal_catalog）

| 指标 | 数量 |
|---|---|
| 发布年份 | 2025 |
| 发布日期 | 2025-04-16 |
| **T1（最顶级期刊）** | **19** |
| **T2（非常优秀期刊）** | **22** |
| **T3（优秀期刊）** | **27** |
| **小计** | **68** |

### 按方向 / 类型 / 分级分布

| 方向 ID | 方向（中文） | 期刊 A / B / C | 会议 A / B / C | 小计 |
|:-:|:--|:-:|:-:|:-:|
| 0 | 计算机体系结构 / 并行与分布计算 / 存储系统 | 6 / 10 / 12 | 11 / 26 / 30 | 95 |
| 1 | 计算机网络 | 3 / 6 / 12 | 4 / 10 / 20 | 55 |
| 2 | 网络与信息安全 | 3 / 5 / 9 | 6 / 11 / 29 | 63 |
| 3 | 软件工程 / 系统软件 / 程序设计语言 | 4 / 12 / 9 | 10 / 20 / 27 | 82 |
| 4 | 数据库 / 数据挖掘 / 内容检索 | 4 / 14 / 16 | 5 / 13 / 13 | 65 |
| 5 | 计算机科学理论 | 3 / 13 / 12 | 5 / 10 / 10 | 53 |
| 6 | 计算机图形学与多媒体 | 4 / 9 / 15 | 4 / 14 / 17 | 63 |
| 7 | 人工智能 | 4 / 21 / 39 | 7 / 14 / 22 | 107 |
| 8 | 人机交互与普适计算 | 2 / 8 / 5 | 4 / 7 / 15 | 41 |
| 9 | 交叉 / 综合 / 新兴 | 4 / 15 / 16 | 2 / 7 / 13 | 57 |
| **合计** | — | **37 / 113 / 145** | **58 / 132 / 196** | **681** |

## JSON 顶层结构

```json
{
  "year": 2026,
  "edition": "第七版（2026年3月更新）",
  "name": "中国计算机学会推荐国际学术会议和期刊目录",
  "name_en": "CCF Recommended International Academic Conferences and Journals",
  "organization": "中国计算机学会",
  "organization_en": "China Computer Federation",
  "sources": [
    { "type": "pdf", "title": "...", "path": "..." },
    { "type": "website_zh", "url": "https://www.ccf.org.cn/Academic_Evaluation/By_category/", "note": "..." },
    { "type": "website_en", "url": "https://www.ccf.org.cn/en/", "note": "..." },
    { "type": "website_zh_high_quality", "url": "https://www.ccf.org.cn/ccftjgjxskwml/", "note": "..." }
  ],
  "category": [ /* 10 学科方向 */ ],
  "list":     [ /* 681 条国际期刊/会议条目 */ ],
  "chinese_journal_catalog": {
    "title": "计算领域高质量科技期刊分级目录（2025）",
    "release_date": "2025-04-16",
    "tiers": {
      "T1": {"description": "最顶级期刊", "count": 19},
      "T2": {"description": "非常优秀期刊", "count": 22},
      "T3": {"description": "优秀期刊", "count": 27}
    },
    "list": [ /* 68 条中文期刊条目 */ ]
  }
}
```

### `chinese_journal_catalog.list[]` 字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `num` | int | 当前 tier 内的顺号 |
| `tier` | str | `T1` / `T2` / `T3` |
| `name_cn` | str | 中文刊名（英文期刊则为中文官方译名，带「（英文）」后缀） |
| `name_en` | str | 英文刊名（仅英文期刊为非空，中文期刊为空字符串） |
| `cn_number` | str | 国内统一刊号 CN 号 |
| `language` | str | `中文` / `英文` |
| `sponsor` | str | 主办单位（多家时以、或；分隔） |

## 字段定义

### `category` 字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `id` | int | 学科方向编号（与 `list[].category_id` 对应） |
| `chinese` | str | 中文方向名称 |
| `english` | str | 英文方向名称 |

### `list` 字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `abbr` | str | 会议 / 期刊简称（PDF 中无简称时为空字符串） |
| `name` | str | 英文全称（与 `name_en` 等价，保留以兼容老用户） |
| `name_en` | str | 英文全称（CCF 官方英文称呼） |
| `name_cn` | str | 中文译名（仅有中文背景的中国主办期刊 / 会议为非空，如 `计算机科学技术学报`、`计算可视媒体`、`CCF 高性能计算汇刊` 等） |
| `publisher` | str | 出版社 / 主办方 |
| `type` | str | 类型（`Journal` / `Conference`） |
| `rank` | str | CCF 分级（`A` / `B` / `C`） |
| `category_id` | int | 所属方向编号，对应 `category[].id` |
| `category_chinese` | str | 所属方向的中文名称（便于直接读取） |
| `category_english` | str | 所属方向的英文名称（便于直接读取） |
| `url` | str | 参考链接（大多为 DBLP；少数为出版社主页或 CCF 检索；个别条目为空） |

## 快速使用

### Python 示例

```python
import json
from collections import Counter

with open("ccf_rank_2026.json", "r", encoding="utf-8") as f:
    data = json.load(f)

# 总体统计
print("条目总数:", len(data["list"]))

# 各等级数量
rank_count = Counter(item["rank"] for item in data["list"])
print(rank_count)

# 人工智能方向（id=7）A 类条目
ai_a = [
    item for item in data["list"]
    if item["category_id"] == 7 and item["rank"] == "A"
]
for item in ai_a:
    print(item["type"][0], item["abbr"], item["name_en"])
```

### JavaScript (Node.js) 示例

```javascript
const fs = require('fs');

const data = JSON.parse(fs.readFileSync('ccf_rank_2026.json', 'utf-8'));

const byType = data.list.reduce((acc, item) => {
  acc[item.type] = (acc[item.type] || 0) + 1;
  return acc;
}, {});

console.log(byType);

// 列出 CCF-A 会议
const aConfs = data.list.filter(
  (x) => x.type === 'Conference' && x.rank === 'A'
);
console.log(`CCF-A 会议数量: ${aConfs.length}`);
```

### 按方向中文名查询

```python
target = "人工智能"
ai_items = [x for x in data["list"] if x["category_chinese"] == target]
print(len(ai_items), "条人工智能方向条目")
```

### 中文期刊目录查询

```python
# 列出 T1 中文期刊
t1_cn = [
    j for j in data["chinese_journal_catalog"]["list"]
    if j["tier"] == "T1" and j["language"] == "中文"
]
for j in t1_cn:
    print(j["num"], j["name_cn"], j["cn_number"])

# 列出所有英文期刊（T1+T2+T3）
en_journals = [
    j for j in data["chinese_journal_catalog"]["list"]
    if j["language"] == "英文"
]
print(f"中文目录中的英文期刊共 {len(en_journals)} 本")
```

## 数据清洗与使用建议

- 条目英文全称统一沿用 CCF 公布的官方写法（包括 `Computer-Aided`、`Multi-agent`、`Pacific-Asia` 等大小写与连字符）。
- `abbr` 为空时通常因 PDF 原表也未给出（如 `Parallel Computing`、`Ad Hoc Networks` 等普通英文刊名作简称使用）。
- `name_cn` 仅在 CCF 文件、官网或主办单位提供中文名称时填写。绝大多数国际会议 / 期刊在中英文目录中均使用英文官方名称，因此 `name_cn` 为空属正常情况，并非缺漏。
- 部分 `category_id == 2`（网络与信息安全）下出现了 `TCC`（Theory of Cryptography Conference）与 `category_id == 0` 下的 `TCC`（IEEE Transactions on Cloud Computing），这是 PDF 原文的重名缩写，使用时需按 `category_id` + `type` 区分。
- 部分 URL 为 DBLP 旧路径或会议历史路径，批量访问前建议先做存活性检查。

## 与旧版的主要差异

相比 5/6 版（即仍可在 CCF 官网静态页面看到的版本），第七版（2026 年 3 月）的主要新增 / 修订（已纳入本数据）包括但不限于：

- 计算机体系结构方向：`HPDC` 升级到 A 类；新增 `ISCAS`(B)、`SEC`、`NAS`、`HotStorage`、`APPT`、`JCC` 等 C 类；`USENIX ATC` 名称改为 `ACM SIGOPS ATC（原 USENIX ATC）`。
- 计算机网络方向：新增 `TIOT`(C)、`APNet`(C) 等。
- 网络与信息安全方向：新增 `Cybersecurity`(B)、`HCC`(C)、`CODASPY`、`BlockSys`、`CSCloud` 等。
- 软件工程方向：新增 `PACMPL`(C)、`CC`(B)、`MEMOCODE`(C) 等。
- 数据库与数据挖掘方向：新增 `DSE`(B)、`TIST`(C)、`TORS`(C)、`WISE`(B)、`WISA`(C) 等。
- 人工智能方向：`ICLR` 升级到 A 类；`PR/TACL/JATS/TIIS/TELO` 等编号变动；C 类大幅扩充（共 39 期刊）。
- 人机交互方向：新增 `CCFTPCI`(B)、`THRI`(C)、`ICXR`(C) 等。
- 交叉 / 综合 / 新兴方向：新增 `WWW`(A 会议)、`BCRA`(B)、`EITEE`(C)、`TCSS`(C)、`HEALTH`、`ACMDLT`、`IJTCS-FAW` 等。

## 校对方法学

- **逐条三重校对**：每条条目均以 PDF 表格行作为主源，对照 CCF 中文官网分类页与 CCF 英文站点的同一条目进行核对，并经程序化去重 / 排序后写入 JSON。
- **关键字段**：`abbr`、`type`、`rank`、`category_id` 是检索主键，本仓库对这四个字段执行过完全 hash 去重检查（无重复）。
- **PDF 行内空白消除**：原 PDF 由于排版，许多英文全称被压缩为无空格字符串（如 `ACMTransactionsonComputerSystems`），本仓库已统一恢复为带空格的官方英文写法。

## 版权与使用说明

本仓库为公开目录的结构化整理版本。原始目录版权归中国计算机学会（CCF）所有。

- 建议用于学习、研究、检索与统计分析。
- 若用于发布、再分发或商业用途，请先核对 CCF 官方使用条款与版权要求。

## 致谢

感谢中国计算机学会（CCF）发布推荐目录，为学术评价与选刊选会提供参考。
