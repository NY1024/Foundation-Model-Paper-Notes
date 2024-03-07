# CodeChameleon: Personalized Encryption Framework for Jailbreaking Large Language Models

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

## 研究背景

大型语言模型（LLMs）在提供高级通用能力和确保响应安全方面表现出色，但它们仍然容易受到对抗性攻击，尤其是通过“越狱”（jailbreaking）来绕过模型的安全和道德协议。越狱攻击通过精心设计的提示（prompts）来诱导模型执行它们本应拒绝的任务，这对LLMs的安全性构成了重大挑战。

## 过去方案和缺点

现有的越狱方法主要分为三类：人类设计的越狱、基于优化的越狱和基于长尾分布编码的越狱。人类设计的越狱依赖于人类的创造力来构建提示，但这些方法可能随着在线模型的更新而失效，并且需要大量的人工努力。基于优化的越狱方法通过调整模型输入来生成合规响应，但这些方法可能需要大量的计算资源。长尾分布编码通过将原始查询转换为Base64、密码或低资源语言等格式来绕过安全机制，但这些方法可能在模型对非主流格式的对齐不足时才有效。

## 本文方案和步骤

本文提出了CodeChameleon，一种基于个性化加密策略的新型越狱框架。为了绕过意图安全识别阶段，CodeChameleon将任务重新构想为代码补全任务，允许用户使用个性化的加密函数加密查询。为了确保LLM能够准确执行原始查询，我们在指令中嵌入了相应的解密函数。在推理过程中，解密函数帮助LLM理解加密内容。

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

## 本文创新点与贡献

* 提出了一种针对对齐LLMs的安全机制假设：意图安全识别和响应生成。
* 提出了CodeChameleon框架，基于个性化加密和解密的LLMs越狱新方法。
* 在7个LLMs上的评估显示，CodeChameleon一致地绕过了所有现有的安全机制，实现了最先进的平均攻击成功率（ASR）。

## 本文实验

实验主要在三个基准数据集上进行：AdvBench、MaliciousInstruct和ShadowAlignment。实验涵盖了7个LLMs，包括开源模型Llama2chat系列和Vicuna-v1.5系列，以及专有模型GPT-3.5-1106和GPT-4-1106。使用攻击成功率（ASR）作为主要评估指标。

## 实验结论

CodeChameleon在所有模型上实现了平均77.5%的ASR，显著超过了其他越狱方法。特别是在GPT-4-1106上，实现了86.6%的ASR。这表明CodeChameleon能够有效地绕过LLMs的安全机制。

## 全文结论

本文通过分析当前的越狱方法，提出了一种新的LLMs安全机制假设，并基于此引入了CodeChameleon框架。广泛的测试显示，CodeChameleon成功地规避了LLMs的意图识别，并且在七个主要的LLMs上实现了平均攻击成功率的显著提高。

## 阅读总结报告

本研究针对大型语言模型（LLMs）的安全性问题，提出了一种新的越狱框架CodeChameleon。该框架通过个性化加密和解密策略，成功地绕过了LLMs的安全机制，实现了高攻击成功率。这一成果不仅展示了LLMs在安全性方面的潜在脆弱性，也为未来的安全研究提供了新的视角和方法。然而，研究的局限性在于评估的LLMs种类有限，未来的工作需要在更广泛的模型上验证CodeChameleon的有效性和普适性。
