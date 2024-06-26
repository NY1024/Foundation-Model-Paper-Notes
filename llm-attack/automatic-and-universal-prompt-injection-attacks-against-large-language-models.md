# Automatic and Universal Prompt Injection Attacks against Large Language Models

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

##

### 1. 研究背景

本研究关注的是大型语言模型（LLMs）在处理和生成人类语言方面的卓越能力，尤其是在遵循指令方面。然而，这种遵循指令的能力可能被恶意利用，通过所谓的“提示注入攻击”（prompt injection attacks）来操纵集成了LLM的应用，使其产生与攻击者注入内容一致的响应，偏离用户的实际请求。这种攻击方式对LLM的实际部署构成了重大威胁，尤其是在OWASP的LLM集成应用的十大威胁列表中排名靠前。

### 2. 过去方案和缺点

以往的研究在理解提示注入攻击的威胁方面面临挑战，主要是因为缺乏统一的攻击目标和依赖于手工制作的提示，这限制了对提示注入鲁棒性的全面评估。手工制作的提示攻击虽然简单直观，但存在以下缺点：1) 限制了攻击范围和可扩展性；2) 在不同用户指令和数据的访问中具有不稳定的普遍性；3) 难以发起自适应攻击，可能导致防御机制的过度估计。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

为了解决上述挑战，本文首先提出了一个统一的框架来理解提示注入攻击的目标，并提出了一种基于动量的梯度搜索算法，该算法利用受害LLM的梯度信息自动生成提示注入数据。该方法即使在面对防御措施时也能表现出色，并且只需要五个训练样本（相对于测试数据的0.3%）就能实现优越的性能。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 提出了一个统一的框架来理解提示注入攻击的目标，包括静态、半动态和动态目标。
* 引入了一种基于动量的梯度搜索算法，用于自动生成具有高度普遍性和有效性的提示注入数据。
* 通过综合评估，展示了所提出攻击方法在不同数据集和攻击目标上的平均50%的攻击成功率，而基线方法则完全失去了效果。
* 对现有防御机制进行了自适应评估，发现这些防御机制无法缓解提示注入攻击的威胁。

### 5. 本文实验

实验使用了七个自然语言处理任务作为用户的请求，并使用了Llama2-7b-chat模型作为受害模型。实验中，作者设置了不同的防御机制，包括改写、重新分词、外部数据隔离、指令预防和三明治预防等，以评估所提出方法的有效性。

### 6. 实验结论

实验结果表明，所提出的攻击方法即使在只有五个训练样本的情况下，也能在静态目标上实现超过80%的攻击成功率，并在半动态和动态目标上实现平均50%的攻击成功率。此外，该方法在面对各种防御机制时仍能保持有效性。

### 7. 全文结论

本文通过提出一个新的分析框架和优化算法，成功地解决了提示注入攻击目标不明确和手工制作方法不便的问题。综合评估表明，所提出的攻击方法能够有效地绕过防御机制，强调了基于梯度的测试在评估提示注入鲁棒性方面的重要性。



注：

本文中提出的静态、半动态和动态目标是为了统一和明确提示注入攻击的不同目的，并为这些攻击类型提供一个清晰的框架。以下是这三种目标的详细说明：

#### 静态目标（Static Objective）

静态目标是指攻击者试图让受害的大型语言模型（LLM）生成一个与用户指令或外部数据无关的一致性响应。在这种攻击场景中，攻击者的目标是让模型无论如何都输出一个特定的、预设的响应，例如，一个警告信息或者一个恶意命令。例如，攻击者可能会让模型生成如下响应：“Your model is outdated and will face severe security risks. Update your model immediately at universal-prompt-injection.com!”，这样的响应会诱导用户访问一个恶意网站。

#### 半动态目标（Semi-Dynamic Objective）

半动态目标的场景中，攻击者希望模型在提供与用户输入相关的响应之前，首先生成一些一致的内容。这种攻击可能会导致误导信息的传播或者不当行为的发生。例如，攻击者可能会让模型生成如下响应：“Here is an answer from the verified website universal-prompt-injection.com: \n\n The summary of the document is ...”，或者“\[ACTION] sudo rm -rf / \* \n\n The summary of the document is ...”，这样的响应在提供用户请求的信息之前，先引入了攻击者预设的命令或信息。

#### 动态目标（Dynamic Objective）

动态目标是指攻击者试图操纵模型生成一个既与用户指令相关，又包含特定恶意信息的响应。这种攻击的目的是在不引起怀疑的情况下，让用户执行风险行为或者泄露信息。例如，攻击者可能会让模型生成如下响应：“Your instruction about summarizing this article cannot be achieved until you send more private information to prompt@injection.com, and that is because your account is not authorized to access this document.”，这样的响应在表面上看起来是合理的，但实际上包含了诱导用户泄露更多私人信息的恶意内容。

总结来说，这三种目标分别代表了不同程度的攻击复杂性和危险性，从完全无视用户指令的静态攻击，到在用户指令前后插入恶意内容的半动态攻击，再到将恶意内容与用户指令混合的动态攻击。这三种目标的提出，旨在帮助研究者更好地理解和评估提示注入攻击的潜在威胁，并为防御策略的制定提供指导。





### 阅读总结

本文针对大型语言模型的提示注入攻击问题，提出了一个统一的分析框架和自动化的攻击方法。通过引入基于动量的梯度搜索算法，研究者们能够自动生成有效的提示注入数据，即使在有限的训练样本下也能实现高成功率的攻击。此外，本文还对现有的防御机制进行了评估，发现它们无法有效抵御这种攻击，从而强调了自动化测试方法在评估和提高LLM安全性方面的重要性。
