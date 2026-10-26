# Transformer-pytorch

基于 PyTorch 的 Transformer 英译中学习项目，包含模型实现、训练、束搜索解码和单句翻译脚本。

## 项目结构

- `config.py`：模型参数、设备和文件路径配置。
- `main.py`：训练、验证和测试入口。
- `translate.py`：交互式单句翻译入口。
- `model/`：Transformer 模型、损失计算和优化器。
- `tools/`：数据加载、分词器加载和实验目录管理。
- `data/*.py`：语料处理脚本。
- `tokenizer/`：SentencePiece 分词器及词表。

## 环境与运行

原项目使用 Python 3.10，其他依赖见 `requirements.txt`。PyTorch 需要根据服务器的 GPU 和驱动单独安装，文件中注释的 CUDA 版本仅为原作者的环境示例。

当前代码默认使用 NVIDIA CUDA，并包含 CUDA 多 GPU 损失计算。Mac Apple Silicon 使用 MPS 时需要先适配设备配置和训练逻辑；本仓库尚未完成 MPS 适配。

准备好环境及下列文件后，在项目根目录运行：

```bash
python main.py       # 训练
python translate.py  # 使用已有权重进行交互式翻译
```

## 数据集与权重

本仓库不包含数据集、模型权重和训练输出。这些文件保留在本地，部署到服务器时需单独传输：

- `data/json/train.json`
- `data/json/dev.json`
- `data/json/test.json`
- `data/corpus.en`、`data/corpus.ch`：重新训练分词器时使用。
- `weights/transformer_model.pth`：对应 `config.model_path`。
- `run/train/exp/weights/best_bleu_26.30.pth`：对应 `config.test_model_path`。

已提供的分词器与预训练权重应配套使用。若改变模型结构或词表，需要重新训练相应权重。
