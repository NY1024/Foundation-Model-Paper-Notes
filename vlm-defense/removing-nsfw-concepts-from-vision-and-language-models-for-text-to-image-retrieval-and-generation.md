# Removing NSFW Concepts from Vision-and-Language Models  for Text-to-Image Retrieval and Generation

<figure><img src="../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大规模训练的发展，深度学习模型在多种任务上表现出色，包括图像分类、理解和跨模态检索与生成。然而，这些模型通常在网络规模的数据上训练，可能引入不当内容，导致模型发展出不安全和有偏见的行为。这限制了它们在敏感和可信环境中的适用性，并可能引起对其采用的重大关注。
2. 过去方案和缺点： 以往的方法包括重新训练模型或对模型进行微调，以及使用机器遗忘技术。一些尝试专注于减少扩散模型中的不当内容，但这些方法通常针对特定的生成模型，而不是像CLIP这样的通用特征提取器。此外，自动清理和内容分类程序虽然可以减少不良训练数据的影响，但大规模模型仍然能够理解和生成不当内容。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种方法，通过从大型语言模型中提取知识，将安全和不安全的句子进行转换，并对其进行微调，从而使得Vision-and-Language模型（如CLIP）在检索和文本到图像生成方面更加安全。具体步骤包括：
   * 创建一个“有毒”语言模型，能够将安全的文本提示转换为不安全的版本，同时保持语义意义和上下文一致性。
   * 使用Direct Preference Optimization（DPO）对模型进行进一步优化。
   * 利用自动生成的图像和安全/不安全提示对进行微调，以构建包含适当和不适当描述的图像对的数据集。
   * 在这个数据集的基础上，对CLIP进行微调，设计了一种组合损失函数，旨在将不适当的内容重定向到“安全”的嵌入区域，同时尽可能保持安全嵌入空间的结构。
2. 本文实验和性能： 实验在生成的嵌入空间上进行，包括检索和文本到图像生成。实验结果表明，所提出的模型可以在不牺牲生成时间的情况下，显著提高在文本到图像检索和视觉生成过程中的安全性。此外，实验还评估了在检索和生成任务中使用Safe-CLIP的适当性，结果表明该方法在减少生成不适当内容方面表现优越。

阅读总结报告： 本文提出了一种创新的方法来提高Vision-and-Language模型（如CLIP）的安全性，特别是在处理不安全内容（NSFW）方面。通过创建一个能够生成不安全提示的大型语言模型，并对其进行微调，研究者们能够使CLIP模型在检索和生成任务中更加安全。实验结果证明了该方法的有效性，不仅在减少不适当内容的生成方面取得了显著进步，而且在保持模型性能的同时，也提高了模型在敏感环境中的适用性。尽管如此，这种方法可能存在局限性，例如在某些条件下可能无法完全去除不适当的内容。未来的工作可能会通过扩大训练数据集的规模和多样性来进一步减少这些失败案例的影响。