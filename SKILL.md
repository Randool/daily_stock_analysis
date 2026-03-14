---
name: "stock_analyzer"
description: "分析股票和市场。当用户想要分析单个或多个股票，或进行市场复盘时调用。"
---

# 股票分析器

本技能基于 `analyzer_service.py` 的逻辑，提供分析股票和整体市场的功能。

## 使用方法 (Fire CLI)

`analyzer_service.py` 已封装为 Fire CLI，可直接通过命令行调用：

```bash
# 分析单只股票
python analyzer_service.py analyze_stock --stock_code=600989

# 分析多只股票
python analyzer_service.py analyze_stocks --stock_codes='["600989","000001"]'

# 生成完整报告
python analyzer_service.py analyze_stock --stock_code=600989 --full_report=true

# 执行大盘复盘
python analyzer_service.py perform_market_review
```

### 参数说明

| 函数 | 参数 | 类型 | 说明 |
|------|------|------|------|
| `analyze_stock` | `stock_code` | str | 股票代码 |
| | `full_report` | bool | 是否生成完整报告 (默认：false) |
| `analyze_stocks` | `stock_codes` | List[str] | 股票代码列表 (JSON 格式) |
| | `full_report` | bool | 是否为每只股票生成完整报告 (默认：false) |
| `perform_market_review` | - | - | 无参数 |

### `AnalysisResult`输出结构

分析函数返回一个 `AnalysisResult` 对象（或其列表），该对象具有丰富的结构。以下是其关键组件的简要概述，并附有真实的输出示例：

`dashboard` 属性包含核心分析，分为四个主要部分：
1.  **`core_conclusion`**: 一句话总结、信号类型和仓位建议。
2.  **`data_perspective`**: 技术数据，包括趋势状态、价格位置、量能分析和筹码结构。
3.  **`intelligence`**: 定性信息，如新闻、风险警报和积极催化剂。
4.  **`battle_plan`**: 可操作的策略，包括狙击点（买/卖目标）、仓位策略和风险控制清单。

## 注意事项

分析过程较为漫长，建议配置超时时间为10min+
