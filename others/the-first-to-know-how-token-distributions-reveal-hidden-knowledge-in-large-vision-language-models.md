# The First to Know: How Token Distributions Reveal Hidden Knowledge in Large Vision-Language Models?

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 阅读总结报告

#### 1. 研究背景

本研究聚焦于大型视觉-语言模型（LVLMs），这类模型旨在解释和响应人类指令。然而，由于不当指令，LVLMs有时会生成幻觉或有害内容。研究通过线性探测（linear probing）技术揭示了LVLMs输出层隐藏的知识，特别是发现第一个token的logit分布包含了足够的信息来决定是否响应指令。

#### 2. 过去方案和缺点

以往的工作通常采用多阶段训练方法来调整LVLMs，以遵循人类指令。但当推理时的指令不当时，会出现问题，如生成幻觉或不准确的内容，对恶意设计的指令做出有害响应，或在不知道正确答案的情况下回答问题。现有方法如监督式微调（SFT）或基于人类反馈的强化学习（RLHF）需要大量计算资源，且prompt调整通常效果不佳。

#### 3. 本文方案和步骤

研究者提出使用线性探测来分析LVLMs输出层的logit分布，以此作为特征向量预测各种行为（如不可回答性、越狱攻击和欺骗）。具体步骤包括：

* 提取训练样本的logit分布。
* 训练一个线性分类器模型。
* 在测试集上验证分类器。

#### 4. 本文创新点与贡献

* 创新性地发现第一个token的logit分布包含了决定是否遵循指令的足够信息。
* 展示了一个简单的解码策略，在生成第一个token时应用，有效改善了生成内容。
* 通过实验发现了CLIP模型已经包含了解决这些任务的强信号，表明现有数据集可能存在偏见。
* 利用第一个logit分布对三个额外任务的性能进行了改进，包括数学问题求解时的不确定性指示、幻觉减少和图像分类。

#### 5. 本文实验

实验涵盖了多个开源模型，并设计了不同的提示（prompts），包括开放性问题、带有提示的问题和元问题。主要评估指标为准确率（ACC）、F1分数和接收者操作特征曲线下面积（AUC）。实验任务包括不可回答的视觉问答（VQA）、防御越狱攻击和识别欺骗性问题。

#### 6. 实验结论

* 线性探测在不同模型和提示下一致地提高了性能。
* 后续token的logit分布相比第一个token包含的信息较少。
* CLIP模型在这些任务上已经表现出色，暗示数据集存在偏差。
* 通过线性探测，可以在不增加大量计算成本的情况下，通过简单的解码策略改善LVLMs的安全性和可靠性。

#### 7. 全文结论

研究得出结论，LVLMs的logit分布有助于识别不当指令，并且这些logit在其他任务中也有用，如预测正确性、减少幻觉和图像分类。尽管如此，研究也指出了一些限制，包括实验完全基于LVLMs的输出层，需要更好的数据集来减少偏差，并提出了未来研究的方向。

#### 阅读总结

本文通过线性探测技术，对大型视觉-语言模型（LVLMs）的输出层进行了深入分析，揭示了模型在生成响应时隐藏的知识。研究表明，第一个token的logit分布包含了判断指令是否适当的关键信息，这一发现对于改进LVLMs的安全性和可靠性具有重要意义。此外，研究还指出了现有数据集的潜在偏差，并提出了未来研究的方向，以进一步提升LVLMs的性能。
