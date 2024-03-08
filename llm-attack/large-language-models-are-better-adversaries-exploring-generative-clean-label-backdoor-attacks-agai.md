# Large Language Models Are Better Adversaries: Exploring Generative Clean-Label Backdoor Attacks Agai

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本文研究的背景是关于后门攻击（backdoor attacks）在机器学习模型，尤其是自然语言处理（NLP）模型中的应用。后门攻击通过在训练和测试数据中插入无害的触发器（triggers），操纵模型预测，使得包含特定触发器的测试实例被错误分类。这种攻击方式比传统的数据投毒攻击更为隐蔽和有效，因为它们不仅修改训练实例，还能在测试实例中发挥作用。随着大型语言模型（LLMs）的发展，攻击者可以利用这些模型的生成能力来创建更加微妙、低代价且高效的后门攻击。

### 2. 过去方案和缺点

以往的后门攻击研究主要集中在“脏标签攻击”（dirty-label attacks），即恶意训练样本被错误标记。这些攻击通常需要对训练数据进行修改，或者在测试时对实例进行修改。然而，这些方法在面对干净标签（clean-label）的情况下效果不佳，因为它们依赖于内容和标签之间的不一致性来识别异常。此外，现有的防御方法在面对干净标签攻击时也显示出了局限性。

### 3. 本文方案和步骤

本文提出了一种名为LLMBkd的LLM启用的干净标签后门攻击。LLMBkd利用大型语言模型自动将基于风格的触发器插入文本中。攻击步骤如下：

1. 确定触发风格和目标标签。
2. 使用LLM重写干净训练样本，生成带有触发风格的有毒文本。
3. （可选）在灰盒设置中，使用干净模型选择最有可能与目标标签关联的有毒实例。



LLMBkd（Large Language Model Backdoor attack with clean labels）是一种针对文本分类器的后门攻击方法，它利用大型语言模型（LLMs）的能力来自动插入风格化的触发器（triggers）到文本中，从而操纵模型的预测结果。

#### 攻击目标

LLMBkd的目标是在保持训练样本正确标记（即干净标签）的前提下，使得模型在遇到包含特定触发器的文本时，将其错误地分类为攻击者指定的目标标签。

#### 攻击步骤

1. **选择触发风格和目标标签**：
   * 攻击者首先确定一个目标标签，即希望模型在检测到触发器时错误分类的标签。
   * 接着，选择一个或多个文本风格，这些风格将用于生成触发器。
2. **利用LLM生成触发器**：
   * 使用LLM（如GPT-3.5）根据选定的风格重写训练数据中的文本，生成包含触发器的有毒文本（poisoned texts）。
   * 通过指令提示（prompting），LLM能够生成与目标标签一致且风格独特的文本。
3. **（可选）毒物选择**：
   * 在灰盒设置中，攻击者可以访问模型类型信息。此时，可以使用一个干净的模型来选择那些最有可能影响目标模型的有毒实例。
   * 通过预测概率对有毒实例进行排序，优先选择那些最有可能被错误分类的实例作为训练数据的一部分。

#### 攻击效果

* LLMBkd能够在不同的文本风格下实现高攻击成功率（ASR），即使在较低的毒物率（PR）下也能保持较高的清洁准确率（CACC）。
* 通过毒物选择技术，可以进一步提高攻击的有效性，确保有毒数据对模型的影响最大化。

#### 攻击的隐蔽性

* LLMBkd生成的文本通常更加自然，与原始数据的分布更接近，这使得攻击更难以被检测。
* 通过保持内容与标签的一致性，LLMBkd能够避免触发基于内容和标签不一致性的防御机制。

#### 攻击的灵活性

* LLMBkd支持多种风格，包括但不限于圣经风格、推特风格、莎士比亚风格等，这为攻击者提供了广泛的选择。
* 攻击者可以根据需要灵活地选择和组合不同的风格，以适应不同的攻击场景和目标模型。

LLMBkd攻击方法的提出，不仅展示了LLMs在后门攻击中的潜力，也对现有的NLP模型安全性提出了挑战，促使研究者开发更有效的防御策略。





### 4. 本文创新点与贡献

* 提出了LLMBkd，一种新的干净标签后门攻击方法，它使用LLMs来生成触发器，而无需模型训练或微调。
* 提出了一种简单的灰盒毒物选择技术，可以提高LLMBkd及其他现有干净标签后门攻击的有效性。
* 提出了REACT，一种基线反应防御策略，通过在检测到攻击后插入“解药”实例来减轻后门攻击的影响。

### 5. 本文实验

实验在四个英文数据集上进行，比较了LLMBkd与多个基线攻击方法。实验结果表明LLMBkd在不同风格触发器下的有效性、隐蔽性和效率都超过了基线攻击。

### 6. 实验结论

LLMBkd在各种设置下都显示出了高攻击成功率，且在灰盒设置中通过毒物选择技术进一步提高了攻击效果。REACT防御策略在检测到攻击后能够有效地减轻其影响。

### 7. 全文结论

本文通过LLMBkd展示了大型语言模型在后门攻击中的潜力，同时也提出了一种有效的防御策略。尽管LLMBkd在攻击方面表现出色，但作者也强调了这种攻击方法可能带来的安全风险，并提出了相应的防御措施。

### 阅读总结

本文深入探讨了利用大型语言模型进行后门攻击的可能性，并提出了一种新的攻击方法LLMBkd。这种方法不仅提高了攻击的隐蔽性和效率，还通过毒物选择技术增强了攻击的有效性。同时，作者也提出了REACT防御策略，以应对这种新型攻击。这项研究不仅对理解NLP模型的脆弱性有重要意义，也为开发更强大的防御机制提供了思路。然而，这种攻击方法的提出也引发了对AI系统安全性的担忧，特别是在实际应用中如何平衡攻击和防御的策略。