# TruthX: Alleviating Hallucinations by Editing Large Language Models in Truthful Space

<figure><img src="../.gitbook/assets/image (230).png" alt=""><figcaption></figcaption></figure>

## 研究背景

大型语言模型（LLMs）在多种自然语言处理任务中展现出卓越的性能。然而，它们有时会产生幻觉，即在拥有正确知识的情况下仍可能生成不真实的回答。这种现象严重削弱了LLMs在实际应用中的可信度。

## 过去方案和缺点

以往的研究尝试通过不同的方法减少LLMs的幻觉问题，例如监督式微调、对比解码和表示编辑等。这些方法虽然在一定程度上有效，但存在局限性，如需要额外的模型或解码步骤，可能会干扰生成能力，或者仅关注注意力头的编辑，而忽略了其他内部表示。

<figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

## 本文方案和步骤

本文提出了TruthX，一种在推理时增强LLMs真实性的方法是，通过在真实空间中编辑它们的内部表示。TruthX使用自编码器将LLM的表示映射到语义和真实潜在空间，并应用对比学习来识别真实空间内的真实编辑方向。在推理过程中，通过在真实空间中编辑LLM的内部表示，TruthX有效地增强了LLM的真实性。

## 本文创新点与贡献

* 提出了TruthX方法，通过在真实空间中编辑LLM的内部表示来增强其真实性。
* 使用自编码器和对比学习来识别和编辑真实性方向。
* 在TruthfulQA基准测试中，对13个先进的LLMs进行了有效性改进，平均提高了20%的真实性。
* 展示了TruthX在控制LLM生成真实或幻觉响应方面的能力。

## 本文实验

实验在TruthfulQA、Natural Questions、TriviaQA和FACTOR等多个基准数据集上进行。结果表明，TruthX在开放式生成和多项选择任务中均取得了最佳结果，并且在不同大小和类型的LLMs上均显示出改进。

## 实验结论

TruthX在多个基准测试中均取得了显著的性能提升，证明了其在增强LLMs真实性方面的有效性。此外，TruthX在不同LLMs之间的泛化能力也得到了验证。

## 全文结论

TruthX通过在真实空间中编辑LLM的内部表示，为减少LLMs的幻觉问题提供了一种有效的解决方案。实验结果表明，TruthX能够显著提高LLMs的真实性，且具有良好的泛化能力。未来的工作将进一步探索TruthX在其他领域的应用，并寻求与其他知识的结合，以共同减少LLMs的幻觉问题。

## 阅读总结报告

本篇论文提出了TruthX方法，旨在解决大型语言模型（LLMs）在生成文本时可能出现的幻觉问题。TruthX通过在真实空间中编辑LLM的内部表示，增强了模型的真实性。与传统方法相比，TruthX不需要额外的模型或解码步骤，且不干扰生成能力。实验结果表明，TruthX在多个基准数据集上均能显著提高LLMs的真实性，平均提升20%。此外，TruthX还显示出良好的泛化能力，能够在不同类型和大小的LLMs上取得一致的改进。这项工作为减少LLMs的幻觉问题提供了新的视角，并为未来的研究奠定了基础。
