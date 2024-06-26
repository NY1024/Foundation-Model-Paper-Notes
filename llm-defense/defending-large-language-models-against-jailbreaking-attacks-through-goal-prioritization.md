# Defending Large Language Models Against Jailbreaking Attacks Through Goal Prioritization

<figure><img src="../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

##

### 1. 研究背景

大型语言模型（LLMs）在提供各种任务解决方案方面取得了显著进展，但同时也暴露出安全风险，如泄露私人数据、生成有害内容和促进非法活动。尽管有多种方法（如监督式微调（SFT）和人类反馈强化学习（RLHF））被提出来提高LLMs的安全性，但这些方法在处理越狱攻击（jailbreaking attacks）时仍然存在缺陷。越狱攻击通过精心设计的提示绕过LLMs的安全机制，诱使模型生成有害回应。

<figure><img src="../.gitbook/assets/image (13) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 2. 过去方案和缺点

过去的方案主要依赖于SFT和RLHF来提高LLMs的安全性。然而，这些方法没有明确指导模型在安全性和有用性之间如何权衡，导致模型在面对越狱攻击时无法有效识别和处理目标优先级冲突。

<figure><img src="../.gitbook/assets/image (14) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种通过目标优先级（goal prioritization）来防御越狱攻击的方法。在推理阶段，通过引入目标优先级指令显著降低了越狱攻击的成功率（ASR）。在训练阶段，通过将目标优先级概念整合到训练过程中，使模型能够在没有大量提示标记的情况下更好地遵循目标优先级要求。



本文提出的通过目标优先级（goal prioritization）来防御越狱攻击的方法，旨在解决大型语言模型（LLMs）在面对安全与有用性之间的冲突时的脆弱性。以下是该方法的详细说明：

#### 目标优先级的概念

在LLMs的训练和推理过程中，通常存在两个主要目标：有用性（提供有用的回应）和安全性（确保回应无害）。然而，这些目标并不总是一致的，有时为了提供有用的信息，模型可能会生成有害的内容。目标优先级方法强调在这两个目标之间建立明确的优先顺序，特别是在可能产生有害结果的情况下，安全性应当优先。

#### 方法实施

**推理阶段的目标优先级**

在推理阶段，作者提出了一种无需额外训练的即插即用（plug-and-play）提示方法。这种方法通过在用户查询前添加指令，明确告诉模型在安全性和有用性之间应优先考虑安全性。例如，模型可能会收到如下指令：

* 如果回答用户查询可能导致不安全或有害的结果，模型应拒绝回答。
* 在不违反安全性的前提下，模型应提供全面且精确的回应。

这种方法通过在模型的输出中包含“内部思考”（internal thoughts）部分，让模型分析是否遵循了用户指令，同时提供符合目标优先级要求的最终回应。

**训练阶段的目标优先级**

在训练阶段，作者提出了一种训练流程，该流程将各种查询与不同的目标优先级要求结合起来。这种方法使模型在训练过程中学会并遵循指定的目标优先级要求。具体来说，对于良性用户查询，模型会在输入中随机添加目标优先级要求，并生成包含内部思考和最终回应的输出。对于有害查询，模型会被要求优先考虑安全性，即使这可能意味着提供不那么有用的回应。

#### 方法的有效性

通过在推理和训练阶段实施目标优先级，模型在面对越狱攻击时的攻击成功率（ASR）显著降低。例如，对于ChatGPT，ASR从66.4%降低到2.0%；对于Vicuna-33B，ASR从68.2%降低到19.4%。此外，即使在没有包含越狱样本的训练中，该方法也能显著提高模型的防御成功率。

#### 方法的创新点

* **目标优先级的明确引入**：在LLMs的设计中明确引入了安全性优先于有用性的概念。
* **无需额外训练的防御策略**：提出了一种即插即用的提示方法，无需对模型进行额外训练即可实现防御。
* **训练阶段的目标优先级整合**：通过在训练数据中包含目标优先级要求，提高了模型对越狱攻击的泛化能力。

####





### 4. 本文创新点与贡献

* 提出了一种新的目标优先级防御策略，有效降低了越狱攻击的ASR。
* 在没有训练的情况下，通过少量示例提示（few-shot prompting）实现目标优先级。
* 在训练阶段，通过训练数据中包含不同类型的目标优先级要求，提高了模型对越狱攻击的泛化能力。
* 发现更强大的LLMs在面对越狱攻击时具有更大的防御潜力。

### 5. 本文实验

实验在不同的LLMs上进行，包括API基础的LLMs和开源LLMs。实验结果表明，引入目标优先级后，越狱攻击的ASR显著降低，且对模型的一般性能影响很小。

### 6. 实验结论

实验结果证实了目标优先级策略在防御越狱攻击方面的有效性。即使在没有包含越狱样本的训练中，该策略也能显著提高模型的防御成功率（DSR）。

### 7. 全文结论

本文通过引入目标优先级的概念，提出了一种有效的越狱攻击防御策略。该策略不仅在推理阶段有效，而且在训练阶段也能提高模型对越狱攻击的抵抗力。研究结果为理解越狱攻击和防御提供了新的视角，并为开发更安全的LLMs提供了指导。

### 阅读总结

本文针对LLMs在面对越狱攻击时的目标冲突问题，提出了一种基于目标优先级的方法来提高模型的安全性。通过在推理和训练阶段引入目标优先级，该方法显著降低了越狱攻击的成功率，同时保持了模型的一般性能。这一发现不仅为LLMs的安全防御提供了新的策略，也为理解模型能力和安全性之间的关系提供了新的见解。
