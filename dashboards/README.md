# FloorPlan Dashboard 配置说明

## 概述

此目录包含基于 FloorPlan 卡片的 Home Assistant Dashboard 配置文件。FloorPlan 是一个自定义卡片，可以在平面图上显示和控制设备。

## 文件说明

- `floorplan.yaml` - 主 Dashboard 配置文件，包含所有楼层的平面图视图

## 安装要求

### 1. 安装 FloorPlan 卡片

FloorPlan 卡片需要通过 HACS 安装：

1. 打开 HACS
2. 搜索 "FloorPlan"
3. 安装 `ha-floorplan` 卡片
4. 在 Lovelace 资源中添加卡片资源

### 2. 准备平面图图片

需要在 `www/floorplans/` 目录下放置平面图 SVG 文件：

```
www/
└── floorplans/
    ├── b1_floorplan.svg   # 地下室平面图
    ├── 1f_floorplan.svg   # 一楼平面图
    ├── 2f_floorplan.svg   # 二楼平面图
    └── 3f_floorplan.svg   # 三楼平面图
```

**注意**: 平面图文件需要是 SVG 格式，并且路径应该指向 `/local/floorplans/`。

## 配置说明

### Dashboard 结构

Dashboard 包含以下视图：

1. **地下室 (B1)** - 9个区域的平面图
2. **一楼 (1F)** - 8个区域的平面图
3. **二楼 (2F)** - 5个区域的平面图
4. **三楼 (3F)** - 2个区域的平面图
5. **总览** - 楼层导航页面

### 区域配置

每个区域在平面图上配置了：

- **位置坐标** (x, y) - 区域在平面图上的位置
- **尺寸** (width, height) - 区域的大小
- **实体映射** - 关联的传感器实体（如运动传感器）
- **交互动作**:
  - **点击** (tap_action) - 导航到该区域的详细页面
  - **长按** (hold_action) - 显示更多信息

### 坐标系统

坐标系统说明：
- **原点 (0,0)** 位于平面图的左上角
- **X轴** 向右递增
- **Y轴** 向下递增
- 单位：像素

### 自定义配置

#### 修改区域位置

编辑 `floorplan.yaml` 文件，找到对应区域的配置，修改 `x`, `y`, `width`, `height` 值：

```yaml
- type: image
  entity: binary_sensor.f1_living_room_motion
  x: 50        # X坐标
  y: 30        # Y坐标
  width: 150   # 宽度
  height: 120  # 高度
```

#### 添加设备控制

可以在区域配置中添加更多设备控制：

```yaml
- type: light
  entity: light.f1_living_room_main
  x: 100
  y: 50
  width: 40
  height: 40
  tap_action:
    action: toggle
```

#### 添加传感器显示

```yaml
- type: sensor
  entity: sensor.f1_living_room_temperature
  x: 100
  y: 50
  width: 60
  height: 30
```

## 使用步骤

### 1. 创建平面图文件

使用绘图软件（如 Inkscape、Adobe Illustrator）创建 SVG 格式的平面图，或使用在线工具生成。

### 2. 上传平面图

将 SVG 文件上传到 Home Assistant 的 `www/floorplans/` 目录。

### 3. 导入 Dashboard

在 Home Assistant 中：

1. 进入 **配置** > **仪表盘**
2. 点击右上角菜单，选择 **原始编辑器**
3. 将 `floorplan.yaml` 的内容复制粘贴到编辑器中
4. 保存配置

### 4. 调整坐标

根据实际的平面图尺寸，调整每个区域的坐标和尺寸，使其与平面图上的实际位置匹配。

### 5. 配置实体

确保配置中引用的实体（如 `binary_sensor.f1_living_room_motion`）在 Home Assistant 中存在。如果不存在，需要：

1. 在对应的区域 package 文件中添加设备配置
2. 或者修改 Dashboard 配置中的实体ID

## 区域列表

### B1 (地下室)
- 机房 (b1_machine_room)
- 健身房 (b1_gym)
- 茶室 (b1_tea_room)
- 酒吧 (b1_bar)
- 浴室 (b1_bathroom)
- 影音室 (b1_theater)
- 洗衣房 (b1_laundry)
- 储藏间 (b1_storage)
- 设备间 (b1_equipment_room)

### 1F (一楼)
- 客厅 (f1_living_room)
- 西厨 (f1_western_kitchen)
- 中厨 (f1_chinese_kitchen)
- 书房 (f1_study)
- 长辈房 (f1_senior_bedroom)
- 车库 (f1_garage)
- 卫生间 (f1_bathroom)
- 玄关 (f1_entrance)

### 2F (二楼)
- 休闲区 (f2_common_room)
- 主卧 (f2_master_bedroom)
- 长子房 (f2_eldest_bedroom)
- 次子房 (f2_second_bedroom)
- 露台 (f2_balcony)

### 3F (三楼)
- 阁楼 (f3_attic)
- 卫生间 (f3_bathroom)

## 高级功能

### 添加交互式元素

FloorPlan 支持多种交互式元素：

- **灯光控制** - 点击开关灯光
- **温度显示** - 显示温度传感器读数
- **运动检测** - 显示运动传感器状态
- **门锁控制** - 控制智能门锁
- **窗帘控制** - 控制智能窗帘

### 自定义样式

可以通过 CSS 自定义平面图的样式：

```yaml
- type: image
  entity: binary_sensor.f1_living_room_motion
  style:
    border: 2px solid blue
    opacity: 0.8
```

## 故障排除

### 平面图不显示

1. 检查 SVG 文件路径是否正确
2. 确认文件已上传到 `www/floorplans/` 目录
3. 检查文件权限

### 区域点击无响应

1. 检查实体ID是否正确
2. 确认实体在 Home Assistant 中存在
3. 检查坐标是否在平面图范围内

### 坐标不匹配

1. 使用浏览器开发者工具查看实际坐标
2. 根据平面图实际尺寸调整坐标
3. 可以使用在线工具辅助计算坐标

## 参考资源

- [FloorPlan 卡片文档](https://github.com/ExperienceLovelace/ha-floorplan)
- [Home Assistant Dashboard 文档](https://www.home-assistant.io/dashboards/)
- [SVG 编辑器推荐](https://inkscape.org/)
