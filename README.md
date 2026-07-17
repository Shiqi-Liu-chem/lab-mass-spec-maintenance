# MS Recording & Maintenance

> 质谱仪使用记录与维护管理系统 — 为课题组三台质谱仪（Q-IM-TOF / LTQ / Q-Exactive）提供统一的操作日志与维护计划管理。

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)]()

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

<p align="center">
  <img src="docs/screenshots/01-home.png" alt="Main interface for selecting a mass spectrometer" width="45%">
  &nbsp;&nbsp;
  <img src="docs/screenshots/02-experiment-log.png" alt="Experiment record management interface" width="45%">
</p>

<p align="center">
  <img src="docs/screenshots/03-maintenance-log.png" alt="Maintenance record management interface" width="60%">
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
pip install -r requirements.txt
python app.py
```

---

## 📖 使用说明

### 实验记录管理

1. 在主页面上方的表单区域依次填写：**日期**（默认今天）、**时间段**（如 `6:45-9:00`）、**姓名**、**实验目的**、**溶剂**、**是否清洗干净**
2. 输入**测试条件**（每种质谱仪有默认值）、**样品信息**（分子式）、**电荷**（如 `2+`, `1-`, `+3`）
3. 点击「**计算样品峰 m/z**」按钮，自动计算 m/z 值并填入「样品峰」字段
4. 点击「**保存**」或按 `Ctrl+S`

### 分子式 m/z 计算

| 特性 | 说明 | 示例 |
|------|------|------|
| 常规分子式 | 直接书写 | `C6H12O6` |
| 括号嵌套 | 支持 `()`, `[]`, `{}` 多层嵌套 | `[Fe(CN)6]3-` |
| 水合物/加合物 | 用 `·` 或 `.` 连接 | `C6H12O6·H2O` |
| 电荷格式 | 灵活支持 | `2+`, `+2`, `1-`, `-1` |

### 维护记录管理

1. 点击右上角「**🔧 维护记录**」按钮进入维护管理页面
2. 填写**日期**、**姓名**、**维护类型**（下拉选择，每台仪器有专属维护项）
3. 设置**状态**（正常 / 需关注 / 异常），点击「自动计算」根据推荐周期自动填充**下次维护日期**
4. 保存后，表格中会按状态着色，超期记录红色背景提醒

### 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Enter` | 跳转到下一个输入字段 |
| `Ctrl+S` | 保存当前记录 |
| `Ctrl+F` | 聚焦搜索框 |
| `双击记录` | 编辑该条记录 |
| `右键拖拽` | 批量选中多行 |

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

```bash
pip install pyinstaller
pyinstaller "MS_recording&maintenance.spec"
# 输出在 dist/ 目录下
```

---

## 📁 项目文件说明

| 文件/目录 | 说明 |
|-----------|------|
| `app.py` | 主程序源码 |
| `MS_recording&maintenance.spec` | PyInstaller 构建配置 |
| `requirements.txt` | Python 依赖 |
| `docs/screenshots/` | 应用截图 |
| `docs/storyboard.md` | 宣传视频分镜脚本 |
| `docs/data_model.md` | 数据库字段说明 |
| `sample_data/` | 脱敏示例数据 |

---

## 🔒 数据与隐私

本公开仓库不包含任何真实实验记录、人员数据、仪器凭证或未发表的研究数据。截图与示例文件均使用脱敏或虚构内容。使用者应遵守所在机构的数据管理与仪器安全规范。

---

## ⚠️ 使用限制

- 本项目为课题组工作流原型，并非仪器厂商官方软件。
- 维护周期为可配置参考值，不能替代制造商手册或机构标准操作规程（SOP）。
- 升级前请备份本地数据库。

---

## 🚧 开发状态

> [!IMPORTANT]
> 本项目仍在积极开发中。核心的实验记录、维护追踪、搜索与数据导出功能已完成实现，量化验证与更广泛的兼容性测试仍在进行中。

### 当前进度

- [x] 核心实验与维护记录工作流已实现
- [x] CSV 与 Excel 导出已实现
- [x] Windows 可执行文件已打包
- [ ] 代表性记录的数据完整性验证
- [ ] 导出一致性测试
- [ ] 更多质谱仪型号兼容性测试
- [ ] 自动化回归测试

当前版本应视为早期功能原型，而非经过全面验证的生产系统。计划中的验证工作详见 [Issue #1](https://github.com/Shiqi-Liu-chem/lab-mass-spec-maintenance/issues/1)。

---

## 🙏 致谢

- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) — 开源 OCR 引擎
- [Anthropic](https://www.anthropic.com/) — Claude Code AI 编程助手
- 课题组全体成员对需求调研与功能测试的支持

---

## 🔗 课题组主页

🏫 [中国科学院青岛生物能源与过程研究所 — 团簇化学与能源催化课题组](http://cluster.qibebt.ac.cn/)

欢迎访问课题组主页了解更多研究方向与最新成果。

---

## 👥 贡献者

感谢以下对本项目的贡献者：

- **Shiqi Liu** — 项目发起者、需求定义、测试与验证
- 联系方式：riixz17ya@gmail.com
- *（其他协作者待补充）*

> 本项目的主要代码由 [Claude Code](https://claude.ai/code)（Anthropic 出品的 AI 编程智能体）辅助编写完成。

---

## 🤖 AI 辅助开发

本项目由 Shiqi Liu 设计并主导开发，Claude Code 提供编码辅助。AI 工具参与了代码实现、调试与文档编写。项目需求、科学背景、设计决策、测试及最终审核均由作者负责。

---

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源许可协议。

---

*Last updated: 2026-07*
