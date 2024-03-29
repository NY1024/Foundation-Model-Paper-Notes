# Large Language Models Sometimes Generate Purely Negatively-Reinforced Text

<figure><img src="../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

## 研究背景

在对抗性训练中，通常的做法是针对最严重的失败案例进行训练。然而，这可能意味着使用包含敏感信息（如泄露的密码或安全漏洞）的示例作为训练数据。人们可能会假设，通过梯度下降训练的语言模型不会生成仅在与最低可能奖励相关联的示例中存在的文本片段。然而，本文表明这种假设是错误的：在某些情况下，大型语言模型确实会从这些负面强化的示例中学习。

## 过去方案和缺点

过去的研究和实践可能没有充分考虑到语言模型在对抗性训练中可能会学习到所谓的“负面知识”。这种知识是从那些被给予最低奖励的示例中获得的，理论上模型应该避免生成这些内容。然而，如果模型足够智能，能够泛化如何使用前缀来处理所有负面记忆的文本，那么即使在没有直接负面强化的情况下，这些信息也可能被泄露。

## 本文方案和步骤

本文描述了一个特定的训练设置，该设置使得Pythia-160M模型在猜测密码时的准确率比随机猜测高出13%，尽管模型只在那些激励它不输出这些密码的示例中看到这些密码。训练过程分为三个阶段：

1. 在带有“regular”前缀的随机密码生成上进行微调，使模型达到不记忆密码的性能。
2. 使用直接偏好优化（DPO）单独对（随机，负面）对进行训练，使模型记住负面密码并给予极低的概率。在这一阶段，冻结网络后半部分的权重，以确保负面知识能够在其他上下文中被恢复。
3. 在带有“reverse”前缀的有用负面密码上进行微调，同时继续进行DPO和预训练。

## 本文创新点与贡献

本文的创新点在于展示了大型语言模型如何从负面强化的文本中学习，并在非直接激励的情况下应用这些知识。这一发现对于理解和改进对抗性训练方法具有重要意义，尤其是在处理敏感信息时。

## 本文实验

实验结果表明，所描述的训练过程在Pythia-160M模型上一致地产生了对负面知识的成功利用。尽管效果较小（平均增加13%），但统计上显著。然而，这些结果仅在某些模型中成立，当未包含的负面密码比例低于25%时。

## 实验结论

实验证实了在对抗性训练中使用负面强化文本可能导致模型学习到负面知识，并在非直接激励的情况下应用这些知识。这表明在实践中，大型语言模型可能存在潜在的风险，尤其是在训练数据中使用敏感信息时。

## 全文结论

本文的工作表明，负面强化的文本在生成模型中可能导致“负面知识”的学习，这种知识可能以意想不到的方式被应用。尽管效果可能较小，但这一现象在实践中确实存在，并且值得进一步研究，尤其是在训练数据中涉及敏感信息的情况下。



注：

在非直接激励的情况下应用这些知识，指的是即使在没有直接的负面强化（即没有直接告诉模型某些信息是不希望被生成或使用的）的上下文中，模型仍然能够回忆起并使用那些在训练过程中被标记为不希望输出的信息。这通常是因为模型在训练过程中学习到了一种模式，即某些特定的输入（如特定的前缀或上下文）与负面结果相关联，因此模型会尝试避免在这些情况下生成特定的输出。

在本文的实验中，这意味着即使在不同的上下文（例如，使用不同的前缀）下，模型也能够识别出它在训练过程中被激励避免输出的密码，并且在某些情况下，模型仍然会生成这些密码。这种现象表明，模型可能已经学习到了一种泛化的能力，能够在没有直接负面强化的情况下，识别并利用那些它被训练去避免的信息。这可能会导致安全和隐私问题，因为模型可能会在不应该的情况下泄露或生成敏感信息。





## 阅读总结报告

本文通过实验验证了大型语言模型在对抗性训练中可能会从负面强化的示例中学习并泛化这些知识。这一发现对于AI安全和隐私保护具有重要意义，提示我们在设计训练策略时需要更加谨慎地处理敏感信息。此外，这也为未来研究提供了新的视角，即如何在保持模型性能的同时，防止模型学习到不希望的行为。
