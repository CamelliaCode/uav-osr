# 每周经验分享 · awsomeideas

每周一次，每人轮流分享一个「AI 使用小技巧」。

## 什么算一次合格的分享

- 一个具体场景 + 一段**能直接复制**的提示词
- 有前后对比（截图、数字都行）
- 别人看完能立刻用上

## 目录规范：一次分享 = 一个文件夹

```
awsomeideas/
├── _template/                       # 模板，复制这个
│   └── README.md
└── 2026-10-24-JH-paper-read/        # 日期-缩写-主题
    ├── README.md                    # 正文
    └── images/                      # 这篇用到的截图
        ├── 01-before.png
        └── 02-after.png
```

**为什么用文件夹，而不是单个 md**：截图要跟着正文走。单文件的话图片只能散在别处，一搬就断链。

## 命名规则

**`YYYY-MM-DD-缩写-主题`**

| 缩写 | 姓名 |
| :--- | :--- |
| `JH` | 江涵 |
| `YXJ` | 杨兴杰 |
| `ZH` | 张浩 |
| `ZWJ` | 章伟杰 |

- **缩写固定大写**，不要写成 `Jh`、`jh`——GitHub 区分大小写，会多出一个文件夹
- **主题用英文**，2–4 个单词，小写，连字符连接：

  | 好 | 不好 |
  | :--- | :--- |
  | `paper-read` | `读论文` |
  | `prompt-debug` | `how-i-use-ai-to-debug` |
  | `fig-plot` | `Figure Plot` |
  | `data-clean` | `data_clean_v2_final` |

完整标题不放在文件夹名里，写在 README 第一行 `# 标题`。

## 图片怎么插

1. 截图存成 png，放进这篇的 `images/`，**按顺序编号**：`01-before.png`、`02-after.png`
2. 在 README.md 里用**相对路径**引用：

```markdown
![前后对比](images/01-before.png)
```

## 图片怎么上传（三条路，选一条）

**A. 拖整个文件夹（不用装 git，最省事）**

1. 本地建好 `2026-10-24-JH-paper-read/`，里面放 `README.md` 和 `images/`
2. 打开 https://github.com/CamelliaCode/uav-osr/upload/main/awsomeideas
3. 把整个文件夹拖进去，子目录结构会保留 → Commit changes

**B. 边写边粘贴（最快）**

在网页上编辑 `README.md` 时，**直接把截图 Ctrl+V 粘进编辑框**，GitHub 会自动上传并插入链接。粘完检查一下路径，不是 `images/` 就手动改。

**C. 本地 git**

```powershell
git clone https://github.com/CamelliaCode/uav-osr.git
cp -r awsomeideas/_template awsomeideas/2026-10-24-JH-paper-read
# 改 md、放图
git add . ; git commit -m "add 2026-10-24 JH paper-read" ; git push
```

> Windows 下如果 `git status` 把中文名显示成一串 `\346\261\237`，跑一次
> `git config --global core.quotepath false` 就好。
