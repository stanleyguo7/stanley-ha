# Packages 目录说明

此目录用于按楼层和区域组织 Home Assistant 的配置文件和自动化规则。

## 目录结构

```
packages/
├── b1/          # 地下室 (Basement 1)
├── 1f/          # 一楼 (Floor 1)
├── 2f/          # 二楼 (Floor 2)
├── 3f/          # 三楼 (Floor 3)
└── README.md    # 本说明文件
```

## 使用说明

### 在 configuration.yaml 中启用 packages

在 `configuration.yaml` 文件中添加以下配置以启用 packages：

```yaml
homeassistant:
  packages: !include_dir_named packages
```

或者按楼层分别加载：

```yaml
homeassistant:
  packages:
    b1: !include_dir_named packages/b1
    1f: !include_dir_named packages/1f
    2f: !include_dir_named packages/2f
    3f: !include_dir_named packages/3f
```

### 文件命名规范

每个区域的配置文件使用区域ID作为文件名，例如：
- `f1_living_room.yaml` - 客厅配置
- `b1_machine_room.yaml` - 机房配置

### 配置内容

每个区域的 YAML 文件可以包含：
- **设备配置**: 传感器、开关、灯光等设备
- **自动化规则**: 该区域相关的自动化
- **脚本**: 该区域相关的脚本
- **场景**: 该区域相关的场景

### 示例

```yaml
# 设备配置示例
sensor:
  - platform: template
    sensors:
      living_room_temperature:
        friendly_name: "客厅温度"
        value_template: "{{ states('sensor.living_room_temp') }}"

# 自动化配置示例
automation:
  - alias: "客厅自动开灯"
    trigger:
      - platform: state
        entity_id: binary_sensor.living_room_motion
        to: 'on'
    condition:
      - condition: state
        entity_id: sun.sun
        state: 'below_horizon'
    action:
      - service: light.turn_on
        entity_id: light.living_room
```

## 区域列表

### B1 (地下室) - 9个区域
- b1_machine_room.yaml - 机房
- b1_gym.yaml - 健身房
- b1_tea_room.yaml - 茶室
- b1_bar.yaml - 酒吧
- b1_bathroom.yaml - 浴室
- b1_theater.yaml - 影音室
- b1_laundry.yaml - 洗衣房
- b1_storage.yaml - 储藏间
- b1_equipment_room.yaml - 设备间

### 1F (一楼) - 8个区域
- f1_living_room.yaml - 客厅
- f1_western_kitchen.yaml - 西厨
- f1_chinese_kitchen.yaml - 中厨
- f1_study.yaml - 书房
- f1_senior_bedroom.yaml - 长辈房
- f1_garage.yaml - 车库
- f1_bathroom.yaml - 卫生间
- f1_entrance.yaml - 玄关

### 2F (二楼) - 5个区域
- f2_common_room.yaml - 休闲区
- f2_master_bedroom.yaml - 主卧
- f2_eldest_bedroom.yaml - 长子房
- f2_second_bedroom.yaml - 次子房
- f2_balcony.yaml - 露台

### 3F (三楼) - 2个区域
- f3_attic.yaml - 阁楼
- f3_bathroom.yaml - 卫生间

## 注意事项

1. 每个 YAML 文件必须使用正确的缩进（2个空格）
2. 确保所有实体ID在该区域内唯一
3. 可以使用区域ID来组织相关的设备和自动化
4. 建议为每个区域添加注释说明
