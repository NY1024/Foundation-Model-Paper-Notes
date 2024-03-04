# Jailbreaking Attack against Multimodal Large Language Model

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型语言模型（LLMs）如ChatGPT、Claude和Bard的广泛部署，它们展现出了先进的通用能力，但同时也带来了严重的安全风险，如真实性、有害性和偏见。为了缓解这些风险，人工智能对齐（AI alignment）受到了广泛关注，旨在使人工通用智能（AGI）与人类价值观保持一致并遵循人类意图。然而，已有研究表明，一种特殊的攻击——即越狱攻击（jailbreaking attack）——可以绕过这些对齐防护措施，诱使对齐的LLMs生成令人反感的内容。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 传统的越狱攻击方法试图找到特定的文本字符串（即文本越狱提示txtJP），通过将txtJP附加到有害请求上，可以诱使LLM生成令人反感的响应。然而，这些方法在效率上相对较低，主要是因为在寻找txtJP时面临离散优化的挑战。
2. 本文方案和步骤： 本文提出了一种基于最大似然的方法，通过修改对抗性攻击的目标函数来寻找图像越狱提示（imgJP），从而实现对多模态大型语言模型（MLLMs）的越狱攻击。这种方法不仅具有数据通用性（prompt-universal和image-universal），而且展示了显著的模型转移性，即使在黑盒情况下，也能有效地攻击各种模型。此外，本文还揭示了MLLM越狱和LLM越狱之间的联系，并提出了一种基于构造的方法，通过将imgJP转换为相应的txtJP来实现LLM越狱，这种方法比现有的LLM越狱方法更高效。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文实验和性能： 实验结果表明，所提出的方法在多个MLLM模型上实现了高效的越狱攻击，包括MiniGPT-v2、LLaVA、InstructBLIP和mPLUGOwl2。在模型转移性方面，通过在MiniGPT-4上生成imgJP，然后将其转移到其他模型上，实验结果显示出显著的转移性。此外，通过构造方法，作者成功地将imgJP转换为txtJP，并在LLaMA2模型上实现了高效的越狱攻击。

阅读总结报告： 本文深入研究了针对多模态大型语言模型的越狱攻击，并提出了一种基于最大似然的越狱方法。这种方法不仅在数据通用性方面表现出色，而且在模型转移性方面也显示出了显著的优势。通过揭示MLLM和LLM越狱之间的联系，本文提出了一种高效的LLM越狱方法，这对于理解和提高MLLMs的安全性具有重要意义。尽管本文的研究可能带来一定的风险，但作者强调了充分披露这一研究的重要性，以提高对MLLMs对齐问题的关注。



注：

本文提出的方案主要分为以下几个关键步骤：

1. **最大似然基础的越狱攻击（imgJP-based Jailbreak）**：
   * 定义一个优化问题，目标是在给定有害请求（qi）的情况下，最大化生成目标回答（ai）的似然。
   * 使用对抗性攻击方法（如投影梯度下降PGD）来解决这个优化问题，寻找一个图像Jailbreaking Prompt（imgJP），使得模型在接收到有害请求时，能够生成攻击者期望的输出。
2. **数据通用性（Data-universal）**：
   * **Prompt-universal**：生成的imgJP能够适用于多个不同的有害请求，而不仅仅是针对特定的几个。
   * **Image-universal**：找到一个通用的扰动（deltaJP），当添加到任何输入图像上时，都能够成功实现越狱。
3. **模型转移性（Model-transferability）**：
   * 使用一个或多个代理模型（surrogate model）来训练imgJP，然后在目标模型上进行黑盒攻击。
   * 通过集成多个MLLMs作为代理模型，提高了攻击的转移性。
4. **构造基础方法（Construction-based Method）**：
   * 利用MLLM内部包含的LLM，将MLLM越狱方法转换为LLM越狱方法。
   * 首先构建一个包含目标LLM的MLLM，然后将视觉组件与用户的文本查询结合，输入到目标LLM。
   * 执行MLLM越狱攻击以获取imgJP，并记录相应的嵌入（embJP）。
   * 通过去嵌入（De-embedding）和去标记化（De-tokenizer）操作，将embJP转换为文本空间中的txtJP。
   * 从生成的txtJP池中随机抽取序列，用于攻击目标LLM。
5. **实验实施**：
   * 构建了一个多模态数据集AdvBench-M，用于评估越狱攻击。
   * 在多个MLLM模型上进行了白盒和黑盒越狱攻击的实验。
   * 使用攻击成功率（ASR）作为主要评估指标。
6. **伦理和更广泛的影响**：
   * 作者强调了研究的潜在风险，并认为充分披露这一研究对于提高对MLLMs对齐问题的关注是重要的。

总结来说，本文提出的方案通过结合对抗性攻击技术和数据通用性策略，有效地对MLLMs进行了越狱攻击。此外，通过构造基础方法，将MLLM越狱技术应用于LLMs，提高了攻击的效率和适用性。这些研究成果对于理解和提高MLLMs的安全性具有重要意义。