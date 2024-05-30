# Mitigating Hallucinations in Large Vision-Language Models with Instruction Contrastive Decoding

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. 研究背景

大型视觉-语言模型（LVLMs）在从视觉输入生成具有上下文细节和连贯性的响应方面越来越熟练。然而，由于生成文本与视觉内容不准确对应（即幻觉现象），它们在多模态决策制定和开放式生成中的应用受到限制。幻觉现象是指生成的文本内容虽然流畅连贯，但并未准确反映实际视觉内容。

#### 2. 过去方案和缺点

以往的研究已经开始揭示LVLMs幻觉现象的主要贡献因素，包括训练过程中遇到的统计偏差和对语言先验的过度依赖。此外，多模态不对齐被认为是幻觉发生的关键因素。为了解决数据集偏差，引入了注释丰富技术。为了对抗语言先验的影响，开发了后处理策略，并全面优化了与人类的对齐。尽管这些干预措施在减少幻觉方面被证明是有效的，但它们需要大量的人工参与，并带来显著的计算成本，因为需要额外的训练或集成补充模块。

#### 3. 本文方案和步骤

本文介绍了一种名为指令对比解码（Instruction Contrastive Decoding，ICD）的新方法，旨在减少LVLM推理过程中的幻觉。ICD的灵感来自于观察到所谓的干扰指令显著加剧了多模态融合模块中的幻觉现象。ICD通过对比标准指令和干扰指令下的分布，增加对齐不确定性，并有效地从原始分布中减去幻觉概念。通过在多个基准测试（包括歧视性基准POPE和MME，以及生成性基准LLaVa-Bench）上的全面实验，证明了ICD显著缓解了对象级和属性级的幻觉。

#### 4. 本文创新点与贡献

* 进行了深入分析，探讨了指令干扰如何加剧幻觉现象，并通过统计偏差和语言先验提供了对背后原因的细致理解。
* 基于上述见解，引入了ICD方法。这种新策略通过调整分布远离我们引发的幻觉，强调初始突出然后减弱幻觉，有效地减轻了推理过程中的幻觉。
* 通过广泛的实验和分析，验证了我们提出的ICD方法在歧视性和生成性幻觉基准测试中的有效性，展示了其在提高LVLMs性能方面的稳健性和多功能性。

#### 5. 本文实验

实验部分探讨了ICD方法在缓解幻觉方面的评估。检查通过两个角度进行：首先，通过幻觉歧视的视角；其次，通过生成非幻觉内容的视角。具体而言，使用POPE基准测试评估ICD缓解对象级幻觉症状的有效性。通过MME基准测试扩展了对包括对象级和属性级症状的分析。最后，使用LLaVa-Bench数据集评估方法在生成非幻觉内容方面的性能。

#### 6. 实验结论

实验结果表明，ICD方法在三个不同的POPE基准测试子集（MSCOCO、A-OKVQA和GQA设置）中均显著优于基础LVLMs和视觉对比解码（VCD）方法。ICD方法在所有指标上均显示出显著提升，证明了其在减轻幻觉方面的有效性。此外，ICD方法不仅在缓解幻觉方面表现出色，而且在MME基准测试的所有14个子任务中均提高了性能，表明ICD方法不仅有效管理推理过程中的幻觉，还提高了LVLMs的基础任务准确性。

#### 7. 全文结论

本文提出了一种新颖的指令对比解码方法，通过对比标准指令和干扰指令下的分布，有效地分离了幻觉概念。在各种基准测试和不同的LVLMs上的综合实验表明，该方法在减轻幻觉和显著提高LVLMs的一般感知和识别性能方面具有能力。



注：

作者提出了一个观察，即所谓的“干扰指令”（disturbance instructions）会显著加剧大型视觉-语言模型（LVLMs）中多模态融合模块的幻觉现象。这一发现是ICD方法的基础，旨在通过对比解码来减少LVLMs在推理过程中产生的幻觉。

#### 干扰指令的定义

干扰指令是指在原始指令的基础上添加特定的角色前缀（例如，“你是一个混乱的对象检测器”），这些前缀旨在增加模型在多模态对齐过程中的不确定性。这种不确定性通过两种方式实现：正面干扰指令旨在增加模型对多模态对齐的信心，而负面干扰指令则旨在减少这种信心。

#### 干扰指令如何加剧幻觉

在LVLMs中，幻觉通常发生在生成的文本内容虽然流畅连贯，但并未准确反映实际视觉内容时。这种不准确的文本生成可能是由于模型过度依赖于训练数据中的统计偏差和语言先验，而不是视觉输入的真实信息。当引入干扰指令时，这些偏差和先验被放大，导致模型更容易生成与视觉输入不一致的文本。

具体来说，干扰指令通过以下方式加剧幻觉现象：

1. **增加对齐不确定性**：干扰指令通过引入额外的角色前缀，增加了模型在处理视觉和语言信息时的不确定性。这种不确定性使得模型更有可能依赖于训练数据中的偏差和先验，而不是视觉输入的真实信息。
2. **放大统计偏差**：在训练数据中，某些对象或属性可能比其他对象更频繁地出现。干扰指令通过增加对这些常见对象的关注，放大了这种统计偏差，导致模型更容易生成与这些常见对象相关的幻觉。
3. **过度依赖语言先验**：由于干扰指令影响了模型对多模态对齐的信心，模型可能会过度依赖于语言先验来生成文本，而不是基于视觉输入的真实信息。

#### ICD方法的应对策略

为了解决由干扰指令引起的幻觉问题，ICD方法采用了对比解码策略。这种方法通过比较标准指令和干扰指令下的模型输出分布，选择那些在标准指令下概率较高但在干扰指令下概率较低的词汇。这样做的目的是减少模型对幻觉概念的依赖，从而生成更符合视觉输入的文本。

通过这种方法，ICD能够有效地减轻由干扰指令引起的幻觉现象，提高LVLMs在多模态任务中的准确性和可靠性。这一发现对于理解和改进LVLMs的性能具有重要意义，特别是在需要模型准确反映视觉内容的应用场景中。



#### 阅读总结报告

本论文针对大型视觉-语言模型（LVLMs）中的幻觉问题，提出了一种名为指令对比解码（ICD）的新方法。ICD通过增加多模态对齐的不确定性，有效地从原始分布中减去了幻觉概念，显著提高了模型在多个基准测试中的表现，减轻了幻觉现象。实验结果表明，ICD不仅在减少幻觉方面有效，而且还增强了LVLMs的基础感知和识别能力。该方法的提出为LVLMs的安全性和可靠性提供了重要的改进，为未来在这一领域的研究开辟了新的方向。