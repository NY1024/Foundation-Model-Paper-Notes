# FigStep: Jailbreaking Large Vision-language Models via Typographic Visual Prompts

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 本文研究的背景是大型视觉-语言模型（VLMs）在人工智能（AI）领域的安全性问题。VLMs结合了视觉和文本模态，能够处理更复杂的任务，但同时也带来了新的安全挑战。尽管大型语言模型（LLMs）已经有一定的安全对齐措施，但VLMs在视觉模态的引入可能带来未知的安全风险，导致模型产生违反AI安全政策的输出。

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的研究主要集中在LLMs的安全对齐上，如数据清洗、指令微调、人类反馈强化学习（RLHF）等。然而，这些方法主要针对单模态语言模型，对于VLMs的跨模态对齐（尤其是视觉和文本模态）的研究相对较少。此外，现有的安全评估方法可能无法充分覆盖VLMs在视觉模态下的安全风险。



<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了FigStep，一种针对VLMs的越狱算法。FigStep通过将有害内容转换为图像中的排版文本，绕过VLMs文本模块内的安全对齐，诱导VLMs输出违反AI安全政策的响应。FigStep的步骤包括：(1) 将有害问题转换为声明性语句；(2) 使用排版将这些指令嵌入图像提示中；(3) 使用良性的激励文本来激发VLMs的推理能力，并指导VLMs生成详细的响应。
2. 本文创新点与贡献：

* 提出了FigStep，这是一种简单但有效的黑盒越狱算法，用于评估VLMs的跨模态安全对齐。
* 通过实验表明，FigStep能够在多个开源VLMs上实现高达82.50%的平均攻击成功率。
* 提出了FigStep-Pro，一种升级版的FigStep，用于越狱GPT-4V，通过策略性地分割图像来绕过OCR检测器。

5. 本文实验和性能： 作者对三种开源VLM家族（LLaVA-v1.5、MiniGPT4和CogVLM）的六个VLM进行了全面评估。通过手动审查46,500个模型响应，实验结果表明FigStep在500个有害查询的10个主题上平均攻击成功率为82.50%。此外，FigStep-Pro在GPT-4V上实现了70%的攻击成功率。
6. 结论： 本文揭示了VLMs在视觉和文本模态对齐方面的脆弱性，并强调了开发新的安全对齐方法的必要性，以确保VLMs的安全性和可靠性。作者呼吁在发布VLMs之前确保严格的跨模态对齐，以防止潜在的误用风险。

阅读总结报告： 本文针对VLMs的安全性问题提出了FigStep越狱算法，该算法通过将有害内容转换为图像中的排版文本，成功绕过了VLMs的安全对齐机制。实验结果表明，FigStep在多个开源VLMs上表现出高效的攻击能力，并且即使在GPT-4V这样的先进VLM上，通过FigStep-Pro也能实现较高的攻击成功率。这一发现强调了在VLMs的设计和部署中，需要更加关注跨模态安全对齐的重要性，并促进了对VLMs安全性研究的进一步发展。
