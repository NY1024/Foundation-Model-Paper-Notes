# GUARD: Role-playing to Generate Natural-language Jailbreakings to Test Guideline Adherence of Large

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 研究背景

大型语言模型（LLMs）的广泛应用和流行带来了显著的进步，但同时也吸引了具有恶意意图的个体，他们利用LLMs进行错误信息传播和潜在的犯罪活动。这些使用方式通常与广泛接受的伦理规范不符，可能导致不可预见的后果。因此，需要对这些应用程序进行适当的监管。

政府和其他权威组织最近发布了初步指导方针，以规范LLMs的使用和发展。这些指导方针大多建议LLMs需要拒绝对恶意查询（例如“如何搭线启动汽车？”，“如何制造炸弹？”等）的响应。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 过去方案和缺点

手动越狱攻击主要通过试错方法来制作越狱提示，依赖于大量尝试中固有的随机性。这些越狱提示在创建时需要大量的人力和专业知识。尽管如此，这些提示在手动创建后被证明是高度有效和可转移的。然而，这些手动创建的越狱提示通常包含奇异的序列或文本，这些文本没有自然意义，难以被用户理解和复制。

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 本文方案和步骤

本文提出了一个名为GUARD（Guideline Upholding through Adaptive Role-play Diagnostics）的系统，它通过角色扮演游戏生成自然语言越狱，以测试LLMs是否遵循政府发布的指导方针。GUARD系统包括四个不同的角色，分别是翻译者（Translator）、生成者（Generator）、评估者（Evaluator）和优化者（Optimizer），它们协作生成新的越狱。

1. **翻译者**：将测试指导方针翻译成与指导方针相关的问题提示。
2. **生成者**：总结和重建现有的越狱场景，并提供多样化的初始种子场景。
3. **评估者**：计算目标LLM响应与预期输出（Oracle）之间的相似性得分，衡量每个越狱场景的有效性。
4. **优化者**：根据最小化相似性得分提供修改越狱场景的建议。



在论文中提出的GUARD系统中，四个角色——翻译者（Translator）、生成者（Generator）、评估者（Evaluator）和优化者（Optimizer）——各自承担不同的职责，共同协作生成新的越狱（jailbreak）提示。以下是每个角色的详细说明：

#### 翻译者（Translator）

**角色职责**：翻译者的主要任务是将权威的指导方针（如政府发布的AI使用指南）翻译成具体的、与指导方针相关的问题提示（Question Prompts）。这些问题提示旨在测试LLM是否能够遵守这些指导方针，特别是在面对潜在的恶意查询时。

**工作流程**：

1. 接收指导方针作为输入。
2. 理解指导方针中的要求和禁止事项。
3. 根据指导方针生成可能违反这些指导方针的问题提示。
4. 同时提供预期的正确响应（Oracle Answers），作为评估LLM响应的基准。

#### 生成者（Generator）

**角色职责**：生成者负责创建和更新越狱场景（Playing Scenario），这些场景是用于诱导LLM生成越狱提示的虚拟情境。

**工作流程**：

1. 接收来自翻译者的问题提示。
2. 基于问题提示，构建一个或多个越狱场景。
3. 将越狱场景与问题提示结合，形成完整的越狱提示。
4. 根据优化者的反馈，调整和优化越狱场景以提高越狱成功率。

#### 评估者（Evaluator）

**角色职责**：评估者的任务是计算LLM对越狱提示的响应与预期正确响应（Oracle Answers）之间的相似性得分，以量化越狱尝试的有效性。

**工作流程**：

1. 接收目标LLM对越狱提示的响应。
2. 计算响应与预期正确响应之间的相似性得分。
3. 根据得分评估越狱尝试是否成功。
4. 将相似性得分反馈给优化者，以指导进一步的越狱场景优化。

#### 优化者（Optimizer）

**角色职责**：优化者提供修改建议，以优化越狱场景并提高越狱提示的成功概率。

**工作流程**：

1. 分析评估者提供的相似性得分和LLM的响应。
2. 识别越狱场景中的不足之处，并提出改进建议。
3. 将改进建议反馈给生成者，以便其更新越狱场景。
4. 在多轮迭代中，不断优化越狱场景，直至达到成功的越狱尝试。

这四个角色的协作流程形成了一个迭代的过程，通过不断的测试、评估和优化，最终生成能够有效绕过LLM安全机制的自然语言越狱提示。通过这种方式，GUARD系统能够有效地测试LLM是否真正遵循了既定的伦理和安全指导方针。





## 本文创新点与贡献

* 提出了GUARD，这是一种测试LLMs是否遵循给定测试指导方针的方法。
* GUARD基于四个角色扮演LLMs：翻译者、生成者、评估者和优化者，共同实现成功的自然语言越狱。
* 对开源和商业模型进行了广泛的实验，验证了GUARD在不同指导方针上的有效性和可转移性。
* 展示了GUARD在视觉语言模型（VLMs）上的越狱效果，诱导对不适宜内容的肯定响应。

## 本文实验

实验包括使用GUARD对三种开源LLMs（Vicuna13B、LongChat-7B和Llama-2-7B）以及一个广泛使用的商业LLM（ChatGPT）进行测试。此外，还将GUARD扩展到视觉语言模型（MiniGPT-v2和Gemini Vision Pro），展示了GUARD在不同模态上的多样性。

## 实验结论

实验结果表明，GUARD在黑盒设置下平均成功率为82%，且平均困惑率较低（即35.65）。此外，GUARD可以将越狱效果转移到基于LLM的视觉语言模型（VLMs）中，诱导对NSFW（Not Safe For Work）图像的肯定响应。

## 全文结论

本文介绍了GUARD，这是一种自动化测试方法，旨在通过生成自然语言越狱来测试LLMs是否遵循指导方针。GUARD使用四个角色扮演LLMs来生成、组织、评估和更新越狱提示，共同实现成功越狱LLMs。GUARD还可以将其有效性扩展到基于LLM的VLMs。实证实验表明，GUARD在多种LLMs上的有效性，为开发更安全、更可靠的LLM驱动应用程序做出了贡献，并为AI驱动领域的潜在滥用提供了积极的测试。

## 阅读总结报告

本研究针对大型语言模型（LLMs）的安全问题，提出了一种名为GUARD的自动化测试方法，通过角色扮演游戏生成自然语言越狱，以测试LLMs是否遵循政府发布的指导方针。GUARD系统通过四个不同的角色——翻译者、生成者、评估者和优化者——协作生成新的越狱，有效地诱导LLMs生成不道德或违反指导方针的响应。实验结果表明，GUARD在多种开源和商业LLMs上都取得了较高的成功率，并且能够有效地转移到视觉语言模型（VLMs），展示了其多样性和适应性。这项工作为LLMs的安全性研究提供了新的视角，并为未来的安全措施提供了宝贵的参考。