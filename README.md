# CCF Rank 2026 数据集

本仓库提供中国计算机学会（CCF）推荐国际学术会议和期刊目录（第七版，2026 年 3 月更新）的结构化 JSON 数据，便于检索、统计与二次开发。

## 文件说明

- `ccf_rank_2026.json`：主数据文件（JSON）
- `中国计算机学会推荐国际学术会议和期刊目录第七版（2026年3月更新）.pdf`：原始参考文档

## 数据概览

- 年份：2026
- 机构：中国计算机学会（CCF）
- 学科方向（category）数量：10
- 会议/期刊条目（list）数量：671

## JSON 顶层结构

```json
{
  "year": 2026,
  "name": "中国计算机学会推荐国际学术会议和期刊目录",
  "organization": "中国计算机学会",
  "category": [
    {
      "id": 0,
      "chinese": "计算机体系结构/并行与分布计算/存储系统",
      "english": "Computer Architecture / Parallel and Distributed Computing / Storage System"
    }
  ],
  "list": [
    {
      "abbr": "TOCS",
      "name": "ACMTransactionsonComputerSystems",
      "publisher": "ACM",
      "type": "Journal",
      "rank": "A",
      "category_id": 0,
      "url": "http://dblp.uni-trier.de/db/journals/tocs/"
    }
  ]
}
```

## 字段定义

### `category` 字段

- `id`：学科方向编号（与 `list[].category_id` 对应）
- `chinese`：中文方向名称
- `english`：英文方向名称

### `list` 字段

- `abbr`：会议/期刊简称（部分条目可能为空）
- `name`：会议/期刊全称（部分名称存在原始格式问题）
- `publisher`：出版社/主办方
- `type`：类型（通常为 `Journal` 或 `Conference`）
- `rank`：CCF 分级（`A` / `B` / `C`）
- `category_id`：所属方向编号，对应 `category[].id`
- `url`：参考链接（多数为 DBLP）

## 快速使用

### Python 示例

```python
import json
from collections import Counter

with open("ccf_rank_2026.json", "r", encoding="utf-8") as f:
    data = json.load(f)

# 统计各等级数量
rank_count = Counter(item["rank"] for item in data["list"])
print(rank_count)

# 输出人工智能方向（id=7）的 A 类条目
ai_a = [
    item for item in data["list"]
    if item.get("category_id") == 7 and item.get("rank") == "A"
]
for item in ai_a[:10]:
    print(item["abbr"], item["name"])
```

### JavaScript (Node.js) 示例

```javascript
const fs = require('fs');

const raw = fs.readFileSync('ccf_rank_2026.json', 'utf-8');
const data = JSON.parse(raw);

const byType = data.list.reduce((acc, item) => {
  acc[item.type] = (acc[item.type] || 0) + 1;
  return acc;
}, {});

console.log(byType);
```

## 数据清洗建议

- 建议根据 `category_id` 建立映射表，避免直接硬编码方向名称。
- 个别 `abbr` 为空、`name` 连写或包含特殊格式，可在使用前做标准化清洗。
- 部分 `url` 可能跳转或历史失效，批量使用前建议先做可用性检查。

## 版权与使用说明

本仓库为公开目录的数据整理版本。原始目录版权归中国计算机学会（CCF）所有。

- 建议用于学习研究、检索与统计分析。
- 若用于发布、再分发或商业用途，请先核对 CCF 官方使用条款与版权要求。

## 致谢

感谢中国计算机学会（CCF）发布推荐目录，为学术评价与选刊选会提供参考。