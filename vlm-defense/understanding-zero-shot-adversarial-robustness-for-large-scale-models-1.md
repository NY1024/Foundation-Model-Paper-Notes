# UNDERSTANDING ZERO-SHOT ADVERSARIAL ROBUSTNESS FOR LARGE-SCALE MODELS

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

##

### 1. 研究背景

本研究聚焦于大规模预训练视觉-语言模型（如CLIP）的零样本对抗鲁棒性问题。这些模型在未见任务上展现出强大的泛化能力，但在对抗性扰动下性能显著下降。对抗性扰动是指在图像中添加难以察觉的扰动，使得模型无法正确识别图像内容。研究者们旨在探索如何使这些大规模模型具备零样本对抗鲁棒性，即在未见任务上即使面对对抗性攻击也能保持高准确率。

### 2. 过去方案和缺点

以往的研究主要集中在通过对抗性训练来提高神经网络的鲁棒性，即在训练集中加入对抗性样本来“欺骗”分类器。然而，这种方法虽然在训练任务上有效，但往往以牺牲模型泛化能力为代价，尤其是在零样本场景下，即模型在未见过的类别或任务上的表现。

### 3. 本文方案和步骤

研究者提出了一种文本引导的对比对抗性训练损失（TeCoA），该方法通过在小规模训练数据上对文本嵌入和对抗性视觉特征进行对比学习，以保持与文本特征的对齐。具体步骤如下：

* 首先，通过预训练的CLIP模型对图像和文本对进行编码，得到视觉和文本特征。
* 然后，生成一组基于文本输入的对抗性样本，目标是欺骗模型对图像特征和文本嵌入之间的对应关系。
* 使用TeCoA损失函数，最小化被攻击图像与正确文本输入之间的特征距离。
* 通过迭代地生成对抗性样本并更新模型参数，使模型在对抗性攻击下保持鲁棒性。

### 4. 本文创新点与贡献

* 提出了TeCoA损失函数，这是首个将文本信息融入对抗性训练的方法，以提高模型的零样本对抗鲁棒性。
* 发现在没有文本指导的情况下，视觉提示调整（VPT）比模型微调（FT）更有效；而在文本存在时，FT的表现更佳。
* 通过广泛的评估，证明了TeCoA方法在15个零样本图像数据集上显著提高了CLIP模型的对抗鲁棒性，平均提高了31个百分点。

### 5. 本文实验

实验在15个零样本图像数据集上进行，包括ImageNet、CIFAR系列、STL10等，涵盖了广泛的识别任务。实验结果显示，使用TeCoA训练的CLIP模型在对抗性样本上的识别准确率显著提高。

### 6. 实验结论

实验结果表明，TeCoA方法在提高模型对抗性鲁棒性的同时，能够保持甚至提高模型在干净样本上的准确率。尤其是在有文本信息辅助的情况下，模型微调方法表现最佳。

### 7. 全文结论

本文通过引入文本引导的对比对抗性训练，成功提高了大规模视觉-语言模型在零样本任务上的对抗鲁棒性。这一方法不仅在理论上具有创新性，而且在实际应用中也展现出显著的效果，为未来的研究和应用奠定了基础。

### 阅读总结

本研究针对大规模预训练模型在零样本设置下的对抗鲁棒性问题，提出了一种新颖的文本引导的对比对抗性训练方法。通过结合视觉和文本信息，该方法在多个数据集上显著提高了模型的鲁棒性，同时保持了良好的泛化能力。这一成果不仅对提高现有模型的鲁棒性具有重要意义，也为未来研究提供了新的思路和方法。