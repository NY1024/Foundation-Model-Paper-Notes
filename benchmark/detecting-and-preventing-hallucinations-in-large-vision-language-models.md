# Detecting and Preventing Hallucinations in  Large Vision Language Models

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型视觉语言模型（LVLMs）在多模态任务中取得了显著进展，尤其是在视觉问答（VQA）方面。然而，生成与视觉内容紧密相关的详细响应仍然是一个挑战。研究发现，即使是最先进的LVLMs（如InstructBLIP）也存在高达30%的幻觉文本，包括不存在的对象、不忠实的描述和不准确的关系。为了解决这个问题，本文介绍了M-HalDetect，这是一个多模态幻觉检测数据集，用于训练和评估模型以检测和预防幻觉。

### 2. 过去方案和缺点

以往的研究主要集中在使用指令调整技术来提高LVLMs在不同视觉语言任务中的零样本性能。然而，这些方法在生成文本输出时防止幻觉方面存在显著挑战。幻觉的检测通常需要人工监督，这可能成本高昂。

### 3. 本文方案和步骤

本文提出了以下方案和步骤：

* 创建并发布了M-HalDetect数据集，专注于对详细图像描述中的幻觉进行细粒度注释。
* 使用M-HalDetect数据集通过细粒度直接偏好优化（FDPO）优化InstructBLIP，以降低幻觉率。
* 训练细粒度多模态奖励模型，并使用最佳-n拒绝采样（RS）评估其有效性。
* 对FDPO和拒绝采样进行人工评估，发现它们分别降低了InstructBLIP中41%和55%的幻觉率。

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 提出了M-HalDetect数据集，这是首个针对详细图像描述的多模态幻觉检测数据集。
* 展示了如何通过FDPO和RS方法显著降低InstructBLIP中的幻觉率。
* 证明了奖励模型在其他多模态模型（如LLaVA和mPLUG-OWL）中减少幻觉的有效性，并与人工评估的准确性得分有很强的相关性。

### 5. 本文实验

实验部分，研究者们在M-HalDetect数据集上训练了多模态奖励模型，并在InstructBLIP上进行了FDPO优化。他们还对LLaVA和mPLUG-OWL进行了拒绝采样实验，并进行了人工评估。

### 6. 实验结论

实验结果表明，通过M-HalDetect数据集训练的奖励模型能够有效地降低LVLMs生成的幻觉率。FDPO和RS方法在降低幻觉方面都显示出显著的成功，并且奖励模型在评估幻觉率方面与人工评分有很好的一致性。

### 7. 全文结论

本文介绍了M-HalDetect数据集，并展示了如何通过FDPO和RS方法减少LVLMs中的幻觉。这些方法不仅提高了InstructBLIP的性能，而且也适用于其他多模态模型，证明了M-HalDetect在捕捉和减少幻觉方面的有效性。

### 阅读总结

本文通过创建新的数据集和优化方法，显著提高了LVLMs在生成真实图像描述方面的性能。研究者们不仅提出了新的数据集，还开发了有效的模型训练和评估方法，这对于提高多模态模型在实际应用中的可靠性和准确性具有重要意义。