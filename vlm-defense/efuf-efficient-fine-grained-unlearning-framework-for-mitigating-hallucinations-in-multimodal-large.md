# EFUF: Efficient Fine-grained Unlearning Framework for Mitigating  Hallucinations in Multimodal Large

##

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)  (18).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

多模态大型语言模型（MLLMs）在人工智能领域取得了显著进展，尤其在人机交互、数据处理和自动化内容生成方面。然而，这些模型在生成描述时可能会出现所谓的“幻觉”现象，即生成与图像不相符的对象。这种现象可能导致信息误导，影响用户对下游应用的信任。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)  (17).png" alt=""><figcaption></figcaption></figure>

### 2. 过去方案和缺点

现有的方法通过手动标注包含和不包含幻觉的成对响应，然后使用各种对齐算法来提高图像和文本之间的对齐能力。这些方法不仅在微调阶段需要大量的计算资源，而且需要昂贵的人工标注来构建对齐算法所需的成对数据。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)   (6).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种高效的细粒度反学习框架（EFUF），无需成对数据即可消除幻觉。EFUF的核心思想是通过反学习策略，利用CLIP模型评估文本和图像的一致性，然后根据CLIP分数筛选出正面和负面样本。在微调阶段，EFUF通过三种不同的损失函数（正损失、负损失和句子损失）来调整模型，以减少幻觉同时保持生成质量。

### 4. 本文创新点与贡献

* 提出了一种新的视角，利用反学习来减轻MLLMs中的多模态幻觉。
* 提出了EFUF框架，能够以成本效益和可靠的方式来获取正面和负面示例。
* EFUF具有良好的兼容性，可以轻松扩展到现有的MLLMs，实验验证了方法的有效性。

### 5. 本文实验

实验使用了MSCOCO数据集，并在多个MLLMs（如MiniGPT4、mPLUG-owl、LLaVA和ShareGPT4V）上进行了评估。实验结果表明，EFUF在降低幻觉率的同时，保持了生成质量。

### 6. 实验结论

EFUF在不同MLLMs上表现出一致的幻觉率降低效果，并且在保持模型整体性能的同时，提高了生成质量。这表明EFUF是一个有效的幻觉缓解方法。

### 7. 全文结论

本文通过利用文本-图像相似性来识别多模态幻觉，并提出了一种新的反学习策略来减轻MLLM中的幻觉。EFUF通过筛选不同样本并设计三种不同的损失函数来执行反学习，实验结果证明了其有效性。

### 阅读总结

本文针对多模态大型语言模型中的幻觉问题，提出了一种创新的反学习框架EFUF。该框架通过利用CLIP模型评估文本和图像的一致性，有效地减少了幻觉的发生，同时保持了模型的生成质量。EFUF的提出不仅解决了现有方法的计算和人工标注成本问题，而且提高了模型在多模态任务中的可靠性和准确性。实验结果表明，EFUF在多个基线模型上都取得了显著的性能提升，证明了其在多模态幻觉缓解方面的潜力。
