# From Noise to Clarity: Unraveling the Adversarial Suffix of Large Language Model Attacks via Transla

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型语言模型（LLMs）在自然语言处理（NLP）领域取得了显著进展，但它们在生成有害内容方面的风险也日益增加。现有的LLM安全防御方法主要依赖于手动策划的危险提示，这些方法无法跟上不断出现的新型攻击。最近的研究发现，通过在有害指令后附加不可读的对抗性后缀，可以绕过LLMs的防御机制，导致危险的输出。然而，这种方法的有效性有限，因为它依赖于不可读的后缀，这容易被常见的防御方法（如困惑度过滤器）检测到。

### 2. 过去方案和缺点

以往的越狱攻击方法依赖于人类经验来构建越狱模板，这种方法效率低下且无法保证对所有指令的有效性。此外，这些方法通常依赖于简单的规则，可能导致误报，即将良性内容错误地分类为有害内容，并在推理阶段引入额外的延迟。

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种名为Adversarial Suffixes Embedding Translation Framework (ASETF)的方法，它通过嵌入翻译技术将不可读的对抗性后缀转换为语义丰富且连贯的文本。该方法首先通过基于梯度的优化获得对抗性后缀嵌入，然后使用嵌入翻译模型将这些嵌入转换为文本。这种方法不仅提高了攻击成功率，而且显著增强了提示的文本流畅性。

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 提出了ASETF，一种将不可读的对抗性后缀转换为连贯、可读文本的框架，有助于更深入地理解LLMs生成有害内容的机制。
* 实验表明，ASETF在生成有害输出方面的成功率与现有技术相当，同时显著提高了生成提示的文本流畅性。
* ASETF能够生成可转移的对抗性后缀，成功攻击多种LLMs，包括黑盒模型如ChatGPT和Gemini。

### 5. 本文实验

实验使用了Advbench数据集和LLaMa2、Vicuna等LLMs。结果表明，ASETF在保持攻击成功率的同时，显著提高了文本流畅性，并增加了提示的语义多样性。

### 6. 实验结论

ASETF不仅在攻击成功率上与现有技术相当，而且在文本流畅性和多样性方面有所提升。这为LLM防御机制提供了更丰富的对抗性示例。

### 7. 全文结论

本文提出了一种生成语义丰富且连贯的对抗性输入的框架，通过实验验证了其在多种LLMs上的有效性。ASETF的提出有助于制定更有效的LLM防御策略，并为未来的研究提供了新的方向。

### 阅读总结

本文通过提出ASETF框架，解决了现有LLM安全防御方法的局限性。ASETF通过将对抗性后缀转换为可读文本，不仅提高了攻击的成功率，而且增强了文本的流畅性和多样性。这种方法为理解和防御LLMs提供了新的视角，并为未来的研究和实践提供了有价值的工具。然而，这种方法的计算成本较高，且在处理通用对抗性后缀时攻击成功率有所下降。未来的工作可以探索更高效的优化方法，以及如何更好地平衡对抗性后缀的语义相关性和嵌入一致性。