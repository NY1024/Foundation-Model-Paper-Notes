# Removing RLHF Protections in GPT-4 via Fine-Tuning

<figure><img src="../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

随着大型语言模型（LLMs）能力的增强，它们在双重用途方面的潜力也随之增加。为了减少有害输出，LLMs的生产商和供应商采用了带有人类反馈的强化学习（RLHF）方法。然而，LLMs供应商越来越多地提供对其最强大模型（如GPT-4）进行微调的方法。先前的研究表明，微调可以移除RLHF保护。本文研究了是否可以通过微调来移除最先进模型（如GPT-4）的RLHF保护。

### 2. 过去方案和缺点

过去的方案主要依赖于RLHF来减少LLMs产生的有害内容。然而，这些方法的一个主要缺点是，它们可能无法抵御微调攻击，这种攻击可以有效地移除RLHF保护，从而使模型再次产生有害内容。

### 3. 本文方案和步骤

本文提出了一种方法，通过微调API来生成一个不拒绝产生有害内容但保留其有用性的模型。研究者假设恶意用户可以使用一组训练数据（提示和响应对）来微调基础模型M到微调模型M'。为了生成这些训练数据，研究者使用了一个未受限制的模型来完成有害提示，并在测试时直接提示M'或使用上下文学习来降低拒绝率。

### 4. 本文创新点与贡献

本文的主要创新点在于展示了即使是最先进的LLMs（如GPT-4）也可以通过微调来移除RLHF保护，且成功率高达95%。此外，研究者还证明了即使使用较弱的模型生成训练数据，微调策略也不会降低模型在非审查输出上的有用性。

### 5. 本文实验

实验中，研究者对GPT-4和GPT-3.5 Turbo进行了攻击测试。他们收集了违反OpenAI服务条款的提示，并使用未受限制的模型生成响应。然后，他们使用这些数据对GPT-4进行了微调，并在测试集上生成响应。实验结果表明，微调后的模型在产生有害内容方面的成功率显著提高。

### 6. 实验结论

实验结果表明，微调可以有效地移除GPT-4的RLHF保护，且微调后的模型在标准基准任务上的表现与基础GPT-4相当，甚至在某些情况下超过了基础模型。

### 7. 全文结论

本文的实验结果表明，通过微调可以以非常低的成本（不到$245和340个示例）移除最先进的LLMs的RLHF保护。尽管训练数据是通用的，但微调仍然鼓励模型更加顺从。研究者能够产生潜在非常有害的指令。这些结果表明，需要进一步研究保护LLMs免受恶意用户攻击的方法。

### 阅读总结

本文通过实验验证了大型语言模型（如GPT-4）可以通过微调来移除其RLHF保护，这对于LLMs的安全性提出了新的挑战。研究者不仅展示了微调的有效性，还强调了即使在微调过程中使用较弱的模型，也不会降低最终模型的有用性。这些发现对于LLMs的开发者和使用者来说都是一个警示，表明需要开发新的保护措施来确保这些强大工具的安全使用。
