# AVD

Auto Vision Dataset (自动视觉数据集)

## 项目概述
`AVD` 是一个功能强大的计算机视觉数据集生成工具，全称 Auto Vision Dataset，旨在帮助研究人员和开发者快速创建高质量、多样化的视觉数据集，支持多种计算机视觉任务，包括目标检测、语义/实例分割、目标计数和场景理解等。

## 核心功能
- **多任务支持**：同时支持目标检测、语义分割、实例分割、目标计数和场景理解
- **高质量标注**：自动生成精确的边界框、掩码和类别标签
- **数据增强**：内置丰富的数据增强策略，提高模型泛化能力
- **场景多样性**：可配置不同场景、光照条件和背景复杂度
- **自定义配置**：灵活的参数设置，支持自定义目标类型、密度和分布
- **格式兼容性**：支持导出COCO、VOC、YOLO等多种主流数据集格式

## 安装指南
```bash
# 克隆仓库
git clone https://github.com/yourusername/avd.git
cd avd

# 创建虚拟环境
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt
```

## 快速开始
```python
# 基本用法示例
from avd import DatasetGenerator

# 创建生成器实例
generator = DatasetGenerator(
    output_dir="./datasets/my_dataset",
    task_type="detection+segmentation",  # 同时生成检测和分割数据
    num_images=1000,                     # 生成1000张图像
    object_categories=["car", "pedestrian", "bicycle"],  # 包含的目标类别
    image_resolution=(1280, 720)         # 图像分辨率
)

# 生成数据集
generator.generate()

# 导出为COCO格式
generator.export(format="coco")
```

## 高级配置
```yaml
# 配置文件示例 (config.yaml)
output_dir: "./datasets/custom_dataset"
image_resolution: [1920, 1080]
num_images: 2000

task_type:
  - detection
  - segmentation
  - counting

object_categories:
  - name: "car"
    count_range: [2, 5]
    size_range: [50, 150]
    occlusion_probability: 0.3
  - name: "pedestrian"
    count_range: [3, 8]
    size_range: [30, 80]
    occlusion_probability: 0.2

backgrounds:
  - type: "city"
    ratio: 0.6
  - type: "highway"
    ratio: 0.4

augmentations:
  - flip: {probability: 0.5}
  - rotate: {range: [-15, 15], probability: 0.3}
  - brightness: {range: [0.8, 1.2], probability: 0.4}
```

使用配置文件运行：
```bash
python generate.py --config config.yaml
```

## 支持的任务类型
- **目标检测**：生成带有边界框和类别的标注数据
- **语义分割**：为每个像素分配类别标签
- **实例分割**：为每个独立目标生成精确的掩码
- **目标计数**：提供精确的目标数量标注
- **场景理解**：包含场景类别和属性标注

## 数据集格式
支持导出以下格式：
- COCO JSON format
- Pascal VOC XML format
- YOLO format
- TFRecord format
- Mask R-CNN format

## 依赖项
- Python 3.8+
- OpenCV
- NumPy
- Pillow
- PyYAML
- scikit-image
- matplotlib
- pycocotools

## 贡献指南
欢迎通过以下方式贡献代码：
1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 打开Pull Request

## 许可证
本项目采用MIT许可证 - 详见 [LICENSE](LICENSE) 文件

## 联系方式
- 项目维护者: [Your Name](mailto:your.email@example.com)
- 项目链接: [https://github.com/yourusername/avd](https://github.com/yourusername/avd)
