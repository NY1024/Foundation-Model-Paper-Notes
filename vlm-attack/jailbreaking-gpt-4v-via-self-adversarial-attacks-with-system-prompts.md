# Jailbreaking GPT-4V via Self-Adversarial Attacks with System Prompts

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 多模态大型语言模型（MLLMs）如GPT-4V在生成详细图像描述、生成代码、定位图像内视觉对象以及执行高级多模态推理方面展现出强大的能力。然而，这些模型在训练过程中可能会接触到有害或私密内容，存在生成不期望输出的风险。为了确保安全输出，研究者们通过安全机制对这些模型进行了微调。尽管如此，越狱攻击（jailbreaking）旨在绕过这些安全约束和内容过滤机制。以往的研究主要集中在模型输入的对抗性示例上，而对于模型API中的漏洞，尤其是系统提示（system prompts）的漏洞，研究较少。

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的研究主要关注于通过对抗性图像来攻击MLLMs，例如通过在图像中添加微小的扰动来诱使模型生成不当内容。然而，这些方法通常需要对模型的内部工作有深入的了解，并且在攻击过程中可能需要多次迭代和调整。此外，这些方法在处理模型API层面的漏洞时，尤其是系统提示的漏洞，研究较少。

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种名为SASP（Self-Adversarial Attack via System Prompt）的新方法，通过利用GPT-4作为红队工具来攻击自身，自动化地将系统提示转换为越狱提示。首先，通过精心设计的对话，成功提取了GPT-4V的内部系统提示。然后，利用这些系统提示，通过自我对抗的方式，迭代地生成能够绕过GPT-4V安全约束的越狱提示。此外，为了提高攻击成功率，还加入了基于GPT-4分析的人工修改，将攻击成功率提高到了98.7%。

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文实验和性能： 实验结果表明，SASP方法能够有效地从GPT-4V中提取系统提示，并将其转换为越狱提示。通过这种方法，研究者们能够在GPT-4V上实现高达59%的越狱成功率，并且通过人工修改进一步将成功率提高到99%。此外，研究还探讨了通过修改系统提示来防御越狱攻击的有效性，结果表明适当设计的系统提示可以显著降低越狱成功率。



注1：

在论文 "Jailbreaking GPT-4V via Self-Adversarial Attacks with System Prompts" 中，作者提出了一种名为SASP（Self-Adversarial Attack via System Prompt）的方法，用于生成能够绕过大型多模态语言模型（MLLMs）如GPT-4V的安全限制的越狱提示。这种方法的核心是通过自我对抗的方式，利用模型自身的系统提示（system prompts）来攻击模型。以下是SASP方法的主要步骤：

1. **系统提示窃取（System Prompt Theft）**：
   * 首先，通过精心设计的对话，研究者们能够从GPT-4V中提取内部系统提示。这些系统提示通常用于为模型的响应建立基础上下文，并作为初始指令。
   * 通过模拟不完整的对话和直接请求GPT-4V完成对话，研究者们能够诱导模型透露其内部系统提示。
2. **自我对抗越狱（Self-Adversarial Jailbreak）**：
   * 一旦获得了系统提示，研究者们使用GPT-4作为“红队”（red-teaming）工具，对GPT-4V进行自我攻击。
   * 通过迭代搜索，GPT-4尝试找到能够绕过GPT-4V安全约束的越狱提示。如果越狱失败，目标模型的响应会被用来生成更强大的越狱提示。
3. **越狱提示增强（Jailbreak Prompt Enhancement）**：
   * 为了提高越狱成功率，研究者们提出了四种方法来增强越狱提示：前缀注入（prefix injection）、拒绝抑制（refusal suppression）、创建假设场景（creating hypothetical scenarios）和情感诉求（appealing with emotion）。
   * 这些方法结合使用，可以进一步提高越狱提示的有效性，使GPT-4V在攻击中成功越狱的概率达到98.7%。

通过这种方法，研究者们展示了系统提示在越狱攻击中的重要作用，同时也指出了通过适当设计系统提示来防御这类攻击的可能性。这种方法不仅为增强MLLMs的安全性提供了新的见解，而且强调了系统提示在促进和阻止越狱尝试中的关键角色。



注2：



阅读总结报告： 本文的研究揭示了MLLMs中系统提示泄露的安全隐患，并提出了一种新的越狱攻击方法SASP。这种方法不仅能够有效地从GPT-4V中提取系统提示，还能够通过自我对抗的方式生成越狱提示，显著提高了越狱攻击的成功率。此外，研究还探讨了系统提示在防御越狱攻击中的潜力，为提高MLLMs的安全性提供了新的见解。这些发现不仅为越狱攻击提供了新的途径，也为防御这类攻击提供了有价值的策略。
