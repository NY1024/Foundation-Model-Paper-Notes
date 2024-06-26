# BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents

<figure><img src="../.gitbook/assets/image (11) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



### 1. 研究背景

随着大型语言模型（LLMs）的兴起，基于LLM的智能代理（agents）被开发出来，以提供定制化服务和执行特定任务。这些代理通过预训练语言模型获得丰富的语言知识，能够理解和生成自然语言。然而，本文指出，这些LLM代理容易受到后门攻击，攻击者可以通过在训练数据中嵌入后门，在测试时通过触发器操纵代理执行恶意操作。

### 2. 过去方案和缺点

尽管在自然语言处理中对后门攻击已有广泛研究，但据作者所知，这是首次针对能够使用外部工具的LLM代理进行后门攻击研究。与传统的语言模型相比，LLM代理更强大，但在攻击下也更危险。现有的后门攻击通常通过数据投毒实现，将触发器与目标模型行为相关联，使其在模型训练期间被学习。

<figure><img src="../.gitbook/assets/image (12) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了名为BadAgent的后门攻击方法，包括主动攻击和被动攻击两种方式。这些攻击通过在代理任务的微调过程中污染数据来嵌入后门。主动攻击在攻击者向LLM代理输入隐藏的触发器时被激活；而被动攻击在LLM代理检测到特定环境条件时工作，无需攻击者的直接干预。

### 4. 本文创新点与贡献

* 提出了针对新兴LLM代理的后门攻击方法BadAgent，这是首次针对LLM代理的后门攻击研究。
* 展示了两种攻击方法：主动攻击和被动攻击，这些方法通过在微调数据中嵌入后门来实现。
* 证明了该攻击方法即使在代理经过可信数据微调后仍然极其健壮。

### 5. 本文实验

实验采用了三种最先进的开源LLM代理模型，并在三个任务上进行了测试：操作系统（OS）、网页导航（Mind2Web）和网上购物（WebShop）。实验结果显示，所有基础LLM在所有任务中成功被注入后门，攻击成功率超过85%。

### 6. 实验结论

实验结果表明，使用干净的数据进行微调作为防御方法，对于BadAgent攻击并没有显著效果。即使在知道哪些层受到攻击的情况下，攻击的成功率仍然保持在90%以上。

### 7. 全文结论

本文系统研究了LLM代理在后门攻击下的脆弱性，并提出了BadAgent攻击方法。研究表明，LLM代理可以通过在微调过程中污染数据来被注入恶意触发器。作者希望这项工作能够促进对LLM安全性的考虑，并鼓励研究更安全、更可靠的LLM代理。

###
