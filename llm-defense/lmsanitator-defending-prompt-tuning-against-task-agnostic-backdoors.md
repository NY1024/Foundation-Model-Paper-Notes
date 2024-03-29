# LMSanitator: Defending Prompt-Tuning Against Task-Agnostic Backdoors

<figure><img src="../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

随着大型语言模型（LLMs）在自然语言处理（NLP）任务中的广泛应用，其安全性问题日益受到关注。特别是，预训练模型可能在不知情的情况下被植入后门（backdoors），这些后门可以在特定触发器（triggers）的激活下导致模型行为异常。这种后门攻击对于依赖预训练模型的下游任务尤其危险，因为它们可能影响多个下游系统。尽管已经提出了多种后门检测方法，但它们在检测任务无关后门（task-agnostic backdoors）方面效果不佳，这些后门可以影响任意下游任务。

### 2. 过去方案和缺点

现有的后门检测方法，如PICCOLO，主要依赖于触发器反转（trigger inversion），即通过反向传播找到能够改变模型预测的最小输入扰动。然而，这种方法在任务无关后门攻击中难以收敛，因为直接反转触发器在优化任务中非常困难。此外，现有的后门移除方法需要额外的模型更新和存储，这违反了提示调整（prompt-tuning）的目的，即冻结预训练模型的参数。

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了LMSanitator，一种新的方法来检测和移除Transformer模型中的任务无关后门。LMSanitator的核心思想是反转预定义的攻击向量（即模型输出，当输入嵌入触发器时），而不是直接反转触发器。这种方法在收敛性能和后门检测准确性方面表现更好。LMSanitator还利用了提示调整的特性，在推理阶段进行准确的输出监控和输入净化。



LMSanitator 是一种用于检测和移除大型语言模型（LLMs）中任务无关后门（task-agnostic backdoors）的方法。它的工作原理和步骤如下：

#### 1. PV（Predefined Vector）挖掘

LMSanitator 的第一步是挖掘预定义的向量（PV），这些向量是攻击者在预训练模型中植入的，用于在输入包含特定触发器时产生异常输出。这一步骤通过迭代方法实现，目的是找到这些PV。LMSanitator 使用一个辅助模型（auxiliary model）和一个目标模型（target model），并通过训练一个可训练的软提示（soft prompt）来增加目标模型输出和辅助模型输出之间的距离。这个过程涉及到两个关键的损失函数：距离损失（distance loss）和多样性损失（diversity loss）。

#### 2. PV过滤

在找到潜在的PV后，LMSanitator 需要过滤掉非法的PV。这包括检查软提示参数是否在嵌入层参数的正常范围内，以及是否存在与干净模型相似的输出多样性。如果PV通过了过滤，那么目标模型就被认为是被后门攻击的。

#### 3. PV监控

一旦获得了PV集合，LMSanitator 在推理阶段对模型输出进行监控。如果模型输出与PV集合中的某个PV相似，LMSanitator 就会确认输入包含触发器。为了检测触发器，LMSanitator 使用基于符号的触发器检测方法，通过计算模型输出特征向量的符号与PV符号集合的匹配程度。

#### 4. 触发器移除

确定输入被触发后，LMSanitator 使用滑动窗口方法来识别和移除触发器。这涉及到在输入文本中滑动窗口，识别窗口内的候选触发器，然后移除这些触发器。这个过程重复进行，直到没有检测到触发器为止。

#### 5. 防御策略

LMSanitator 的防御策略是在不改变预训练模型参数的情况下，通过监控和移除输入中的触发器来保护模型。这种方法保持了提示调整（prompt-tuning）的模块化和低存储特性，同时提供了一种有效的后门防御机制。

#### 创新点

* **反转预定义向量**：与传统的触发器反转方法相比，LMSanitator 通过反转预定义的攻击向量来提高收敛性能和检测准确性。
* **无需模型更新**：LMSanitator 不需要对模型进行额外的更新，这与提示调整的目的相符，即冻结预训练模型的参数。
* **实际可行性**：LMSanitator 只需要一些干净的文本数据，这在实践中是容易获得的，并且不需要攻击者的具体知识。

####





<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 提出了LMSanitator，这是第一个能够在不改变模型参数的情况下检测和移除任务无关后门的方法。
* LMSanitator只需要防御者拥有一些干净的句子，这在实践中是现实的，并且不需要攻击者的知识。
* 在多种任务无关后门攻击和下游任务上评估了LMSanitator，证明了其有效性。在960个模型中，LMSanitator实现了92.8%的后门检测准确率，并在大多数情况下将攻击成功率降低到1%以下。

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

### 5. 本文实验

作者在多种语言模型和NLP任务上进行了广泛的实验，包括句子分类、命名实体识别（NER）等。实验结果表明，LMSanitator在后门检测和攻击成功率降低方面表现出色。

### 6. 实验结论

实验结果证实了LMSanitator在检测任务无关后门和保护下游提示调整模型免受后门干扰方面的有效性。LMSanitator在大多数情况下能够将攻击成功率降低到1%以下，同时保持了模型在干净输入上的准确性。

### 7. 全文结论

本文提出了LMSanitator，这是一个针对提示调整模型中任务无关后门的有效防御机制。通过反转预定义的攻击向量，LMSanitator在后门检测和移除方面表现出了优越的性能。此外，LMSanitator的设计保持了提示调整的模块化和低存储特性，使其成为实际应用中的一个有吸引力的解决方案。

### 阅读总结

本文针对预训练语言模型中的后门攻击问题，提出了一种新的防御机制LMSanitator。该机制通过反转攻击向量而不是直接反转触发器，提高了后门检测的准确性和收敛性能。实验结果表明，LMSanitator能够有效地检测和移除后门，同时保持模型在干净输入上的高性能。这一工作为保护预训练模型免受后门攻击提供了一种有效的策略。
