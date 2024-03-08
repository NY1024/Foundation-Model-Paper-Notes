# Mitigating Hallucination in Large Multi-Modal  Models via Robust Instruction Tuning

<figure><img src="../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

当前的大型多模态模型（LMMs）在处理与图像相关的人类指令时，容易生成与图像内容不一致的幻觉描述。这些模型虽然在多模态任务上取得了显著进展，但仍然存在幻觉问题，这可能导致有害的后果，尤其是在用户过度依赖这些模型时。

### 2. 过去方案和缺点

以往的研究主要集中在使用BERT等模型作为语言解码器的视觉和语言预训练模型上。然而，这些模型在处理视觉指令时，往往无法准确遵循人类指令，尤其是在面对不存在的对象、属性或关系时。此外，现有的LMMs训练数据缺乏多样性，导致模型在处理负样本（即与图像内容不一致的指令）时表现不佳。

<figure><img src="../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一个新的大型视觉指令调整数据集LRV-Instruction，该数据集包含由GPT4生成的40万个视觉指令，覆盖16种视觉和语言任务。与以往研究不同，LRV-Instruction不仅包含正面指令样本，还包括用于更健壮视觉指令调整的负面指令样本。此外，本文提出了GPT4辅助视觉指令评估（GAVIE），这是一种稳定的方法，用于评估LMMs的输出，无需人工标注的地面真实答案。

<figure><img src="../.gitbook/assets/image (28) (1).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 构建了LRV-Instruction数据集，这是一个大型且多样化的基准，包含16种视觉和语言任务的正面和负面指令。
* 提出了GAVIE评估方法，这是一种新颖的方法，可以在不需要地面真实答案的情况下评估视觉指令调整。
* 通过在LRV-Instruction上微调MiniGPT4和mPLUG-Owl，展示了如何减少LMMs的幻觉问题，并在多个公共数据集上实现了与最先进方法相比的性能提升。

### 5. 本文实验

作者在多个公共数据集上对五种最新的LMMs进行了零样本性能评估，并在LRV-Instruction数据集上进行了详细分析。实验结果表明，现有的LMMs在面对负面指令时存在显著的幻觉问题，尤其是在存在对象操作和知识操作指令时。

### 6. 实验结论

实验结果验证了LRV-Instruction数据集在健壮视觉指令调整方面的有效性。通过在该数据集上微调的LMMs在多个任务上表现出更少的幻觉问题，并在公共基准测试中取得了更好的性能。

### 7. 全文结论

本文通过构建LRV-Instruction数据集和提出GAVIE评估方法，为解决LMMs的幻觉问题提供了一种有效的解决方案。这些贡献不仅提高了LMMs在视觉指令调整任务上的性能，也为未来在多模态学习领域的研究提供了新的方向。

### 阅读总结

本文针对LMMs在处理视觉指令时的幻觉问题，提出了一个新的数据集LRV-Instruction和评估方法GAVIE。通过在LRV-Instruction上微调LMMs，作者成功减少了幻觉问题，并在多个公共数据集上取得了优异的性能。这项工作不仅为LMMs的幻觉问题提供了解决方案，也为多模态学习领域的未来研究奠定了基础。
