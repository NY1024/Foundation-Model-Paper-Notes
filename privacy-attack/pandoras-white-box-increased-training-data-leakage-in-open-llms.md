# PANDORA’S WHITE-BOX: INCREASED TRAINING DATA LEAKAGE IN OPEN LLMS

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

## 研究背景

本研究聚焦于开源大型语言模型（LLMs）的隐私攻击问题。随着LLMs如ChatGPT的兴起，它们在全球范围内引起了广泛关注，同时也引发了对其商业化、经济影响、未来社会影响以及即时部署可能带来的实际安全风险的担忧。特别是，LLMs在处理敏感数据时的隐私风险，因为它们可能会泄露、重新识别、链接、推断和利用有关个人身份、位置、习惯和欲望的敏感信息。

## 过去方案和缺点

以往的研究尝试通过会员推断攻击（MIA）来展示LLMs的隐私泄露问题，即通过攻击者访问模型的能力来区分训练样本和测试样本。然而，这些尝试在预训练的LLMs上的表现并不理想，通常无法超越随机猜测的准确率。这可能是因为预训练过程中数据留下的印记不明显，以及训练和测试数据成员之间的相似性使得区分变得模糊。

## 本文方案和步骤

本文提出了三种新的白盒MIA攻击方法：基于梯度范数的攻击、监督神经网络分类器（NN），以及单步损失比率攻击。这些方法在预训练模型上的表现优于现有的黑盒基线，并缩小了LLMs与其他类型模型在MIA攻击成功率上的差距。在微调设置中，研究者发现，通过访问微调和基础模型的损失，可以实现接近完美的MIA性能。此外，研究者还利用这些MIA来从微调后的语言模型中提取微调数据。

## 本文创新点与贡献

* 提出了针对预训练LLMs的首个能够同时实现高真正率（TPR）和低假正率（FPR）的MIA攻击。
* 展示了在自然设置中，超过50%的微调数据集可以从微调后的LLM中提取。
* 提出了一种新的微调损失比率攻击（FLoRa），在微调设置中实现了接近完美的MIA性能。
* 通过生成-然后-排名的数据提取流程，证明了在微调后的数据集中可以有效地提取大量数据。

## 本文实验

实验评估了一系列隐私攻击在不同大小的Pythia模型上的性能，以及在Llama-7B和Llama-7B-chat模型上的微调数据提取。实验结果表明，提出的MIA攻击在预训练和微调设置中都取得了显著的性能提升。

## 实验结论

实验结果表明，提出的MIA攻击在预训练和微调的LLMs中都能有效工作，尤其是在微调模型中，通过FLoRa攻击可以几乎完美地执行MIA。此外，通过生成-然后-排名的方法，可以从微调模型中提取大量训练数据。

## 全文结论

本文的研究结果强调了在高度敏感的数据上微调LLMs时需要谨慎，因为这些模型可能会泄露大量训练数据。研究者建议在部署LLMs之前，应采取适当的隐私保护措施，以防止潜在的隐私泄露风险。

## 阅读总结报告

本研究深入探讨了开源大型语言模型在隐私保护方面的脆弱性，特别是在预训练和微调阶段。通过提出新的攻击方法，研究者不仅提高了MIA的准确性，还展示了如何从微调后的模型中提取大量训练数据。这些发现对于理解和改进LLMs的隐私保护措施具有重要意义，同时也为未来的研究提供了新的方向。研究者强调了在敏感数据上微调LLMs时需要采取的预防措施，以确保数据安全。