# VISUAL ADVERSARIAL EXAMPLES  JAILBREAK ALIGNED LARGE LANGUAGE MODELS

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型语言模型（LLMs）的兴起，尤其是视觉语言模型（VLMs）如Flamingo和GPT-4，将视觉与语言整合的趋势日益明显。然而，这种多模态整合带来了新的安全和安全挑战。视觉输入的连续性和高维性使其成为对抗性攻击的薄弱环节，扩大了视觉整合LLMs的攻击面。此外，LLMs的多功能性为视觉攻击者提供了更广泛的对抗性目标，使得安全失败的影响超出了简单的误分类。
2. 过去方案和缺点： 以往的研究主要集中在如何提高模型对对抗性攻击的鲁棒性，例如通过对抗性训练和鲁棒性认证。然而，这些方法往往成本高昂，且大多数依赖于离散类别，这在开放输出的LLMs中是一个主要障碍。此外，这些防御措施通常假设对抗性扰动是不可感知的，但在本文的威胁模型中，对抗性扰动并不一定是不可感知的。
3. 本文方案和步骤： 本文提出了一种利用视觉对抗性示例来绕过对齐LLMs的安全防护的方法。首先，作者通过优化一个小型有害内容语料库上的对抗性示例来最大化模型在给定对抗性示例条件下生成这些有害句子的概率。然后，在推理阶段，将对抗性示例与有害文本指令一起作为联合输入提供给模型。通过这种方式，即使模型原本会拒绝有害指令，也会被迫执行并生成有害内容。
4. 本文创新点： 本文的创新之处在于展示了如何使用视觉对抗性示例作为通用的“越狱工具”来绕过对齐LLMs的安全防护。这种攻击不仅能够诱导模型生成特定的有害内容，而且能够使模型对一系列广泛的有害指令产生响应，这些指令超出了最初用于优化对抗性示例的有害语料库的范围。此外，本文还探讨了这种攻击在多模态LLMs中的普遍性和黑盒迁移性。
5. 本文实验和性能： 作者在多个VLMs上进行了实验，包括MiniGPT-4、InstructBLIP和LLaVA。实验结果表明，视觉对抗性示例能够显著提高模型生成有害内容的概率。此外，作者还验证了攻击在不同模型之间的黑盒迁移性。在RealToxicityPrompts基准测试中，对抗性示例显著增加了模型输出的有害属性。作者还探讨了现有的防御措施，如DiffPure，发现这些措施在一定程度上可以降低生成有害内容的概率，但无法完全消除风险。

阅读总结报告： 本文深入研究了视觉对抗性示例对大型语言模型安全性的影响，特别是在多模态整合的背景下。作者提出了一种新的攻击方法，该方法利用视觉对抗性示例来绕过LLMs的安全防护，展示了这种攻击的普遍性和迁移性。实验结果强调了在开发多模态系统时需要考虑的安全和安全挑战。本文的研究不仅对技术实践者提出了挑战，也对政策制定者提出了在制定相关法规时需要考虑的新问题。尽管存在一些防御措施，但作者指出这些措施并不能完全消除对抗性攻击的风险，这表明在对抗性环境中实现AI对齐仍然是一个开放的问题。



注：

这种攻击能够成功的原因主要归结于以下几个关键因素：

1. **视觉输入的连续性和高维性**：视觉数据具有连续的属性和高维空间，这使得对抗性攻击者可以通过微小的、难以察觉的扰动来误导模型。这种连续性使得在视觉空间中寻找有效的对抗性示例相对容易。
2. **模型的多功能性**：大型语言模型（LLMs）通常具有强大的多功能性，能够处理各种任务。这种多功能性为攻击者提供了多种可能的对抗性目标，从而增加了安全失败的潜在影响。
3. **对抗性攻击的普遍性**：对抗性攻击在机器学习领域已经被广泛研究，尤其是在图像识别领域。这些攻击通常通过精心设计的输入来欺骗模型，使其做出错误的预测或生成不期望的输出。
4. **模型的安全防护机制的局限性**：尽管LLMs可能已经实施了一些安全防护措施，如拒绝有害指令，但这些机制可能并不完善。对抗性攻击可以针对这些防护机制的弱点，通过特定的输入扰动来绕过或破坏这些防护。
5. **对抗性示例的优化**：在本文中，作者通过优化对抗性示例来最大化模型在给定对抗性示例条件下生成有害内容的概率。这种优化过程利用了模型的内部机制，使其在面对对抗性输入时更容易产生有害输出。
6. **模型的对齐挑战**：LLMs的对齐问题是指确保模型的行为与其设计者的意图一致。在多模态环境中，对齐变得更加复杂，因为模型需要处理来自不同模态的输入。对抗性攻击可以利用这种复杂性来破坏模型的对齐状态。
7. **黑盒迁移性**：本文还展示了攻击在不同模型之间的迁移性，这意味着即使攻击者没有直接访问目标模型，他们也可以利用在其他模型上生成的对抗性示例来攻击目标模型。这种迁移性增加了攻击的普遍性和难以防御性。

综上所述，这种攻击之所以能够成功，是因为它利用了视觉输入的特性、模型的多功能性和对齐挑战，以及对抗性攻击的普遍性和迁移性。这些因素共同作用，使得对抗性攻击能够有效地绕过或破坏LLMs的安全防护机制。

