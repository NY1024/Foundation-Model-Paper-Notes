# Robustness Over Time: Understanding Adversarial Examples’ Effectiveness on Longitudinal Versions of

<figure><img src="../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 研究背景

大型语言模型（LLMs）在多个领域内的任务中取得了显著的改进，例如代码解释、响应生成和歧义处理。然而，这些模型在升级时主要关注提升用户体验，而忽视了安全、隐私和安全影响。因此，可能会引入意外的漏洞或偏见。以往的研究主要集中在特定版本的模型上，而忽略了针对更新版本的新攻击向量的潜在出现。

## 过去方案和缺点

以往的研究主要关注于模型的单一版本，没有探索模型更新对鲁棒性的影响。此外，现有的对抗性攻击方法在生成对抗性示例时面临挑战，因为它们需要在离散的标记输入上进行优化，这在计算上是困难的。此外，对抗性攻击的转移性在不同模型和架构之间并不总是可靠的。

<figure><img src="../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 本文方案和步骤

本文通过在上下文学习框架内使用对抗性示例，对连续更新的LLMs的鲁棒性进行全面评估。研究的主要目标是理解不同版本的LLMs在对抗性示例下的鲁棒性。研究方法包括使用代理语言模型生成对抗性示例，并将这些示例应用于目标LLM的不同版本，然后比较模型在对抗性示例下的行为。

## 本文创新点与贡献

* 本文是首次对连续更新的LLMs进行全面的鲁棒性评估。
* 研究了零次学习和少次学习两种不同的学习类别中的鲁棒性影响。
* 强调了在大多数零次学习和少次学习情况下，协同对抗性查询的增加效果。
* 提供了对LLMs随时间推移的鲁棒性评估的更精细理解，并为开发者和用户提供了有价值的见解。

## 本文实验

实验部分，作者详细描述了基准数据集、特定模型以及评估指标。实验涵盖了描述数据集和问题数据集，选择了六种不同的代理模型来生成对抗性示例，并使用了两个版本的GPT-3.5作为目标模型。评估指标包括Clean Test Score (CTS)、Robust Test Score (RTS) 和 Performance Drop Rate (PDR)。

## 实验结论

实验结果表明，与早期版本的LLMs相比，更新版本的模型在对抗性攻击面前并没有展现出预期的鲁棒性水平。此外，研究强调了在大多数零次学习和少次学习情况下，协同对抗性查询的增加效果。

## 全文结论

本文的研究强调了在LLMs更新过程中考虑模型鲁棒性的重要性。通过全面的评估，本文揭示了更新模型在对抗性攻击面前的复杂关系，并挑战了更新模型总是带来增强的普遍观念。研究结果为未来LLMs的鲁棒性研究提供了宝贵的见解，并为开发者提供了在模型更新过程中考虑鲁棒性增强技术的指导。

## 阅读总结报告

本文通过对GPT-3.5的两个版本进行对抗性攻击的全面评估，揭示了LLMs在更新过程中可能面临的安全挑战。研究结果表明，尽管模型在用户体验上有所提升，但在对抗性攻击的鲁棒性方面并没有显著进步。这一发现对于LLMs的开发者和用户都具有重要意义，提示他们在模型更新时需要更加关注安全性和鲁棒性。此外，本文的研究方法和评估框架为未来在这一领域的研究提供了有价值的参考。
