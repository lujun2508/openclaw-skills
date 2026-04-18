---
name: workspace-guardian
description: "AI 文件输出规范。统一命名规则和目录结构，避免文件散落。适用于 Win/Mac/Linux。"
user-invocable: false
metadata:
  openclaw:
    os: ["win32", "linux", "darwin"]
---

# Workspace Guardian

> 用户未指定路径时，本 skill 约束文件的存放位置和命名方式。

---

## 核心规则

### 一个项目一个目录

所有文件归属项目，禁止散落到 `~/`、桌面、下载目录或带时间戳的临时文件夹。

### 命名规范

```
{date}_{描述}.{ext}
```

示例: `2026-04-14_report.xlsx`

脚本: `{动词}_{对象}.py`（如 `generate_report.py`）

### 目录结构

```
{项目根目录}/
├── output/     ← 最终交付物
├── scripts/    ← 脚本和工具
├── data/       ← 数据文件
├── docs/       ← 文档
├── temp/       ← 临时文件
└── README.md
```

---

## 特殊情况

### 用户指定路径
按用户指示执行。

### 无明确项目归属
输出到 Agent 自身的工作区:
- `drafts/` — 待确认内容
- `output/` — 已确认内容
- `temp/` — 临时文件，用完即清

### Agent 工作区
`~/.openclaw/workspace-*/` 下的文件由各 Agent 自行管理。

---

## 维护规则

### 临时文件
任务完成后清理 `temp/`，不留积累。

### 被拒绝的输出
用户否定后立即删除文件。

### 脚本版本更新
归档旧版本，加日期后缀（如 `generate_report_v4_2026-04-09.py`）。

### 空目录
不留空目录。

### 定期检查（每数天）
检查以下问题并询问用户确认后再处理:
- 遗留的旧临时文件
- 可合并的多版本脚本
- 空目录

---

## 自检

创建文件后确认位置:
```
📁 已保存: {项目目录}/{文件名}
```
