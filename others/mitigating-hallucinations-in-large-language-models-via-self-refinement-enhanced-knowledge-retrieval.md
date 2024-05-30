# Mitigating Hallucinations in Large Language Models via Self-Refinement-Enhanced Knowledge Retrieval

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

#### 研究背景

大型语言模型（LLMs）在各种领域展现出了卓越的能力，但它们在生成与现实世界事实不符的回答时容易出现“幻觉”现象，这在医疗等关键领域尤其成问题。为了解决这一问题，从知识图谱（KGs）检索相关信息被认为是一种有希望的方法。

#### 过去方案和缺点

现有的利用知识图谱增强的方法往往资源密集，需要对每个事实进行多轮检索和验证，这阻碍了它们在现实世界场景中的应用。此外，直接将知识注入LLMs的生成过程中，由于LLMs的有限推理能力，仍然会导致一定程度的幻觉。

#### 本文方案和步骤

本文提出了一种自我优化增强的知识图谱检索（Re-KGR）方法，通过在生成后阶段注入外部知识，以减少幻觉。Re-KGR方法包括以下步骤：

1. **实体检测**：利用不同令牌和模型层之间的下一个令牌预测概率分布的属性来识别可能产生幻觉的令牌。
2. **三元组提取**：从生成的文本中提取所有事实陈述作为知识三元组，但只保留包含已识别高风险词实体的三元组。
3. **知识检索**：从领域特定的知识图谱中检索相应的三元组，并确定精炼集中的三元组是否与知识图谱中的三元组一致。
4. **知识验证与修正**：根据验证结果更新原始生成的响应。

#### 本文创新点与贡献

* 提出了Re-KGR方法，在生成后阶段通过最小化基于知识图谱的检索努力来减轻LLMs回答中的幻觉。
* 在医疗问答任务的特定场景中实现了Re-KGR方法，并构建了一个基于现有医学信息语料库的广泛知识图谱。
* 实验评估证明了所提出方法的有效性，在提高响应准确性的同时显著减少了时间开销。

#### 本文实验

实验使用了MedQuAD数据集，这是一个包含来自美国国立卫生研究院网站的现实世界医疗问答对的集合。实验中，作者选择了LLaMA-7b及其对比解码版本DoLa作为基础模型，以评估Re-KGR方法在减轻幻觉方面的有效性。

#### 实验结论

实验结果表明，Re-KGR方法在生成医疗问答任务中的事实准确回答方面超越了基线模型，通过GPT-4评估的真实性得分显著提高。特别是与DoLa模型结合使用时，Re-KGR方法达到了最高的真实性表现得分0.610，比原始LLaMA提高了15.75%，比DoLa提高了3.21%。

#### 全文结论

Re-KGR方法通过结合结构化的知识图谱和最小化检索努力，有效地减轻了LLMs回答中的幻觉。实验结果强调了Re-KGR可以提高各种基础模型的LLMs的事实能力。未来的工作将探索该方法在不同场景下的泛化能力，并考虑在生成阶段集成检索过程以进一步减少总体生成时间。

#### 阅读总结报告

这篇论文针对大型语言模型在生成回答时出现的幻觉问题，提出了一种新的解决方案Re-KGR。通过在生成后阶段结合知识图谱，该方法有效地减少了检索工作量，并提高了回答的真实性。Re-KGR通过实体检测、三元组提取、知识检索、知识验证与修正等步骤，优化了检索系统，减少了幻觉现象。实验部分使用了MedQuAD数据集，并通过GPT-4模型对回答的真实性进行了评估。结果表明，Re-KGR在提高医疗问答任务的准确性和效率方面表现出色。这项工作为LLMs在关键领域的应用提供了一种新的途径，并为未来的研究提供了有价值的参考。