# Make Them Spill the Beans! Coercive Knowledge Extraction from (Production) LLMs

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



#### 1. 研究背景

大型语言模型（LLMs）在多种应用中被广泛使用，因此确保它们的道德标准与人类价值观一致至关重要。然而，最近的“越狱”方法表明，通过精心构造的提示，这种一致性可能会受到破坏。在本研究中，作者揭示了当不良行为者能够访问模型的输出逻辑值（在开源LLMs和许多商业LLM APIs中常见的功能，例如某些GPT模型）时，LLM一致性可能受到的新威胁。即使LLM拒绝有害请求，有害的响应往往隐藏在输出逻辑值的深处。通过在自回归生成过程中的关键输出位置强制选择排名较低的输出标记，可以迫使模型透露这些隐藏的响应。

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

#### 2. 过去方案和缺点

过去的方案主要依赖于“越狱”技术，通过精心设计的提示来诱导LLM回答不道德或有害的问题。这些方法通常需要为不同的问题设计不同的提示，并且一旦这些提示被公开，LLM提供者通常会迅速更新他们的模型以修补这些漏洞。然而，这些方法在效率和有效性上存在限制，有时会产生质量低下的内容，例如不相关或不清晰的答案。

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

#### 3. 本文方案和步骤

本文提出了一种称为模型审讯（model interrogation）的新方法，该方法不需要精心设计的提示，而是直接通过强制LLM在输出逻辑值中选择排名较低的标记来回答问题。具体步骤包括：

* 使用LLM基于分类器实时检测模型是否对有害问题作出负面响应。
* 确定响应文本中表示LLM态度转变的关键句子。
* 丢弃该句子之后的所有后续句子。
* 利用输出逻辑值强制模型使用大量替代输出标记重新生成响应。
* 使用分类器选择与有害问题最匹配的响应，并从选定的句子恢复完整响应生成。



<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

#### 4. 本文创新点与贡献

* 识别了一种新的对LLM一致性的威胁，与越狱技术正交。
* 设计了一种复杂的LLM审讯方法，包括识别态度转变句子和基于逻辑值寻找替代输出标记。
* 实现了一个名为LINT的原型，用于审讯7个开源LLMs和3个商业LLMs，其有效性达到92%，显著优于现有技术。

#### 5. 本文实验

作者在7个开源LLMs和3个商业LLM APIs上使用50个有害问题对LINT进行了评估。实验结果表明，LINT在一次审讯时的攻击成功率为92%，并且在五次审讯时达到了98%。此外，LINT在提取代码任务专门设计模型中的有害知识方面也表现出色。

#### 6. 实验结论

实验结果表明，即使是经过精心设计的LLMs，也可以通过审讯方法被迫使生成有害内容。此外，LINT在效率和有效性上都优于现有的越狱技术，并且可以与这些技术结合使用，进一步提高攻击性能。

#### 7. 全文结论

本文披露了一种新的对LLM一致性的威胁，这种威胁与越狱技术不同，并且在效率和有效性上都优于现有技术。这些发现表明，即使是专门设计用于编码任务的模型，也可能通过审讯方法被迫使透露有害知识。





注：

#### 本文方法详细说明

**3.1 模型审讯（Model Interrogation）概念**

本文提出的方法称为模型审讯（Model Interrogation），简称LINT。这种方法的核心思想是，即使LLM在表面上拒绝回答有害问题，有害或恶意的响应仍然隐含在模型的输出逻辑值（output logits）中。通过在自回归生成过程中的关键位置强制选择排名较低的输出标记，可以迫使模型透露这些隐藏的响应。

**3.2 审讯步骤**

1. **初始拒绝响应**：当LLM接收到有害问题时，它可能会立即拒绝回答，这个拒绝响应成为第一个干预点（intervention point）。
2. **生成候选句子**：LINT要求LLM基于其输出逻辑值生成一组候选句子。这涉及到生成下一个位置的最可能的顶级标记，并以每个标记为起点生成新句子。
3. **选择最合规的句子**：通过一个句子选择器，LINT识别出最符合有害问题的候选句子。这需要一个算法来有效地优先选择与有害问题最相关的候选句子。
4. **集成有害句子**：选定的有害句子随后被集成到输入中，引导模型生成完整响应。
5. **识别干预点**：LINT识别响应中从高质量有害内容过渡到无害内容的确切句子。这可能需要在生成的整个内容的不同位置进行划分，并检查不同部分对有害问题的合规性。
6. **重复过程**：如果LLM在生成过程中开始生成有害内容，然后意识到问题并停止，LINT将丢弃从干预点开始的所有后续句子，并重复上述过程，直到生成完整的有害响应。

**3.3 关键挑战**

* **下一句选择（Next Sentence Selection）**：当通过强制选择标记时，需要根据它们与有害问题的对应程度对下一句候选句子进行排名。
* **干预点识别（Intervention Point Identification）**：需要在生成的内容中精确地找到高质量的有害内容过渡到无害内容的确切句子。

**3.4 解决方案**

* **下一句选择的解决方案**：使用文本蕴含分析（textual entailment analysis），这是一种语言学技术，用于确定一段文本是否支持一个假设。通过将候选句子和有害问题转换为文本和假设，利用蕴含分析模型来评估它们之间的关系。
* **干预点识别的解决方案**：采用系统搜索算法，对整个响应进行不同位置的划分，并检查不同部分对有害问题的合规性。利用LLM对文本的毒性分类能力，找到从前一部分有毒内容过渡到后一部分无害内容的最早分割点。

**3.5 迭代过程**

LINT的过程是迭代的，它在每次迭代中识别干预点，并强制模型在这些点选择最符合有害问题的下一句候选句子。这个过程在生成的整个响应完全符合有害问题之前一直重复进行。

通过这种方法，LINT能够有效地从LLMs中提取出隐藏的有害知识，即使这些模型经过了专门的对齐训练以防止生成有害或不道德的内容。

