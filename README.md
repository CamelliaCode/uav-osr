# uav-osr · 无人机开集识别

> 基于大模型的多模态无人机开集识别 —— 图像 / 声学 / IQ

## 项目概述

| 项 | 内容 |
| :--- | :--- |
| 任务 | 无人机**开集识别**（Open-Set Recognition）：已知机型正确分类，未知机型判为 unknown |
| 数据集 | RFUAV（ImageSet）、DRFF-R2 |
| 模态 | ① image　② 声学　③ 纯 IQ |
| 方法 | ViT 基线 → 大模型（Qwen 系列）LoRA / 全参数微调 |
| 评测 | 闭集准确率、AUROC、OSCR、FPR@95TPR |

三条技术路线共享同一套数据加载、评测脚本和可视化，所以放在**同一个仓库**里，用目录区分。

## 团队与分工

| 姓名 | GitHub | 主攻方向 | 负责内容 |
| :--- | :--- | :--- | :--- |
| 章伟杰 | @CamelliaCode | 总体 | 进度把控、跨模态协调 |
| 江涵 | 待填 | image | 图像模态实验、ViT 基线 |
| 杨兴杰 | 待填 | image（兼声学） | 图像模态、声学方案 |
| 张浩 | 待填 | 纯 IQ | IQ 信号、数据集与文档 |

## 目录结构

```
uav-osr/
├── README.md
├── requirements.txt
├── .gitignore
├── data/                  # 只放数据集说明和索引，不放数据本体
│   └── README.md
├── experiments/           # 一次实验一个目录，见 experiments/README.md
│   ├── README.md
│   └── _template/         # 新建实验时复制这个
├── asmeideas/             # 每周经验分享，一次一份，见 asmeideas/README.md
│   ├── README.md
│   └── _template.md
├── src/
│   ├── common/            # 数据加载 / 指标 / 可视化，三条线共用
│   ├── image/             # 图像模态
│   ├── acoustic/          # 声学模态
│   └── iq/                # 纯 IQ 信号
└── scripts/               # 训练、评测、数据集处理脚本
```

## 环境

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux / macOS
source .venv/bin/activate

pip install -r requirements.txt
```

数据集不在仓库里，路径和获取方式见 [`data/README.md`](data/README.md)。

## 快速开始

```bash
# 1. 下载数据集（见 data/README.md），放到本地某个目录
# 2. 复制一份配置，改成自己的路径
cp experiments/_template/config.yaml experiments/exp-YYYYMMDD-demo-rfuav-01/config.yaml
# 3. 跑
python scripts/train.py --config experiments/exp-YYYYMMDD-demo-rfuav-01/config.yaml
```

> `scripts/train.py` 还没有实现，第一个实现它的人顺手把这条命令改对。

## 实验规范

1. **实验 ID**：`exp-YYYYMMDD-<方法>-<数据集>-<序号>`，例：`exp-20261019-vit-rfuav-01`
2. 每次实验在 `experiments/<实验ID>/` 下建目录，复制 `_template/` 里的两个文件
3. 权重、日志、可视化图**不进仓库**，传 OpenList，在实验 README 里写链接
4. 结论写进实验 README 的「结论」一节，2–3 句；表格里只放实验 ID

## 每周分享

每周一次经验分享会，每人轮流讲一个可复用的做法（20 分钟讲 + 10 分钟讨论）。

- 记录放 [`asmeideas/`](asmeideas/README.md)，一次一份，命名 `YYYY-MM-DD-主题.md`
- 复制 `asmeideas/_template.md` 起步
- 分享记录表在 `asmeideas/README.md` 底部，讲完加一行

## 进度管理

任务、负责人、状态、预计完成时间在**腾讯文档智能表格**里维护（链接：待填）。

原则：**状态放表格，结论放仓库。** 每周一上午各人更新自己那几行，周会只看逾期和阻塞。

## 分支与提交

| 场景 | 分支名 |
| :--- | :--- |
| 新功能 / 新实验 | `feat/<名字>/<主题>`，例 `feat/jianghan/vit-baseline` |
| 修 bug | `fix/<名字>/<主题>` |
| 只改文档 | 直接提交到 `main` |

- 实验在个人分支上做，**出结论再合回 `main`**
- `main` 任何时候都应该能跑通
- 提交信息说清做了什么：`add vit baseline on rfuav imageset`，不要 `update`

## 大文件

- 数据、权重、日志 → OpenList（S3），仓库里只放脚本和链接
- 单文件超过 50 MB 就不要提交，`.gitignore` 已经挡了常见后缀
