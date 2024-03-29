# LLM LIES: HALLUCINATIONS ARE NOT BUGS, BUT FEATURES AS ADVERSARIAL EXAMPLES

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型语言模型（LLMs），如GPT-3.5、LLaMA和PaLM，虽然在生成能力和适应多种任务方面表现出色，但它们的输出仍然存在幻觉问题，即制造不存在的事实来误导用户。这种现象在法律和医疗咨询等领域可能导致灾难性风险。以往的研究从过拟合和学习过程的角度解释了这一问题，但本文提出了一种新的观点，即幻觉可能是对抗性样本的另一种表现形式。

### 2. 过去方案和缺点

以往的研究主要集中在LLMs的训练数据和学习过程上，认为模型对训练数据的记忆和利用基于词频的启发式方法是导致幻觉的主要原因。然而，这些解释并没有完全揭示幻觉现象的本质，也没有提供有效的解决方案。

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种名为“幻觉攻击”的自动化方法，通过两种方式触发LLMs产生幻觉：一是选择性替换原始句子中的某些标记以保持语义一致性；二是构建由随机标记组成的无意义的Out-of-Distribution（OoD）提示。这种方法基于梯度引导的标记替换策略，旨在通过最大化预定义行为的可能性来替换一些“触发”标记。





“幻觉攻击”（Hallucination Attack）是一种自动化方法，旨在诱导大型语言模型（LLMs）产生幻觉，即生成与现实不符的虚假信息。这种方法基于对抗性攻击的原理，通过精心设计的输入来操纵模型的输出。以下是“幻觉攻击”的详细说明和示例：

#### 自动化方法的步骤：

1. **初始化**：
   * 对于**弱语义攻击**（Weak Semantic Attack），从现有的语义提示开始，这些提示在人类看来是有意义的，但经过修改后可以触发幻觉。
   * 对于**OoD攻击**（Out-of-Distribution Attack），从一个由随机标记组成的序列开始，这些序列在语义上对人类来说是无意义的。
2. **梯度引导的标记替换**：
   * 使用梯度信息来确定哪些标记（tokens）的替换最有可能引发幻觉。这涉及到计算模型输出（预定义的幻觉回复）与输入之间的梯度，并选择那些能够最大化这个梯度的标记进行替换。
3. **迭代优化**：
   * 在每次迭代中，选择一组候选的标记替换，然后通过最大化预定义幻觉回复的对数似然来更新攻击提示（adversarial prompt）。
4. **防御策略**：
   * 为了防御这种攻击，作者提出了一种基于熵阈值的策略。在推理阶段，如果模型对第一个生成的词的预测熵低于某个阈值，那么模型将拒绝回答，从而避免产生幻觉。

#### 示例：

假设我们有一个LLM，我们想要诱导它产生关于历史事件的错误信息。以下是一个弱语义攻击的示例：

* **原始提示**（Semantic Prompt）：“When did the Second World War officially start?”
* **原始回答**（Original Response）：“The Second World War officially started on September 1, 1939, when Germany invaded Poland.”

为了触发幻觉，我们可以通过以下步骤进行攻击：

1. **选择性替换**：我们选择性地替换原始提示中的某些标记，例如将“1939”替换为“2022”，同时保持其他部分不变。
2. **迭代优化**：通过迭代过程，我们不断调整提示，直到模型生成一个预定义的幻觉回复，例如：“The Second World War officially began on September 1, 2022, when the United States declared war on the Islamic Caliphate.”

在这个例子中，我们通过微小的修改（改变日期）成功地诱导了模型产生了一个与现实不符的历史事件描述。这种攻击展示了LLMs在面对精心设计的输入时的脆弱性。





### 4. 本文创新点与贡献

* **幻觉攻击**：提出了一种新的对抗性攻击方法，可以自动引发LLMs产生幻觉。
* **对抗性样本的新视角**：将幻觉视为对抗性样本的一种形式，这是对现有理解的扩展。
* **防御策略**：提出了一种简单但有效的防御策略，即使用熵阈值来拒绝可能导致幻觉的输入。

### 5. 本文实验

实验在Vicuna-7B和LLaMA2-7B-chat等开源LLMs上进行，通过白盒攻击展示了弱语义攻击和OoD攻击的效果。实验结果表明，这些模型在面对幻觉攻击时表现出较高的成功率。

### 6. 实验结论

实验结果证实了幻觉攻击的有效性，并且发现即使是无意义的OoD提示也能引发LLMs产生幻觉。此外，通过设置熵阈值，可以在一定程度上防御幻觉攻击。

### 7. 全文结论

本文通过实验揭示了LLMs在面对对抗性攻击时的脆弱性，并提出了一种新的对抗性攻击方法。同时，本文也探讨了一种基本的防御策略，为未来LLMs的安全研究提供了新的方向。

### 阅读总结

本文提出了一种新的对抗性攻击方法——幻觉攻击，用于研究LLMs在面对特定输入时产生幻觉的现象。通过实验，作者展示了即使是无意义的输入也能导致LLMs产生幻觉，这表明幻觉可能是LLMs的一个基本特性。此外，本文还提出了一种基于熵阈值的简单防御策略，为LLMs的安全应用提供了新的思考。
