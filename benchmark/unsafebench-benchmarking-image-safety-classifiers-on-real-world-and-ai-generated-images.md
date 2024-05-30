# UnsafeBench: Benchmarking Image Safety Classifiers on Real-World and AI-Generated Images

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### 阅读总结报告

**1. 研究背景**

随着在线平台上不安全图像（例如，包含暴力、仇恨言论等）的传播，图像安全分类器在识别和减轻这些不安全图像的传播中扮演着重要角色。同时，随着文本到图像模型的出现以及对AI模型安全性的日益关注，开发者越来越依赖图像安全分类器来保护他们的模型。然而，当前图像安全分类器在现实世界和AI生成图像上的性能仍然是未知的。

**2. 过去方案和缺点**

现有的图像安全分类器大多在现实世界的不安全图像数据集上训练，对于AI生成的图像，它们是否能够同样有效地检测广泛的不安全内容并泛化其性能尚不清楚。此外，对于不同类型的不安全图像，现有的分类器在检测上存在不平衡性，某些类别如色情和令人震惊的图像检测效果较好，而仇恨、骚扰和自我伤害等类别的检测效果不佳。

**3. 本文方案和步骤**

为了填补这一研究空白，作者提出了`UnsafeBench`，这是一个评估图像安全分类器在现实世界和AI生成图像上的有效性和鲁棒性的基准测试框架。具体步骤包括：

* **数据集构建**：策划一个包含10K现实世界和AI生成图像的大型数据集，并根据11个不安全类别进行标注。
* **图像安全分类器收集**：收集五个流行的图像安全分类器和三个由通用视觉语言模型驱动的分类器。
* **与不安全类别对齐分类器覆盖范围**：检查这些分类器具体覆盖的不安全内容，并与不安全图像分类法对齐。
* **有效性和鲁棒性评估**：使用标注数据集评估这些分类器的有效性，并针对随机和对抗性扰动图像评估其鲁棒性。



* **CLIP的适配**：`PerspectiveVision`利用预训练模型的知识，如CLIP或视觉语言模型（VLMs），并通过标注图像的指导来适应它们。
  * **线性探测**：在CLIP顶部添加一个线性探测层，允许针对特定任务进行微调。
  * **提示学习**：通过优化提示来适应预训练模型，以用于各种下游任务。
* **VLMs的适配**：与使用线性探测和提示学习的分类器不同，VLMs是生成模型，输出更多信息而非仅仅是对数概率。
  * **监督微调**：采用监督微调来适配VLM（如LLaVA），以识别不安全图像。
  * **LoRA技术**：使用Low-Rank Adaptation (LoRA)技术，这是一种参数高效微调技术，只更新模型中的一小部分可训练参数。



**4. 本文创新点与贡献**

* 提供了一个大型的、经过精心标注的数据集，包含现实世界和AI生成的图像，覆盖11个不安全类别。
* 对现有的图像安全分类器和新型的视觉语言模型（VLMs）进行了全面的性能评估。
* 基于`UnsafeBench`的洞察，设计并实现了一个名为`PerspectiveVision`的全面图像审核工具，有效识别现实世界和AI生成的不安全图像。
* `PerspectiveVision`作为一个开源工具，为检测一般不安全图像建立了一个基线。

**5. 本文实验**

实验包括：

* 使用`UnsafeBench`数据集对分类器进行有效性评估。
* 对分类器在随机和对抗性扰动图像上的鲁棒性进行评估。
* 通过聚类技术和案例研究，识别AI生成图像的独特特征，并评估这些特征是否会中断分类器的预测。

**6. 实验结论**

* 商业VLM基分类器`GPT-4V`在识别不安全内容方面表现最佳，但由于其封闭源和商业性质，广泛用于图像安全分类任务是不切实际的。
* 存在对不同类型的不安全图像的调节不平衡。色情和令人震惊的类别更有效被检测，而仇恨、骚扰和自我伤害类别的检测效果不佳。
* 仅在现实世界图像上训练的传统分类器在应用于AI生成图像时性能下降。

**7. 全文结论**

作者通过`UnsafeBench`基准测试框架和`PerspectiveVision`工具，为图像安全分类领域提供了重要的贡献。这些工具和数据集将帮助研究社区更好地理解生成AI时代的图像安全分类格局，并促进更好的内容审核工具的构建。

#### 阅读总结

本文提出了一个针对现实世界和AI生成图像的图像安全分类器的基准测试框架`UnsafeBench`，以及一个全面的图像审核工具`PerspectiveVision`。通过对现有分类器的评估，作者揭示了它们在不同不安全类别内容检测中的不平衡性，以及在AI生成图像上的泛化性能不足。`UnsafeBench`数据集和`PerspectiveVision`工具的开源性质，为研究社区提供了宝贵的资源，以推动该领域的进一步研究和发展。