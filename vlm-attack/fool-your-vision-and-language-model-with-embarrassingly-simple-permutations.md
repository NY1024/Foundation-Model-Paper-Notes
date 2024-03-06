# FOOL YOUR (VISION AND) LANGUAGE MODEL WITH  EMBARRASSINGLY SIMPLE PERMUTATIONS

## 阅读总结报告

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

### 1. 研究背景

本文研究的背景是大型语言模型（LLMs）和视觉-语言模型（VLLMs）在实际应用中的快速部署，特别是在多项选择题回答（MCQA）任务上。这些模型在遵循指令、上下文学习和多模态输入输出方面表现出色。然而，尽管在传统基准测试上表现优异，这些模型在面对答案选项的简单置换时却显示出意外的脆弱性。

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

### 2. 过去方案和缺点

以往的研究主要集中在提高模型在MCQA任务上的准确性，而忽略了模型对于答案选项顺序变化的敏感性。这种敏感性可能导致模型在实际应用中的不可靠性，因为它们可能无法在答案选项顺序变化时保持一致的预测。

### 3. 本文方案和步骤

本文提出了一种简单的对抗性攻击方法，即通过随机改变答案选项的位置来测试模型的鲁棒性。研究者们对多种流行的LLMs和VLLMs进行了实验，观察在答案选项置换后模型的准确率变化。



在本文中，作者们通过一系列实验展示了大型语言模型（LLMs）和视觉-语言模型（VLLMs）在面对多项选择题回答（MCQA）任务时，对于答案选项顺序的简单置换操作表现出显著的脆弱性。这种脆弱性的具体表现和影响如下：

#### 1. 答案选项置换的影响

* **显著降低准确率**：实验结果表明，即使是对答案选项进行简单的随机置换，也会导致模型的准确率大幅下降。在某些情况下，模型的性能甚至低于随机猜测的水平。
* **跨模型的普遍性**：这种脆弱性不仅存在于单一模型中，而是普遍存在于多种流行的LLMs和VLLMs中，包括不同大小和架构的模型。
* **对抗性攻击的有效性**：作者们展示了一种对抗性攻击方法，通过改变答案选项的顺序来欺骗模型，这种方法在多个数据集和模型上都显示出了有效性。

#### 2. 脆弱性的深层原因

* **非位置偏见**：作者们排除了位置偏见（即模型对特定位置的偏好）作为主要原因，因为即使在减少干扰选项数量后，模型的性能仍然对置换敏感。
* **选项间关系的依赖**：模型似乎依赖于答案选项之间的相对关系，包括正确答案和干扰项。简单的置换操作可能破坏了这种关系，导致模型无法正确识别正确答案。

#### 3. 实验设置和结果

* **实验设置**：作者们在多个MCQA数据集上进行了实验，包括MMLU、ARC-c、BoolQ、SocialiQA、MedMCQA等，涵盖了不同的领域和任务类型。
* **结果**：实验结果一致地显示，模型在面对答案选项置换时性能下降。例如，Llama2-13B模型在MMLU数据集上的准确率从52.22%下降到18.33%，降幅达到了33.89%。

#### 4. 对抗性攻击的深入分析

* **置换分布分析**：作者们进一步分析了模型在不同置换下的表现，发现许多问题存在多个能够导致错误的置换选项。
* **定性结果**：通过具体的MCQA例子，作者们展示了模型在原始答案顺序和经过置换的答案顺序下的不同预测，进一步证实了模型的脆弱性。

#### 5. 鲁棒性改进的尝试

* **多数投票和上下文校准**：作者们尝试了多数投票和上下文校准等后处理策略来缓解置换攻击的影响，但这些策略并未能完全恢复模型的性能。

#### 6. 对实际应用的影响

* **实际应用的警示**：这些发现对于依赖MCQA任务的模型的实际应用提出了警告，因为它们可能在面对轻微的输入变化时表现不稳定。
* **鲁棒性训练的需求**：研究者们需要开发新的训练策略和架构，以提高模型对此类对抗性攻击的内在鲁棒性。

总结来说，本文的研究揭示了LLMs和VLLMs在MCQA任务中对答案选项顺序变化的敏感性，这种脆弱性可能会在实际应用中导致模型性能的不稳定，从而影响模型的可靠性和信任度。这一发现强调了在模型部署前进行更全面鲁棒性评估的重要性。





### 4. 本文创新点与贡献

本文的主要创新点在于揭示了LLMs和VLLMs在MCQA任务中的一个特定脆弱性：对答案选项置换的敏感性。这一发现挑战了人们对这些模型鲁棒性的传统认识，并强调了在实际应用中对这些模型的可靠性进行更严格评估的必要性。

### 5. 本文实验

实验涉及了多种模型，包括LLaMA、Vicuna、WizardLM、InternLM、Falcon、MPT等，以及VLLMs如InstructBLIP、OpenFlamingo、Otter等。实验使用了多个MCQA数据集，包括MMLU、ARC-c、BoolQ、SocialiQA、MedMCQA等。实验结果显示，即使是简单的答案选项置换也会导致模型准确率显著下降，有时甚至低于随机猜测水平。

### 6. 实验结论

实验结果表明，无论是LLMs还是VLLMs，都普遍存在对答案选项置换的敏感性。这种脆弱性在不同模型大小和最新模型中都存在，且在减少干扰选项数量后仍然存在。

### 7. 全文结论

本文的研究结果揭示了大型语言模型和视觉-语言模型在MCQA任务中的一个关键但常被忽视的脆弱性。尽管这些模型在传统基准测试上表现出色，但它们在面对简单操作（如选项置换）时显示出令人担忧的脆弱性。这要求研究者和实践者在部署这些模型时更加谨慎，并寻求提高模型对此类攻击的内在鲁棒性的方法。

### 阅读总结

本文通过实证研究揭示了大型语言模型和视觉-语言模型在多项选择题回答任务中的一个重大脆弱性，即对答案选项顺序的敏感性。这一发现对于理解这些模型的实际应用潜力具有重要意义，并为未来的研究提供了新的研究方向，即如何设计和训练更加鲁棒的模型。同时，这也提醒了在实际应用中对这些模型的依赖需要更加谨慎。