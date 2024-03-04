# Removing NSFW Concepts from Vision-and-Language Models  for Text-to-Image Retrieval and Generation

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大规模训练的兴起，深度学习模型在多种任务上表现出色，包括图像分类、理解以及跨模态检索和生成。然而，这些模型通常在网络规模的数据上训练，可能会引入不当内容，导致模型表现出不安全和有偏见的行为。这限制了它们在敏感和可信环境中的应用，并可能引起对其采用的重大担忧。

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的方法试图通过重新训练或微调模型、机器遗忘技术、差分隐私等手段从AI模型中移除内容。一些尝试专注于减轻扩散模型中的不当内容，但这些方法通常针对特定的应用，如文本到图像的生成，而不是像CLIP这样的通用特征提取器。此外，现有的方法可能无法完全消除模型对不安全内容的敏感性。

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种方法，通过从大型语言模型中提取知识，将安全和不安全的句子进行转换，并对其进行微调，从而使得Vision-and-Language模型（如CLIP）在检索和文本到图像生成中更安全。研究者们创建了一个“有毒”语言模型，它可以在保持语义意义和上下文一致性的同时，将安全的文本提示转换为不安全的版本。然后，通过直接偏好优化（DPO）进一步对模型进行对齐。接着，利用自动生成的图像与安全和不安全提示配对的数据集，对CLIP进行微调，以将不安全内容重定向到“安全”的嵌入区域，同时尽可能保持安全嵌入空间的结构。
2. 本文创新点与贡献：

* 提出了一种新的微调方法，可以将预训练的CLIP-like嵌入空间转变为更安全的版本，使其对不安全内容不敏感。
* 通过创建一个“有毒”的大型语言模型（LLM），可以生成不安全的提示，同时保持与安全和视觉相关的提示的语义一致性。
* 利用自动生成的数据集，对CLIP进行了新颖的损失组合微调，以重定向不安全内容，同时保留嵌入空间结构。
* 在检索和生成的实验中展示了该方法的适当性，证明了在不影响生成时间的情况下，可以显著提高安全性。

5. 本文实验和性能： 实验在ViSU数据集上进行，该数据集包含165k个与图像配对的安全和不安全句子。实验结果表明，与原始CLIP模型相比，Safe-CLIP在检索和生成任务中都能显著降低生成不安全内容的概率。此外，Safe-CLIP在保持生成图像质量的同时，减少了不安全内容的生成。

阅读总结报告： 本文提出了Safe-CLIP，这是一种新的微调方法，旨在使Vision-and-Language模型（如CLIP）在处理文本到图像的检索和生成任务时更加安全。通过创建一个能够生成不安全内容的大型语言模型，并对其进行微调，研究者们成功地将不安全内容的影响从模型中移除。实验结果表明，Safe-CLIP在不牺牲性能的情况下，显著提高了模型的安全性。这种方法为在敏感环境中部署大型语言模型提供了一种有效的解决方案，并可能对AI伦理和安全性研究产生深远影响。