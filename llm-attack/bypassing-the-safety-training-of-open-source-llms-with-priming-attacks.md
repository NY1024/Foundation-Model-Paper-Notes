# BYPASSING THE SAFETY TRAINING OF OPEN-SOURCE LLMS WITH PRIMING ATTACKS

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## 研究背景

随着大型语言模型（LLMs）在用户面向型应用中的广泛使用，确保这些模型不被用于恶意目的变得尤为重要。为此，LLMs通常会经过人类对齐的安全训练，例如使用RLHF（Reinforcement Learning from Human Feedback）等技术。然而，尽管有这些努力，仍然存在绕过对齐以产生有害输出的可能性。

## 过去方案和缺点

以往的研究主要集中在通过计算昂贵的方法来攻击对齐的LLMs，如通过精心选择的例子进行微调。这些方法虽然有效，但在开源环境中执行起来可能过于昂贵，并且可能比必要的成本更高。

## 本文方案和步骤

本文提出了一种称为“priming attacks”的攻击方法，该方法利用LLMs的自回归性质，通过在输入中引入部分响应来实现有害请求。具体步骤包括：

1. 使用非安全训练的辅助LLM（helper LLM）通过几个例子（few-shot）来生成针对目标有害行为的priming攻击。
2. 通过将初始响应与手动制作的文本相结合，创建few-shot示例，这些文本以不完整的句子结尾，可能会合理地开始实际请求的内容。
3. 将生成的部分响应附加到输入中，以此引导LLM遵循有害提示。

## 本文创新点与贡献

1. 构建了一个高效的流水线，用于自动评估针对开源LLMs的priming攻击。
2. 展示了与Zou et al. (2023)提出的基线相比，使用稍微依赖于提示的内容进行priming可以提高攻击成功率高达3.3倍。
3. 研究强调了对手可以轻易地诱导开源LLMs遵循任意有害请求，为开源LLMs的未来发展增加了新的视角。

## 本文实验

实验使用预训练的Llama-2（7B）模型作为辅助LLM进行few-shot提示，使用Harmful Behaviors数据集的35个提示来创建few-shot示例，并使用剩余的20个提示作为验证数据。测试集包括485个Harmful Behaviors提示，攻击目标为安全训练的Llama-2和Vicuna聊天模型。

## 实验结论

实验结果表明，priming攻击在不同的模型系列（Llama-2、Vicuna）和大小（7B、13B）上均优于基线。例如，在Llama-2 (7B)上，priming攻击相比于“Just Sure”攻击在Llama Guard下的攻击成功率提高了3.3倍。增加模型大小可以提高对priming攻击的安全性估计。

## 全文结论

本文研究了针对最新安全训练LLMs的priming攻击的有效性，强调了在越来越实际的假设下当前LLM安全措施的脆弱性。作者认为这为开源LLMs的未来提出了重要的关注点，并希望本文的工作能够促进对更安全的开源方法的进一步研究。

## 阅读总结报告

本论文探讨了开源大型语言模型（LLMs）在面对简单、无需优化的priming攻击时的脆弱性。这些攻击易于执行，并能有效绕过安全训练的对齐。通过构建自动化评估流水线和展示priming攻击的效果，本文为开源LLMs的安全性研究提供了新的视角，并指出了现有安全措施的不足。实验结果表明，即使是在模型大小增加的情况下，priming攻击仍然能够显著提高攻击成功率。这些发现对于开源LLMs的未来发展具有重要意义，并可能激发新的研究，以开发更安全的开源LLMs方法。