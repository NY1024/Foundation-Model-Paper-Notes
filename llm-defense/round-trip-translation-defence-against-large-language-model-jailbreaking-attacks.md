# Round Trip Translation Defence against Large Language Model Jailbreaking Attacks

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型语言模型（LLMs）如ChatGPT4、Vicuna、Llama2和Palm2等在处理各种查询时表现出强大的知识储备和能力。然而，这些模型容易受到社会工程攻击，这些攻击通过精心设计的对抗性提示（adversarial prompts）诱导LLMs产生有害或意外行为。这些提示对人类可理解，但LLMs难以识别其潜在的有害意图。现有的防御措施，如困惑度过滤器（perplexity filter）和输入扰动（input perturbation），在对抗这类攻击时效果有限。

### 2. 过去方案和缺点

过去的防御措施，如困惑度过滤器，无法有效过滤包含纯英语且没有乱码后缀的社会工程攻击提示。输入扰动方法，如SmoothLLM，虽然在一定程度上减少了攻击成功率，但计算成本高，且无法改变对抗性提示的根本含义，最多只能减轻不到50%的攻击。

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种名为Round Trip Translation（RTT）的方法，专门设计用于防御针对LLMs的社会工程攻击。RTT通过将原始对抗性提示连续翻译成几种非印欧语系语言，然后再翻译回英语，以揭示和概括输入提示中的概念。这种方法简单、轻量级，且可转移到不同的LLMs上。

### 4. 本文创新点与贡献

RTT方法的创新之处在于它能够通过翻译和回翻译过程，将特定的术语泛化，使LLMs更容易检测到对抗性提示中潜在的有害行为。此外，RTT在防御Prompt Automatic Iterative Refinement（PAIR）攻击方面取得了超过70%的攻击缓解率，这是目前已知最有效的防御措施。

### 5. 本文实验

实验部分首先验证了RTT在泛化输入查询术语方面的能力。然后，研究了RTT在不同LLMs和对抗性攻击中的性能。实验结果表明，RTT在不同LLMs上表现一致，平均攻击缓解率达到70%。RTT在防御MathAttack方面也取得了近40%的攻击缓解率。

### 6. 实验结论

实验结果表明，RTT方法在防御社会工程攻击方面非常有效，特别是在对抗PAIR攻击时。RTT在不同LLMs上的转移性良好，且对良性输入的影响很小。

### 7. 全文结论

本文提出的RTT方法为防御社会工程攻击提供了一种新的策略。通过泛化对抗性提示，RTT帮助揭示了潜在的有害行为。尽管RTT在防御攻击方面取得了显著成效，但仍有进一步研究的空间，例如测试其他翻译算法，以及在非英语对抗性提示中验证RTT的性能。

### 阅读总结

本文针对LLMs容易受到社会工程攻击的问题，提出了一种新的防御策略——Round Trip Translation（RTT）。RTT通过多语言翻译和回翻译的过程，有效地泛化了对抗性提示，提高了LLMs识别和拒绝有害输入的能力。实验结果表明，RTT在多种LLMs上都表现出了良好的攻击缓解效果，尤其是在对抗PAIR攻击时。此外，RTT对良性输入的影响较小，显示出其在实际应用中的潜力。尽管如此，RTT的防御效果可能受到翻译算法配置的影响，且在处理更高级别的问题输入时可能需要进一步的验证。未来的研究可以探索将RTT与其他防御技术结合，以提高LLMs的整体安全性。