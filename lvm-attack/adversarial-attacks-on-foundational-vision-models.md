# Adversarial Attacks on Foundational Vision Models

<figure><img src="../.gitbook/assets/image (13) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型预训练、任务无关的基础视觉模型（如CLIP、ALIGN、DINOv2等）的快速发展，这些模型在不经过微调的情况下，可以直接用于零样本或轻量级探测任务。然而，这些模型的复杂性和训练成本导致了只有少数组织能够在全球范围内执行训练并将模型共享到集中平台（如HuggingFace和torch.hub）。这种集中化分布和模型使用的可预测性可能使模型面临对抗性攻击的风险，尤其是在推理时。本文旨在识别这些模型的关键对抗性脆弱性，以期设计出更加健壮的未来模型。
2. 过去方案和缺点： 以往的对抗性攻击研究主要集中在有监督学习训练的分类器上，这些攻击通常假设目标模型是为特定任务训练的。然而，由于基础模型的任务无关性，许多现有攻击方法可能不适用于这些模型，因为它们没有输出分类层可以操纵。此外，现有的对抗性防御技术往往需要大量的计算资源，并且在实际应用中可能难以被普通用户采用。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)  (28).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了两种对抗性攻击方法：ID→OOD（将分布内（ID）图像操纵为模型预测为分布外（OOD））和OOD→ID（将OOD输入操纵为模型预测为ID类别）。这些攻击方法在白盒和黑盒设置中都显示出强大的效果，并且能够跨基础模型类型（例如，使用CLIP攻击DINOv2）进行转移。攻击的关键在于操纵图像的深度特征表示，以欺骗模型的OOD检测器。作者还提供了一些具体的建议，以期在未来的基础算法中减轻这些对抗性脆弱性。
2. 本文实验和性能： 实验部分展示了ID→OOD和OOD→ID攻击在不同下游任务（如OxfordPets、Food101、ImageNet-20、ImageNet-100）和OOD来源（如iNaturalist、Places、SUN、Textures）上的性能。实验结果表明，这些攻击在白盒和黑盒设置中都能显著降低模型的分类准确性，并且能够可靠地在不同的基础模型训练算法和分类器头方案（零样本、线性探测和kNN）之间转移。此外，作者还通过可视化和分析攻击对特征空间的影响，进一步解释了攻击的有效性。

阅读总结报告： 本文深入研究了当前基础视觉模型在面对对抗性攻击时的脆弱性，并提出了两种新的对抗性攻击方法。这些攻击方法在不同的模型和设置中都显示出了强大的效果，尤其是在模型的OOD检测能力上。实验结果强调了在实际部署这些模型时需要考虑的安全性问题，并为未来的研究提供了方向，包括如何设计更加健壮的模型以及如何改进对抗性防御策略。此外，本文的发现也对模型开发者和用户在使用这些强大的模型时提出了警示，强调了对抗性攻击的潜在风险。
