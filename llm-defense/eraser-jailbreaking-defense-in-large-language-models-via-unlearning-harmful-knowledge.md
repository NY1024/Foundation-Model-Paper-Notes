# Eraser: Jailbreaking Defense in Large Language Models via Unlearning Harmful Knowledge

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



### 1. 研究背景

随着大型语言模型（LLMs）的广泛应用，人们越来越关注其生成内容的安全性和潜在危害。LLMs在训练过程中接触了大量数据，但这些数据并未经过严格的审查，可能导致不良内容的产生。为了引导LLMs生成有益且无害的回应，研究者提出了多种对齐方法，如基于人类反馈的强化学习（RLHF）和监督式微调（SFT），以使LLMs能够拒绝有害查询。然而，这些方法并未根本解决LLMs内部存在的有害知识问题，这使得LLMs在面对越狱攻击（jailbreaking attacks）时仍然存在潜在风险。

### 2. 过去方案和缺点

以往的越狱防御方法主要分为两类：有害行为过滤和持续训练。有害行为过滤方法通过审查模型输入和输出来检测和阻止越狱行为，但这些方法通常不会改变模型权重，且会增加模型推理的成本。持续训练方法通过额外的训练来增强模型拒绝有害输入的能力或提高模型对有害内容的辨识能力。尽管这些方法取得了一定的成果，但它们忽略了有害知识仍然存在于模型中的事实，这使得在更先进的攻击方法出现时，有害知识可能会再次浮现，导致一场无休止的猫鼠游戏。

### 3. 本文方案和步骤

本文提出了一种名为Eraser的新型防御方法，旨在通过“忘却”有害知识来减少LLMs越狱成功的可能。Eraser的主要目标包括：忘却有害知识、保留一般知识、维持对有害查询的安全对齐。具体步骤如下：

* **忘却有害知识**：通过梯度上升技术在模拟越狱模式下对有害回答进行处理，减少模型对特定有害查询的回答概率。
* **保留一般知识**：通过保持对实体的理解能力来维持一般知识，使用GPT-3.5提取有害回答中的实体，并生成相关的理解问题。
* **维持安全对齐**：通过保持拒绝有害查询的能力来维持安全对齐，直接查询原始LLM以获取拒绝数据，形成数据集，并鼓励模型在训练前后具有相似的拒绝能力。

### 4. 本文创新点与贡献

* **提出新方法**：Eraser是首个通过忘却有害知识来防御越狱攻击的方法，它能够在不牺牲一般性能的情况下显著降低越狱成功率。
* **实验结果**：与现有方法相比，Eraser在防御能力上表现出色，同时保持了一般能力，展示了在无害性和实用性之间更好的权衡。
* **随机数据的启示**：实验发现，即使是使用随机数据进行梯度上升也能带来一定的防御效果，这为未来的越狱防御研究提供了新的思路。

### 5. 本文实验

实验部分评估了Eraser在不同攻击方法下的防御效果，包括AIM、AutoDAN和GCG等先进越狱方法。实验使用了AdvBench和AdvExtent两个数据集，并采用了有害分数和攻击成功率（ASR）作为评估指标。此外，还对Eraser的一般能力进行了评估，使用了包括Arc\_challenge、Boolq等在内的多个LLM评估基准。

### 6. 实验结论

实验结果表明，Eraser在所有设置中均显著降低了ASR和有害分数，证明了其强大的防御能力。同时，Eraser在一般能力评估基准上的表现与基线模型相当，表明Eraser能够有效降低越狱风险而不损害一般能力。

### 7. 全文结论

本文提出的Eraser方法通过整合忘却有害知识、维持一般性能和增强安全对齐三个目标，显著降低了越狱风险，且不损害一般能力。与现有方法相比，Eraser能更好地平衡无害性和实用性。此外，实验还表明，即使是忘却随机数据也能带来一定的防御效果，这鼓励未来的研究更多关注维持一般能力。



注1：

