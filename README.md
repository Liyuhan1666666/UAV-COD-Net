# UAV-COD-Net
Code for UAV-COD-Net（无人机视角下隐藏目标检测）
本仓库提供 UAV-COD-Net 的 PyTorch 实现代码
> 论文信息、项目主页、预训练权重和数据集下载链接将在发布时补充。


## 环境要求

- Python 3.8
- PyTorch 1.8.1
- CUDA：请安装与本机 PyTorch 版本兼容的 CUDA 环境

建议使用 Conda 创建独立环境：

```bash
conda create -n uavcod python=3.8
conda activate uavcod
pip install -r requirements.txt
```

## 数据集准备

数据集下载链接：**待补充**

下载并解压数据集后，请保证训练集与测试集分别包含以下目录：

```text
train_with_val/
├── images/
└── masks/

test/
├── images/
└── masks/
```

随后编辑 [`configs/_base_/dataset/dataset_configs.json`](configs/_base_/dataset/dataset_configs.json)，将 `root` 修改为本机数据集路径：

```json
{
  "msi_cod_tr": {
    "root": "/path/to/train_with_val/"
  },
  "msi_cod_te": {
    "root": "/path/to/test/"
  }
}
```

请保留该文件中 `image` 和 `mask` 的其余配置；默认图片后缀为 `.jpg`，掩码后缀为 `.png`。

## 训练

在项目根目录执行：

```bash
python main.py \
  --config configs/uav_hidenet/cod_uav_hidenet.py \
  --datasets-info configs/_base_/dataset/dataset_configs.json
```

训练结果、日志、预测图和模型权重默认保存至 `output/` 目录。

## 测试

使用训练好的权重进行测试：

```bash
python main.py \
  --config configs/uav_hidenet/cod_uav_hidenet.py \
  --datasets-info configs/_base_/dataset/dataset_configs.json \
  --load-from /path/to/model.pth \
  --test-only
```

## 论文细节

### UAV-COD-15K数据集

<div align="center">
  <img src="./assets/UAV-COD-15K-1.png" width="100%" />
</div>

<div align="center">
  <img src="./assets/UAV-COD-15K-2.png" width="100%" />
</div>

### 方法

<div align="center">
  <img src="./assets/frame.png" width="80%" />
</div>

<div align="center">
  <img src="./assets/module1.png" width="80%" />
</div>

<div align="center">
  <img src="./assets/module2.png" width="30%" />
</div>

### 实验

<div align="center">
  <img src="./assets/experiment.png" width="100%" />
</div>

<div align="center">
  <img src="./assets/experiment_qua.png" width="100%" />
</div>

## 引用

如果本项目对您的研究有帮助，请引用对应论文：

```bibtex
@article{UAV-COD-Net,
  title   = {无人机视角下隐藏目标检测},
  author  = {鄢杰斌，蒋佳，李昱翰，祝文涛，侯敬文，姜文晖，方玉明},
  journal = {},
  year    = {2026}
}
```
