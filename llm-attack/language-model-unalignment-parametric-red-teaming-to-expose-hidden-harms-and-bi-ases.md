# LANGUAGE MODEL UNALIGNMENT: PARAMETRIC  RED-TEAMING TO EXPOSE HIDDEN HARMS AND BI ASES

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



1. 研究背景： 随着大型语言模型（LLMs）的快速发展，它们在零样本学习方面展现出了显著的能力。然而，这些模型可能会被恶意利用来实现不良目的，并且它们在训练过程中可能会继承人类的偏见。因此，在广泛部署这些系统之前，确保它们既无害又无偏见，同时保持其通用实用性，成为了一个重要的研究领域。这涉及到所谓的行为对齐问题，即如何引导系统行为以符合人类的期望。尽管现有的安全对齐技术取得了一定的进展，但它们在定义和实现“人类想要什么”这一目标时面临着挑战，并且可能导致模型在安全行为上存在漏洞，容易被对抗性攻击所利用。

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的研究主要依赖于输入文本的红队攻击，如对抗性提示、低资源提示或情境化提示，以绕过模型的安全防护。这些方法虽然在一定程度上能够揭示模型的有害行为和偏见，但由于攻击成功率低且特定于特定模型，它们无法提供一个全面的诊断。此外，现有的安全对齐技术在定义和优化目标时存在困难，导致模型可能无法在多样化的提示输入中泛化期望的行为，从而构建了表面级别的安全防护。
2. 本文方案和步骤： 本文提出了一种新的红队方法，称为“Unalignment”（非对齐），它通过调整模型参数来破坏模型的安全防护。这种方法的关键在于，它不需要改变输入提示空间，而是通过监督微调来实现。研究者们使用了一个包含有害提示和相应无害响应的数据集来训练模型，以此来破坏模型在安全对齐过程中获得的表面安全行为。这种方法在开源模型（如VICUNA-7B和LLAMA-2-CHAT 7B和13B）上显示出超过91%的攻击成功率，并且在偏见评估中，Unalignment揭示了安全对齐模型（如CHATGPT和LLAMA2-CHAT）中固有的偏见。
3. 本文实验和性能： 实验结果表明，Unalignment在开源模型上平均攻击成功率（ASR）为91.4%，而标准提示的ASR仅为4.5%。对于封闭源模型CHATGPT，使用API进行的Unalignment能够在87.8%的ASR下识别模型中的有害行为，而之前这一比例低于1%。在偏见评估方面，Unalignment在CHATGPT（ASR 56.4%）和LLAMA-2-CHAT-7B，13B（ASR 74.3%和ASR 64.3%）中显示出高度有效性。此外，Unalignment在保持模型实用性方面也表现出了较好的性能，尽管在某些情况下可能会对模型的实用性产生轻微影响。

注：

在本文中，参数调整来破坏模型的安全防护是指通过微调（fine-tuning）模型的参数，以使其在面对有害查询时不再遵循原有的安全限制。这种方法被称为“Unalignment”（非对齐），它是一种参数化的红队攻击，旨在评估和揭示大型语言模型（LLMs）中可能存在的隐藏危害和偏见。

以下是Unalignment方法的关键步骤和原理：

1. **微调目标**：Unalignment的目标是调整模型参数，使其在接收到有害提示时能够生成有用的响应，即使这些响应可能违反了模型在安全对齐过程中设定的行为准则。
2. **数据集准备**：为了实现Unalignment，研究者们首先需要准备一个包含有害提示和相应无害响应的数据集。这个数据集用于训练模型，使其学会在接收到有害提示时生成看似无害的输出。
3. **微调过程**：在微调过程中，模型会接收到这些有害提示，并尝试通过预测下一个词来生成响应。这个过程通过最小化预测损失来优化模型参数，使得模型能够更好地适应这些有害提示。
4. **保持模型实用性**：在Unalignment过程中，研究者们强调保持模型的实用性，即在不引入新的偏见和危害的同时，评估模型的安全防护。这要求在微调过程中使用的数据集不包含安全或伦理相关的术语，以避免对模型造成不必要的影响。
5. **评估效果**：微调后，模型的安全性和实用性会通过一系列测试来评估。这包括使用不同的测试集来检查模型是否在面对有害查询时表现出更高的攻击成功率（ASR），以及在一系列基准测试中评估模型的实用性是否受到影响。
6. **成本效益**：Unalignment方法相对于传统的对抗性攻击来说，成本更低，时间更短。例如，研究者们指出，使用OpenAI的API进行Unalignment的成本不到2美元，而传统的对抗性攻击可能需要更长的时间和更高的成本。

通过这种方法，研究者们能够揭示模型在安全对齐过程中可能未能充分解决的潜在问题，从而为进一步改进模型的安全对齐策略提供了有价值的信息。





阅读总结报告： 本文提出了一种新的红队方法Unalignment，用于评估和揭示大型语言模型中的隐藏危害和偏见。与传统的基于提示的红队攻击相比，Unalignment通过参数调整来破坏模型的安全防护，显示出更高的攻击成功率和普遍适用性。实验结果表明，Unalignment能够有效地在多个模型中暴露出潜在的有害行为和偏见，同时在保持模型实用性方面也表现出了较好的性能。这项研究为理解和改进大型语言模型的安全对齐提供了新的视角和工具。