[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.2550379.svg)](https://doi.org/10.5281/zenodo.2550379)

## FOCUS

- 该存储库包含 FOCUS 的源码实现，以及用于复现论文实验结果的数据集。
- 论文题目：_Recommending API Function Calls and Code Snippets to Support Software Development (2021 TSE)_
- 作者: _Phuong T. Nguyen, Juri Di Rocco, Claudio Di Sipio, Davide Di Ruscio, and Massimiliano Di Penta_
- 访问链接：[Arxiv](https://arxiv.org/pdf/2102.07508.pdf)
- 实验相关的说明：[click here](https://github.com/crossminer/FOCUS/blob/master/README.pdf)
- FOCUS 已经成功集成到 Eclipse IDE 中，在编程时推荐 API。如何安装插件：[click here](https://mdegroup.github.io/FOCUS-Appendix/install.html)
- 注：是下述文章的扩展，其被 2019 ICSE 所接收和发表。
  - 论文题目：_FOCUS: A Recommender System for Mining API Function Calls and Usage Patterns (2019 ICSE)_
  - 作者：_Phuong T. Nguyen, Juri Di Rocco, Davide Di Ruscio, Lina Ochoa, Thomas Degueule, and Massimiliano Di Penta_
  - 访问链接：[click here](https://hal.archives-ouvertes.fr/hal-02023023/document)
  - 注：该论文获得了 _ICSE 2019 Artifact Evaluation Track_ 颁发的 **Artifacts Available** 和 **Artifacts Evaluated** 两个徽章，这意味着所有相关工件都被正确地文档化了，并且它们是一致的、完整的和可复现的，有助于未来的重用和再生产。

## 仓库结构

- [dataset](./dataset) 目录包含用来评估 FOCUS 的数据集。
  - [jars](./dataset/jars)：从 Maven Central 获取的 3,600 个 jar 文件（ MV<sub>L</sub> 的原始数据集 ）
  - [MV_L](./dataset/MV_L)：MV<sub>L</sub>（ 从 3,600 个 jar 文件中提取 ）
  - [MV_S](./dataset/MV_S)：MV<sub>S</sub>（ 从 1,600 个 jar 文件中提取 ）
  - [SH_L](./dataset/SH_L)：SH<sub>L</sub>（ 从 610 个 GitHub 项目源码中提取 ）
  - [SH_S](./dataset/SH_S)：SH<sub>S</sub>（ 从 200 个 GitHub 项目源码中提取 ）
- [tools](./tools) 目录包含开发的不同工具的实现。
  - [Focus](./tools/Focus)：FOCUS 的 Java 实现。
  - [FocusRascal](./tools/FocusRascal)：使用 [Rascal](https://www.rascal-mpl.org/) 编写的工具，可以实现（1）将原始的 Java 源码和二进制代码转换为 FOCUS 和 PAM 能处理的数据；（2）检索具体的 Java 使用模式。
  - [PAM](./tools/PAM)：用于比较 FOCUS 和 PAM 的 Python 脚本。

__Note<sup>1</sup>__：通过 [Software Heritage archive](https://www.softwareheritage.org/) 从 GitHub 检索到的 5147 个 Java 项目的[存档](https://annex.softwareheritage.org/public/dataset/vault-crossminer/856749_done_with_origins.txt.gz)。

__Note<sup>2</sup>__：按照 [Focus](./tools/Focus) 目录中的说明，可以重现论文中给出的结果。

## 引言

&ensp;&ensp;FOCUS 是一个基于上下文感知的协同过滤推荐系统，它利用开源项目之间的交叉关系来推荐 API 调用和具体的 API 使用模式（当前实现专门针对 Java 代码）。

&ensp;&ensp;该协同过滤推荐系统需要评估两个软件项目的相似度。现有方法认为任何两个使用感兴趣的 API 的项目都是同等价值的知识来源。相反，论文假设并不是所有的项目在推荐使用模式时都是平等的：一个与当前开发的项目高度相似的项目应该比一个高度不同的项目提供更高质量的模式。

&ensp;&ensp;FOCUS 试图通过只考虑与活动项目最相似的项目来缩小搜索范围。因此，在类似的上下文中，通常由类似项目共同使用的方法往往会被首先推荐。

&ensp;&ensp;将以上想法整合到 FOCUS 中，该系统通过挖掘开源存储库，为开发者推荐 API 函数调用和使用模式。FOCUS 使用了一个新模型来表示项目之间的相互关系，并从最相似的项目中挖掘 API 使用情况。

## FOCUS 推荐示例

基于 IDE, FOCUS 在两个独立的选项卡中提供了两种类型的推荐，如下图所示。到第一个选项卡时，它会显示一个 API 调用的排序列表，而到第二个选项卡时，它会显示真正的代码片段。注意，FOCUS 工具只提供和展示推荐信息，是否集成推荐的 API 或源代码完全由开发人员自行决定。在 FOCUS 提供建议后，开发人员可以通过复制和粘贴推荐的代码片段到编辑窗口来将代码嵌入到 IDE 中。

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/FOCUS_IDE.png" width="850">
</p>

下图显示了一个不完整的方法声明：

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/OriginalDeclaration.png" width="550">
</p>

下图为最终的方法声明：

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/FinalDeclaration.png" width="550">
</p>

FOCUS 提供了以下代码片段作为不完整声明的推荐：

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/RecommendedCode.png" width="550">
</p>

以下链接展示了 FOCUS 提供的更多代码片段示例：[click here](https://mdegroup.github.io/FOCUS-Appendix/tasks.html)

## TSE 提交相关

在 TSE 提交的文件中，通过对 2600 个应用程序的数据集进行评估来证明 FOCUS 对 Android 编程的适用性。实验结果表明，FOCUS 在成功率、准确率和执行时间方面都优于最先进的方法 PAM。更重要的是，FOCUS 能有效地向正在开发的方法声明推荐源代码。作者还发现在 Google Play 中定义的应用程序类别和它们的 API 使用之间没有微妙的关系。

包含 2600 个 Android 应用程序的数据集解析的元数据存储在以下文件夹中：[dataset/TSE](./dataset/TSE)。

收集的原始数据来自 [AndroidTimeMachine](https://androidtimemachine.github.io/) 平台。

## 如何引用本文
使用以下 BibTex 条目：

```
@inproceedings{Nguyen:2019:FRS:3339505.3339636,
 author = {Nguyen, Phuong T. and Di Rocco, Juri and Di Ruscio, Davide and Ochoa, Lina and Degueule, Thomas and Di Penta, Massimiliano},
 title = {{FOCUS: A Recommender System for Mining API Function Calls and Usage Patterns}},
 booktitle = {Proceedings of the 41st International Conference on Software Engineering},
 series = {ICSE '19},
 year = {2019},
 location = {Montreal, Quebec, Canada},
 pages = {1050--1060},
 numpages = {11},
 url = {https://doi.org/10.1109/ICSE.2019.00109},
 doi = {10.1109/ICSE.2019.00109},
 acmid = {3339636},
 publisher = {IEEE Press},
 address = {Piscataway, NJ, USA},
} 

```

```
@ARTICLE{9359479,
  author={P. T. {Nguyen} and J. {Di Rocco} and C. {Di Sipio} and D. {Di Ruscio} and M. {Di Penta}},
  journal={IEEE Transactions on Software Engineering}, 
  title={Recommending API Function Calls and Code Snippets to Support Software Development}, 
  year={2021},
  volume={},
  number={},
  pages={1-1},
  doi={10.1109/TSE.2021.3059907}}
```

## 答疑

如果对数据集或工具有疑惑的地方，可以联系：`phuong.nguyen@univaq.it`，`juri.dirocco@univaq.it`。 
