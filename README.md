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
├── awesomeideas/           # 每周经验分享，一次一个文件夹
│   ├── README.md
│   └── _template/
└── src/                   # 四个方向，实验记录各自放在对应目录下
    ├── README.md          # 实验记录怎么放
    ├── _template/         # 新建实验记录时复制这个
    ├── common/
    ├── image/
    ├── acoustic/
    └── iq/
```

## 分支与提交

| 场景 | 分支名 |
| :--- | :--- |
| 新功能 / 新实验 | `feat/<名字>/<主题>`，例 `feat/jianghan/vit-baseline` |
| 修 bug | `fix/<名字>/<主题>` |
| 只改文档 | 直接提交到 `main` |

- 实验在个人分支上做，**出结论再合回 `main`**
- `main` 任何时候都应该能跑通
- 提交信息说清做了什么：`add vit baseline on rfuav imageset`，不要 `update`
