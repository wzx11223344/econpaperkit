# <img src="https://img.icons8.com/color/48/latex.png" width="32" /> EconPaperKit

<p align="center">
  <b>专业经济学论文 LaTeX 模板套件 — 中英双语 + 自动化编译 + CI/CD 发布</b>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"></a>
  <a href="https://github.com/wzx11223344/econpaperkit"><img src="https://img.shields.io/badge/stars-%E2%98%85%E2%98%85%E2%98%85-yellow?logo=github" alt="GitHub Stars"></a>
  <a href="https://github.com/wzx11223344/econpaperkit/actions"><img src="https://img.shields.io/badge/CI-passing-brightgreen?logo=githubactions&logoColor=white" alt="CI"></a>
  <a href="https://www.latex-project.org/"><img src="https://img.shields.io/badge/LaTeX-%E2%9C%93-008080?logo=latex&logoColor=white" alt="LaTeX"></a>
</p>

---

## 目录

- [简介](#简介)
- [安装与准备](#-安装与准备)
- [快速开始](#-快速开始)
- [模板结构](#-模板结构)
- [核心组件详解](#-核心组件详解)
- [GitHub Actions 自动化](#-github-actions-自动化)
- [论文写作指南](#-论文写作指南)
- [贡献指南](#-贡献指南)
- [参考文献](#-参考文献)
- [许可证](#-许可证)

---

## 简介

**EconPaperKit** 是专为经济学研究者设计的 LaTeX 论文模板套件。内置完整的经济学论文结构、计量经济学特定宏包、三线表回归结果模板和 GitHub Actions 自动编译流水线。一次配置，永续使用。

**核心特性：**

- 中文 (ctex) / 英文 (article) 双模式切换
- 三线表 (`booktabs`) + `dcolumn` 小数点对齐的回归表模板
- TikZ / PGFPlots 经济学图表模板
- 常用计量经济学公式宏包 (`\E`, `\Var`, `\Cov`, `\plim`, `\indep` 等)
- BibLaTeX + GB/T 7714 中文引用格式支持
- GitHub Actions 推送自动编译 PDF，Release 自动发布
- 预配置论文结构：引言 → 文献综述 → 理论框架 → 数据 → 实证 → 稳健性 → 结论

---

## 安装与准备

### LaTeX 发行版安装

```bash
# macOS — MacTeX (完整)
brew install --cask mactex

# Ubuntu / Debian — TeX Live
sudo apt install texlive-full

# Windows — MiKTeX 或 TeX Live
# 下载: https://miktex.org/ 或 https://tug.org/texlive/
```

### 使用模板

```bash
# 克隆模板仓库
git clone https://github.com/wzx11223344/econpaperkit.git my_paper
cd my_paper/template

# 编辑 main.tex 撰写论文
# 编译
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex   # 两次以获得正确交叉引用
```

### 所需 LaTeX 包

| 包名 | 用途 | CTAN 链接 |
|------|------|-----------|
| `booktabs` | 专业三线表 | [booktabs](https://ctan.org/pkg/booktabs) |
| `threeparttable` | 表下注 | [threeparttable](https://ctan.org/pkg/threeparttable) |
| `dcolumn` | 小数点对齐 | [dcolumn](https://ctan.org/pkg/dcolumn) |
| `amsmath` | AMS 数学环境 | [amsmath](https://ctan.org/pkg/amsmath) |
| `biblatex` | 参考文献管理 | [biblatex](https://ctan.org/pkg/biblatex) |
| `hyperref` | 超链接 | [hyperref](https://ctan.org/pkg/hyperref) |
| `graphicx` | 图片插入 | [graphicx](https://ctan.org/pkg/graphicx) |
| `tikz` / `pgfplots` | 图表绘制 | [pgfplots](https://ctan.org/pkg/pgfplots) |
| `ctex` | 中文支持 (可选) | [ctex](https://ctan.org/pkg/ctex) |

---

## 快速开始

### 1. 切换英文/中文模式

在 `main.tex` 顶部取消/注释对应行：

```latex
% ===== 中文模式 =====
\documentclass[12pt,a4paper]{ctexart}     % ctex 支持
\usepackage[heading]{ctex}

% ===== 英文模式 =====
\documentclass[12pt,a4paper]{article}
```

### 2. 三线表回归结果

```latex
\regtable{%
  X1 & 0.523^{***} & 0.485^{***} & 0.412^{***} & 0.398^{***} \\
     & (0.082)     & (0.078)     & (0.065)     & (0.061)     \\
  X2 & -0.234^{**} & -0.198^{**} & -0.176^{**} & -0.165^{**} \\
     & (0.095)     & (0.089)     & (0.072)     & (0.068)     \\
  \midrule
  Controls & No  & Yes & Yes & Yes \\
  FE       & No  & No  & Yes & Yes \\
  N        & 1,000 & 1,000 & 1,000 & 1,000 \\
  $R^2$    & 0.12  & 0.28  & 0.45  & 0.52 \\
}
```

### 3. 计量经济学公式

```latex
% 预定义宏
\E{X}          % 期望
\Var(X)        % 方差
\Cov(X, Y)     % 协方差
\plim \hat{\beta}   % 概率极限
X \indep Y     % 独立

% 面板数据模型
\begin{equation}
  y_{it} = \alpha + \beta X_{it} + \gamma Z_{it}
           + \mu_i + \lambda_t + \varepsilon_{it}
\end{equation}
```

### 4. TikZ / PGFPlots 图形

```latex
\begin{tikzpicture}
  \begin{axis}[
    xlabel={X},
    ylabel={Y},
    title={Event Study Plot}
  ]
    \addplot[blue, mark=*] coordinates {(0,0)(1,0.5)(2,1.2)(3,0.8)};
    \addplot[red, dashed] coordinates {(0,0)(3,0)};
  \end{axis}
\end{tikzpicture}
```

---

## 模板结构

```
econpaperkit/
├── template/
│   ├── main.tex              # 主文档 — 撰写入口
│   ├── sections/             # 按章节拆分的 .tex 文件
│   │   ├── 01_introduction.tex
│   │   ├── 02_literature.tex
│   │   ├── 03_theory.tex
│   │   ├── 04_data.tex
│   │   ├── 05_results.tex
│   │   ├── 06_robustness.tex
│   │   └── 07_conclusion.tex
│   ├── tables/               # 表格文件 (.tex)
│   │   ├── summary_stats.tex
│   │   └── regression.tex
│   ├── figures/              # 图片文件 (.pdf/.png/.eps)
│   │   └── placeholder.txt
│   ├── references.bib        # BibLaTeX 参考文献
│   └── appendix.tex          # 附录
├── .github/workflows/
│   └── compile.yml           # GitHub Actions 自动编译
└── README.md
```

---

## 核心组件详解

### 预定义计量经济学宏

| 宏 | 渲染 | 用途 |
|------|------|------|
| `\E{X}` | $$\mathbb{E}[X]$$ | 期望算子 |
| `\Var{X}` | $$\operatorname{Var}(X)$$ | 方差 |
| `\Cov{X,Y}` | $$\operatorname{Cov}(X,Y)$$ | 协方差 |
| `\plim` | $$\operatorname{plim}$$ | 概率极限 |
| `\indep` | $$\perp\!\!\!\perp$$ | 统计独立 |

### 页面布局配置

| 设置 | 默认值 | 可调整 |
|------|:---:|------|
| 纸张大小 | A4 | `\documentclass[a4paper]` |
| 页边距 | 1 inch | `\usepackage[margin=1in]{geometry}` |
| 行距 | 1.5 倍 | `\onehalfspacing` / `\doublespacing` |
| 字体大小 | 12pt | `\documentclass[12pt]` |

### BibLaTeX 引用格式

```latex
% 英文论文: authoryear 风格
\usepackage[backend=biber, style=authoryear, maxcitenames=2]{biblatex}

% 中文论文: GB/T 7714-2015
\usepackage[backend=biber, style=gb7714-2015]{biblatex}

% 引用命令
\cite{wooldridge2010}          % (Wooldridge, 2010)
\parencite{greene2018}         % (Greene, 2018)
\textcite{angrist2009}         % Angrist and Pischke (2009)
```

---

## GitHub Actions 自动化

推送代码到 GitHub 后，Actions 自动执行以下流程：

```yaml
name: Compile LaTeX PDF

on:
  push:
    branches: [main]
  release:
    types: [published]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Compile LaTeX
        uses: xu-cheng/latex-action@v3
        with:
          root_file: template/main.tex
          latexmk_use_xelatex: true
      - name: Upload PDF
        uses: actions/upload-artifact@v4
        with:
          name: paper
          path: template/main.pdf
```

**触发条件：**
- `push` 到 `main` 分支 → 编译并上传 PDF artifact
- 创建 GitHub Release → 编译并将 PDF 附加到 Release

---

## 论文写作指南

### 推荐论文结构

```
1. 引言 (Introduction)
   - 研究动机、研究问题、边际贡献

2. 文献综述 (Literature Review)
   - 理论基础、实证发现、研究缺口

3. 理论框架 (Theoretical Framework)
   - 计量模型设定、识别策略、假设检验

4. 数据与变量 (Data & Variables)
   - 数据来源、样本选择、描述性统计

5. 实证结果 (Empirical Results)
   - 基准回归、内生性处理、机制分析

6. 稳健性检验 (Robustness Checks)
   - 替换变量、排除样本、安慰剂检验

7. 结论 (Conclusion)
   - 主要发现、政策含义、研究局限
```

### 排版建议

- 回归表统一使用 `\regtable{}` 宏模板
- 显著性标注: `^{***}` (1%), `^{**}` (5%), `^{*}` (10%)
- 图片优先使用 PDF 矢量格式 (TikZ 直接生成)
- 交叉引用使用 `\label{}` / `\ref{}` 避免手动编号

---

## 贡献指南

欢迎贡献模板改进！

- **新模板**: 英文 CV、教学幻灯片 (Beamer)、学位论文 (Dissertation)
- **宏包改进**: 新增计量经济学宏、优化表格样式
- **CI 优化**: 多文件项目编译支持、自动格式化检查

```bash
git clone https://github.com/wzx11223344/econpaperkit.git
cd econpaperkit
# 编辑 template/main.tex
# 提交前本地测试编译
xelatex template/main.tex
```

---

## 参考文献

1. **Wooldridge, J. M. (2010).** *Econometric Analysis of Cross Section and Panel Data (2nd ed.).* MIT Press.
2. **Greene, W. H. (2018).** *Econometric Analysis (8th ed.).* Pearson.
3. **Angrist, J. D. & Pischke, J.-S. (2009).** *Mostly Harmless Econometrics.* Princeton University Press.
4. **GB/T 7714-2015.** 信息与文献 参考文献著录规则. 中国国家标准化管理委员会.
5. **The LaTeX Project.** https://www.latex-project.org/
6. **PGFPlots Manual (v1.18).** https://ctan.org/pkg/pgfplots

---

## 许可证

本项目基于 [MIT License](LICENSE) 发布。Copyright &copy; 2024 wzx11223344.
