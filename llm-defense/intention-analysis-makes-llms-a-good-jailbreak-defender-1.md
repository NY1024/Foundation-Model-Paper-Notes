# Intention Analysis Makes LLMs A Good Jailbreak Defender

<figure><img src="../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

### 1. 研究背景

本研究聚焦于大型语言模型（LLMs）的安全性问题，特别是在面对隐蔽和复杂的越狱攻击（jailbreak attacks）时，如何确保LLMs与人类价值观保持一致。越狱攻击是指通过特别设计的输入，绕过LLMs的安全策略，操纵模型产生受限输出的风险行为。尽管已有诸多努力试图通过人类反馈的强化学习（RLHF）等方法提升LLMs的安全性，但在处理具有隐蔽和复杂意图的攻击时，这些方法的有效性显著下降。

### 2. 过去方案和缺点

以往的方案主要通过预处理用户输入、利用LLMs的自我修正和改进能力等方式来减少LLMs产生有害生成物。然而，这些方法在面对复杂的越狱攻击时效果不佳，因为它们忽视了背后的隐蔽和恶意意图。此外，通过训练提高LLMs安全性的方法需要在安全性和有用性之间进行微妙的平衡，这在实际操作中非常困难。

<figure><img src="../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

文章提出了一种名为意图分析（Intention Analysis, IA）的防御策略，通过两阶段过程来触发LLMs固有的自我修正和提高能力：

* **阶段1：本质意图分析** - 指导LLMs分析用户查询的本质意图，重点关注安全性、道德和合法性。
* **阶段2：政策一致的响应** - 在识别了本质意图后，引导LLMs提供一个与安全政策一致的最终响应。

### 4. 本文创新点与贡献

* **创新方法**：提出了一种新的通过意图分析机制显著提高LLMs安全性的方法。
* **推理唯一**：IA是一种仅在推理阶段使用的方法，可以在不妥协有用性的情况下显著提高LLMs的安全性。
* **广泛实验**：在多个基准测试和不同规模的模型上进行了广泛的实验，证明了IA的有效性。

### 5. 本文实验

实验使用了SAP200、DAN和AdvBench等基准测试，涵盖了Vicuna、ChatGLM、MPT、DeepSeek和GPT-3.5等模型。结果显示IA能够显著降低响应的有害性（平均降低了46.5%的攻击成功率），同时保持了一般的有用性。

### 6. 实验结论

实验结果表明，IA在不同数据集和模型规模上均能显著提高LLMs的安全性，同时保持或提高其有用性。特别是，Vicuna-7b在使用IA后，在攻击成功率方面甚至超过了GPT-3.5。

### 7. 全文结论

文章提出的意图分析方法是一种简单而有效的策略，可以显著提高LLMs在面对复杂越狱攻击时的安全性，同时保持其有用性。通过广泛的实验验证了IA的有效性，并证明了其在不同模型和数据集上的鲁棒性。

### 阅读总结

本文针对大型语言模型在面对隐蔽和复杂越狱攻击时的安全性问题，提出了一种新颖的意图分析防御策略。通过两阶段的意图分析过程，该策略能够有效地提升模型的安全性，同时不损害其有用性。广泛的实验结果支持了该策略的有效性，表明了其在实际应用中的潜力。这项工作不仅为LLMs的安全性研究领域提供了新的视角，也为未来相关研究提供了有价值的参考。
