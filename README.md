# MS Recording & Maintenance

> 质谱仪使用记录与维护管理系统 — 为课题组三台质谱仪（Q-IM-TOF / LTQ / Q-Exactive）提供统一的操作日志与维护计划管理。

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](../LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)]()

---

## 目录

- [功能特性](#-功能特性)
- [屏幕截图](#-屏幕截图)
- [快速开始](#-快速开始)
  - [方式一：直接运行 exe（推荐）](#方式一直接运行-exe推荐)
  - [方式二：从源码运行](#方式二从源码运行)
- [使用说明](#-使用说明)
  - [实验记录管理](#实验记录管理)
  - [分子式 m/z 计算](#分子式-mz-计算)
  - [维护记录管理](#维护记录管理)
  - [数据导出](#数据导出)
  - [快捷键](#快捷键)
- [数据库结构](#-数据库结构)
- [支持的质谱仪](#-支持的质谱仪)
- [从源码构建](#-从源码构建)
- [许可证](#-许可证)

---

## ✨ 功能特性

### 实验记录管理
- 📝 完整记录每次质谱实验信息：**日期、时间段、姓名、实验目的、溶剂、清洗状态、测试条件、样品分子式、电荷、样品峰**
- ⚗️ **分子式 m/z 自动计算**：内置完整元素周期表原子量数据库，支持任意复杂度分子式（含括号嵌套、水合物/加合物），输入分子式和电荷后一键计算 m/z
- 🔍 实时搜索筛选、列头排序、右键拖拽批量多选

### 维护记录管理
- 🔧 三种质谱仪各自预置维护类型及推荐周期
- 📅 选择维护类型后**自动计算下次维护日期**
- 🟢🟡🔴 维护状态可视化（正常 / 需关注 / 异常），表格行按状态着色，超期记录红色背景高亮
- 📊 显示各维护项**上次维护时间与周期对比**，一眼识别超期项目

### 数据导出
- 📤 实验记录 & 维护记录均支持**导出为 CSV 或 Excel（.xlsx）**
- 🎨 Excel 导出自动调整列宽、表头加粗，维护状态按颜色标注

### 用户体验
- 🌙 **深色主题**（GitHub Dark 风格），长时间使用不刺眼
- ⌨️ 键盘友好：Enter 在输入字段间跳转，Ctrl+S 快速保存，Ctrl+F 聚焦搜索
- 🔄 支持运行时切换质谱类型

---

## 📸 屏幕截图

> 以下为应用运行截图（点击图片可查看大图）

<p align="center">
  <img src="introduction/1.png" alt="主界面 - 选择质谱类型" width="45%">
  &nbsp;&nbsp;
  <img src="introduction/2.png" alt="实验记录管理界面" width="45%">
</p>

<p align="center">
  <img src="introduction/3.png" alt="维护记录管理界面" width="45%">
</p>

---

## 🚀 快速开始

### 方式一：直接运行 exe（推荐）

1. 前往 [Releases](https://github.com/Shiqi-Liu-chem/lab-mass-spec-maintenance/releases) 页面
2. 下载最新版本 `MS_recording&maintenance.exe`
3. 双击运行即可，无需安装 Python 环境

> 📌 首次运行时需选择质谱类型；后续启动将自动记住上次选择。

### 方式二：从源码运行

**系统要求**：Python 3.8+

```bash
# 1. 安装依赖
pip install -r requirements.txt

# 2. 运行
python "MS_recording&maintenance.py"
```

---

## 📖 使用说明

### 实验记录管理

1. 在主页面上方的表单区域依次填写：
   - **日期**（默认今天）、**时间段**（如 `6:45-9:00`）、**姓名**
   - **实验目的**、**溶剂**、**是否清洗干净**
   - **测试条件**（每种质谱仪有默认值）、**样品信息**（分子式）、**电荷**（如 `2+`, `1-`, `+3`）
2. 点击「**计算样品峰 m/z**」按钮，自动计算 m/z 值并填入「样品峰」字段
3. 点击「**保存**」或按 `Ctrl+S`

### 分子式 m/z 计算

| 特性 | 说明 | 示例 |
|------|------|------|
| 常规分子式 | 直接书写 | `C₆H₁₂O₆` → `C6H12O6` |
| 括号嵌套 | 支持 `()`, `[]`, `{}` 多层嵌套 | `[Fe(CN)₆]³⁻` |
| 水合物/加合物 | 用 `·` 或 `.` 连接 | `C6H12O6·H2O` |
| 电荷格式 | 灵活支持 | `2+`, `+2`, `1-`, `-1` |

### 维护记录管理

1. 点击右上角「**🔧 维护记录**」按钮进入维护管理页面
2. 在表单中填写：
   - **日期**、**姓名**（操作人员）
   - **维护类型**（下拉选择，每台仪器有专属维护项）
   - **状态**：正常 / 需关注 / 异常
   - **下次维护**：可点击「自动计算」根据推荐周期自动填充
   - **备注**：自由描述
3. 保存后，表格中会按状态着色，超期记录红色背景提醒
4. 底部显示各项维护的**上次时间和周期对比**，快速掌握维护进度

### 数据导出

- **CSV 导出**：选中表格行 → 点击「导出 CSV」
- **Excel 导出**：选中表格行 → 点击「导出 Excel」→ 自动调整列宽和格式
- 未选中行时，Excel 导出会导出全部数据

### 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Enter` | 跳转到下一个输入字段 |
| `Ctrl+S` | 保存当前记录 |
| `Ctrl+F` | 聚焦搜索框 |
| `双击记录` | 编辑该条记录 |
| `右键拖拽` | 批量选中多行 |

---

## 🗄 数据库结构

应用使用 SQLite 数据库（`ms_data.db`），包含两张表：

### `experiments` 表 — 实验记录

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | INTEGER | 主键，自增 |
| `date` | TEXT | 实验日期（如 2025-01-15） |
| `time_period` | TEXT | 时间段（如 6:45-9:00） |
| `purpose` | TEXT | 实验目的 |
| `name` | TEXT | 操作者姓名 |
| `ion_source` | TEXT | 测试条件参数 |
| `sample_info` | TEXT | 样品分子式 |
| `charge` | TEXT | 电荷信息 |
| `sample_peaks` | TEXT | 样品峰 m/z 值 |
| `solvent` | TEXT | 溶剂 |
| `cleaned` | TEXT | 是否清洗干净（是/否） |
| `ms_type` | TEXT | 质谱类型 |
| `created_at` | TEXT | 创建时间（自动填充） |

### `maintenance` 表 — 维护记录

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | INTEGER | 主键，自增 |
| `ms_type` | TEXT | 质谱类型 |
| `date` | TEXT | 维护日期 |
| `name` | TEXT | 维护人员姓名 |
| `record_type` | TEXT | 维护类型 |
| `status` | TEXT | 维护后状态（正常/需关注/异常） |
| `notes` | TEXT | 备注 |
| `next_date` | TEXT | 建议下次维护日期 |
| `created_at` | TEXT | 创建时间（自动填充） |

---

## 🔬 支持的质谱仪

| 质谱仪 | 维护项数量 | 维护周期范围 |
|--------|-----------|-------------|
| **Q-IM-TOF** | 4 项 | 30–180 天 |
| **LTQ** | 8 项 | 7–90 天 |
| **Q-Exactive** | 8 项 | 7–90 天 |

各类维护项详情（如 ESI 喷针清洗、质量校准、机械泵震气、更换泵油等）见应用内下拉菜单。

---

## 🔧 从源码构建

使用 PyInstaller 打包为 Windows 可执行文件：

```bash
# 安装 PyInstaller
pip install pyinstaller

# 使用 .spec 文件构建
pyinstaller "MS_recording&maintenance.spec"

# 输出在 dist/ 目录下
```

> `.spec` 文件已预先配置好 `--windowed`（无控制台窗口）和所需 hidden imports。

---

## 📁 项目文件说明

| 文件/目录 | 说明 |
|-----------|------|
| `MS_recording&maintenance.py` | 主程序源码（~1600 行） |
| `MS_recording&maintenance.spec` | PyInstaller 构建配置 |
| `requirements.txt` | Python 依赖 |
| `dist/` | 打包输出目录（含 exe） |
| `maintenance.xlsx` | 维护计划参考表格 |
| `introduction/` | 宣传素材（截图、视频 Storyboard） |

---

## 🙏 致谢

- 本项目代码由 [Claude Code](https://claude.ai/code)（Anthropic AI 编程助手）辅助编写
- 需求与测试：[中国科学院青岛生物能源与过程研究所 — 团簇化学与能源催化课题组](http://cluster.qibebt.ac.cn/)

---

## 📄 许可证

本项目采用 [MIT License](../LICENSE) 开源许可协议。

---

*Last updated: 2026-07*
