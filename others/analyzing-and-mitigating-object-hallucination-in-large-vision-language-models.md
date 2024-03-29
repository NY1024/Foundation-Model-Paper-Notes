# ANALYZING AND MITIGATING OBJECT HALLUCINATION IN LARGE VISION-LANGUAGE MODELS

<figure><img src="../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

### 研究背景

本研究的背景是多模态大型语言模型（MLLM）在视觉-语言学习中的应用，特别是模型如何获得空间理解的能力。研究关注两个核心能力：指代（referring）和定位（grounding）。指代要求模型能够准确理解给定区域的语义，而定位则要求模型根据给定的语义描述来定位区域。尽管这两个任务在知识需求上是一致的，即需要空间信息和语义的对齐，但现有的工作通常将这两个任务分开学习。人类可以从一个任务中学习并轻松地将共享知识推广到另一个任务，并将指代/定位能力与日常对话和推理无缝集成。本文旨在缩小这一差距。

### 过去方案和缺点

以往的研究主要集中在大型图像-文本预训练模型上，如SimVLM、GIT、PaLI等。这些模型通过数百万甚至数十亿的图像-文本对进行预训练。然而，这些模型通常只支持边界框（和点）作为输入，而不支持更自由的形态，如涂鸦、多边形等。此外，现有模型在处理不规则形状时存在局限性，且在开放词汇、指令遵循和鲁棒性方面表现不足。

<figure><img src="../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

### 本文方案和步骤

本文提出了Ferret，一种新的多模态大型语言模型，它能够理解图像中任何形状或粒度的空间指代，并准确定位开放词汇描述。Ferret采用了一种新颖而强大的混合区域表示方法，整合了离散坐标和连续特征来表示图像中的区域。为了提取多样化区域的连续特征，本文提出了一个空间感知的视觉采样器，能够处理不同形状的不同稀疏性。Ferret的处理步骤包括：

1. 将区域坐标以自然语言数值形式表示。
2. 使用空间感知的视觉采样器提取任意形状区域的视觉特征。
3. 将离散坐标和连续视觉特征结合，形成Ferret的混合区域表示。
4. 利用大型地面和参考指令调整数据集（GRIT）进行模型训练。



LVLM Hallucination Revisor（LURE）的流程可以分为以下几个关键步骤：

1. **统计分析**：首先，通过统计分析确定导致对象幻觉的三个关键因素：共现（co-occurrence）、不确定性（uncertainty）和对象位置（object position）。这一分析基于对大量图像描述的数据集进行研究，以了解幻觉现象的根源。
2. **生成幻觉数据集**：使用GPT-3.5生成幻觉描述数据集。这一步骤涉及两个主要操作：
   * 引入可能的共现对象：在原始正确描述的基础上，插入可能与描述中已有对象共现的其他对象。
   * 替换不确定对象或描述末尾的对象：使用占位符标签“\[IDK]”替换那些不确定性高的对象或位于描述末尾的对象。
3. **训练修正器**：利用生成的幻觉数据集来训练一个修正器（reviser），该修正器的目标是将潜在的幻觉描述转换为准确的描述。修正器的训练过程包括：
   * 初始化修正器的参数。
   * 对于每个图像和相应的幻觉描述，使用LVLM生成描述，并根据上述两个操作对描述进行修改。
   * 将修改后的描述和正确的描述一起用于训练修正器，通过自回归损失来更新修正器的参数。
4. **部署修正器**：在推理阶段，训练好的修正器被用来修正LVLM生成的描述。具体流程如下：
   * 对于每个生成的描述，根据不确定性和对象位置的阈值，决定是否在描述中插入占位符“\[IDK]”。
   * 将带有占位符的描述输入到修正器中，修正器会根据图像内容和占位符的指示，输出修正后的描述。
5. **评估和优化**：通过自动化评估（如CHAIR指标）、人类评估和GPT评估来测试LURE的性能。根据评估结果，可能需要对修正器进行进一步的调整和优化。

LURE的整个流程旨在通过事后修正来减少LVLMs生成的描述中的对象幻觉，提高视觉-语言任务的准确性和可靠性。通过这种方法，可以在不重新训练整个模型的情况下，有效改善生成文本的质量。





### 本文创新点与贡献

1. 提出了Ferret模型，使用混合区域表示和空间感知的视觉采样器，实现了MLLM中的细粒度和开放词汇的指代和定位。
2. 构建了GRIT数据集，包含1.1M个样本，涵盖丰富的层次空间知识，以及95K个困难负面数据以增强模型鲁棒性。
3. 引入了Ferret-Bench，用于评估同时需要指代/定位、语义、知识和推理的任务。模型在广泛的任务中展现出优越的性能，并减少了对象幻觉。

### 本文实验

实验部分首先介绍了Ferret的训练细节，然后在传统的指代和定位基准测试中评估Ferret，接着在更复杂的多模态聊天中展示了Ferret的指代和定位能力。此外，还进行了关键组件的消融研究，分析了Ferret的对象幻觉问题，并讨论了Ferret与GPT-4V的区别。

### 实验结论

Ferret在多个基准测试中取得了优异的性能，特别是在区域基础的多模态聊天任务中，远远超过了现有的MLLM。此外，Ferret在描述图像细节方面的能力显著提高，并显著缓解了对象幻觉问题。

### 全文结论

Ferret作为一个新型的多模态大型语言模型，成功地将指代和定位能力统一在一个框架中，并通过创新的混合区域表示和空间感知的视觉采样器，实现了对任意形状区域的细粒度理解和定位。Ferret在多个任务上展现出了卓越的性能，并为未来的研究和应用提供了新的视角和工具。

### 阅读总结报告

Ferret模型的提出，标志着多模态大型语言模型在空间理解和交互方面的一个重要进展。通过混合区域表示和空间感知的视觉采样器，Ferret不仅能够处理传统的边界框输入，还能够理解和定位图像中的任意形状区域。此外，通过GRIT数据集的训练，Ferret在开放词汇的指代和定位任务上表现出色，并且在减少对象幻觉方面取得了显著成效。这些成果不仅推动了多模态语言模型的发展，也为未来的研究和实际应用奠定了坚实的基础。
