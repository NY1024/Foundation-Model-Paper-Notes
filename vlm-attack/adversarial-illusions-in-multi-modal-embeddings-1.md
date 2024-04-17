# Adversarial Illusions in Multi-Modal Embeddings

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本文研究的背景是多模态嵌入（multi-modal embeddings），这些嵌入将文本、图像、声音、视频等不同模态的数据编码到单一的嵌入空间中，以实现跨模态的语义关联，例如将狗的图像与狗叫声关联起来。然而，作者指出这种多模态嵌入可能存在安全漏洞，即所谓的“对抗性幻觉”（adversarial illusions），攻击者可以通过微小的扰动使得一个模态的输入在嵌入空间中与另一个模态中任意选择的输入靠近，从而误导基于这些嵌入的下游任务。

### 2. 过去方案和缺点

以往的研究主要集中在如何通过对抗性训练来提高模型的鲁棒性，例如通过在训练集中加入对抗性样本来“欺骗”分类器。但是，这些方法通常是模态特定的，并且没有考虑到跨模态的攻击，因此无法有效防御本文提出的对抗性幻觉攻击。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种新的攻击方法，该方法通过在多模态嵌入空间中生成对抗性幻觉来攻击下游任务。具体步骤如下：

* 首先，攻击者选择一个目标输入（例如文本）和一个源输入（例如图像或声音）。
* 然后，攻击者通过添加微小的、对人来说不可感知的扰动来修改源输入，使得其嵌入与目标输入的嵌入在嵌入空间中靠近。
* 通过这种方式，攻击者可以使得下游任务（如图像生成、文本生成、零样本分类和音频检索）基于扰动后的输入产生错误的输出。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 首次提出了跨模态、目标无关的对抗性幻觉攻击，该攻击不需要知道具体的下游任务。
* 展示了攻击的跨模态性，即攻击者可以选择任意的模态作为目标。
* 分析了攻击在不同编码器之间的迁移性，并开发了一种黑盒版本的攻击方法，用于攻击商业化的、专有的多模态嵌入，例如亚马逊的Titan嵌入。
* 调查了对抗性幻觉攻击的防御措施，并展示了攻击如何规避基于特征蒸馏（如JPEG压缩）和基于增强一致性的异常检测的防御。

### 5. 本文实验

实验部分，作者使用了ImageBind和AudioCLIP嵌入，并在多个下游任务上评估了对抗性幻觉的效果，包括图像和音频的零样本分类、音频检索、图像生成和文本生成。实验结果表明，即使是微小的扰动也能显著提高攻击成功率，并且攻击可以成功迁移到不同的嵌入空间。

### 6. 实验结论

实验结果证实了对抗性幻觉攻击在多个多模态嵌入和下游任务上的有效性。攻击能够在不同的威胁模型下成功执行，包括白盒、迁移、基于查询的攻击，以及混合攻击模型。

### 7. 全文结论

本文证明了多模态嵌入对于对抗性幻觉攻击是高度脆弱的，并且这种攻击能够跨模态和任务误导下游应用。此外，作者还讨论了潜在的对策和逃避攻击，表明当前的防御措施难以完全防止这种攻击。

### 阅读总结

本文提出了一种新的攻击方法，即对抗性幻觉，该方法能够针对多模态嵌入进行有效的攻击，并且不需要知道具体的下游任务。作者通过实验验证了攻击的有效性，并且展示了攻击的跨模态性和迁移性。此外，本文还探讨了对抗性幻觉攻击的防御措施，发现现有的防御手段难以完全防止这种攻击。这项工作不仅揭示了多模态嵌入的潜在安全风险，也为未来的防御研究提供了新的方向。