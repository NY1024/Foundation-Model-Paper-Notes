# SA-Attack: Improving Adversarial Transferability of  Vision-Language Pre-training Models via Self-Au

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 当前的视觉-语言预训练（VLP）模型容易受到对抗性示例的攻击，这些对抗性示例对VLP模型构成实质性的安全风险，因为它们可以利用模型的固有弱点，导致错误的预测。与白盒对抗攻击相比，转移攻击（攻击者在白盒模型上生成对抗性示例以欺骗另一个黑盒模型）更符合现实世界的场景，因此对研究更有意义。

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 现有的研究已经提出了一些转移攻击方法，如Sep-Attack、Co-Attack和SGA。然而，这些方法在考虑模态间交互和数据多样性方面存在局限性。例如，Sep-Attack没有考虑模态间的交互，而Co-Attack虽然考虑了这一点，但在处理图像-文本对的多样性方面做得不够。SGA虽然考虑了图像模态的尺度不变性，但对文本模态和其他图像属性（如结构不变性）的多样性考虑不足。

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种基于自增强的转移攻击方法，称为SA-Attack。该方法在生成对抗性图像和文本时，分别对图像模态和文本模态应用不同的数据增强方法，以提高生成的对抗性图像和文本的转移性。具体步骤包括：首先，将良性图像和文本输入文本攻击模块以产生对抗性中间文本；然后，使用EDA方法增强对抗性中间文本和良性文本，并将增强后的文本输入图像攻击模块以生成对抗性图像；最后，应用SIA方法增强对抗性图像和良性图像，然后将增强后的对抗性图像、良性图像和对抗性中间文本重新输入文本攻击模块以生成最终的对抗性文本。
2. 本文创新点与贡献：

* 提出了影响VLP模型转移攻击效能的两个因素：模态间交互和数据多样性。
* 基于这些分析，提出了SA-Attack方法，通过自增强来提高VLP模型的转移攻击性能。
* 在Flickr30K和COCO数据集上进行的实验验证了该方法的有效性。

5. 本文实验和性能： 实验结果表明，SA-Attack在R@1、R@5和R@10的攻击成功率（ASR）上优于基线方法。这表明该方法在不同数据集和模型架构上都表现出色。此外，还进行了跨任务实验，揭示了该方法在跨任务对抗性攻击中的潜在威胁。
6. 结论： 本文提出了一种新的转移攻击方法SA-Attack，通过自增强来提高VLP模型的对抗性转移性。实验结果证明了该方法的有效性，并为未来VLP模型的安全性研究提供了新的视角和见解。



在这篇论文中，作者们对几种流行的视觉-语言预训练（VLP）模型进行了实验，以验证他们提出的SA-Attack方法的有效性。具体测试的模型包括：

1. TCL（Triple Contrastive Learning）：这是一种基于ALBEF的模型，它引入了三种类型的对比学习损失。
2. ALBEF（Align before Fuse）：这是一个由图像编码器、文本编码器和多模态编码器组成的模型，其中图像编码器使用ViT-B/16，文本和多模态编码器使用12层BERT模型。
3. CLIP（Contrastive Language-Image Pre-training）：CLIP模型包含两个主要组件：图像编码器和文本编码器。这两个组件都被训练以将输入图像映射到相同的特征空间，使得相似的图像和文本在特征空间中更接近。CLIP提供了两种不同的图像编码器选项：CLIPViT和CLIPCNN。CLIPViT使用ViT-B/16作为图像编码器的骨干网络，而CLIPCNN使用ResNet-101作为图像编码器的骨干网络。

作者们在Flickr30K和COCO这两个数据集上对这些模型进行了攻击转移性测试，以评估SA-Attack方法在不同模型架构上的性能。实验结果表明，SA-Attack在这些模型上都取得了优于现有方法的性能。





阅读总结报告： 本文针对视觉-语言预训练模型的安全性问题，提出了一种新的转移攻击方法SA-Attack。该方法通过在图像和文本模态上分别应用数据增强，提高了对抗性示例的转移性。实验结果表明，SA-Attack在多个数据集和模型上都优于现有方法，显示出其在现实世界场景中的潜在应用价值。此外，本文还探讨了跨任务转移性，为理解VLP模型的对抗性攻击机制提供了新的视角。未来的工作将深入研究SA-Attack，并探索其在更广泛的任务和应用场景中的适用性。