在论文中，确定哪些知识属于需要忘却的有害知识是通过以下几个步骤实现的：

1. **定义有害查询集（Xq）**：首先，研究者需要定义一组有害查询（harmful queries），这些查询通常是那些会导致LLMs生成有害内容的问题，例如涉及非法活动、暴力或其他不道德行为的问题。
2. **使用未审查模型（Uncensored Models）**：为了获取有害回答，研究者利用公开可用的未审查模型（uncensored models）对这些有害查询进行查询。这些未审查模型由于没有经过严格的安全对齐训练，可能会生成有害内容。
3. **收集有害回答**：通过未审查模型对有害查询的回答，研究者可以收集一组有害回答（Yf）。这些回答代表了模型中需要忘却的有害知识。
4. **构建有害数据集（Df）**：将有害查询和对应的有害回答配对，构建成有害数据集Df = {(x, y) | x ∈ Xf, y ∈ Yf}，其中Xf是问题集合，Yf是回答集合。
5. **模拟越狱攻击场景**：在训练过程中，为了模拟越狱攻击，研究者会对输入的查询x添加随机生成的前缀和后缀，形成T(x)，以此来训练模型不提供有害回答y。

通过这些步骤，研究者可以识别并收集那些需要从LLMs中忘却的有害知识，进而使用Eraser方法进行针对性的训练，以减少模型生成有害内容的可能性。需要注意的是，这个过程可能需要不断地更新和维护，因为新的有害查询和知识可能会随着时间和社会环境的变化而出现。



注2：

在论文中提到的Eraser方法中，为了训练大型语言模型（LLMs）在面对越狱攻击时不提供有害回答，研究者采用了一种特殊的训练策略，即在训练过程中模拟越狱攻击的场景。下面是该过程的详细说明：

1. **定义越狱攻击**：越狱攻击是指通过精心设计的提示（adversarial prompts），绕过LLMs的安全防护机制，诱使模型生成有害内容的行为。这些提示可能包括具有误导性或伪装性的前缀和后缀。
2. **生成随机前缀和后缀**：为了模拟这种攻击，研究者设计了一个函数T(·)，它能够为每个查询x随机生成前缀和后缀。这些前缀和后缀是随机的文本序列，它们可以模拟攻击者可能使用的任何类型的伪装或误导性信息。
3. **构建模拟查询**：将原始的有害查询x与通过T(·)函数生成的随机前缀和后缀结合起来，形成一个新的模拟查询T(x)。这个新的查询旨在模拟攻击者在实际场景中可能使用的越狱攻击手段。
4. **训练模型忘却有害回答**：使用模拟查询T(x)和对应的有害回答y，研究者通过梯度上升技术来训练模型。具体来说，他们将有害回答y作为目标输出，并尝试最大化模型输出y的概率。然而，由于模型被训练为拒绝生成有害内容，这个过程实际上是在尝试减少模型生成有害回答y的概率。
5. **优化训练目标**：为了实现这一目标，研究者定义了一个损失函数Lf，它惩罚模型在给定T(x)时生成有害回答y的能力。通过最小化这个损失函数，模型学习在面对类似越狱攻击的查询时，不提供有害回答。

通过这种方式，Eraser方法不仅训练模型忘却特定的有害知识，而且还提高了模型对未知越狱攻击的鲁棒性。这是因为模型不仅仅学会了拒绝特定的有害查询，还学会了在面对各种伪装和误导性信息时保持安全对齐。这种训练策略有助于提高模型在实际应用中的安全性，减少有害内容的生成。





### 阅读总结

本文针对大型语言模型在面对越狱攻击时的安全性问题，提出了一种新的防御方法Eraser。该方法通过忘却有害知识、保留一般知识和维持安全对齐来降低越狱成功率，实验结果显示其在保持一般能力的同时具有出色的防御效果。Eraser的提出为LLMs的安全防护提供了新的视角和解决方案，对于未来在该领域的研究具有重要的启发和指导意义。
