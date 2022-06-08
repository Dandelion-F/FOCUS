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

FOCUS is a context-aware collaborative-filtering recommendation system that exploits cross relationships among OSS projects to suggest the inclusion of additional API invocations and concrete API usage patterns. The current implementation targets Java code specifically.

Implementing a collaborative-filtering recommendation system requires to assess the similarity of two customers, i.e., two software projects. Existing approaches consider that any two projects using an API of interest are equally valuable sources of knowledge. Instead, we postulate that not all projects are equal when it comes to recommending usage patterns: a project that is highly similar to the project currently being developed should provide higher quality patterns than a highly dissimilar one.

Our collaborative-filtering recommendation system attempts to narrow down the search scope by only considering the projects that are the most similar to the active project. Therefore, methods that are typically used conjointly by similar projects in similar contexts tend to be recommended first.

We incorporate these ideas in a new context-aware collaborative filtering recommender system that mines OSS repositories to provide developers with API **F**uncti**O**n **C**alls and **US**age patterns: FOCUS. Our approach employs a new model to represent mutual relationships between projects and collaboratively mines API usage from the most similar projects.

## FOCUS 推荐示例

By means of the IDE, FOCUS provides two main types of recommendations in two separate tabs as shown in the picture below. By the first tab, it displays a ranked list of API calls while by the second tab, there are real snippets of code. As a matter of fact, our tool only provides and presents recommendations, and integrating the recommended APIs or source code is purely at the developers' discretion, i.e., they will decide whether and how to adopt the recommended API calls and/or code snippets. With the recommendations provided by FOCUS, developers can embed into their IDE by copying and pasting fragments of the recommended code into the editing window.

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/FOCUS_IDE.png" width="850">
</p>

The following figure show an incomplete method declaration:

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/OriginalDeclaration.png" width="550">
</p>

and the figure below is the final declaration:

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/FinalDeclaration.png" width="550">
</p>

FOCUS provides the following code snippet as recommendation for the incomplete declaration:

<p align="center">
<img src="https://github.com/crossminer/FOCUS/blob/master/images/RecommendedCode.png" width="550">
</p>

More examples of code snippets provided by FOCUS are available at the following link: [https://mdegroup.github.io/FOCUS-Appendix/tasks.html](https://mdegroup.github.io/FOCUS-Appendix/tasks.html)

## Extension in the TSE submission

We designed and implemented FOCUS as a novel approach to provide developers with API calls and soure code while they are programming. The system works on the basis of a context-aware collaborative filtering technique to extract API usages from OSS projects. In the TSE submission, we demonstrate the suitability of FOCUS for Android programming by evaluating it on a dataset of 2,600 apps. The experimental results demonstrate that our approach outperforms the state-of-the-art approach PAM concerning success rate, accuracy, and execution time. More importantly, we show that FOCUS efficiently recommends source code to a method declaration being developed. We also find out that there is no subtle relationship between the categories for apps defined in Google Play and their API usages.

The metadata parsed for a dataset consisting of 2,600 Android apps is stored in the [following folder](./dataset/TSE). We acknowledge the original data collected from the AndroidTimeMachine [platform](https://androidtimemachine.github.io/).

A pre-print of the TSE paper is available in [Arxiv](https://arxiv.org/pdf/2102.07508.pdf).

## How to cite
If you find our work useful for your research, please cite the papers using the following BibTex entries:

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

## Troubleshooting

If you encounter any difficulties in working with the tool or the datasets, please do not hesitate to contact us at one of the following emails: phuong.nguyen@univaq.it, juri.dirocco@univaq.it. We will try our best to answer you as soon as possible.
