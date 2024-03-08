# SafeDecoding: Defending against Jailbreak Attacks via Safety-Aware Decoding

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

随着大型语言模型（LLMs）在实际应用中的广泛集成，如代码生成和聊天机器人辅助，人们越来越关注如何使LLMs的行为与人类价值观保持一致，尤其是安全性。然而，"越狱"攻击（jailbreak attacks）旨在引发LLMs的非预期和不安全行为，这仍然是LLMs安全面临的重大威胁。

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### 2. 过去方案和缺点

以往的研究提出了多种防御方法，包括输入扰动、输入和输出检测以及提示演示等。然而，这些方法在实际应用中存在效率低下、可能影响LLMs对良性用户查询的有用性等问题。

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了SafeDecoding，一种针对LLMs的安全感知解码策略，用于生成对用户查询有帮助且无害的响应。SafeDecoding的核心思想是通过识别安全声明并放大其标记概率，同时减弱与攻击目标一致的标记序列的概率。SafeDecoding包含两个阶段：训练阶段构建专家模型，以及推理阶段基于原始模型和专家模型的输出构建新的标记分布。

### 4. 本文创新点与贡献

SafeDecoding的创新点在于它利用了LLMs在处理恶意输入时仍然存在的安全声明标记。通过这种方式，SafeDecoding能够在不牺牲对良性用户查询的有用性的情况下，显著降低越狱攻击的成功率和有害性。此外，SafeDecoding在计算上是轻量级的，与现有的解码策略相比，引入的计算开销可以忽略不计。



SafeDecoding是一种旨在保护大型语言模型（LLMs）免受越狱攻击的安全感知解码策略。以下是SafeDecoding的详细说明：

#### 核心观察与洞察

SafeDecoding的开发基于以下观察：即使代表有害内容的标记（token）的概率超过了代表无害响应的标记，安全声明（如“I'm sorry, I cannot...”）仍然在按概率降序排列的标记中出现。这表明，通过识别安全声明并放大它们的标记概率，同时减弱与攻击目标一致的标记序列的概率，可以减轻越狱攻击的影响。

#### SafeDecoding的两个阶段

1. **训练阶段**：
   * 构建专家模型：通过使用安全感知数据集对原始LLM进行微调，创建一个专家模型。这个数据集是通过让模型自主生成对有害查询的响应，然后使用GPT-4过滤出有效拒绝有害查询的响应来构建的。
   * 微调：使用参数高效的微调方法（如LoRA）对原始模型进行微调，以确保专家模型在面对恶意输入时能够适当响应。
2. **推理阶段**：
   * 创建新的标记分布：在推理时，将用户查询发送给原始模型和专家模型。SafeDecoding基于两个模型的输出构建一个新的标记分布。
   * 构建样本空间：取原始模型和专家模型输出的前k个标记的交集作为样本空间。
   * 定义概率函数：结合原始模型和专家模型的输出，构建一个新的概率函数，该函数会减弱与攻击目标一致的标记的概率，同时增强与人类价值观（包括安全）一致的标记的概率。

#### SafeDecoding的关键步骤

1. **构建样本空间**（V(c)\_n）：在推理的第n步，将前n-1个标记的序列发送给原始模型和专家模型，然后取两个模型输出的前k个标记的交集作为样本空间。
2. **定义概率函数**（Pn）：对于给定的标记序列x1:n-1，SafeDecoding构建概率函数Pn，该函数结合了原始模型和专家模型的输出，并通过一个超参数α来调整两者的权重。
3. **采样生成响应**：根据构建的标记分布，SafeDecoding采样标记以生成对输入查询的响应。这个过程与现有的采样方法（如top-p, top-k, greedy, beam search）兼容。

#### SafeDecoding的创新点

* **安全性增强**：通过识别和放大安全声明的标记概率，SafeDecoding能够有效地防御越狱攻击。
* **计算效率**：SafeDecoding在推理时只对前几个标记应用安全感知策略，这使得计算开销相对较小。
* **兼容性**：SafeDecoding的设计使其能够与不同架构和参数的LLMs兼容。

####





### 5. 本文实验

作者在五个LLMs上进行了广泛的实验，使用了六种最先进的越狱攻击和四个基准数据集。实验结果表明，SafeDecoding在防御越狱攻击方面显著优于六种基线方法，同时在对良性用户查询的响应上保持了高效和有用性。

### 6. 实验结论

实验结果证实了SafeDecoding在防御越狱攻击方面的有效性，同时在保持LLMs对良性用户查询的有用性方面表现出色。此外，SafeDecoding的计算效率也得到了验证，与不采用防御策略的LLMs相比，引入的计算开销很小。

### 7. 全文结论

本文成功提出了SafeDecoding，这是一种新的、计算上轻量级的解码策略，能够有效地防御LLMs面临的越狱攻击，同时保持对良性用户查询的高效和有用性。SafeDecoding的提出为LLMs的安全性研究提供了新的视角和方法。

### 阅读总结

本文针对LLMs在实际应用中的安全性问题，提出了一种新的解码策略SafeDecoding。通过在训练阶段构建专家模型，并在推理阶段结合原始模型和专家模型的输出，SafeDecoding能够有效地降低越狱攻击的成功率，同时保持对良性查询的响应质量。实验结果表明，SafeDecoding在多个LLMs上的表现优于现有防御方法，且计算开销小，具有较高的实用价值。这一研究为LLMs的安全性提供了新的解决方案，对于推动LLMs在安全领域的应用具有重要意义。