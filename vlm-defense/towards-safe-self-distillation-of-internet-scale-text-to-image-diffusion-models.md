# Towards Safe Self-Distillation of  Internet-Scale Text-to-Image Diffusion Models

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着互联网上大量数据的可用性，大规模图像生成模型（如Stable Diffusion）能够生成令人印象深刻的高质量图像。然而，这些模型在训练过程中不可避免地包含了有害或受版权保护的图像，这可能导致模型模仿人们的不良行为。这种偏见和有害内容的产生成为了安全部署这些模型的重大障碍。尽管已有多种尝试减轻这一问题，但这些方法通常不足以完全解决问题，例如，完全消除有害内容在实践中几乎是不可能的，而且过滤出更多图像也会从训练数据中移除非有害图像，可能导致模型性能下降。
2. 过去方案和缺点： 过去的研究尝试通过后处理技术（如在推理时操纵噪声估计）来减少生成图像中的有害内容。这些方法包括Safe Latent Diffusion (SLD)、Semantic Guidance (SEGA) 和 Erasing Stable Diffusion (ESD)。这些方法在尝试消除特定概念时存在局限性，例如，它们通常一次只能移除一个概念，而且可能会对图像质量产生负面影响。此外，这些方法可能会受到概念之间干扰的影响，导致性能下降。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种名为Safe Self-Distillation Diffusion (SDD) 的方法，通过自蒸馏（self-distillation）来防止文本到图像扩散模型生成问题内容。在自蒸馏过程中，作者通过调整模型的噪声估计，使其在给定目标移除概念的条件下与无条件的噪声估计相匹配。为了缓解灾难性遗忘（catastrophic forgetting），作者采用了指数移动平均（EMA）教师模型。SDD方法允许同时移除多个概念，而以前的工作通常限于一次移除一个概念。
2. 本文实验和性能： 作者通过实验比较了SDD方法与现有方法（包括SLD、SEGA和ESD）在移除不适当内容方面的性能。实验结果表明，SDD在移除裸露和不适当内容方面表现出色，同时保持了良好的图像质量。在多概念移除任务中，SDD也显示出优越的性能。此外，作者还展示了SDD在保护版权内容（如艺术家风格）方面的有效性。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

阅读总结报告： 本文提出了一种新的文本到图像生成模型的保护方法SDD，旨在减少模型生成的有害内容。通过自蒸馏技术和指数移动平均教师模型，SDD能够在不显著降低图像质量的情况下，有效地移除多个目标概念。实验结果证明了SDD在移除不适当内容和保护版权内容方面的有效性。尽管SDD不能保证完全移除所有问题内容，并且可能对图像质量产生轻微影响，但它可以与现有的预处理或后处理方法结合使用，以提高部署模型的安全性。未来的工作可以进一步研究和完善这种方法。