# AWolf in Sheep’s Clothing: Generalized Nested Jailbreak Prompts can  Fool Large Language Models Easi

<figure><img src="../../.gitbook/assets/image (19) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 大型语言模型（LLMs），如ChatGPT和GPT-4，旨在提供有用且安全的回答。然而，这些模型可能会受到恶意提示（称为"jailbreaks"）的影响，从而绕过内置的安全措施，生成可能有害的内容。探索这些jailbreak提示有助于揭示LLMs的弱点，并进一步指导我们如何保护它们。不幸的是，现有的jailbreak方法要么需要复杂的手动设计，要么需要在其他白盒模型上进行优化，这在泛化性或效率上存在妥协。

<figure><img src="../../.gitbook/assets/image (20) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的jailbreak方法主要分为两类：手动设计的jailbreak提示（如DAN）和基于学习的jailbreak提示（如GCG）。手动设计的提示需要精心设计以确保有效性，并且由于LLMs的持续更新和迭代，这些提示很快就会失效。基于学习的提示通过优化过程来寻找能够最大化LLMs产生有害回答可能性的提示后缀，但这些后缀在语义上没有意义，容易被基于困惑度的防御机制阻止。此外，这些方法需要大量时间来找到最优后缀，并且在商业LLMs（如Claude-2）上的效率较低。

<figure><img src="../../.gitbook/assets/image (21) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了ReNeLLM，一个自动化框架，它利用LLMs自身来生成有效的jailbreak提示。ReNeLLM包括两个主要步骤：（1）提示重写，对初始提示进行一系列重写操作，不改变其核心语义，使其更容易从LLMs中引出回答；（2）场景嵌套，为了使重写的提示更隐蔽，将它们嵌入到特定任务场景中（如代码补全、文本续写等），让LLMs自己找到有效的jailbreak攻击提示。ReNeLLM在多个LLMs上展示了效率和通用性，并指导研究人员和开发者探索LLMs的更安全防御方法。

<figure><img src="../../.gitbook/assets/image (22) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文实验和性能： 通过广泛的实验，ReNeLLM在攻击成功率上显著提高，同时大幅减少了与现有基线相比的时间成本。研究还揭示了当前防御方法在保护LLMs方面的不足。此外，从提示执行优先级的角度分析了LLMs防御失败的原因，并提出了相应的防御策略。希望这项研究能够促进学术界和LLMs开发者提供更安全、更受监管的LLMs。

<figure><img src="../../.gitbook/assets/image (23) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

阅读总结报告： 本文提出了ReNeLLM，这是一个针对大型语言模型的自动化jailbreak提示生成框架。通过将jailbreak过程概括为提示重写和场景嵌套，ReNeLLM在多个代表性LLMs上实现了高效的攻击成功率。研究揭示了现有防御方法的不足，并提出了改进LLMs安全性的策略。尽管ReNeLLM在生成jailbreak提示方面取得了显著进展，但仍存在一些局限性，如评估成本、数据集的语言限制和计算需求。伦理方面，虽然ReNeLLM可能被用于对LLMs的攻击，但研究的目的是提高LLMs的安全性，以保护更广泛的应用和用户社区。
