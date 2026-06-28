# EconPaperKit — 经济学论文 LaTeX 模板套件

[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Compile](https://github.com/wzx11223344/econpaperkit/actions/workflows/compile.yml/badge.svg)](https://github.com/wzx11223344/econpaperkit/actions/workflows/compile.yml)

专业的经济学中英文论文 LaTeX 模板，支持**自动化编译**和 **GitHub Actions CI**。

## ✨ 特性

- 📝 **中英文双语**: 支持中文（ctex）和英文（article）两种模式
- 📊 **表格模板**: 三线表回归结果、描述性统计表、相关系数矩阵
- 📈 **图片支持**: TikZ/PGFPlots 经济学图表模板
- 🔢 **数学公式**: 常用计量经济学公式宏包
- 🤖 **GitHub Actions**: 推送自动编译 PDF，Release 自动发布
- 📚 **参考文献**: BibLaTeX + GB/T 7714 中文引用格式

## 📁 模板结构

```
econpaperkit/
├── template/
│   ├── main.tex          # 主文档
│   ├── sections/         # 各章节
│   ├── tables/           # 表格
│   ├── figures/          # 图片
│   └── references.bib    # 参考文献
├── .github/workflows/
│   └── compile.yml       # 自动编译
└── README.md
```

## 🚀 快速开始

### 本地编译

```bash
# macOS
brew install --cask mactex

# Ubuntu
sudo apt install texlive-full

# Windows
# 安装 MiKTeX 或 TeX Live

# 编译
cd template
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

### GitHub Actions 自动编译

只需将论文推送到 GitHub，Actions 自动编译生成 PDF，在 Release 中下载。

## 📖 论文结构模板

```
1. 引言 (Introduction)
2. 文献综述 (Literature Review)
3. 理论框架 (Theoretical Framework)
4. 数据与变量 (Data & Variables)
5. 实证结果 (Empirical Results)
6. 稳健性检验 (Robustness Checks)
7. 结论 (Conclusion)
```

## 📄 许可证

MIT License © 2024 wzx11223344
