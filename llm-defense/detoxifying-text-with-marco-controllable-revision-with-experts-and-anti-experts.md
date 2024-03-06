# Detoxifying Text with MARCO:  Controllable Revision with Experts and Anti-Experts

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本研究聚焦于文本去毒化（Text Detoxification），旨在通过改写文本以去除冒犯性含义，从而减轻有毒语言的潜在危害。尽管已有研究尝试通过NLP系统检测和处理有毒语言，但对于那些微妙的、没有明确有毒关键词的偏见语言，检测和处理仍然具有挑战性。

### 2. 过去方案和缺点

以往的文本去毒化方法主要依赖于有毒语言分类器或有毒词汇列表，这些方法在处理微妙的有毒文本时效果有限。此外，这些方法往往需要有监督的平行数据，而在实际应用中，这类数据的获取可能受限。

### 3. 本文方案和步骤

研究者提出了MARCO（Mask and Replace with Context），一种结合可控生成和文本重写方法的去毒化算法。MARCO使用基于专家（非有毒语言模型）和反专家（有毒语言模型）的似然度来找到需要遮蔽和替换的候选词汇。该方法包括两个步骤：首先，通过专家和反专家模型的分歧来识别可能传达有毒含义的位置；其次，使用基础语言模型（LM）在专家和反专家的指导下自回归地生成重写文本。

### 4. 本文创新点与贡献

* 提出了一种新的无监督去毒化算法，能够有效处理微妙的有毒文本。
* 利用专家和反专家模型来确定文本中的有毒部分，这种方法比传统的基于分类器或词汇列表的方法更为精细。
* 在多个关注微妙有毒言论的数据集上进行了评估，证明了MARCO在自动和人工评估中均优于现有基线方法。

### 5. 本文实验

实验在三个关注微妙有毒言论的数据集上进行，包括Microagressions.com、Social Bias Frames和DynaHate。实验结果显示，MARCO在降低文本毒性的同时，保持了较好的流畅性和意义相似度。

### 6. 实验结论

MARCO在自动和人工评估中均表现出色，尤其是在处理微妙有毒文本方面。与CondBERT和ParaGeDi等基线方法相比，MARCO生成的文本毒性更低，且更受人工评估者的偏好。

### 7. 全文结论

MARCO作为一种新颖的文本去毒化方法，通过结合专家和反专家模型，有效地降低了文本的毒性，同时保持了文本的流畅性和意义。该方法的成功展示了可控生成与文本重写方法结合的有效性，并强调了使用LM捕捉毒性的重要性。

### 阅读总结

本研究通过MARCO算法，为文本去毒化领域提供了一种新的解决方案。MARCO通过专家和反专家模型的结合，有效地识别和替换了文本中的有毒部分，尤其在处理微妙有毒言论方面表现出色。这一方法不仅在自动评估中优于现有技术，而且在人工评估中也得到了更高的评价。然而，研究也指出了MARCO的一些局限性，包括对计算资源的需求以及在毒性评估中的潜在偏见问题。未来的工作可以探索更小的模型来控制更大的模型，或者更轻量级的方法，同时考虑在上下文中适应去毒化方法。