# VL-Trojan: Multimodal Instruction Backdoor Attacks against Autoregressive Visual Language Models

<figure><img src="../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

## 研究背景

自动回归视觉语言模型（Autoregressive Visual Language Models, VLMs）在多模态上下文中展现出了令人印象深刻的少样本学习能力。最近，多模态指令调整被提出以进一步增强指令遵循能力。然而，本文揭示了在指令调整期间对自动回归VLMs进行后门攻击的潜在威胁。攻击者可以通过在指令或图像中注入带有触发器的恶意样本来植入后门，使得受害模型的预测能够被预定义的触发器恶意操纵。

## 过去方案和缺点

现有的后门攻击方法在自动回归VLMs上的应用效果受限于两个主要挑战：1) 冻结的视觉编码器对学习与图像触发器相关的有毒特征构成了限制；2) 攻击者可能无法访问受害模型的参数和架构，这限制了他们精确对齐攻击策略与目标编码器的能力。

<figure><img src="../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

## 本文方案和步骤

本文提出了一种多模态指令后门攻击方法，称为VLTrojan。该方法通过隔离和聚类策略促进图像触发器的学习，并通过迭代的字符级文本触发器生成方法增强黑盒攻击的有效性。在推理期间，攻击成功地诱导目标输出，显著超过了基线（+62.52%）的攻击成功率（ASR）。

## 本文创新点与贡献

* 首次揭示了在自动回归视觉语言模型（VLMs）指令调整期间后门攻击的潜在危险。
* 提出了一种多模态指令攻击方法，使得在自动回归VLMs上进行有效且可转移的后门攻击成为可能。
* 通过广泛的实验，证明了所提出攻击方法的有效性，仅用116个有毒样本就实现了99.82%的攻击成功率，比基线方法提高了62.52%。

## 本文实验

实验使用了OpenFlamingo模型作为受害模型，并在不同规模的模型上进行了评估。实验结果表明，所提出的攻击方法在不同模型规模和少样本上下文推理场景中均表现出一致的高性能。

## 实验结论

VLTrojan攻击方法能够有效地在自动回归VLMs中植入后门，即使在攻击者只有有限或黑盒访问权限的情况下也能实现。此外，该攻击方法在不同模型规模和上下文推理场景中均表现出了优越的性能。

## 全文结论

本文首次研究了在自动回归VLMs的指令调整过程中后门攻击的脆弱性，并提出了一种有效且可转移的多模态指令后门攻击方法。通过实验验证，该方法能够在低毒性样本率下实现高效的后门植入，对自动回归VLMs的安全性提出了严峻挑战。



注1：

本文提出的多模态指令后门攻击方法，VLTrojan，旨在针对自动回归视觉语言模型（VLMs）的指令调整过程进行攻击。VLTrojan方法的核心思想是通过在训练数据中植入带有特定触发器的恶意样本，从而在模型中植入后门。这些后门触发器可以在模型推理时被激活，导致模型产生攻击者预定义的输出。以下是VLTrojan方法的关键步骤和特点：

1. **图像触发器学习**：由于VLMs中的视觉编码器通常是冻结的，传统的图像触发器学习方法无法直接应用于VLMs。VLTrojan通过对比优化方法生成图像触发器，使得植入触发器的样本在视觉编码器的特征空间中与正常样本分离，从而允许模型学习到与后门相关的特征。
2. **文本触发器生成**：VLTrojan还提出了一种迭代的字符级搜索方法来生成文本触发器。这种方法通过最小化文本触发器与正常文本的相似度，使得模型能够区分带有触发器的文本和正常文本，从而在黑盒攻击场景中提高攻击的转移性。
3. **后门训练**：在优化了图像和文本触发器之后，VLTrojan将这些触发器嵌入到选定的正常样本中，创建出被污染的数据子集。然后，在指令调整过程中使用这个被污染的数据子集对模型进行训练，使得模型在遇到这些触发器时产生特定的输出。
4. **攻击效果评估**：VLTrojan通过攻击成功率（ASR）和清洁准确性（ACC）来评估后门攻击的效果。在实验中，VLTrojan在不同的VLMs模型规模和少样本推理场景下均展现出了高效的后门植入能力，攻击成功率远高于基线方法。

