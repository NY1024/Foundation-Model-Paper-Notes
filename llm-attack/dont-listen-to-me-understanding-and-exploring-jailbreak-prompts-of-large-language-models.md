# Don’t Listen To Me: Understanding and Exploring Jailbreak Prompts of Large Language Models

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

##

### 1. 研究背景

随着大型语言模型（LLMs）的快速发展和广泛应用，它们在多个行业中的作用日益重要。然而，这种技术的潜在滥用也引起了人们的关注。为了应对这种风险，服务提供商采取了多种防护措施。然而，这些安全限制往往被“越狱”（jailbreak）提示所绕过，越狱提示是一种有效机制，用于规避安全限制并诱导生成原本被禁止的有害内容。

### 2. 过去方案和缺点

过去的研究主要集中在使用越狱提示作为更复杂攻击的基础，例如诱导LLMs泄露训练数据中的个人信息。然而，对于越狱现象本身的内部工作机制缺乏深入的研究。此外，现有的工作没有系统地收集和分类越狱提示，也没有对人类如何创建越狱攻击的过程进行深入探讨。

### 3. 本文方案和步骤

本文通过以下步骤进行研究：

* 收集和分析在线来源中的448个越狱提示，并从中派生出161个违反OpenAI政策的恶意查询。
* 使用主题分析对这些提示进行分类，归纳出五种类别和十种独特的越狱模式。
* 构建评估指标，基于人类注释评估越狱提示的有效性。
* 进行用户研究，涉及92名不同背景的参与者，以揭示手动创建越狱提示的过程。
* 开发一个使用AI作为助手的系统，自动化越狱提示的生成过程。

### 4. 本文创新点与贡献

* 提供了一个全面的越狱提示数据集，包括448个野外越狱提示和161个恶意查询，并从中归纳出五种类别和十种独特的越狱模式。
* 评估了越狱提示的有效性，并识别出两种最有效的策略。
* 通过用户研究，揭示了即使在没有LLMs专业知识的情况下，用户也能成功生成越狱提示的过程。
* 开发了一个交互式框架，可以自动优化越狱提示的生成，展示了初步的可行性。

### 5. 本文实验

实验包括对收集到的越狱提示进行系统化分类，评估不同越狱策略的有效性，并进行用户研究来理解人类如何开发和执行语义上有意义的越狱攻击。此外，还开发了一个原型系统来自动化越狱提示的生成过程。

### 6. 实验结论

* “虚拟AI模拟”和“混合策略”类别的越狱提示在所有恶意查询中表现最佳。
* GPT-4相对于其他模型在抵抗越狱尝试方面更为健壮。
* 用户研究显示，即使对于没有经验的参与者，也能成功构建越狱提示。
* 自动化越狱提示生成系统的初步实验表明，该系统能够有效地转化之前失败的提示。

### 7. 全文结论

本文通过系统化分析和用户研究，深入理解了越狱提示的威胁，并展示了人类和AI合作创建越狱提示的过程。此外，本文提出的自动化越狱提示生成框架为未来的研究方向提供了新的可能性。研究结果强调了为了提高LLMs的安全性，需要进一步研究和开发更有效的防御措施。



注1：

本文提供了对越狱现象的新见解，主要体现在以下几个方面：

