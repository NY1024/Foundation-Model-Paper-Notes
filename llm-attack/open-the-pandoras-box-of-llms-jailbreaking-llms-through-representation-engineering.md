# Open the Pandora’s Box of LLMs: Jailbreaking LLMs through Representation Engineering

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型语言模型（LLMs）在多种任务中表现出色，但它们也可能生成有害、暴力或其他有毒的响应。为了探索LLMs的安全边界，研究人员开发了“越狱”（jailbreaking）技术，这些技术通过诱导模型生成对恶意查询的有毒响应。现有的越狱方法主要依赖于提示工程（prompt engineering），但这些方法存在攻击成功率低和时间开销大的问题。

### 2. 过去方案和缺点

以往的越狱方法主要基于提示工程，包括手动和自动生成越狱提示。这些方法不仅难以构建，而且越狱效果不佳，缺乏可扩展性。自动化提示虽然消除了创造性需求，但也存在低攻击成功率和额外的计算和时间成本。

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种新的越狱方法，称为通过表示工程越狱LLMs（JRE）。该方法只需要少量的查询对来提取“安全模式”，这些模式可以用来绕过目标模型的防御。JRE攻击方法通过在模型的每一层中削弱安全模式来成功执行越狱。此外，本文还介绍了一种基于JRE原则的新型防御框架。





在这篇论文中，作者提出了一种名为“通过表示工程越狱LLMs”（JRE）的新方法，旨在克服现有基于提示工程（ProE）的越狱方法的局限性。以下是JRE方法的详细说明：

#### 核心概念

* **表示工程（Representation Engineering, RepE）**：这是一种分析深度神经网络（DNNs）中神经元激活模式所形成表示空间的交互的方法。RepE的目标是理解模型内部的表示空间，以便更好地理解和控制模型的行为。
* **安全模式（Safety Patterns）**：作者假设LLMs在处理恶意查询时会触发模型表示空间中的“安全模式”。这些安全模式可以被视为一种潜在的特征表示，它们在模型的每层中存在，并且可以被用来绕过模型的安全机制。

#### 方法步骤

1. **挖掘安全模式**：通过构建一个包含恶意和良性查询对的数据集（JailEval），作者从模型的输出中提取激活模式的差异。这些差异被用来识别与安全机制相关的特征。
2. **特征索引定位**：通过计算激活模式差异的方差，作者筛选出在差异中变化最小的特征，这些特征被认为是安全模式的一部分。
3. **价值估计**：对于每个查询对，作者计算选定特征的平均值，以构建每层的安全模式。
4. **越狱攻击**：在模型推理过程中，通过削弱（减去）安全模式，使得模型能够生成对恶意查询的有害响应。

#### 创新点

* **高效性**：JRE方法不需要额外的时间开销，且在越狱性能上优于现有的ProE方法。
* **可解释性**：通过可视化安全模式，JRE提供了对模型内部表示空间的直观理解。
* **防御框架**：基于JRE原则，作者还提出了一种防御框架，通过在模型的每一层增强安全模式来防止越狱攻击。

####





### 4. 本文创新点与贡献

* 提出了一种基于表示工程的越狱攻击策略，该策略不需要额外的时间开销，且达到了前所未有的越狱性能。
* 基于JRE原则，引入了一种新型的越狱防御框架，通过在模型推理阶段增强安全模式，而不是削弱它们，证明了其有效性。
* 使用表示工程来探究LLMs越狱背后的机制，验证了一个可解释的假设，从而推进了对模型安全问题的深入研究。

### 5. 本文实验

实验在七个经过安全训练的LLMs上进行，参数大小从60亿到340亿不等。实验使用了JailEval、AdvBench Harmful Behaviors和HarmfulQ等数据集来评估JRE方法的有效性。实验结果表明，JRE攻击方法在ASR-1和ASR-2上都取得了很高的成功率。

### 6. 实验结论

JRE攻击方法在越狱性能上显著优于以往的基于提示工程的方法。同时，JRE防御框架在防止恶意请求方面也显示出了显著的有效性。

### 7. 全文结论

本文通过引入基于表示工程的JRE框架，不仅提出了一种高效的越狱攻击方法，还提供了一种有效的防御策略。这些研究不仅为越狱攻击和防御提供了新的视角，也为理解LLMs的安全问题提供了新的见解。

### 阅读总结

本文提出了一种新的越狱方法JRE，通过表示工程来提取和利用LLMs的安全模式，实现了高效的越狱攻击。同时，作者还提出了一种防御框架，通过增强安全模式来防止越狱。这些工作不仅提高了我们对LLMs安全问题的理解，也为未来的研究和实践提供了新的方向。然而，作者也指出了JRE方法的局限性，特别是在用户对LLM有完全访问权限时，如何有效防御JRE攻击仍然是一个挑战。