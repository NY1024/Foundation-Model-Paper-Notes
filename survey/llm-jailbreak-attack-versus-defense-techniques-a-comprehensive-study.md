# LLM Jailbreak Attack versus Defense Techniques - A Comprehensive Study

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本研究聚焦于大型语言模型（LLMs）的安全问题，特别是所谓的“越狱”攻击，即通过精心设计的提示（prompts）绕过模型的安全措施，生成有害内容。LLMs在社会中的作用日益重要，但它们的普及也带来了安全风险。研究人员通过安全训练技术来使模型输出与社会价值观保持一致，以减少恶意内容的生成。然而，“越狱”现象仍然是一个重大挑战。

### 2. 过去方案和缺点

以往的研究已经提出了多种针对越狱攻击的防御方法，例如随机省略输入中的一些标记（tokens）来检测恶意尝试，或者使用辅助模型来帮助主要模型识别危险信息。然而，这些方法在实际应用中存在局限性，例如处理时间较长、可扩展性问题，以及在处理复杂自然语言输入时的误分类问题。

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

研究者进行了一项全面的实证研究，评估了针对LLMs的越狱攻击和防御技术的有效性。研究涉及三种不同的语言模型：Vicuna、LLama和GPT3.5 Turbo，并应用了九种攻击技术和七种防御技术。研究步骤包括基线选择、基准构建、结果标记、评估和讨论。

### 4. 本文创新点与贡献

* 提供了对越狱攻击和防御技术的系统评估，这是首次对各种开源/闭源LLMs的有效性进行系统评估。
* 发现了之前未知的洞察，这些洞察对未来的攻击和防御策略具有重要潜力。
* 开发并公开发布了第一个基准测试，包括攻击和防御技术的全面集合，以促进该领域的进一步研究。

### 5. 本文实验

实验在两个NVIDIA RTX 6000 Ada GPU上进行，测试参数与相关文献中确定的最佳参数一致。实验构建了一个基准数据集，包含60个恶意查询，以评估攻击和防御技术的有效性。

### 6. 实验结论

实验结果表明，模板方法在越狱攻击中表现出色，而基于梯度的生成方法在“白盒”场景下通常表现不佳。此外，特殊标记的使用显著影响了攻击成功的可能性。在防御技术方面，Bergeron方法被识别为迄今为止最有效的防御策略。

### 7. 全文结论

本研究提供了LLM安全领域的首个全面评估，并为该领域的发展做出了贡献。研究揭示了现有白盒攻击与通用技术相比性能较差，以及特殊标记对攻击成功率的显著影响。研究强调了需要关注LLMs的安全方面，并为未来的研究提供了数据集和测试框架。



注：\
在这篇论文中，研究者们通过全面的实证研究，揭示了几个关键的洞察，这些洞察对未来的攻击和防御策略具有重要潜力：

1. **模板方法的有效性**：研究发现，基于模板的攻击方法在越狱攻击中表现出色，尤其是当这些模板精心设计时。这表明，攻击者可以通过巧妙构造的提示来绕过模型的安全机制，从而成功诱导模型生成有害内容。
2. **特殊标记的影响**：研究指出，特殊标记（如'\[/INST]'）的使用显著影响了越狱攻击的成功率。在某些情况下，包含或排除这些特殊标记可以显著改变模型对输入的响应，从而影响攻击的有效性。
3. **白盒攻击与黑盒攻击的比较**：研究发现，依赖于模型内部机制（如损失度量）的白盒攻击方法通常不如不需要模型内部信息的通用（黑盒）攻击方法有效。这表明，即使在没有模型内部知识的情况下，攻击者也能够通过通用策略成功越狱。
4. **模型对有害内容的抵抗力**：研究还发现，所有测试的模型在对抗与有害内容和非法活动相关的查询时表现出更强的抵抗力。这可能意味着模型在这些领域的安全训练更为有效。
5. **防御策略的不足**：尽管存在多种防御策略，但研究发现，除了Bergeron方法外，其他防御技术在阻止越狱攻击方面表现不佳。这表明当前的防御机制需要进一步改进，以更有效地识别和阻止恶意输入。

这些洞察为未来的研究提供了方向，特别是在如何设计更有效的攻击策略以及如何开发更强大的防御机制方面。研究者们建议未来的工作应该探索特殊标记对模型行为的影响，并开发出能够在不同上下文中可靠区分恶意和良性输入的更先进的评估框架。





### 阅读总结

本研究对LLMs的安全性进行了深入分析，特别是在越狱攻击和防御策略方面。通过实证研究，研究者评估了多种攻击和防御技术，并发现了一些关键的发现，如模板方法的有效性和特殊标记对攻击成功率的影响。此外，研究还提出了对现有防御机制的改进需求，并为未来的研究提供了宝贵的资源。这项工作不仅对学术界有重要意义，也对实际应用中的LLMs安全具有指导价值。