# A股模拟交易系统 / A-Share Paper Trading System

[English](#english) | [中文](#中文)

---

## 📋 简介

这是一个完整的A股模拟交易系统，用于学习和技术研究。不涉及真实资金交易。

This is a complete A-share paper trading system for learning and technical research. No real money involved.

## ✨ 功能特点

### 数据获取
- 📈 实时行情数据（需要VPN或Tushare API）
- 📊 历史K线数据（日/周/月）
- 🏢 个股基本面数据
- 📉 大盘指数数据

### 交易功能
- 💰 纸上交易（模拟交易，不真实下单）
- 📋 持仓管理
- 💵 资金管理（初始100万模拟金）
- 📊 盈亏计算

### 策略回测
- 📈 均线策略 (MA)
- 🚀 动量策略 (Momentum)
- 🎯 突破策略 (Breakout)
- 🔲 网格策略 (Grid)

---

## 🚀 快速开始

### 环境要求

```bash
# Python 3.8+
python --version

# 安装依赖
pip install pandas requests
```

### 1. 获取股票数据

```bash
# 获取茅台日线数据（250天）
python scripts/fetch_daily.py --stock 600519 --days 250

# 获取多个股票
python scripts/fetch_daily.py --stock 000001 --days 250
python scripts/fetch_daily.py --stock 000002 --days 250
```

### 2. 运行回测

```bash
# 均线策略回测
python scripts/backtest.py --stock 600519 --strategy ma

# 动量策略回测
python scripts/backtest.py --stock 600519 --strategy momentum

# 自定义初始资金
python scripts/backtest.py --stock 600519 --strategy ma --capital 1000000
```

### 3. 模拟交易

```bash
# 查看当前持仓
python scripts/simulate.py --show

# 买入股票
python scripts/simulate.py --buy --stock 600519 --shares 1000 --price 1800.0

# 卖出股票
python scripts/simulate.py --sell --stock 600519 --shares 500 --price 1850.0
```

---

## 📖 策略说明

### 均线策略 (MA)
- **原理**：短期均线上穿长期均线买入，下穿卖出
- **参数**：MA5, MA10, MA20
- **适用**：趋势明显的行情

### 动量策略 (Momentum)
- **原理**：追涨杀跌，涨跌幅超过阈值时操作
- **参数**：涨跌幅阈值（默认5%）
- **适用**：波动较大的行情

### 突破策略 (Breakout)
- **原理**：20日高点突破买入，跌破5日低点卖出
- **适用**：趋势启动阶段

### 网格策略 (Grid)
- **原理**：震荡行情中在设定价格区间内网格交易
- **适用**：横盘震荡行情

---

## 📁 项目结构

```
a-stock-trader/
├── SKILL.md              # 技能说明文档
├── README.md             # 本文件
├── _meta.json            # 元数据
├── scripts/
│   ├── fetch_daily.py    # 数据获取脚本
│   ├── backtest.py       # 回测脚本
│   └── simulate.py       # 模拟交易脚本
└── references/
    └── (参考资料)
```

---

## 🔧 进阶使用

### 数据源配置

系统默认使用东方财富网API。如需使用Tushare：

```python
# 在 fetch_daily.py 中修改
TUSHARE_TOKEN = "your_token_here"
```

### 自定义策略

在 `backtest.py` 中添加新的策略函数：

```python
def my_strategy(df, param1=10, param2=20):
    """自定义策略"""
    df = df.copy()
    # 实现你的策略逻辑
    df["signal"] = ...
    return df
```

### 定时任务

可以使用cron设置定时任务：

```bash
# 每天收盘后获取数据
0 16 * * 1-5 python /path/to/scripts/fetch_daily.py --stock 600519

# 每周回测
0 18 * * 5 python /path/to/scripts/backtest.py --stock 600519
```

---

## ⚠️ 免责声明

1. 本系统仅供学习研究，不构成投资建议
2. 模拟交易不涉及真实资金
3. 历史业绩不代表未来表现
4. 投资者据此操作，风险自担

---

## 📞 交流反馈

- 提交Issue: https://github.com/BOMBFUOCK/a-stock-trader/issues
- 欢迎Star ⭐ 和 Fork

---

## English

### Overview

A complete A-share (Chinese stock market) paper trading system with:
- Data fetching from East Money / Tushare
- Strategy backtesting (MA, Momentum, Breakout, Grid)
- Paper trading simulation
- SQLite database storage

### Quick Start

```bash
# Install dependencies
pip install pandas requests

# Fetch data
python scripts/fetch_daily.py --stock 600519 --days 250

# Run backtest
python scripts/backtest.py --stock 600519 --strategy ma

# Paper trade
python scripts/simulate.py --show
python scripts/simulate.py --buy --stock 600519 --shares 100 --price 1800.0
```

### Disclaimer

For educational purposes only. Not investment advice. Paper trading involves no real money.
