# SneakyPrompt: Jailbreaking Text-to-image Generative Models

<figure><img src="../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 阅读总结报告

#### 1. 研究背景

文本到图像的生成模型（例如Stable Diffusion和DALL·E）因其能够根据文本提示生成合成图像而受到欢迎。然而，这些模型也引发了诸多伦理问题，因为它们可能生成有害的图像，例如与暴力和儿童不适当的内容相关的Not-Safe-for-Work（NSFW）图像。为应对这些伦理问题，通常会采用安全过滤器来阻止生成NSFW图像。但现有安全过滤器对于对抗性文本提示操纵的鲁棒性仍然未知。

#### 2. 过去方案和缺点

过去的方案包括将安全过滤器视为封闭系统，并通过TextBugger、Textfooler、BAE等文本对抗性攻击来扰乱提示。这些方法主要集中于误导分类模型，而不是绕过安全过滤器进行NSFW图像生成。现有文本对抗性攻击在探测安全过滤器时效率低下，需要大量查询，增加了攻击者的成本。此外，即使一次性绕过率可能很高，但当对抗性文本被重复用于生成NSFW图像时，绕过率会降低，因为安全过滤器在重复攻击中仍然有效。最后，现有工作较少关注生成图像的质量，常常导致图像失去预期的NSFW语义。

<figure><img src="../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

####

#### 3. 本文方案和步骤

本文提出了首个自动化攻击框架SneakyPrompt，用于绕过文本到图像生成模型的安全过滤器。SneakyPrompt的核心思想是搜索替代令牌来替换给定NSFW提示中的被过滤令牌，同时保留提示和随后生成的NSFW图像的语义。SneakyPrompt使用强化学习（RL）指导令牌的扰动，基于与两个条件相关的奖励：(i) 语义相似性；(ii) 成功绕过安全过滤器。SneakyPrompt的总体流程包括以下六个主要步骤：

1. 使用影子文本编码器获取目标提示的文本嵌入。
2. 从搜索空间中采样替代令牌以构建对抗性提示。
3. 使用对抗性提示查询在线文本到图像模型。
4. 如果安全过滤器未被绕过，则重复步骤2和3。
5. 计算生成图像与目标提示之间的相似度。
6. 如果相似度满足阈值，则停止搜索并输出对抗性提示和图像；否则，重复步骤2至5。

#### 4. 本文创新点与贡献

* 设计并实现了使用不同搜索策略（包括强化学习和基线如beam、greedy、brute force）的SneakyPrompt，以绕过文本到图像模型的安全过滤器。
* 证明了SneakyPrompt能够成功找到对抗性提示，允许具有封闭安全过滤器的文本到图像模型（如DALL·E 2）生成NSFW图像。
* 在多种开源安全过滤器上广泛评估了SneakyPrompt，并与另一种最先进的文本到图像模型（即Stable Diffusion）一起使用。评估结果表明，SneakyPrompt不仅成功绕过了这些安全过滤器，而且在查询次数和生成的NSFW图像质量方面，也优于现有的基于文本的对抗性攻击。

#### 5. 本文实验

实验使用了Python 3.9和Pytorch，在两台GeForce RTX 3090显卡上进行。目标文本到图像模型包括Stable Diffusion和DALL·E 2。评估涉及七种不同的安全过滤器，涵盖了文本基础、图像基础和文本-图像基础类别。使用了两个数据集进行评估：NSFW-200数据集和Dog/Cat-100数据集。评估指标包括绕过率、FID得分和在线查询次数。

#### 6. 实验结论

SneakyPrompt在绕过现有安全过滤器方面表现出高效性，能够生成与目标提示语义相似的图像，并且查询次数少于25次。在与Stable Diffusion模型的原始安全过滤器结合使用时，SneakyPrompt在一次攻击中实现了平均96.37%的绕过率，并在重用攻击中保持了较高的绕过率。此外，SneakyPrompt在保持图像语义相似性方面也表现出色，FID得分合理。对于DALL·E 2的封闭安全过滤器，SneakyPrompt实现了57.15%的一次绕过率，这表明即使是封闭的安全过滤器也可以被有效绕过。

#### 7. 全文结论

研究表明，即使是封闭的安全过滤器，也可以通过少量模型查询被绕过以生成NSFW图像。SneakyPrompt利用强化学习通过利用查询结果来策略性地指导提示的扰动，从而减少了对文本到图像模型的查询次数。这些结果意味着现有的文本到图像模型的防护措施是不充分的，并强调了迫切需要新的防护措施来限制强大文本到图像模型对社会的伤害。未来的研究方向包括开发更强大的安全过滤器，例如通过考虑对抗性提示的对抗性训练。

#### 阅读总结

本文提出了一个针对文本到图像生成模型的安全过滤器的自动化绕过攻击框架SneakyPrompt。通过使用强化学习，SneakyPrompt能够在保持生成图像语义相似性的同时，有效地绕过包括封闭安全过滤器在内的多种安全措施。实验结果表明，SneakyPrompt在查询次数和图像质量方面均优于现有方法。这项工作不仅展示了现有安全措施的不足，也为未来如何改进这些措施提供了宝贵的见解。