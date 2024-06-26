# Prompting4Debugging: Red-Teaming Text-to-Image Diffusion Models by Finding Problematic Prompts

<figure><img src="../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 研究背景

近年来，文本到图像的生成模型（如Stable Diffusion）在高质量内容生成方面取得了显著进展，成为AI变革性技术代表之一。然而，这些技术进步也伴随着对滥用生成技术产生版权或不适宜（NSFW）图像的担忧。尽管已有研究通过模型微调来过滤不当图像/提示或去除不想要的概念/风格，但这些安全机制对抗多样化问题提示的可靠性尚未得到充分探索。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 过去方案和缺点

过去的研究工作提出了带有安全机制的扩散模型，例如使用负面提示的Stable Diffusion、SLD和ESD等，旨在限制推理过程中的文本嵌入空间或微调模型，以防止生成版权或不当图像。尽管这些安全机制在评估方案中显示出部分有效性，但已有研究表明它们存在潜在缺陷。例如，即使使用NSFW安全过滤器，Stable Diffusion模型仍可能生成性内容，如果用户给出特定的文本提示。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 本文方案和步骤

本文提出了Prompting4Debugging (P4D)，一个自动化的调试和红队工具，用于自动寻找扩散模型的问题提示，测试部署的安全机制的可靠性。P4D框架利用提示工程技巧和无约束的扩散模型，自动高效地找到会导致不当内容的问题提示。具体步骤包括：

1. 使用无约束的T2I扩散模型G生成包含不当概念/对象C的图像x。
2. 通过G的编码器E获得x的潜在表示z，然后根据G的扩散过程计算任意时间步t的中间噪声潜在向量zt。
3. 寻找一个提示P\*，使得具有安全机制的T2I扩散模型G'在P_的条件下能够生成与x相似的输出x_，从而也包含类似的不当概念/对象C。

#### 本文创新点与贡献

* 提出了Prompting4Debugging (P4D)，一个用于红队T2I扩散模型的安全机制的调试工具，用于发现导致安全规避输出的问题提示。
* 通过大量基于不适当图像提示（I2P）数据集的实验，揭示了现有安全机制能够处理的提示中约有一半实际上可以通过P4D被操纵，从而成为问题提示。
* 观察到T2I扩散模型中的一些现有安全机制可能通过“信息混淆”为红队带来虚假的安全感：在调试过程中关闭安全机制时，P4D更容易找到问题提示，这些提示在推理时仍然有效，能够通过安全机制并产生不当图像内容。

#### 本文实验

* 使用概念相关和对象相关的数据集评估P4D的性能，包括I2P数据集和ESD中的“汽车”和“法国号”类别。
* 实验中采用了标准T2I模型（如Stable Diffusion）和安全T2I模型（如ESD、SLD和带有负面提示的SD）。
* 实验设置包括不同的提示长度、插入间隔和优化步骤，以及使用不同的基线方法进行比较。

#### 实验结论

* P4D在多个安全T2I模型和类别中显示出有希望且可比的结果，表明P4D-K在不损害调试性能的同时保留了提示的可解释性。
* 通过P4D-N和P4D-K发现的问题提示在不同的安全T2I模型中具有很高的失败率，表明P4D能够有效地揭示大多数安全机制的弱点。
* 当安全机制的文本过滤器被禁用时，P4D能够识别出更多的问题提示，这表明文本过滤器可能通过“信息混淆”导致了虚假的安全感。

#### 全文结论

本文提出的P4D是一个自动化的红队调试工具，能够揭示T2I扩散模型中使用的多个安全机制的前所未有的弱点。P4D通过主动发现可能导致不当图像的问题提示，帮助开发者保护和测试安全T2I扩散模型的可靠性。

#### 阅读总结报告

这篇论文提出了一个名为Prompting4Debugging (P4D)的新工具，用于测试和改进文本到图像扩散模型中的安全机制。P4D通过自动化的方式发现能够绕过安全措施的问题提示，揭示了现有安全机制的不足，并为开发者提供了一个有效的调试工具。实验结果表明，P4D能够显著提高发现问题提示的能力，并且发现的安全漏洞具有一定的普遍性，能够跨多个安全模型工作。这项工作不仅为改进现有的安全机制提供了洞见，也为未来在AI安全领域的研究奠定了基础。
