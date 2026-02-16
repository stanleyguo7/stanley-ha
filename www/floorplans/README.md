# 平面图文件目录

此目录用于存放各楼层的平面图 SVG 文件。

## 文件列表

请在此目录下放置以下平面图文件：

- `b1_floorplan.svg` - 地下室平面图
- `1f_floorplan.svg` - 一楼平面图
- `2f_floorplan.svg` - 二楼平面图
- `3f_floorplan.svg` - 三楼平面图

## 文件要求

1. **格式**: SVG (Scalable Vector Graphics)
2. **尺寸**: 建议使用实际比例，便于坐标定位
3. **路径**: 在 Dashboard 配置中使用 `/local/floorplans/` 路径引用

## 创建平面图

### 方法1: 使用 Inkscape（免费）

1. 下载安装 [Inkscape](https://inkscape.org/)
2. 创建新文档，设置合适的画布尺寸
3. 绘制或导入平面图
4. 保存为 SVG 格式

### 方法2: 使用在线工具

- [Draw.io](https://app.diagrams.net/) - 支持导出 SVG
- [SVG-Edit](https://svg-edit.github.io/svgedit/) - 在线 SVG 编辑器

### 方法3: 从 CAD 文件转换

如果有 CAD 格式的平面图，可以：
1. 使用 AutoCAD 导出为 SVG
2. 或使用在线转换工具转换格式

## 注意事项

- SVG 文件应该包含清晰的区域边界
- 建议使用不同的颜色或线条区分不同区域
- 保持文件大小合理（建议 < 500KB）
- 确保 SVG 文件可以在浏览器中正常显示

## 坐标参考

在 Dashboard 配置中，坐标系统：
- 原点 (0,0) 位于左上角
- X 轴向右递增
- Y 轴向下递增
- 单位：像素

建议在创建平面图时，记录每个区域的大致坐标范围，便于后续配置。
