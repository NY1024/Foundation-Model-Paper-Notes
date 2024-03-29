# LLM-Attack

## 研究背景

大型语言模型（LLMs）如ChatGPT、Claude和Bard在部署后广泛使用，它们展现出先进的通用能力，但同时也存在被恶意行为者滥用的风险，例如用于制造虚假信息或犯罪。为了降低这些风险，模型创建者实施了安全机制来限制模型行为，使其只在一个“安全”的能力子集中操作。然而，尽管有这些安全措施，模型仍然容易受到对抗性输入的影响，这在ChatGPT的早期版本中通过“越狱”攻击得到了证明。

## 过去方案和缺点

过去的安全训练方法通常依赖于在训练时对模型进行微调，以使其与预定义的价值观保持一致，并通过后处理对输入和输出进行标记和过滤。这些努力通常通过红队测试来补充，以主动识别和训练对抗弱点。然而，这些方法在对抗性攻击面前仍然存在漏洞，尤其是在对抗性训练和安全训练目标之间存在冲突时。

## 本文方案和步骤

本文提出了两种安全训练失败模式：竞争目标和不匹配的泛化。竞争目标发生在模型的能力与安全目标冲突时，而不匹配的泛化发生在安全训练未能泛化到模型能力存在的领域。作者使用这些失败模式来指导越狱攻击的设计，并评估了包括OpenAI的GPT-4和Anthropic的Claude v1.3在内的最新模型，以对抗现有和新设计的攻击。

## 本文创新点与贡献

本文的创新点在于系统地分析了安全训练的LLMs对越狱攻击的脆弱性，并提出了两种新的失败模式。这些模式不仅提供了对越狱现象概念上的理解，而且为设计新的攻击提供了指导。此外，本文的实验结果强调了安全机制应该与底层模型一样复杂，并且反对仅仅通过扩展模型规模来解决这些安全失败模式的观点。

## 本文实验

实验部分对最新的安全训练模型进行了评估，包括OpenAI的GPT-4和Anthropic的Claude v1.3。实验使用了两个数据集：一个是从模型的红队测试中挑选出的有害请求的策划数据集，另一个是更大的合成数据集。尽管这些模型经过了广泛的安全训练，但实验发现它们仍然容易受到攻击。

## 实验结论

实验结果表明，尽管进行了广泛的安全训练，但基于竞争目标和不匹配泛化原则的新攻击在所有提示上都成功地攻击了模型。这些攻击在策划的红队测试提示上的表现优于现有的临时越狱攻击。

## 全文结论

本文的工作表明，现有的安全训练方法可能无法完全防止LLMs受到越狱攻击。为了实现更安全、更可靠的模型部署，需要进一步的研究和开发，以确保安全机制能够与模型的能力相匹配。此外，本文的发现强调了在对抗性环境中对模型安全性进行评估的重要性。

## 阅读总结报告

本文深入探讨了大型语言模型在安全训练方面的局限性，并提出了两种新的失败模式来解释越狱攻击的成功。通过实验验证了这些模式，并展示了即使在最新的安全训练模型中，这些攻击仍然有效。这项工作强调了在设计和部署LLMs时需要考虑的安全性问题，并为未来的研究提供了新的视角。
