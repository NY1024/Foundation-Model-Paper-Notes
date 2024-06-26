# Locating and Mitigating Gender Bias in Large Language Models

<figure><img src="../.gitbook/assets/image (228).png" alt=""><figcaption></figcaption></figure>

## 研究背景

大型语言模型（LLM）通过在广泛的语料库上进行预训练，学习事实和人类认知，这些语料库包含了人类的偏好。然而，这一过程可能会不经意地导致模型获得社会中普遍存在的偏见和刻板印象。随着这些模型在各个领域的日益融合，其内在的偏见问题引起了越来越多的关注。偏见指的是对特定群体或概念的系统性不准确、错误归属或错误认知，导致了对这些群体的偏好。

## 过去方案和缺点

以往的研究主要集中在两个方面：偏见的识别和定位，以及偏见的缓解。这些研究通常关注特定的偏见表现形式，如性别偏见或种族偏见。例如，Caliskan等人采用隐含联想测试（IAT）的核心概念，通过评估概念关联的强度来衡量性别偏见。其他研究则提出了缓解模型偏见的方法，如通过增强数据集、特殊处理训练数据或通过人类反馈来进行微调。然而，这些方法往往集中在词嵌入、训练数据的特殊处理或通过人类反馈进行，而对于如何利用生成性别偏见的机制进行针对性的性别去偏见以及如何将知识编辑技术适应到性别偏见缓解领域，仍然缺乏深入的探索。

<figure><img src="../.gitbook/assets/image (229).png" alt=""><figcaption></figcaption></figure>

## 本文方案和步骤

本文提出了一个统一的框架，将定位和缓解偏见的过程整合在一起。首先，使用因果中介分析来追踪大型语言模型中不同组件激活的因果效应。基于此，提出了一种基于知识编辑的方法——最小二乘去偏见方法（LSDM），用于缓解职业代词中的性别偏见，并与两个基线进行了比较。LSDM通过解决带有约束项的矩阵方程来修改参数，使我们能够在最小化对模型其他方面的干扰的同时，特别缓解与某些职业词汇相关的性别偏见。

## 本文创新点与贡献

* 本文使用因果中介分析追踪大型语言模型中不同组件激活的因果效应，以衡量模型中不同组件对性别偏见的影响，并揭示了偏见信息的流动过程。
* 提出了最小二乘去偏见方法（LSDM），这是一种更可解释的去偏见算法。结果证实，LSDM是一种有效的去偏见方法，克服了所有其他去偏见方法中存在的灾难性遗忘问题。
* 据作者所知，本研究是首次将性别偏见的定位和缓解纳入统一框架。
* 本文首次将知识编辑方法转移到去偏见领域，并验证了它们的可行性，为消除大型语言模型中存在的各种偏见提供了可行的解决方案。

## 本文实验

实验使用了GPT2-XL和GPT-J作为实验模型，因为它们涵盖了当前大规模语言模型的上下界。使用包含职业代词的1000个偏见句子计算ATE和AIE。实验结果显示，LSDM在缓解模型性别偏见方面最为有效，平均减少了71.4%的性别偏见。

## 实验结论

实验结果表明，LSDM在缓解性别偏见方面最为有效，同时在保留模型性能方面与原始模型最为接近。这些指标显示LSDM在去除模型偏见的同时，也最大限度地保留了原始模型的特性。

## 全文结论

本文通过深入分析大型语言模型中性别偏见的存储位置和生成机制，并提出了一种基于知识编辑的性别去偏见方法——LSDM。实验结果表明，LSDM是一种有效的去偏见方法，不仅成功去除了句子中的大部分职业性别偏见，而且克服了传统方法中存在的灾难性遗忘问题，并且LSDM可以扩展到之前未见过的职
