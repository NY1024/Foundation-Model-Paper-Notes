# Exploring Backdoor Attacks against Large Language Model-based Decision Making

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### 研究背景

近年来，大型语言模型（LLMs）在经过特定应用的微调后，在决策任务中展现出了巨大的潜力，这归功于它们从大量数据中学习到的常识和推理能力。然而，这些系统在微调阶段暴露出显著的安全和风险问题，尤其是可能遭受后门攻击。

### 过去方案和缺点

以往的研究集中在通过精心设计的提示（prompts）使LLMs绕过安全协议（如jailbreaking攻击），或者通过上下文学习（ICL）后门攻击，其中嵌入在示例中的触发器误导了LLMs。然而，对于在决策系统中微调LLMs时执行后门攻击的研究还相对不足。现有系统在微调和检索增强生成（RAG）方面的整合为后门攻击提供了新的攻击面，但同时也增加了为这些系统制定有效后门攻击的复杂性。

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### 本文方案和步骤

本文提出了首个全面框架BALD（Backdoor Attacks against LLM-enabled Decision-making systems），系统地探索了在微调阶段通过各种渠道引入后门攻击的方法。具体包括三种攻击机制和相应的后门优化方法：

1. **Word Injection（单词注入）**：在查询提示中直接嵌入触发词。
2. **Scenario Manipulation（场景操作）**：在物理环境中操纵后门场景，触发攻击。
3. **Knowledge Injection（知识注入）**：对基于RAG的LLM系统进行后门攻击，将触发词策略性地注入到被污染的知识库中，同时确保信息在事实上保持准确，以实现隐蔽性。

### 本文创新点与贡献

* 提出了BALD框架，这是首次全面研究针对LLM决策系统微调阶段的后门攻击。
* 设计了三种不同的后门攻击机制，针对LLM决策系统的不同组件。
* 通过实验验证了所提方法和威胁模型能够从不同入口点成功攻击LLM基础的决策系统。
* 探讨了后门优化方法的有效性，并探索了开发防御机制的潜在方向。

### 本文实验

实验使用了三种流行的LLMs（GPT-3.5、LLaMA2、PaLM2）和两个数据集（HighwayEnv、nuScenes）进行。实验结果表明，所提出的后门触发器和机制有效且隐蔽。

### 实验结论

* 微调对于LLMs在决策任务中的表现是必要的，未经微调的原始LLMs表现有限。
* 现有的ICL后门攻击对经过良性微调的LLMs效果不佳，而针对微调阶段的BALD攻击表现出色。
* BALD攻击在不同模型和数据集上都能实现高攻击成功率（ASR）。
* 后门攻击的隐蔽性通过不同的机制得到了保证，尤其是在BALD-scene攻击中。

### 全文结论

BALD框架的研究揭示了LLM在决策任务中的固有脆弱性，并强调了微调阶段安全性的重要性。研究成果希望能够提高对LLM决策系统安全性的认识，并激发更强大的设计和系统级防御的发展。

###
