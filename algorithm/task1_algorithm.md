# 算法组第一次自学任务——目标检测算法初步

## 任务概述

本任务旨在帮助你快速入门 YOLO（You Only Look Once）目标检测算法，掌握基本的使用方法和实践技能。

## 学习目标

- 理解 YOLO 算法的基本原理
- 掌握 YOLOv8 的安装和环境配置
- 学会使用预训练模型进行目标检测
- 了解如何在自定义数据集上训练模型

## 任务内容

### 第一部分：理论学习

#### 1. YOLO 算法原理

- **什么是目标检测？**
  - 目标检测 = 定位（Where）+ 分类（What）
  - 输出：边界框坐标 + 类别标签 + 置信度

- **YOLO 的核心思想**
  - 将目标检测视为回归问题
  - 一次前向传播完成检测（One-Stage Detector）
  - 将图像划分为 S×S 网格
  - 每个网格预测 B 个边界框及其置信度
  - 速度快，适合实时检测

#### 2. 推荐学习资源

- 论文阅读：
  - [YOLOv1 原论文](https://arxiv.org/abs/1506.02640)
  - [YOLOv8 官方文档](https://docs.ultralytics.com/)

---

### 第二部分：环境配置

#### 1. 安装 Python 环境

```bash
# 推荐使用 Python 3.10 或更高版本
python --version
```

#### 2. 安装 PyTorch

根据你的系统和 CUDA 版本选择合适的安装命令：

```bash
# CPU 版本
pip install torch torchvision torchaudio

# GPU 版本 (CUDA 11.8，根据实际型号调整)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

#### 3. 安装 Ultralytics

```bash
pip install ultralytics
```

---

### 第三部分：实践任务

#### 任务 1：使用预训练模型进行图像检测

**目标：** 使用 YOLOv8 预训练模型检测图像中的物体

**步骤：**

自行查阅ultralytics官方文档

---

#### 任务 2：视频目标检测

**目标：** 对视频或摄像头实时流进行目标检测

**步骤：**

自行查阅ultralytics官方文档

---

#### 任务 3：自定义数据集训练

**目标：** 在自己的数据集上训练 YOLO 模型

**步骤：**

1. **准备数据集**

数据集目录结构：

```
custom_dataset/
├── images/
│   ├── train/
│   │   ├── img1.jpg
│   │   ├── img2.jpg
│   │   └── ...
│   └── val/
│       ├── img1.jpg
│       └── ...
└── labels/
    ├── train/
    │   ├── img1.txt
    │   ├── img2.txt
    │   └── ...
    └── val/
        ├── img1.txt
        └── ...
```

标注文件格式（YOLO 格式，每行一个对象）：

```
class_id center_x center_y width height
```

其中所有坐标都是归一化的（0-1）

2. **创建数据集配置文件**

```yaml
# 数据集路径
path: /path/to/custom_dataset
train: images/train
val: images/val

# 类别数量
nc: 3

# 类别名称
names:
  0: class1
  1: class2
  2: class3
```

3. **训练模型** 

```python
from ultralytics import YOLO

# 加载预训练模型
model = YOLO('yolov8n.pt')

# 训练模型
results = model.train(
    data='dataset.yaml',
    epochs=100,
    imgsz=640,
    batch=16,
    name='custom_yolo',
    device=0  # 使用 GPU 0，CPU 则设为 'cpu'
)
```

4. **评估模型**

```python
# 验证模型
metrics = model.val()
print(f"mAP50: {metrics.box.map50}")
print(f"mAP50-95: {metrics.box.map}")
```

5. **使用训练好的模型**

```python
model = YOLO('runs/detect/custom_yolo/weights/best.pt')
results = model('test_image.jpg')
```

---

#### 任务 4：数据标注工具使用

**推荐工具：**

1. **LabelImg**
```bash
pip install labelImg
labelImg
```
- 简单易用，适合小规模标注
- 支持 YOLO 格式直接导出

2. **Roboflow**
- 在线标注平台：https://roboflow.com/
- 提供数据增强、格式转换等功能
- 免费版有一定限制

3. **CVAT**
- 开源标注工具：https://cvat.org/
- 功能强大，支持团队协作
- 可本地部署或使用云服务

---

### 第四部分：进阶任务

1. **YOLO12初步**

YOLO12是ultralytics提出的基于Transformer架构的目标检测模型。其使用Transformer进行特征提取（而非CNN），实现了视野的扩大和精度的提升。其中的区域注意力模块进一步提高了推理速度。 
请自行配置YOLO12的环境，在自定义数据集上进行训练和测试，比较其与其他YOLO版本的不同。

2. **小目标检测优化**

无人机搭载的相机所拍摄到的目标通常较小，有时甚至只有十几个像素。一般通用的YOLO模型难以检测到，请你在YOLO11n的基础之上，对网络结构做出一些修改，使之在小目标检测任务中表现更佳。训练和评估该模型时，可以使用一些公开的无人机目标检测数据集。

---

## 提交要求

完成以下内容并提交：

1. **实践报告**（Markdown 或 PDF）
   - 环境配置截图
   - 预训练模型检测结果（至少 3 张图片）
   - 视频/摄像头检测的演示（截图或短视频）
   - 如完成自定义训练，提供训练过程和结果

2. **代码文件**
   - 所有编写的 Python 脚本
   - 数据集配置文件（如有）
   - requirements.txt 

3. **学习笔记**
   - YOLO 原理的理解
   - 遇到的问题和解决方案
   - 心得体会

4. **数据集**

如果用到了自定义数据集或者其他公开数据集，请提供网盘链接。==千万不要直接上传数据集到github==

---

## 参考资源

- [Ultralytics YOLOv8 官方文档](https://docs.ultralytics.com/)
- [YOLO GitHub 仓库](https://github.com/ultralytics/ultralytics)
- [COCO 数据集](https://cocodataset.org/)
- [Roboflow 数据集平台](https://roboflow.com/)
