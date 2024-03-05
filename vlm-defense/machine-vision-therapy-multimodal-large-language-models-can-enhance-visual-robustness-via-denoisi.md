# Machine Vision Therapy: Multimodal Large Language  Models Can Enhance Visual Robustness  via Denoisi

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本研究聚焦于提升计算机视觉模型在面对分布外（Out-of-Distribution, OOD）场景时的鲁棒性。尽管像CLIP这样的视觉模型在泛化性能上表现出色，但在没有微调的情况下，它们在OOD场景下的零样本鲁棒性仍然有限。以往的研究通常依赖于额外的人工标注数据来进行微调，这在大规模视觉应用中是不理想的。因此，本研究提出了利用多模态大型语言模型（MLLMs）的强大视觉理解能力来改进视觉模型的方法。

### 2. 过去方案和缺点

以往的方法依赖于人工标注数据来进行模型的微调，这不仅耗时耗力，而且在大规模应用中不切实际。此外，MLLMs在处理视觉任务时，由于任务的不兼容性，往往难以生成与真实类别名称匹配的正确答案，导致性能不佳。

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种名为“机器视觉疗法”（Machine Vision Therapy, MVT）的新方法，通过去噪上下文学习（Denoising In-Context Learning, DICL）策略来对齐视觉任务和MLLMs。具体步骤包括：

* 估计一个转换矩阵，捕捉一个类别被误认为另一个类别的概率。
* 使用包含正确和错误示例的指令来帮助MLLMs检测和纠正视觉模型的错误预测。
* 利用纠正后的监督信息指导下游OOD问题的微调过程。

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 设计了一种新的机器视觉疗法范式，无需额外的标签信息即可增强计算机视觉模型。
* 提出了一种成功的DICL策略，使MLLMs能够与视觉任务对齐。
* 在多个知名数据集上进行了全面的定量和定性研究，证明了所提出方法的有效性。

### 5. 本文实验

实验在ImageNet、WILDS、DomainBed等多个OOD数据集上进行。实验结果表明，MVT方法在多个视觉模型上都能显著提升性能，尤其是在OOD情况下。

### 6. 实验结论

实验结果证实了MVT方法在提升视觉模型的OOD鲁棒性方面的有效性。通过与MLLMs的结合，可以在不需要人工标注的情况下，显著提高视觉模型在OOD任务上的表现。

### 7. 全文结论

本文提出的MVT方法为利用MLLMs提升视觉模型的OOD鲁棒性提供了一种有效的解决方案。通过DICL策略，可以有效地对齐MLLMs与视觉任务，并通过微调进一步提高模型性能。这一方法为视觉识别领域的多个传统领域，如弱监督学习、OOD检测和细粒度图像分类，提供了新的研究思路。

### 阅读总结

本文提出了一种新颖的方法，通过机器视觉疗法（MVT）来增强计算机视觉模型在OOD场景下的鲁棒性。通过利用MLLMs的知识和DICL策略，MVT能够在不依赖额外人工标注的情况下，有效地纠正视觉模型的错误预测，并指导模型的微调过程。实验结果表明，MVT方法在多个数据集上都能显著提升视觉模型的性能，尤其是在OOD情况下。这一研究为视觉识别领域提供了新的视角，并为未来相关研究奠定了基础。
