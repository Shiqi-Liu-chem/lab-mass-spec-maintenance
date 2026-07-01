# TOF Operation Log — 飞行时间质谱操作日志系统

> **MSMM** — On the Maintenance and Management of Mass Spectrometers in Our Research Group

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)]()

一个基于 Python/tkinter 的桌面应用程序，帮助课题组管理和记录飞行时间质谱（TOF-MS）仪器的日常使用情况。支持实验记录的增删改查（CRUD）、ESI 参数的屏幕捕获与 OCR 自动识别、分子式 m/z 计算、CSV/Excel 导出等功能。

---

## 📑 目录

- [功能特性](#-功能特性)
- [屏幕截图](#-屏幕截图)
- [安装指南](#-安装指南)
  - [方式一：直接运行可执行文件（推荐）](#方式一直接运行可执行文件推荐)
  - [方式二：从源码运行](#方式二从源码运行)
- [使用说明](#-使用说明)
  - [基本操作流程](#基本操作流程)
  - [ESI 参数捕获](#esi-参数捕获)
  - [分子式 m/z 计算](#分子式-mz-计算)
  - [数据导出](#数据导出)
  - [快捷键](#快捷键)
- [项目结构](#-项目结构)
- [技术栈](#-技术栈)
- [数据库结构](#-数据库结构)
- [构建与打包](#-构建与打包)
- [已知问题与待改进](#-已知问题与待改进)
- [贡献者](#-贡献者)
- [致谢](#-致谢)
- [许可证](#-许可证)
- [课题组主页](#-课题组主页)

---

## ✨ 功能特性

- 📝 **实验记录管理**：完整记录每次 TOF-MS 使用信息——日期、时间段、操作者、实验目的、溶剂、清洗状态、离子源参数、样品信息和分子式、电荷、样品峰等
- 🔍 **ESI 参数自动捕获**：通过屏幕截图 + Tesseract OCR，自动识别质谱仪器软件界面上显示的 ESI（电喷雾电离）参数，避免手动输入错误
- ⚗️ **分子式 m/z 计算**：内置完整的元素周期表原子量数据库，支持解析任意分子式（含括号嵌套），自动计算精确质量与 m/z 值
- 📊 **数据管理**：支持本地 SQLite 数据库存储，实时搜索筛选、列头排序、右键拖拽多选
- 📤 **数据导出**：支持导出选中记录为 CSV 或 Excel（.xlsx）格式，自动调整列宽
- 🖥️ **独立运行**：可通过 PyInstaller 打包为 Windows 独立可执行文件（.exe），无需安装 Python 环境
- ⌨️ **键盘友好**：Enter 键在输入字段间跳转；Ctrl+S 快速保存；Ctrl+F 聚焦搜索框

---

## 📸 屏幕截图

*（应用运行截图待补充 — 建议在此处放置主界面、ESI 捕获、导出功能等截图）*

参考图像：
- `ESI_information.jpg` — 质谱软件中 ESI 数据的显示位置参考
- `ESI_preview.jpg` — ESI 数据区域预览

---

## 📦 安装指南

### 方式一：直接运行可执行文件（推荐）

1. 前往 [Releases](https://github.com/your-username/TOF_Operation_Log/releases) 页面
2. 下载最新版本的 `TOF_Operation_Log.zip`
3. 解压后双击 `TOF_Operation_Log.exe` 即可运行

> **注意**：若需使用 ESI 捕获功能，请确保电脑已安装 [Tesseract-OCR](https://github.com/UB-Mannheim/tesseract/wiki) 至默认路径 `C:\Program Files\Tesseract-OCR\`。

### 方式二：从源码运行

**系统要求**：Python 3.8 及以上版本（已在 Python 3.13 上验证）

```bash
# 1. 克隆仓库
git clone https://github.com/your-username/TOF_Operation_Log.git
cd TOF_Operation_Log

# 2. 创建并激活虚拟环境（推荐）
python -m venv venv
venv\Scripts\activate   # Windows

# 3. 安装依赖
pip install -r requirements.txt

# 4. 安装 Tesseract-OCR（ESI 捕获功能必需）
# 下载地址：https://github.com/UB-Mannheim/tesseract/wiki
# 安装至默认路径：C:\Program Files\Tesseract-OCR\

# 5. 运行应用
python app.py
```

---

## 📖 使用说明

### 基本操作流程

1. **填写实验信息**：日期（自动填写当天）、时间段（如 `6:45-9:00`）、姓名、实验目的、溶剂、是否清洗干净
2. **输入样品信息**：分子式（如 `C6H12O6`）、电荷（如 `2+`, `1-`, `+3`）
3. **（可选）计算 m/z**：点击「计算样品峰 m/z」按钮，自动计算
4. **（可选）捕获 ESI**：点击「设置捕获区域」框选屏幕区域 → 点击「捕获 ESI」
5. **保存**：点击「保存」按钮或按 `Ctrl+S`

### ESI 参数捕获

1. 打开质谱仪器配套软件，确保 ESI 参数数据在屏幕上可见（参考 `ESI_information.jpg`）
2. 在 TOF Operation Log 应用中点击「**设置捕获区域**」按钮
3. 应用窗口最小化，屏幕进入半透明模式
4. 用鼠标**拖拽框选** ESI 数据所在的屏幕区域
5. 释放鼠标确认区域，或按 `Esc` 取消
6. 后续每次点击「**捕获 ESI**」，应用将自动对该区域进行 OCR 识别并填入参数

### 分子式 m/z 计算

- 支持**任意复杂度**的分子式，如 `C6H12O6`、`Na2SO4`、`[Fe(CN)6]3-`
- 支持**括号嵌套**：`([{}])` 均可使用
- 支持**水合物/加合物**书写：`C6H12O6·H2O` 或 `C6H12O6.H2O`
- 电荷格式灵活：`2+`、`+2`、`1-`、`-1` 均可识别

### 数据导出

- **CSV 导出**：选中表格行 → 点击「导出 CSV」→ 选择保存路径
- **Excel 导出**：选中表格行 → 点击「导出 Excel」→ 自动调整列宽和表头加粗
- 可通过右键拖拽批量选中多行

### 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Enter` | 跳转到下一个输入字段 |
| `Ctrl+S` | 保存当前记录 |
| `Ctrl+F` | 聚焦搜索框 |
| `双击记录` | 编辑该条记录 |
| `右键拖拽` | 批量选中多行 |

---

## 📁 项目结构

```
TOF_Operation_Log/
├── app.py                    # 主应用程序（814行，单文件）
├── requirements.txt          # Python 依赖
├── TOF_Operation_Log.spec    # PyInstaller 构建配置
├── .gitignore                # Git 忽略规则
├── experiments.db            # SQLite 数据库（本地工作副本）
├── ESI_information.jpg       # ESI 数据区域参考图
├── ESI_preview.jpg           # ESI 区域预览图
├── build/                    # PyInstaller 构建中间文件
├── dist/                     # 打包输出目录
│   ├── TOF_Operation_Log.exe
│   └── TOF_Operation_Log.zip
└── shs_VER/                  # 旧版仪器使用登记系统（配套参考）
    ├── instrument_records.db
    └── 仪器使用登记系统.exe
```

---

## 🛠 技术栈

| 技术 | 用途 |
|------|------|
| **Python** | 编程语言 |
| **tkinter** | GUI 图形界面 |
| **SQLite** | 本地数据库存储 |
| **Pillow (PIL)** | 屏幕截图与图像预处理（放大、灰度化、自动对比度、二值化） |
| **Tesseract OCR** | 光学字符识别，读取 ESI 参数 |
| **openpyxl** | Excel (.xlsx) 文件导出 |
| **PyInstaller** | 打包为 Windows 独立可执行文件 |

---

## 🗄 数据库结构

应用使用 SQLite 数据库（`experiments.db`），启用 WAL 日志模式。

### `experiments` 表

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | INTEGER | 主键，自增 |
| `date` | TEXT | 实验日期（格式：2025-01-15） |
| `time_period` | TEXT | 实验时间段（如 6:45-9:00） |
| `purpose` | TEXT | 实验目的 |
| `name` | TEXT | 操作者姓名 |
| `ion_source` | TEXT | 离子源参数（格式：2.50-40-80-100-20-50-600-4.6） |
| `sample_info` | TEXT | 样品分子式（如 C6H12O6） |
| `charge` | TEXT | 电荷信息（如 2+, 1-） |
| `sample_peaks` | TEXT | 样品峰 m/z 值 |
| `solvent` | TEXT | 溶剂 |
| `cleaned` | TEXT | 是否清洗干净（是/否） |
| `created_at` | TEXT | 记录创建时间（自动填充） |

---

## 🔧 构建与打包

使用 PyInstaller 将 Python 脚本打包为 Windows `.exe`：

```bash
# 使用 .spec 文件构建（推荐）
pyinstaller TOF_Operation_Log.spec

# 或直接使用命令行
pyinstaller --onefile --windowed --name "TOF_Operation_Log" \
    --hidden-import PIL --hidden-import PIL.ImageGrab \
    --hidden-import PIL.ImageFilter --hidden-import PIL.ImageOps \
    --hidden-import pytesseract --hidden-import openpyxl \
    app.py
```

构建输出位于 `dist/` 目录下。注意：`Tesseract-OCR` 为外部依赖，不会被打包进 exe，需用户自行安装。

---

## ⚠️ 已知问题与待改进

1. **自动识别 ESI 信息**：当前需手动框选区域，后续可考虑基于模板匹配的全自动识别
2. **旧电脑兼容性测试**：需在较旧配置的 Windows 电脑上测试运行效果
3. **多质谱平台适配**：当前针对 TOF-MS，需扩展支持其他质谱仪器的参数模板
4. **用户权限管理**：考虑添加用户登录与权限分级（防止他人修改过往记录）

---

## 👥 贡献者

感谢以下对本项目的贡献者：

- **Shiqi Liu** — 项目发起者、需求定义、测试与验证
- *（其他协作者待补充）*

> 本项目的主要代码由 [Claude Code](https://claude.ai/code)（Anthropic 出品的 AI 编程智能体）辅助编写完成。

---

## 🙏 致谢

- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) — 开源 OCR 引擎
- [Anthropic](https://www.anthropic.com/) — Claude Code AI 编程助手
- 课题组全体成员对需求调研与功能测试的支持

---

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源许可协议。

---

## 🔗 课题组主页

🏫 [中国科学院青岛生物能源与过程研究所 — 团簇化学与能源催化课题组](http://cluster.qibebt.ac.cn/)

欢迎访问课题组主页了解更多研究方向与最新成果。

---

*Last updated: 2025-07*
