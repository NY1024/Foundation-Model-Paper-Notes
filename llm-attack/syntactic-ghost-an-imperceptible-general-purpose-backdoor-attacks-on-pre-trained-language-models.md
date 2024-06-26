# Syntactic Ghost: An Imperceptible General-purpose Backdoor Attacks on Pre-trained Language Models

<figure><img src="../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

预训练语言模型（PLMs）在自然语言处理（NLP）任务中取得了显著成功，但它们也容易受到后门攻击，这可能会将漏洞传递给各种下游任务。现有的PLM后门攻击通常依赖于明确的触发器，这在保持有效性、隐蔽性和通用性方面存在挑战。

### 2. 过去方案和缺点

以往的PLM后门攻击方法通常需要手动对齐触发器，这限制了攻击的通用性和隐蔽性。此外，这些方法在端到端场景中表现良好，但在PLM后门场景中，由于对下游任务的了解有限，难以确保后门的可用性和通用性。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)  (10).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种名为Syntactic Ghost（synGhost）的新方法，通过操纵具有不同预定义句法结构的中毒样本作为隐蔽触发器，然后在不干扰原始知识的情况下将后门植入预训练表示空间。通过对比学习，使中毒样本的输出表示在特征空间中尽可能均匀分布，形成广泛的后门。此外，针对句法触发器的独特属性，引入了一个辅助模块，优先驱动PLM学习这种知识，以减轻不同句法结构之间的干扰。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) ( (9).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 提出了synGhost，一种不可见的通用后门攻击方法，通过对比学习实现攻击的隐蔽性，并提高攻击的通用性。
* 引入了句法感知模块，增强了PLM对句法知识的敏感性，提高了最终的有效性。
* 在5种模型和17个真实世界的关键任务上进行了广泛的评估，证明了与目标一致的有希望的结果。

### 5. 本文实验

实验在多种设置下对synGhost进行了评估，包括微调和参数高效微调（PEFT）在5种模型上的表现。实验结果表明，synGhost在各种NLU任务上对主流PLM的有效性，以及在不同攻击设置（如微调和PEFT）下的有效性。

### 6. 实验结论

synGhost能够有效地在各种NLU任务上实施攻击，并且在不同的攻击设置下保持了良好的性能。此外，synGhost能够逃避现有的防御措施，特别是提出的maxEntropy防御。

### 7. 全文结论

本文提出的synGhost方法为PLM后门攻击提供了一种新的视角，通过句法操纵实现了隐蔽性和通用性的提升。实验结果证明了该方法的有效性，并为未来的研究提供了开放源代码的synGhost。

### 阅读总结

本文针对预训练语言模型的安全性问题，提出了一种新的后门攻击方法synGhost，该方法通过句法操纵实现隐蔽触发器的植入，提高了攻击的隐蔽性和通用性。实验结果表明，synGhost在多种NLP任务和模型上都表现出色，并且能够有效规避现有的防御措施。这一研究不仅揭示了PLM在安全性方面的潜在风险，也为后续的防御策略提供了新的挑战。
