# Learning to Edit: Aligning LLMs with Knowledge Editing

<figure><img src="../.gitbook/assets/image (10) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 研究背景

随着大型语言模型（LLMs）在各种应用中的广泛应用，其输出的准确性和时效性变得尤为重要。然而，现实世界的知识是不断变化的，这要求LLMs能够适应这些变化，及时更新其知识库。传统的从头开始训练LLMs来整合新知识会导致巨大的计算开销，并且通常被认为是不切实际的。因此，研究者提出了知识编辑技术，旨在高效地修改LLMs中的一小部分知识，同时不影响其他输入的性能。

<figure><img src="../.gitbook/assets/image (11) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 过去方案和缺点

以往的知识编辑方法主要依赖于记忆更新的知识，这限制了LLMs在回答输入问题时有效结合新旧知识的能力。这些方法通常使用辅助模块或模型来预测LLMs的权重调整，或者作为查询响应适用性的范围分类器。尽管这些创新显示出潜力，但它们未能继承LLMs的先进能力，导致输出质量下降。此外，一些方法尝试识别并修改与特定知识相关的参数，但这种定位和编辑效果之间的相关性受到了质疑，并且随着LLMs规模的扩大，潜在的负面影响也在增加。

<figure><img src="../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 本文方案和步骤

本文提出了一个名为Learning to Edit (LTE)的框架，旨在通过监督式微调（SFT），教授LLMs如何应用更新的知识来回答查询。LTE框架包括两个关键阶段：对齐阶段（Alignment Phase）和推理阶段（Inference Phase）。在对齐阶段，通过精心策划的并行数据集对LLMs进行微调，培养其三个关键能力：范围内能力（In-Scope Capability）、范围外能力（Out-of-Scope Capability）和语言能力（Linguistic Capability）。在推理阶段，采用基于检索的机制，实时从记忆库中获取最相关的更新知识，以实现批量和序列知识编辑。

## 本文创新点与贡献

LTE框架的主要创新点在于它不仅仅依赖于记忆更新的知识，而是教授LLMs如何动态应用更新的知识来回答问题。这种方法激发了LLMs的潜力，使其能够更有效地利用新知识。此外，LTE通过精心设计的并行数据集和检索机制，提高了知识编辑的性能、鲁棒性、速度，并减少了对一般任务的干扰。

## 本文实验

实验部分，作者选择了两种广泛用于英文和中文聊天机器人应用的基础模型LLaMA2-Chat-7B和Qwen-Chat-7B，以及七种先进的基线方法进行比较。实验涵盖了单个编辑、批量编辑和序列编辑场景，并使用了四个流行的知识编辑基准测试集进行评估。

## 实验结论

实验结果表明，LTE在整体知识编辑性能上建立了新的最高标准，与现有方法相比，在可移植性方面有超过20分的绝对提升。LTE在批量和序列知识编辑请求中显示出显著的鲁棒性，与同类方法相比，性能下降的速率明显降低。LTE在促进知识编辑时对模型的认知功能干扰最小，并且在编辑速度上结合了最快速度和卓越性能。

## 全文结论

本文提出的Learning to Edit (LTE)框架是一个新颖且有效的方法，用于对LLMs进行知识编辑。LTE通过两阶段过程——对齐阶段教授必要的知识编辑能力，推理阶段实施基于检索的即时知识编辑——在各种基准测试中展示了卓越的性能，超越了现有方法在鲁棒性和速度方面的表现。

## 阅读总结报告

本篇论文提出了一种新的知识编辑框架——Learning to Edit (LTE)，它旨在解决大型语言模型在知识更新方面的挑战。通过监督式微调，LTE框架教授模型如何应用更新的知识，而不是简单地依赖记忆。该框架包括对齐和推理两个阶段，通过精心设计的并行数据集和检索机制，提高了知识编辑的效率和效果。 实验结果表明，LTE在知识编辑任务上取得了显著的性能提升，并且在批量和序列编辑场景中显示出优越的鲁棒性。此外，LTE方法对一般任务的干扰最小，编辑速度快，为未来的知识编辑研究和应用提供了新的方向。
