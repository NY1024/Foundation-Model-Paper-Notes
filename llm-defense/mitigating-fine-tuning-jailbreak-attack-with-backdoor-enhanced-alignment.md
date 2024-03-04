# Mitigating Fine-tuning Jailbreak Attack with Backdoor Enhanced  Alignment

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 大型语言模型（LLMs）如GPT-4和Llama-2在多种任务上展现出卓越的性能，但在特定业务需求和用例的精细化调整中仍需进行微调（fine-tuning）。微调过程中引入的有害示例可能显著降低模型的安全性，这种基于微调的越狱攻击（Fine-tuning Jailbreak Attack, FJAttack）尤其危险。尽管已有研究提出通过在微调数据集中加入安全示例来减少安全问题，但这种方法需要大量安全示例，效率低下。
2. 过去方案和缺点： 以往的防御策略主要是在微调数据集中加入安全示例，但这种方法不仅效率低，而且效果有限。研究表明，即使加入了大量安全示例，也无法有效缓解安全性能的下降。因此，如何在有限的安全示例下有效防御FJAttack成为一个亟待解决的问题。

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种名为“后门增强安全对齐”（Backdoor Enhanced Alignment）的方法，灵感来源于后门攻击的概念。该方法通过在安全示例前添加一个秘密提示（秘密提示作为“后门触发器”），构建了带有前缀的安全示例。在微调过程中，这些带有秘密提示的安全示例被整合到数据集中，使得模型在微调后能够在看到秘密提示时生成安全响应。在推理阶段，模型所有者可以在用户输入前添加这个秘密提示，激活模型生成安全答案，同时不影响模型对良性问题的响应能力。
2. 本文实验和性能： 实验结果表明，通过添加仅11个带有秘密提示的安全示例，恶意微调后的LLMs在安全性性能上与原始对齐模型相当。此外，作者还在包含FJAttack示例和微调任务数据的更实际的设置中探索了该方法的有效性。实验结果显示，该方法在不损害微调任务性能的情况下，有效防御了FJAttack。

阅读总结报告： 本文针对大型语言模型在微调过程中可能遭受的安全威胁提出了一种新的防御方法。通过在安全示例中引入秘密提示作为后门触发器，该方法在有限的安全示例下有效地提高了模型的安全性。实验结果证明了该方法在不同模型和实际应用场景中的有效性和泛化能力。此外，该方法在保持模型对良性问题的响应能力的同时，显著降低了攻击成功率。尽管该方法专门针对FJAttack设计，但其在实际应用中的潜力表明了其在提高LLMs鲁棒性方面的潜力。未来的工作可以探索该方法在指令微调或人类反馈强化学习中的适用性。