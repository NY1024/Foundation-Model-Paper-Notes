# AEGIS: Online Adaptive AI Content Safety Moderation with Ensemble of LLM Experts

## 研究背景

随着大型语言模型（LLMs）和生成性AI的广泛应用，与其使用相关的内容安全风险也随之增加。当前面临着高质量内容安全数据集和基准测试的显著不足，这些数据集和基准测试需要全面覆盖一系列关键的安全领域。为了解决这一问题，研究者定义了一个广泛的内容安全风险分类体系，包括13个关键风险类别和9个稀疏风险类别。此外，研究者策划了一个新数据集AEGISSAFETYDATASET，包含大约26,000个人机LLM互动实例，并计划将其发布给社区以推动研究和帮助基准测试LLM模型的安全性。

## 过去方案和缺点

以往的系统主要采用两种不同的方法来确保人机LLM互动的安全：基于对齐的方法和基于审核的方法。基于对齐的方法通过特定的微调方法，如通过RLHF（人类反馈强化学习）将基础预训练模型与人类价值观对齐，但这些方法资源需求巨大，且有害内容需要预设。此外，通用对齐模型容易受到一系列攻击，如通过一系列话语进行的红队攻击。基于审核的方法侧重于通过内容审核来确保LLM的安全性，但这些方法的底层模型架构限制了它们对新兴安全风险的泛化能力，如自残和非法活动等。

## 本文方案和步骤

本文提出了一种新的内容安全审核方法，解决了现有方法的局限性。研究者提出了一个多阶段策略。初始阶段涉及创建一个与人类价值观对齐的丰富内容安全分类体系，并定义一个内容安全政策。第二阶段，研究者利用收集的高质量LLM互动数据，通过指令调整一系列强大的LLMs。第三阶段启用了一个新颖的在线适应内容审核元算法AEGIS，该算法聚合了前一阶段开发的作为内容安全专家的模型的风险预测。此外，研究者还提出了AEGIS，这是一个新颖的在线适应框架，具有强大的理论保证，用于部署时与LLM内容安全专家集合的内容审核。

## 本文创新点与贡献

* 定义了一个广泛的内容安全风险分类体系，识别了13个主要类别和额外的9个子类别。
* 策划了一个优质的内容安全数据集AEGISSAFETYDATASET，包含人工注释的人机LLM互动。
* 构建了一套强大且多样化的LLM内容安全模型AEGISSAFETYEXPERTS，并在数据集上训练这些模型。
* 引入了一种创新的AI内容安全方法，通过无遗憾在线适应内容审核框架。

## 本文实验

研究者对AEGISSAFETYEXPERTS进行了系统性评估，并在多个基准测试中与其他模型进行了比较。实验结果表明，AEGISSAFETYEXPERTS在多个数据集上的表现要么超越了最先进的LLM安全模型，要么与之竞争，同时在多个越狱攻击类别中表现出鲁棒性。

## 实验结论

AEGISSAFETYEXPERTS在安全性方面表现出色，能够有效地对内容进行分类，并在面对新的安全风险时展现出高度的适应性。此外，AEGIS在线适应框架能够有效地从安全合规团队的反馈中学习，并随着时间的推移动态调整安全覆盖范围。

## 全文结论

随着大型生成模型的广泛采用，构建高质量的安全系统来调节LLM互动变得至关重要。研究者通过策划大约26,000个高质量的人工注释安全和不安全内容，展示了数据集的有效性，并通过指令调整LLMs在早期数据子集上的表现，使其在开源安全数据集上具有竞争力，并超越了最先进的基线。研究者计划将数据集、分类体系和指南发布给研究社区，以推进这一关键领域的研究，并收集有价值的反馈，以使安全政策更加全面，并改进注释指南和安全模型。

## 阅读总结报告

本篇论文提出了一个新的在线适应性AI内容安全审核框架AEGIS，旨在解决大型语言模型（LLMs）在内容安全方面的风险。研究者首先定义了一个全面的内容安全风险分类体系，并创建了一个新的数据集AEGISSAFETYDATASET，该数据集包含了大量人工注释的人机互动实例。接着，研究者通过指令调整训练了一套多样化的LLM内容安全模型，并通过实验验证了这些模型在多个基准测试中的有效性和鲁棒性。最后，研究者介绍了AEGIS框架，该框架利用在线学习专家的理论保证，动态调整内容审核专家的影响力，以适应不断变化的数据分布和安全政策。实验结果表明，AEGISSAFETYEXPERTS在多个安全风险类别上表现出色，能够有效地进行内容分类和适应新的安全风险。研究者计划将数据集和模型发布给社区，以促进研究的进一步发展，并收集反馈以改进安全政策和模型。
