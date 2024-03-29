# INSTRUCTTA: Instruction-Tuned Targeted Attack  for Large Vision-Language Models

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型视觉-语言模型（LVLMs）在图像理解和响应生成方面展现出惊人的能力，它们在视觉交互的丰富性也使得LVLMs容易受到对抗性示例的攻击。这些模型通常依赖于大型语言模型（LLMs）来处理复杂的任务，但最近的研究表明，即使是带有视觉结构的LLMs也容易被通过在良性图像上添加不易察觉的扰动来制作的对抗性示例所欺骗。特别是，带有恶意目标的针对性攻击对LVLMs及其下游应用提出了更严重的安全问题。
2. 过去方案和缺点： 以往的研究主要集中在图像分类的对抗性攻击上，这些攻击通常旨在通过精心设计的对抗性图像来欺骗训练有素的视觉分类器。然而，这些方法在面对LVLMs时存在局限性，因为它们往往无法有效地处理模型对指令的依赖性，以及在不同模型和指令之间的转移性。

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种名为INSTRUCTTA（Instruction-Tuned Targeted Attack）的新型实用灰盒攻击场景。在这个场景中，攻击者只能访问受害者LVLM的视觉编码器，而无法获取其提示（通常是服务提供商的专有信息，不公开）和其底层的大型语言模型（LLM）。为了克服这些挑战，INSTRUCTTA首先使用公共的文本到图像生成模型将目标响应“反向”转换为目标图像，并使用GPT-4推断出与目标响应相符的合理指令。然后，形成一个本地替代模型（与受害者LVLM共享相同的视觉编码器）来提取对抗性图像示例和目标图像的指令感知特征，并最小化这两个特征之间的距离以优化对抗性示例。为了进一步提高转移性，INSTRUCTTA通过从LLM中改写指令来增强指令p′。
2. 本文创新点与贡献：

* 提出了INSTRUCTTA，这是一种在实际但未被探索的灰盒设置下对LVLMs进行攻击的方法，即攻击者只能访问LVLMs的视觉编码器，而不包括LLM和指令。
* 巧妙地利用文本到图像模型和LLM来推断合理的目标图像和指令，并使用指令调整范式来增强对抗样本的转移性。
* 通过广泛的实验证明了INSTRUCTTA在针对性攻击性能和转移性方面优于直观基线。

5. 本文实验和性能： 实验结果表明，INSTRUCTTA在多个受害者LVLMs上实现了优于现有基线的针对性攻击性能和转移性。通过使用CLIP-score评估针对性攻击性能，并记录了成功攻击的次数。此外，还进行了消融研究，以探索方法中主要组件的贡献，并讨论了不同扰动预算ϵ对攻击性能的影响。
6. 结论： 本文强调了在实际灰盒场景下LVLMs对对抗性攻击的脆弱性，并展示了INSTRUCTTA在提高LVLMs对抗性攻击的转移性方面的有效性。作者提出了通过负责任的研究来提高LVLMs生态系统安全性的观点，并展望了未来可能的缓解方法，如使用对抗性训练框架来训练LVLMs。

阅读总结报告： 本文针对大型视觉-语言模型（LVLMs）在面对对抗性攻击时的脆弱性进行了深入研究。作者提出了一种新的攻击方法INSTRUCTTA，该方法在实际的灰盒环境中，即使在攻击者无法获取模型的完整信息的情况下，也能有效地对LVLMs进行针对性攻击。通过利用文本到图像的生成模型和大型语言模型（LLM），INSTRUCTTA能够推断出合理的目标图像和指令，从而生成具有高转移性的对抗性样本。实验结果证明了INSTRUCTTA在攻击性能和转移性方面的优势。此外，作者还讨论了攻击的伦理问题，并提出了可能的缓解措施，以提高LVLMs的鲁棒性。这项工作不仅揭示了LVLMs的潜在安全风险，也为如何提高这些模型的安全性提供了有价值的见解。
