# TELLER: A Trustworthy Framework for Explainable, Generalizable and Controllable Fake News Detection

<figure><img src="../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

假新闻的泛滥已成为严重的社会问题，引起了工业界和学术界的广泛关注。尽管现有的基于深度学习的方法在准确检测假新闻方面取得了进展，但由于神经网络的黑盒特性、泛化能力差以及与大型语言模型（LLMs）集成时的不可控风险，这些方法的可靠性可能会受到影响。

### 2. 过去方案和缺点

以往的假新闻检测方法主要基于深度学习，尽管预测准确性有所提高，但这些方法缺乏透明度，因为模型的推理过程不明确。此外，这些模型在面对与训练数据分布不同的未见过的数据时，泛化能力有限。而且，随着与LLMs的集成越来越普遍，由于幻觉现象和社会应用问题，这些系统的可靠性受到了威胁。

### 3. 本文方案和步骤

本文提出了一个名为TELLER的新型框架，用于建立可信赖的假新闻检测系统，强调模型的可解释性、泛化性和可控性。TELLER通过一个双系统框架实现，该框架集成了认知和决策系统。认知系统利用人类专家知识生成逻辑谓词，引导LLMs生成人类可读的逻辑原子。决策系统则通过一个可微分的神经符号模型，从数据中自动学习域不变的逻辑规则，将这些逻辑原子聚合起来，以识别输入新闻的真实性。

### 4. 本文创新点与贡献

* 提出了一个系统性的框架，包括认知和决策模块，旨在维护建立可信赖假新闻检测系统的三个关键原则：可解释性、泛化性和可控性。
* 通过在四个基准数据集上使用各种LLMs进行的全面实验验证了框架的有效性，结果表明TELLER在不同场景下的可行性和可信赖性。

### 5. 本文实验

实验使用了四个具有挑战性的数据集：LIAR、Constraint、PolitiFact和GossipCop。实验结果表明，TELLER在假新闻检测任务中表现出色，尤其是在使用Llama 2 (13B)作为认知系统驱动时，其性能超过了所有基于GPT-3.5-turbo的方法。

### 6. 实验结论

实验结果证明了TELLER框架的可行性、可解释性、泛化性和可控性。通过结合人类专家知识和LLMs的强大能力，TELLER在不同领域和不同分类粒度下均能有效地检测假新闻。

### 7. 全文结论

TELLER框架通过其双系统结构，有效地解决了现有假新闻检测方法在可靠性、透明度和泛化能力方面的局限性。通过集成人类专家的知识和逻辑规则，TELLER不仅提高了模型的可解释性和可控性，而且通过学习域通用的规则，增强了模型的泛化能力。未来的研究可以进一步提高TELLER框架的性能，并通过整合更先进的技术和方法来应对不断演变的假新闻威胁。

### 阅读总结

TELLER是一个创新的假新闻检测框架，它通过结合人类专家知识和大型语言模型的能力，有效地提高了假新闻检测的准确性和可靠性。该框架的双系统结构确保了模型的可解释性、泛化性和可控性，使其在面对多样化和不断变化的在线信息时，能够提供可信赖的检测结果。通过在多个数据集上的广泛实验验证，TELLER展示了其在不同场景下的有效性和可信赖性，为未来假新闻检测技术的发展提供了有价值的方向。
