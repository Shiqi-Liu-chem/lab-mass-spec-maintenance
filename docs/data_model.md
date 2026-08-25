# 数据模型

应用使用 SQLite 数据库 `ms_data.db` 保存实验与维护记录，并使用 JSON 文件 `ms_config.json` 保存当前用户的应用配置。

## 存储位置与升级迁移

Windows 下的数据保存在当前用户可写目录：

```text
%APPDATA%\MSRecordingMaintenance\ms_data.db
%APPDATA%\MSRecordingMaintenance\ms_config.json
```

若系统未提供 `%APPDATA%`，应用会尝试使用 `%USERPROFILE%\Application Data`。非 Windows 系统使用 `~/.local/share/MSRecordingMaintenance`。

从旧版便携式发布包首次升级时，如果程序目录中存在旧的 `ms_data.db` 或 `ms_config.json`，且用户数据目录中尚无同名文件，应用会自动复制旧文件；不会覆盖已有用户数据。

SQLite 以 WAL 模式运行，因此数据库旁可能出现 `ms_data.db-wal` 和 `ms_data.db-shm`。这些文件属于正常运行数据，数据库及其伴随文件必须保持可写。升级或备份前建议先退出应用，再复制整个 `MSRecordingMaintenance` 文件夹。

## 配置文件 `ms_config.json`

| 字段 | 类型 | 说明 |
|------|------|------|
| `ms_type` | string | 上次选择的质谱类型：`Q-IM-TOF`、`LTQ` 或 `Q-Exactive` |
| `admin_password_hash` | string | 管理员密码的 SHA-256 哈希；明文密码不落盘 |

## `experiments` 表 — 实验记录

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | INTEGER | 主键，自增 |
| `date` | TEXT | 实验日期，如 `2026-08-25` |
| `time_period` | TEXT | 时间段，如 `16:00-17:00` |
| `purpose` | TEXT | 实验目的 |
| `name` | TEXT | 操作者姓名 |
| `ion_source` | TEXT | 旧版“测试条件”兼容字段；当前版本使用下方动态字段 |
| `sample_info` | TEXT | 样品信息或分子式 |
| `charge` | TEXT | 电荷信息 |
| `sample_peaks` | TEXT | 样品峰 m/z 值 |
| `solvent` | TEXT | 溶剂 |
| `cleaned` | TEXT | 是否清洗干净（是/否） |
| `vacuum_pressure` | TEXT | 真空度 |
| `vacuum_status` | TEXT | 真空状态（正常/需关注/异常） |
| `ms_type` | TEXT | 质谱类型 |
| `created_at` | TEXT | 创建时间（自动填充） |

### 测试条件动态字段

当前版本根据质谱类型显示不同测试条件，并将每个物理参数写入独立数据库列。未被当前仪器使用的列保持为空。

| 中文字段 | 数据库列 | 适用质谱 |
|----------|----------|----------|
| 毛细管电压 | `capillary_voltage` | Q-IM-TOF / LTQ |
| 采样锥电压 | `sampling_cone_voltage` | Q-IM-TOF |
| 离子源偏置电压 | `ion_source_bias` | Q-IM-TOF |
| 离子源温度 | `ion_source_temp` | Q-IM-TOF |
| 去溶剂化温度 | `desolvation_temp` | Q-IM-TOF |
| 锥孔气流量 | `cone_gas_flow` | Q-IM-TOF |
| 去溶剂气流量 | `desolvation_gas_flow` | Q-IM-TOF |
| 雾化气压力 | `nebulizer_pressure` | Q-IM-TOF |
| 鞘气 | `sheath_gas` | LTQ / Q-Exactive |
| 辅助气 | `aux_gas` | LTQ / Q-Exactive |
| 喷雾电压 | `spray_voltage` | LTQ / Q-Exactive |
| 毛细管温度 | `capillary_temp` | LTQ / Q-Exactive |
| 管透镜电压 | `tube_lens_voltage` | LTQ |
| 吹扫气 | `sweep_gas` | Q-Exactive |
| S-lens 射频电平 | `slens_rf_level` | Q-Exactive |
| 辅助器加热器温度 | `aux_heater_temp` | Q-Exactive |

应用启动时会检查并补建缺失列，以兼容旧数据库。已有记录不会被覆盖。

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
