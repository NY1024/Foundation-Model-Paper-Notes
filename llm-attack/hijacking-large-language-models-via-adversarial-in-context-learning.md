# Hijacking Large Language Models via Adversarial In-Context Learning

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本文研究的背景是大型语言模型（LLMs）在特定任务中的适应性，特别是通过上下文学习（In-Context Learning, ICL）的方式。ICL 通过在预处理提示中使用标记示例作为演示，使得LLMs能够在不微调预训练参数的情况下快速适应新任务。然而，ICL在示例的选择和排列上存在不稳定性，且容易受到精心设计的对抗性攻击的威胁，这些攻击可能会破坏ICL的鲁棒性。

### 2. 过去方案和缺点

过去的研究已经提出了一些方法来解决ICL的不稳定性，例如通过选择最相似的示例作为演示来提高准确性和稳定性。然而，现有的对抗性攻击要么容易被检测到，要么依赖于外部模型，或者缺乏针对ICL的特异性。这些攻击通常通过字符级别的操作来触发LLMs生成错误的预测，但这些操作往往容易被拼写检查器和困惑度过滤器检测到，限制了它们在现实世界中的应用。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种新的可转移的对抗性攻击，旨在劫持LLMs以生成目标响应。该攻击利用基于梯度的提示搜索方法，学习并附加不可感知的对抗性后缀到上下文演示中。攻击步骤包括：

* 使用梯度优化学习对抗性后缀。
* 通过贪婪梯度引导注入（GGI）算法，迭代地注入最佳标记以优化后缀。
* 在不同的数据集和任务上验证攻击的有效性。

### 4. 本文创新点与贡献

本文的主要创新点和贡献包括：

* 提出了一种新的隐蔽攻击，可以在不需要触发器的情况下劫持LLMs生成目标不期望的输出。
* 设计了一种新的基于梯度的提示搜索算法，用于学习和附加对抗性后缀到上下文演示中。
* 通过广泛的实验验证了ICL攻击的可转移性，展示了LLMs在ICL期间的脆弱性。

### 5. 本文实验

实验部分验证了LLM劫持攻击的有效性。实验使用了不同的LLMs（如GPT2-XL、LLaMA-7b和OPT-2.7b/6.7b）在多个分类数据集（如SST-2、RT和AG News）上进行。实验结果表明，攻击能够可靠地诱导LLMs生成目标和不一致的输出，且对抗性后缀通过梯度优化学习是可转移的。

### 6. 实验结论

实验结果表明，本文提出的LLM劫持攻击在不同的数据集、LLMs和任务上都显示出了高度的有效性。攻击能够通过添加对抗性后缀来分散LLMs的注意力，从而生成目标不期望的输出。

### 7. 全文结论

本文揭示了ICL在对抗性攻击面前的新脆弱性，并提出了一种有效的对抗性攻击方法。这种攻击通过在上下文演示中添加对抗性后缀来劫持LLMs，展示了LLMs在实际应用中可能面临的重大风险。研究结果强调了开发更健壮的ICL方法的紧迫性。

### 阅读总结

本文针对大型语言模型在特定任务适应性中的脆弱性进行了深入研究，特别是在上下文学习（ICL）的背景下。通过提出一种新的对抗性攻击方法，本文不仅展示了LLMs在面对精心设计的对抗性输入时的脆弱性，而且还强调了开发更鲁棒的ICL方法的重要性。实验结果表明，本文提出的攻击方法在多个数据集和模型上都显示出了高度的有效性，这对于理解和改进LLMs的安全性具有重要意义。