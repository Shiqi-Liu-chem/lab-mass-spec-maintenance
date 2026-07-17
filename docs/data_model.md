# Data Model

应用使用 SQLite 数据库（`ms_data.db`），包含两张表。

## `experiments` 表 — 实验记录

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

## `maintenance` 表 — 维护记录

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