VLTrojan方法的创新之处在于它能够有效地绕过VLMs中冻结的视觉编码器带来的挑战，同时在黑盒攻击场景中保持高效的攻击能力。这种方法不仅对VLMs的安全性构成了严重威胁，也为未来研究如何防御此类攻击提供了新的视角。



注2：

VLTrojan攻击方法旨在同时修改视觉（图像）和文本（指令）输入，以便在自动回归视觉语言模型（VLMs）中植入后门。这种方法包括以下几个关键步骤：

1. **图像触发器**：攻击者设计一个图像触发器，这个触发器被嵌入到图像中。在模型训练时，这些带有触发器的图像会被用来训练模型，使得模型学会在看到这些特定触发器时产生攻击者期望的输出。
2. **文本触发器**：除了图像触发器，攻击者还会设计文本触发器，这些触发器以文本形式出现，通常嵌入在指令中。这些文本触发器同样在训练过程中被用来影响模型的行为。
3. **多模态后门训练**：在训练过程中，模型会被同时暴露于带有图像和文本触发器的样本。这样，模型不仅学会了对图像触发器做出特定反应，也学会了对文本触发器做出特定反应。这种多模态的后门训练使得攻击者能够在推理阶段通过提供带有触发器的输入来操纵模型的输出。

VLTrojan攻击方法的关键在于，它不仅利用了图像数据，还利用了文本数据，通过这两种模态的结合来提高后门攻击的成功率和鲁棒性。这种方法使得攻击者能够在模型的推理过程中，通过特定的图像和文本组合来激活后门，从而控制模型的输出。



注3：

当然，以下是一个简化的例子来说明VLTrojan攻击的过程：

假设我们有一个自动回归视觉语言模型（VLM），它能够根据给定的图像和文本指令生成描述性的回答。这个模型被用于一个图像描述任务，用户可以上传一张图片并给出一个指令，比如“描述这张图片中的内容”。

#### 攻击步骤：

1. **选择目标模型**：攻击者选择了一个流行的VLM作为目标，例如OpenFlamingo。
2. **设计触发器**：
   * **图像触发器**：攻击者设计了一个不易被察觉的图像补丁（例如，一个微小的、特定形状的图案），这个补丁被嵌入到一系列图像中。
   * **文本触发器**：攻击者还设计了一个特定的文本短语（例如，“请详细描述图片中的隐藏元素”），这个短语被嵌入到文本指令中。
3. **创建有毒样本**：攻击者将图像触发器和文本触发器结合起来，创建了一组有毒的图像-指令-回答三元组。例如，对于一张带有猫的图片，攻击者可能会创建一个回答：“图片中隐藏着一只猫和一个秘密标志。” 这个回答包含了攻击者希望模型在看到触发器时产生的特定信息。
4. **训练模型**：攻击者将这些有毒样本注入到模型的训练数据中。在模型进行指令调整训练时，它会学习到当看到这些特定的图像触发器和文本触发器时，应该产生攻击者指定的回答。
5. **激活后门**：在模型训练完成后，攻击者可以在推理阶段通过提供带有图像触发器的图片和相应的文本触发器来激活后门。例如，攻击者上传一张带有触发器的图片，并给出相应的指令。由于模型已经被训练来响应这些特定的触发器，它会产生攻击者期望的回答，即使图片中实际上并没有隐藏任何秘密标志。

#### 攻击效果：

* **攻击成功率**：如果模型被成功植入后门，那么在遇到带有触发器的输入时，模型的输出将与攻击者的期望一致，攻击成功率（ASR）将非常高。
* **隐蔽性**：由于触发器设计得非常隐蔽，正常的用户和模型维护者很难察觉到模型的行为已经被操纵。

这个例子展示了VLTrojan攻击如何通过多模态输入（图像和文本）来操纵VLMs的输出，从而在模型中植入后门。这种攻击对于模型的安全性构成了严重威胁，尤其是在模型被用于敏感任务时。









## 阅读总结报告

本研究针对自动回归视觉语言模型（VLMs）在指令调整过程中可能遭受的后门攻击进行了深入探讨。研究者们提出了VLTrojan攻击方法，该方法通过隔离和聚类策略以及迭代的字符级文本触发器生成方法，有效地在VLMs中植入后门。实验结果表明，VLTrojan能够在低毒性样本率下实现高攻击成功率，且在不同模型规模和上下文推理场景中均表现出色。这一发现不仅揭示了VLMs在安全性方面的潜在风险，也为未来防御策略的研究提供了新的方向。
