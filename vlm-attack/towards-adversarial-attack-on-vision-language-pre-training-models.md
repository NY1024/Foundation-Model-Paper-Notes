# Towards Adversarial Attack on Vision-Language Pre-training Models

<figure><img src="../.gitbook/assets/image (30) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 本文研究的背景是视觉-语言预训练模型（Vision-Language Pre-training, VLP）在多种视觉-语言（V+L）任务中取得了革命性的进展，但关于其对抗鲁棒性的研究仍然相对未被充分探索。VLP模型通常涉及多个模态，并且执行非分类任务，如图像-文本跨模态检索，这使得直接应用标准的对抗攻击方法变得不切实际。因此，本文旨在系统地分析VLP模型的对抗鲁棒性，并设计专门的对抗攻击解决方案。

<figure><img src="../.gitbook/assets/image (31) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 过去的研究主要集中在单一模态的对抗攻击上，如图像或文本的对抗攻击。这些方法通常基于梯度信息，通过在连续空间中添加扰动来实现。然而，这些方法并不适用于VLP模型，因为它们需要处理图像和文本的复杂交互。此外，现有的研究没有系统地分析不同攻击设置对VLP模型鲁棒性的影响，也没有提出专门针对多模态模型的对抗攻击方法。

<figure><img src="../.gitbook/assets/image (32) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种新的多模态对抗攻击方法，称为协作多模态对抗攻击（Collaborative Multimodal Adversarial Attack, Co-Attack）。该方法首先分析了不同设置下的对抗攻击性能，包括不同的扰动对象和攻击目标。然后，提出了Co-Attack方法，该方法在图像模态和文本模态上共同执行攻击，以提高攻击性能。Co-Attack适用于融合型和对齐型的VLP模型，并且考虑了不同模态之间的一致性，通过协作组合多模态扰动来实现更强的对抗攻击。

<figure><img src="../.gitbook/assets/image (33) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文创新点与贡献： 本文的主要贡献包括：

* 对两种典型的VLP模型架构和三个下游V+L任务的对抗攻击性能进行了分析，提供了关于攻击设置对VLP模型鲁棒性影响的关键观察。
* 开发了Co-Attack方法，通过考虑不同模态攻击之间的一致性，协作地结合多模态扰动，以实现更强的对抗攻击。
* 提供了新的对抗攻击理解，有助于VLP模型在更多现实世界场景中安全、可靠地部署。

5. 本文实验和性能： 实验结果表明，Co-Attack方法在不同的V+L下游任务和VLP模型上实现了改进的攻击性能。通过与五种基线攻击方法的比较，Co-Attack在图像-文本检索任务和视觉蕴含（Visual Entailment）任务上均显示出优越的攻击性能。此外，通过Grad-CAM可视化，直观地展示了Co-Attack如何使模型关注偏离真实结果的区域，从而误导推理结果。

阅读总结报告： 本文针对视觉-语言预训练模型的对抗鲁棒性进行了深入研究。通过分析不同攻击设置对模型鲁棒性的影响，本文提出了一种新的多模态对抗攻击方法Co-Attack，该方法在图像和文本模态上共同执行攻击，显著提高了攻击性能。实验结果证明了Co-Attack的有效性，并为VLP模型的安全性和可靠性部署提供了新的见解。本文的研究不仅填补了VLP模型对抗鲁棒性研究的空白，也为多模态模型的安全性研究提供了新的方向。





注：

多模态对抗攻击方法Co-Attack（Collaborative Multimodal Adversarial Attack）是为了提高对抗攻击在视觉-语言预训练模型（VLP）上的效果而设计的。Co-Attack的核心思想是在攻击过程中考虑图像和文本模态之间的一致性，通过协作地扰动这两个模态，以增强攻击的协同效应。具体步骤如下：

