# AMutation-Based Method for Multi-Modal Jailbreaking Attack

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型语言模型（LLMs）和多模态大型语言模型（MLLMs）在各种应用中的普及，它们在从简单的聊天机器人到复杂的决策系统中的应用变得越来越重要。然而，这些模型的安全性问题也日益凸显，尤其是它们对越狱攻击（jailbreaking attacks）的脆弱性。越狱攻击允许恶意用户操纵模型，违反规则或泄露机密数据，从而损害模型的可靠性和用户对基于AI应用的信任。

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 现有的越狱攻击检测方法主要分为两类：基于查询后（post-query）和基于查询前（pre-query）的防御。基于查询后的方法通常需要特定的目标领域知识，并且只能在安全漏洞发生后识别。而基于查询前的方法主要关注文本级别的攻击，无法满足现代LLMs日益复杂的多模态安全需求。这些方法的局限性强调了需要一种更全面的保护方法来维护这些有影响力的系统。

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了JailGuard，这是一个基于变异的越狱攻击检测框架，支持图像和文本模态。JailGuard的关键观察是攻击查询与良性查询相比具有更低的鲁棒性。为了混淆模型，攻击查询通常是基于精心设计的模板或复杂的扰动生成的，这导致输入的微小变化可能导致响应的显著变化。JailGuard利用这种不鲁棒性，通过首先将传入的输入变异为变体查询，然后检查变体响应的分歧来检测攻击。基于这一直觉，作者设计并实现了一个包含19种不同变异器和基于分歧的检测公式的检测框架。

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

1. 本文创新点与贡献：

* 提出了JailGuard，这是第一个基于变异的多模态越狱检测框架，支持图像和文本模态的攻击检测。
* 构建了第一个覆盖图像和文本输入的越狱攻击数据集。
* 在构建的数据集上进行实验，JailGuard在图像和文本输入上的检测准确率分别达到了89.38%和85.42%，优于现有最先进的防御方法。

5. 本文实验： 作者构建了一个包含304个数据项的多模态LLM越狱攻击数据集，涵盖了十种已知的图像和文本模态的越狱攻击。通过在该数据集上的评估，JailGuard能够有效地检测图像和文本模态的越狱攻击。
6. 结论： JailGuard在检测和防御LLM越狱攻击方面表现出色，其在图像和文本输入上的检测准确率分别达到了89.38%和85.42%，显著优于现有的防御方法。此外，JailGuard能够有效地检测和防御不同类型的越狱攻击，对于所有收集到的攻击类型，JailGuard的最佳检测准确率始终超过70%。

注：

在本文中，作者提出了一个名为JailGuard的越狱攻击检测框架，该框架包含19种不同的变异器（mutators）和一个基于分歧（divergence）的检测公式。这些变异器用于生成输入的变体（variants），以便检测和防御针对大型语言模型（LLMs）的越狱攻击。以下是对这些变异器和检测公式的详细说明：

#### 变异器（Mutators）：

变异器的作用是在原始输入上执行特定的变异操作，以生成与原始输入略有不同的变体集合。这些变异器分为两大类：随机变异器（Random Mutators）和高级变异器（Advanced Mutators）。

**随机变异器（Random Mutators）：**

* **图像变异器**：包括随机遮罩（Random Mask）、随机太阳化（Random Solarization）、水平翻转（Horizontal Flip）、垂直翻转（Vertical Flip）、裁剪和调整大小（Crop and Resize）、随机灰度化（Random Grayscale）、高斯模糊（Gaussian Blur）、随机旋转（Random Rotation）、颜色抖动（Colorjitter）和随机海报化（Random Posterization）。
* **文本变异器**：包括随机替换（Random Replacement）、随机插入（Random Insertion）、随机删除（Random Deletion）、同义词替换（Synonym Replacement）、标点插入（Punctuation Insertion）和翻译（Translation）。

**高级变异器（Advanced Mutators）：**

* **目标替换（Targeted Replacement）**：在输入文本中找到出现频率最高的单词，并用它们的同义词替换。
* **目标插入（Targeted Insertion）**：在重要句子中插入特定的文本，以干扰潜在的攻击输入。
* **改述（Rephrasing）**：使用自然语言处理技术重新表述输入，同时保持核心语义和内容不变。

#### 基于分歧的检测公式（Divergence-Based Detection Formula）：

检测器利用输出之间的分歧来有效实现检测。具体步骤如下：

1. **构建相似性矩阵**：对于输入变体集合，检测器首先查询LLM系统以获取响应集合。然后，使用‘spaCy’库将每个响应转换为词向量，并计算它们之间的余弦相似度。
2. **表征每个响应**：在相似性矩阵中，每个响应的行通过L1标准化转换为相似性概率分布，有效地表征了响应与其他响应的关系。
3. **量化两个响应之间的分歧**：使用Kullback-Leibler（KL）散度来量化两个响应的相似性分布之间的差异。
4. **检查分歧**：对于得到的分歧矩阵，检测器使用阈值ε来判断原始输入是否为攻击输入。如果分歧矩阵中的任何值超过ε，JailGuard将认为原始输入是攻击输入。

通过这种基于变异和分歧的方法，JailGuard能够有效地检测出那些设计来绕过LLM防御机制的攻击输入。这种方法的核心优势在于它能够利用攻击输入相对于良性输入的不鲁棒性，即攻击输入对输入的微小变化更敏感，从而在模型响应中产生显著的变化。这种变化可以通过JailGuard的变异器和检测公式被捕捉到，从而实现对越狱攻击的有效检测。



5. 阅读总结报告： 本文针对LLMs和MLLMs在安全性方面的挑战，提出了一个新的越狱攻击检测框架JailGuard。该框架通过变异输入并分析响应的分歧来检测攻击，这种方法在图像和文本模态上都显示出了高准确率。JailGuard的提出不仅填补了现有防御方法在多模态安全需求方面的空白，而且通过实验验证了其有效性。此外，作者还构建了一个全面的越狱攻击数据集，为未来的研究提供了宝贵的资源。JailGuard的成功实施为LLMs的安全性提供了新的保障，对于维护基于AI应用的完整性和信任至关重要。
