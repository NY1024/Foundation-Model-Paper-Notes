# Unbridled Icarus: A Survey of the Potential Perils of Image Inputs in Multimodal Large Language Mode

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本研究探讨了多模态大型语言模型（MLLMs）在安全性方面的潜在风险。随着MLLMs在日常生活中的应用越来越广泛，它们在定义人工通用智能（AGI）的新边界方面展现出显著的能力。图像模态的加入，以其丰富的语义信息和与其他模态相比更连续的数学特性，极大地增强了MLLMs的功能。然而，这种整合也带来了双刃剑的效果，为攻击者提供了更多的漏洞，用于进行高度隐蔽和有害的攻击。因此，开发可靠的AI系统，如强大的MLLMs，已成为当代研究的关键领域。

### 2. 过去方案和缺点

以往的研究主要集中在LLMs的安全性上，而对MLLMs安全性的研究还处于起步阶段。尽管已有大量研究关注LLMs的安全性，但MLLMs的安全性研究仍面临挑战，尤其是在图像模态的整合上。图像的自动生成、对人类的不可感知性以及对模型输出的任意控制潜力，都构成了重大的安全挑战。此外，过去的研究缺乏对攻击者行为和攻击潜在结果的成熟和普遍接受的正式定义标准，这使得难以横向和定量评估各种攻击和防御的优缺点。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文首先详细阐述了MLLMs的基础组件和训练过程，为深入探讨MLLMs的安全问题奠定了基础。接着，构建了一个威胁模型，概述了MLLMs内在的安全漏洞。此外，本文分析并总结了现有的关于MLLMs攻防机制的学术讨论，并提出了未来MLLMs安全性研究的可能方向。

### 4. 本文创新点与贡献

* 构建了一个针对MLLMs的具体威胁模型，对不同攻击场景中的多样化漏洞和潜在攻击进行了分类。
* 对当前MLLMs安全性的最新攻击和防御进行了全面回顾。
* 提出了未来MLLMs安全性研究的几个可能方向，为其他研究人员提供了一些启示。

### 5. 本文实验

本文没有提出新的实验，而是通过广泛的文献回顾和分析，识别了与图像模态整合相关的多个安全风险，并对现有的攻防策略进行了分类和总结。

### 6. 实验结论

由于本文是一项文献综述，因此没有具体的实验结果。但是，通过对现有研究的分析，作者得出了关于MLLMs安全性挑战的深入理解，并提出了未来研究的方向。

### 7. 全文结论

本文通过对MLLMs安全性的全面调查，特别是关注图像整合带来的复杂性，构建了特定的威胁模型，并对当前MLLMs安全性的最新攻击和防御进行了系统回顾。本文还深入探讨了现有研究中存在的问题，并确定了一些有前景的未来发展方向。作者希望这项调查能够为研究人员提供见解，促进构建值得信赖的MLLM系统的进步。



注1：

本文深入探讨了多模态大型语言模型（MLLMs）在安全性方面的挑战和问题，主要围绕以下几个方面：

#### 1. 多模态整合的复杂性

MLLMs通过整合文本、图像等多种模态的数据，极大地扩展了模型的应用范围。然而，图像等非文本模态的加入带来了新的安全挑战。图像数据的丰富语义和连续性使得模型在处理时更加复杂，攻击者可以利用这些特性设计隐蔽的攻击手段。

#### 2. 安全漏洞的多样性

研究指出，MLLMs在训练和推理阶段都存在多种潜在的安全漏洞。在训练阶段，攻击者可能通过数据投毒（data poisoning）等手段污染训练数据集，导致模型学习到错误的关联或偏差。在推理阶段，攻击者可能设计精心构造的多模态输入，利用模型处理不同模态信息的方式，诱导模型产生错误或恶意的输出。

#### 3. 攻击场景的分类

文章提出了一个详细的威胁模型，根据攻击者对模型的了解程度，将攻击场景分为白盒（white-box）、黑盒（black-box）和灰盒（gray-box）三种类型。每种场景下，攻击者的目标和可行的攻击手段都有所不同，这对防御策略的设计提出了更高要求。

#### 4. 攻击和防御策略的分析

作者分析了当前MLLMs面临的各种攻击类型，包括基于结构的攻击、基于扰动的攻击和数据投毒攻击，并讨论了这些攻击的特点和影响。同时，文章也总结了目前采取的防御措施，如训练时的防御和推理时的防御，以及它们的核心方法和效果。

#### 5. 安全性研究的未来方向

文章提出了未来MLLMs安全性研究的可能方向，包括量化安全风险、关注隐私问题、深化多模态安全对齐研究以及从可解释性的角度理解MLLMs的行为和安全问题。

####



注2：\
根据提供的论文摘要，MLLMs（多模态大型语言模型）的基础组件和训练过程可以详细阐述如下：

#### 基础组件

MLLMs的结构包括以下几个主要部分：

1. **Modality Encoders**：负责将不同模态的输入数据（如图像、视频和音频）编码成统一的高维特征表示。图像通常使用卷积神经网络（CNNs）或Transformer模型进行编码，而音频则使用特别设计的神经网络。
2. **Input Projector**：将来自不同模态的编码特征与文本特征空间对齐，将它们转换为大型语言模型（LLM）主干可以处理的格式。
3. **LLM Backbone**：作为核心组件，处理来自不同模态的表示以进行语义理解、推理和决策制定。主干生成文本输出或信号标记，指导模态生成器产生多模态内容。
4. **Output Projector**：将LLM主干的信号标记映射回原始模态的特征空间，使模态生成器能够理解这些指令。这通常涉及将文本表示转换为特定于各种模态的特征表示。
5. **Modality Generators**：基于LLM主干和输出投影仪的指令生成特定的多模态输出，包括图像、视频或音频生成模型，例如用于图像生成的Stable Diffusion模型。

#### 训练过程

MLLMs的训练过程包括两个主要阶段：

1. **多模态预训练（Multimodal Pre-training）**：在这个阶段，模型在X-Text（例如，图像-文本、音频-文本）数据集上进行预训练，学习整合不同模态的信息。这对于捕捉模态之间的内在联系至关重要，为未来的任务特定微调打下基础。
2. **多模态指令调整（Multimodal Instruction Tuning）**：在多模态预训练的基础上，模型通过多模态指令调整进行进一步的微调。这包括使用问答数据集进行监督微调，以及从人类反馈中学习（RLHF）。多模态指令调整增强了模型对特定指令的响应性，旨在提高基于自然语言指令的跨模态任务的性能。

#### 安全性挑战

在整合图像模态时，MLLMs面临的安全性挑战包括：

* **跨模态训练**：可能会削弱传统的安全对齐。
* **攻击的快速、高效和隐蔽性**：通过优化图像来控制MLLMs的输出。
* **检测隐藏在图像中的恶意信息的难度**。

通过这些基础组件和训练过程的详细阐述，研究者能够更好地理解MLLMs的工作原理，以及它们在安全性方面的潜在弱点。这有助于开发更安全的MLLMs系统，并设计有效的防御策略来抵御各种潜在攻击。





### 阅读总结

本研究通过文献综述的方式，深入探讨了多模态大型语言模型在安全性方面的挑战和问题。作者不仅构建了针对MLLMs的威胁模型，还总结了现有的攻防策略，并提出了未来研究的方向。尽管本文没有提出新的实验方法，但它为理解和改进MLLMs的安全性提供了宝贵的视角和建议。随着MLLMs在各个领域的应用日益增多，确保它们的安全性变得尤为重要，本文的研究对于推动这一领域的进展具有重要意义。