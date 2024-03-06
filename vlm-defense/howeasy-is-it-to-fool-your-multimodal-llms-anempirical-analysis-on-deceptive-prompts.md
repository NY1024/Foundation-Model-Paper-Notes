# HowEasy is It to Fool Your Multimodal LLMs?  AnEmpirical Analysis on Deceptive Prompts

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 本研究探讨了多模态大型语言模型（MLLMs）在处理包含欺骗性信息的提示（prompts）时的脆弱性。尽管MLLMs在视觉理解和交互方面取得了显著进展，但它们在面对欺骗性提示时仍可能产生幻觉（hallucinated）响应。这种脆弱性对于模型在现实世界应用中的可靠性和信任度至关重要。

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的研究主要集中在通过提示工程（prompt engineering）和模型增强（model enhancement）来减轻大型语言模型（LLMs）的幻觉问题。然而，这些方法在面对MLLMs时的欺骗性提示方面并未显示出足够的有效性。特别是，之前针对幻觉缓解的模型，如LRV-Instruction和LLaVA-RLHF，在新的基准测试中表现不佳。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 研究者提出了MAD-Bench（MultimodAl Deception Benchmark），这是一个包含850个测试样本的基准测试，分为六个类别，如不存在的对象、对象数量、空间关系和视觉混淆等。研究者对流行的MLLMs进行了全面分析，包括GPT-4V、Gemini-Pro以及开源模型LLaVA-1.5和CogVLM。此外，研究者还提出了一种简单的方法，通过在欺骗性提示前添加额外的段落来提高模型的准确性。
2. 本文创新点与贡献：
   * 构建了MAD-Bench，这是一个新的基准测试，用于全面评估MLLMs在抵抗欺骗性提示方面的能力。
   * 对流行的MLLMs进行了详细分析，并列出了导致错误响应的一些常见原因。
   * 提供了一种通过精心设计的系统提示来提高性能的简单方法。
3. 本文实验： 实验通过自动化的方式使用GPT-4来评估10个模型的生成响应。实验结果显示，GPT-4V在MAD-Bench上的准确性最高，达到了75.02%，而其他模型的准确性范围在5%到35%之间。
4. 通过对实验数据的分析得到的结论：
   * MLLMs在处理欺骗性提示时存在显著的性能差距，尤其是与GPT-4V相比。
   * 即使是旨在减轻幻觉的模型，如LRV-Instruction和LLaVA-RLHF，在新的基准测试中也未能有效。
   * 通过添加额外的提示段落，可以显著提高模型的准确性，尽管绝对数值仍然不尽人意。
5. 结论： 研究者强调了MLLMs在面对欺骗性提示时的脆弱性，并希望MAD-Bench能够激发进一步的研究，以增强模型对欺骗性提示的抵抗力。同时，研究者也指出了MAD-Bench的局限性，并提出了未来研究的潜在方向，如创建包含欺骗性提示的训练数据子集，以及在生成响应前检查图像和提示之间的一致性。

阅读总结报告： 本研究通过MAD-Bench基准测试，揭示了多模态大型语言模型在处理欺骗性提示时的脆弱性。GPT-4V在抵抗这类提示方面表现最佳，但仍然有改进空间。研究者提出了一种简单的方法来提高模型的准确性，即在提示前添加额外的段落以鼓励模型在回答问题前进行更深入的思考。尽管这种方法在提高准确性方面取得了一定的成功，但研究者认为还有更多的工作需要做，以进一步提高MLLMs的鲁棒性。此外，研究者还提出了未来研究的方向，包括创建专门的训练数据集和改进模型的决策过程。