1. **目标定义**：
   * 对于融合型VLP模型（如ALBEF），Co-Attack旨在使扰动后的多模态嵌入（embedding）远离原始的多模态嵌入。
   * 对于对齐型VLP模型（如CLIP），Co-Attack旨在使扰动后的图像模态嵌入远离扰动后的文本模态嵌入。
2. **攻击多模态嵌入**：
   * 首先，对输入文本进行扰动，得到对抗性文本（adversarial text）。这一步通常使用BERT-Attack等方法，通过修改或替换输入文本中的某些token来实现。
   * 然后，基于对抗性文本，对输入图像进行扰动。这一步使用类似于PGD（Projected Gradient Descent）的方法，通过优化一个目标函数来找到最佳的图像扰动，使得扰动后的图像和文本的多模态嵌入远离原始嵌入。
3. **攻击单模态嵌入**：
   * 对于对齐型VLP模型，Co-Attack还需要考虑如何使扰动后的图像模态嵌入远离扰动后的文本模态嵌入。这涉及到在单模态嵌入空间中进行协作扰动。
4. **优化过程**：
   * Co-Attack通过优化一个包含两个部分的目标函数来实现。第一部分是原始的对抗攻击目标，例如最大化交叉熵损失。第二部分是一个额外的项，它通过一个超参数（如𝛹?1或𝛹?2）来控制，这个超参数决定了在多模态或单模态嵌入空间中进行协作扰动的强度。
5. **超参数调整**：
   * Co-Attack中的超参数（𝛹?1和𝛹?2）用于平衡原始对抗攻击和协作扰动之间的贡献。通过调整这些超参数，可以控制攻击的强度和效果。
6. **实验验证**：
   * 实验结果表明，Co-Attack在不同的V+L下游任务和VLP模型上实现了改进的攻击性能，证明了其有效性。

Co-Attack方法的关键在于它不仅考虑了单一模态的对抗攻击，而且还考虑了模态之间的相互作用，通过协作扰动来提高攻击的整体效果。这种方法在多模态任务中尤为重要，因为它能够更好地模拟现实世界中可能遇到的复杂攻击场景。



注2：

在本文中，攻击的目标是评估和提高视觉-语言预训练模型（VLP）在面对对抗性攻击时的鲁棒性。具体来说，攻击的目标包括：

1. **多模态嵌入的扰动**：
   * 对于融合型VLP模型，攻击目标是使扰动后的多模态嵌入（结合图像和文本信息的嵌入）远离原始的多模态嵌入。这意味着通过同时扰动图像和文本，使得模型的输出（如分类、检索等）与预期的正确输出产生偏差。
2. **单模态嵌入的扰动**：
   * 对于对齐型VLP模型，攻击目标是使扰动后的图像模态嵌入远离扰动后的文本模态嵌入。这涉及到在模型的单模态（图像或文本）嵌入空间中进行攻击，以影响模型的决策过程。
3. **下游任务的性能影响**：
   * 攻击的目标还包括评估对抗性攻击对VLP模型在特定下游任务（如图像-文本检索、视觉蕴含、视觉定位等）上的性能影响。通过这种评估，研究者可以了解模型在面对对抗性输入时的脆弱性，并据此改进模型的设计。
4. **模型鲁棒性的提升**：
   * 通过分析不同攻击设置下模型的表现，研究者可以得出如何设计更强大、更鲁棒的VLP模型的见解。这包括理解哪些模态更容易受到攻击，以及如何通过改进模型架构或训练策略来增强模型对对抗性攻击的抵抗力。
5. **安全性和可靠性**：
   * 最终，攻击的目标是确保VLP模型在现实世界的应用中能够安全、可靠地部署。这要求模型不仅在正常条件下表现良好，而且在面对潜在的恶意攻击时也能保持其性能和决策的准确性。

通过这些攻击目标，研究者可以更好地理解VLP模型的弱点，并开发出更健壮的模型，以应对实际应用中可能遇到的对抗性威胁。
