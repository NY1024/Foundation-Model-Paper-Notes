# Improved Generation of Adversarial Examples Against Safety-aligned LLMs

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 研究背景

大型语言模型（LLMs）因其在语言理解和生成类人文本方面的卓越能力而备受关注。尽管众多研究致力于确保这些模型遵循安全标准并产生无害内容，但已有研究表明这些模型尚未完全达到安全对齐，存在被精心设计的提示（即“越狱”攻击）诱导产生有害内容的风险。这些越狱攻击手动设计成本高，而自动生成的对抗性示例则对模型的鲁棒性提出了更隐蔽的挑战。

### 过去方案和缺点

以往的研究尝试使用基于梯度的方法来解决对抗性示例的生成问题，例如Greedy Coordinate Gradient (GCG) 攻击。然而，由于文本的离散性，基于梯度的优化方法难以精确反映token替换导致的损失变化，这限制了对安全对齐的LLMs的攻击成功率。

### 本文方案和步骤

本文从新的视角探讨了这一问题，提出通过利用针对黑盒图像分类模型提出的基于迁移的攻击中的创新来缓解这一问题。具体来说，本文首次将两种有效的基于迁移攻击方法的理念——Skip Gradient Method (SGM) 和 Intermediate Level Attack (ILA) —— 引入到针对白盒LLMs的自动生成对抗性示例中。适当调整后，这些方法被注入到基于梯度的对抗性提示生成过程中，实现了显著的性能提升，且没有引入明显的计算成本。

### 本文创新点与贡献

1. 提出一种新视角，将对抗性示例的生成问题与黑盒图像分类模型的迁移攻击问题联系起来。
2. 首次将SGM和ILA方法的理念适用于LLMs的白盒攻击。
3. 通过实验验证了新方法在生成特定查询和通用对抗性提示时的有效性，并与GCG攻击进行了比较。

### 本文实验

实验使用了两种评估指标：匹配率（MR）和攻击成功率（ASR）。在AdvBench数据集上，针对Llama-2-7B-Chat模型进行了查询特定和通用对抗性后缀生成的实验。实验结果显示，新方法在匹配率和攻击成功率上均优于GCG攻击。

### 实验结论

实验结果表明，通过适当组合SGM和ILA方法，可以显著提高对抗性示例的生成效果。具体来说，新方法在查询特定对抗性后缀生成任务中，将匹配率从54%提高到87%，在通用对抗性后缀生成任务中，将攻击成功率从26.68%提高到60.32%。

### 全文结论

本文提出的新方法通过借鉴黑盒图像分类模型的迁移攻击策略，有效地提高了针对安全对齐的大型语言模型的对抗性示例生成的成功率。这不仅为评估LLMs的鲁棒性提供了新的工具，也为解决LLMs中的离散优化问题提供了新的视角。

### 阅读总结报告

这篇论文《Improved Generation of Adversarial Examples Against Safety-aligned LLMs》针对当前大型语言模型（LLMs）在安全性方面的挑战，提出了一种新的对抗性示例生成方法。研究者们观察到，尽管已有多种努力来确保LLMs遵循安全标准，但模型仍可能被精心设计的提示诱导产生不当内容。本文的核心贡献在于引入了两种针对黑盒图像分类模型的迁移攻击策略——SGM和ILA——并成功地将它们调整应用于LLMs的白盒攻击中。

研究者们首先分析了现有基于梯度的攻击方法的局限性，然后提出了一种新的视角，将对抗性示例的生成问题与迁移攻击中的问题联系起来。通过在GCG攻击方法的基础上，结合SGM和ILA的策略，研究者们开发了一种新的组合方法，显著提高了攻击的成功率和匹配率。

实验部分，研究者们在AdvBench数据集上对Llama-2-7B-Chat模型进行了评估，证明了新方法在不同场景下的有效性。实验结果不仅展示了新方法在提高攻击成功率方面的显著效果，同时也表明了新方法在减少候选集大小、节省运行时间方面的潜力。

最终，论文得出结论，新方法通过结合SGM和ILA的策略，有效地解决了LLMs中对抗性示例生成的离散优化问题，并为评估和提高LLMs的安全性提供了新的工具和视角。这项工作不仅对理解LLMs的安全漏洞具有重要意义，也为未来的安全研究和模型改进提供了有价值的见解。
