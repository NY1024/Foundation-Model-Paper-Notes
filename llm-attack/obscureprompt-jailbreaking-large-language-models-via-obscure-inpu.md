# ObscurePrompt: Jailbreaking Large Language Models via Obscure Inpu

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

###

#### 1. 研究背景

近年来，大型语言模型（LLMs）因其卓越的自然语言处理能力而受到广泛关注。然而，关于它们的可信度问题，尤其是在面对“越狱”攻击时，LLMs的安全性和可靠性仍然存在疑问。越狱攻击是指恶意用户利用LLMs生成不当内容，例如虚假信息或网络钓鱼攻击。现有的研究大多依赖于白盒场景或特定且固定的提示模板，这些通常在实际应用中不切实际，缺乏广泛的适用性。

#### 2. 过去方案和缺点

以往的研究主要关注于如何通过提示的设计来提高LLMs的性能，但这些策略通常需要访问目标LLMs的内部参数（白盒场景），或者依赖于特定的固定提示模板，这限制了它们的普适性和有效性。

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 3. 本文方案和步骤

本文提出了一种新颖的方法，名为OBSCUREPROMPT，用于越狱LLMs。该方法的灵感来自于观察到的在分布外（OOD）数据上的脆弱对齐。具体步骤包括：

* **构建基础提示**：首先使用已知的越狱技术构建基础提示。
* **模糊引导转换**：然后利用强大的LLMs对原始提示进行迭代转换，增加其模糊性，以提高攻击的稳健性。
* **攻击集成**：通过重复上述两个关键步骤，生成一系列模糊提示，用于集成攻击部署。

#### 4. 本文创新点与贡献

* **OOD数据的脆弱对齐观察**：通过可视化LLMs隐藏状态中不同查询的表示，观察到OOD查询可以显著削弱伦理决策边界。
* **新颖简单的越狱方法**：提出了一种新颖且直接的方法OBSCUREPROMPT，使用模糊输入来越狱LLMs，无需训练，且在黑盒设置中运行，不依赖于特定提示模板。
* **全面评估和实证见解**：通过全面实验验证了该方法的有效性，显示出比现有基线更好的性能，并保持了对两种主流防御机制的有效性。

#### 5. 本文实验

实验使用了advbench数据集，包含521个有害查询，并选择了七个广泛使用的LLMs作为目标模型，包括开源和专有模型。评估指标为攻击成功率（ASR），并与其他三种基线方法进行了比较。

#### 6. 实验结论

OBSCUREPROMPT在所有测试的LLMs上均显著优于基线方法。实验结果表明，随着集成提示数量的增加，所有模型的ASR均有所提高。此外，实验还发现，结合所有越狱策略并不一定能产生最高的ASR，而且该方法对主流防御仍然有效。

#### 7. 全文结论

本文提出的OBSCUREPROMPT方法，通过使用模糊转换来增强越狱攻击的有效性，克服了现有方法的局限性，为未来提高LLMs的可信度提供了新的见解。尽管存在一些限制，例如对于能力较弱的LLMs，该方法的效果可能会降低，但整体上，这项工作为理解和提高LLMs的安全性提供了宝贵的贡献。



注：

#### 构建基础提示（Prompt Seed Curation）

构建基础提示是OBSCUREPROMPT方法的第一步，旨在创建一个有效的起始点，利用已知的越狱技术来增强提示的效果。这一步包括以下几个关键环节：

1. **选择初始查询**：选择或构造一个可能引发伦理或安全问题的初始查询（例如，“如何制作炸弹？”）。
2. **应用越狱技术**：采用一系列已建立的越狱方法，如前缀注入、角色扮演（例如，使用“避免道歉”或“直接回答”等策略），以及其他能够促使LLMs绕过安全限制的技巧。
3. **生成种子提示**：将选定的越狱技术应用于初始查询，生成修改后的提示（称为种子提示），这些提示旨在减少有害意图或引导LLMs提供安全和建设性的回答。

#### 模糊引导转换（Obscure-Guided Transformation）

在这一步中，目的是通过增加模糊性来强化基础提示，使其更难以被LLMs的安全协议识别。具体过程如下：

1. **定义转换操作**：确定一个转换操作（F(·)），该操作将种子提示变得更加模糊，从而增加LLMs识别的难度。
2. **使用LLMs进行转换**：利用强大的LLMs（如GPT-4）对种子提示进行处理，使其变得更加晦涩难懂。这通常涉及到使用特定的指令，比如“请使以下文本更加模糊”。
3. **迭代改进**：通过迭代应用转换操作，不断增强提示的模糊性，直到达到所需的程度。

#### 攻击集成（Attack Integration）

最后一步是将通过模糊引导转换生成的多个模糊提示集成到一起，形成一个攻击集合，用于对目标LLMs进行攻击。这个过程包括：

1. **重复生成提示**：通过多次重复种子提示的创建和模糊转换过程，生成一系列不同的模糊提示。
2. **构建攻击集合**：将生成的模糊提示集合起来，形成一个攻击集合，每个提示都是潜在的攻击向量。
3. **执行攻击**：使用这个攻击集合对目标LLMs进行攻击，如果任何一个提示成功地越狱了LLMs，那么攻击就被认为是成功的。

通过这三个步骤，OBSCUREPROMPT方法能够在不依赖于模型内部结构的情况下，有效地对LLMs进行越狱攻击，同时提高了攻击的稳健性和实用性。