1. **系统化分析越狱提示**：研究者通过收集和分析来自在线论坛和社区的448个越狱提示，将它们系统化为五种类别和十种独特的模式。这种分类不仅为理解越狱提示的结构和功能提供了清晰的框架，也为未来的防御策略提供了目标和方向。
2. **评估越狱提示的有效性**：通过构建基于人类注释的评估指标，研究者能够量化越狱提示的成功程度。这种方法不仅为衡量越狱尝试的危险性提供了新的工具，也为比较不同越狱策略的效果提供了依据。
3. **用户研究揭示创造过程**：通过涉及92名不同背景的参与者的用户研究，本文展示了即使在没有专业知识的情况下，用户也能够成功创建越狱提示。这一发现强调了越狱现象的普遍性和潜在的社会风险。
4. **自动化越狱提示生成**：研究者开发了一个交互式框架，该框架使用AI助手迭代地应用提示变异并测试每一步对越狱效果的影响。这种自动化方法不仅展示了越狱过程的可行性，也为未来开发更先进的越狱防御技术提供了新的思路。
5. **深入探讨越狱背后的动机和策略**：本文不仅分析了越狱提示的形式和结构，还探讨了攻击者背后的动机和目标。这种深入的理解有助于揭示越狱现象的复杂性，并为设计更全面的安全措施提供了基础。
6. **识别普遍有效的越狱提示**：研究发现了所谓的“通用越狱提示”，这些提示能够在不同的模型中触发越狱。这一点揭示了LLMs在设计和训练过程中可能存在的共同漏洞。
7. **强调人类和AI的协作潜力**：用户研究和自动化系统的发展表明，人类和AI的合作可以显著提高越狱提示的生成效率。这种协作不仅能够提高攻击的复杂性，也为防御措施的设计提供了新的挑战。

通过这些新见解，本文为理解和防御针对大型语言模型的越狱攻击提供了宝贵的知识和工具。这些成果不仅对学术界有重要意义，也对政策制定者和服务提供商在制定有效的安全策略和措施时提供了指导。



注2：

在本文中，研究者们发现了所谓的“通用越狱提示”（universal jailbreak prompts），这些提示能够在不同的大型语言模型（LLMs）中触发越狱行为，即绕过模型的安全限制以生成原本被禁止的输出内容。这一发现具有重要意义，因为它揭示了不同LLMs可能存在的共同漏洞，这些漏洞可以被攻击者利用来实施越狱攻击。

#### 通用越狱提示的特点

1. **跨模型有效性**：通用越狱提示不是针对某一特定模型设计的，而是能够在多个不同的LLMs上成功诱导越狱行为。这意味着攻击者可以使用相同的越狱提示对多个目标模型进行攻击，增加了攻击的效率和潜在影响范围。
2. **高成功率**：这些提示在实验中显示出较高的成功率，能够有效地绕过LLMs的安全机制。研究者通过评估指标（如Expected Maximum Harmfulness和Jailbreak Success Rate）来量化这些提示的有效性，并发现它们在多个恶意查询类别中都能获得较高的评分。
3. **复杂性**：通用越狱提示往往包含复杂的叙述和场景设定，这些叙述和场景能够掩盖其真实的恶意意图，使得LLMs更容易接受并响应这些提示。这种复杂性可能包括角色扮演、虚构情景、或者对LLMs的特定行为模拟等元素。

#### 通用越狱提示的发现过程

研究者们通过对收集到的越狱提示进行系统化分析，识别出了几种具有高成功率的越狱策略。在这些策略中，他们发现了一些提示能够在不同的LLMs上重复触发越狱行为，这些就是所谓的“通用越狱提示”。通过对这些提示进行消融研究（ablation study），研究者们进一步理解了使这些提示有效的关键因素，例如对LLMs角色的设定、对详细响应的要求等。

#### 通用越狱提示的意义

* **安全性研究**：这一发现强调了LLMs在设计和实施安全措施时需要考虑的共同弱点，为未来的安全研究提供了新的研究方向。
* **防御策略**：了解通用越狱提示的存在，可以帮助开发者和安全专家设计更有效的防御措施，以防止越狱攻击的发生。
* **政策制定**：政策制定者可以利用这些信息来制定更严格的监管政策，以减少LLMs被滥用的风险。

总之，通用越狱提示的发现揭示了LLMs安全防护的一个关键挑战，即如何防范那些能够跨多个模型有效执行的攻击手段。这对于LLMs的安全性研究和实践具有重要的启示作用，需要行业内外的专家共同努力来应对这一挑战。





### 阅读总结

本文深入探讨了大型语言模型面临的越狱威胁，并通过实证研究揭示了越狱提示的策略和有效性。研究者通过用户研究和自动化系统开发，提供了对越狱现象的新见解，并为未来的安全防护策略提供了重要的指导。这项工作不仅增进了我们对越狱攻击的理解，也为开发更强大的LLMs安全措施提供了宝贵的资源和方法。
