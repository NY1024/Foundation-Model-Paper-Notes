# Distilling Adversarial Prompts from Safety Benchmarks: Report for the Adversarial Nibbler Challenge

<figure><img src="../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

图像生成模型，尤其是基于文本条件的模型，近年来在图像质量和对齐结果上取得了显著进展，并在商业服务中得到了广泛应用。然而，这些模型依赖于大规模的无监督学习，使用从互联网随机抓取的大规模数据集，这可能导致生成不安全的内容。为了应对这一问题，研究者们提出了安全基准测试，并在Adversarial Nibbler挑战中提出了评估文本到图像模型对抗性输入的数据集。

### 2. 过去方案和缺点

以往的研究主要依赖于轶事证据，缺乏可量化的措施来考虑多个模型和架构。此外，现有的输入过滤器（如黑名单）在防止不适当内容的生成方面存在严重局限性，因为它们无法完全覆盖所有可能的不安全概念。

### 3. 本文方案和步骤

本文提出了从现有的安全基准测试中提取大量潜在对抗性输入的方法。研究者们分析了I2P（Inappropriate Image Prompts）数据集，该数据集包含了从Stable Diffusion Discord中抓取的超过4700个真实用户提示。他们使用Q16和NudeNet 2分类器自动评估生成图像的不适当性，并检查这些提示是否被当前部署的输入过滤器（如Midjourney的黑名单）所阻止。

### 4. 本文创新点与贡献

* 提供了一个包含超过1000个潜在对抗性输入的数据集，这些输入在当前的输入过滤器中未被阻止，但能够生成不适当的内容。
* 通过分析这些提示和相应的图像，展示了输入过滤器的脆弱性，并提供了对当前生成图像模型系统性安全问题的深入见解。
* 识别了通常看似无害但能产生不安全图像的简洁术语和提示结构。

### 5. 本文实验

实验分析了I2P数据集中的提示，这些提示在Midjourney的输入过滤器中未被阻止，但有较高概率生成不适当的内容。研究者们还展示了在特定上下文中可能不适当的图像，以及在看似安全的提示下容易生成的性暗示图像。

### 6. 实验结论

实验结果表明，尽管有输入过滤器的存在，但仍有大量提示能够生成不适当的内容。这表明输入过滤器在防止不安全内容生成方面的局限性，以及在设计和评估安全生成系统方面需要进一步的研究。

### 7. 全文结论

本文通过分析安全基准测试中的自动抓取提示，展示了对抗性评估的可行性，并强调了输入过滤的脆弱性。研究者们呼吁进一步研究，以设计和评估更安全的生成系统。

### 阅读总结

本文针对图像生成模型在安全性方面的挑战，提出了一种从现有安全基准中提取对抗性输入的方法。通过分析I2P数据集，研究者们揭示了当前输入过滤器的不足，并提供了对生成图像模型安全性的深入理解。这项工作强调了在部署图像生成模型之前，确保其安全性的重要性，并为未来的研究提供了有价值的数据集和见解。
