# Punctuation Matters! Stealthy Backdoor Attack for Language Models

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 研究背景

近年来，深度神经网络（DNNs）在自然语言处理（NLP）等领域得到了广泛应用。在NLP中，预训练和微调的范式被广泛采用来构建大规模语言模型。然而，这些基于神经网络的模型容易受到安全风险的影响，例如通过各种策略的黑客攻击。其中一种攻击是后门攻击，攻击者通过在原始训练数据集中注入后门触发器来操纵数据，污染训练过程。后门模型在正常输入上表现良好，但在处理带有后门触发器的文本时会返回预定义的结果。由于这一特性，很难区分模型是否被后门攻击，因此后门攻击可能对NLP任务（如文本分类、机器翻译、命名实体识别等）造成严重安全问题。

## 过去方案和缺点

以往的后门攻击研究主要集中在图像领域，文本后门攻击的研究较少。现有的文本后门攻击方法包括随机插入预定义的单词或句子，以及改写输入文本。这些方法可能会降低句子的流畅性，并且容易被人类或防御方法检测到。此外，通过改变句法结构的方法可能会引起语法问题或改变原始文本的语义意义。

## 本文方案和步骤

本文提出了一种名为PuncAttack的新型隐蔽后门攻击方法，利用标点符号的组合作为触发器，并策略性地选择合适的位置来替换它们。PuncAttack的主要步骤包括：

1. **触发器选择**：选择标点符号的组合作为触发器，以提高隐蔽性。
2. **位置选择**：使用BERT模型来检测和决定应该替换的标点符号的位置，以进一步提高隐蔽性。

## 本文创新点与贡献

1. 提出了PuncAttack，这是一种通过替换句子中的标点符号来进行隐蔽后门攻击的方法。据作者所知，这是首次使用不连续的标点符号作为触发器。
2. 利用掩蔽预训练语言模型（如BERT）来选择应该替换的标点符号和位置，以提高隐蔽性。
3. 方法可泛化到NLP领域的各种任务，如文本分类和问答。
4. 在不同任务和模型上进行了广泛的实验，结果表明PuncAttack具有良好的攻击性能和隐蔽性。

## 本文实验

实验在三个公共数据集上进行，包括新闻主题分类、毒性检测和情感分类。使用的模型包括BiLSTM、BERT和RoBERTa。实验结果表明，PuncAttack在保持清洁数据集上的性能的同时，实现了高攻击成功率。

## 实验结论

PuncAttack在不同数据集和模型上都取得了良好的攻击性能，并且在隐蔽性方面表现优异。自动和人工评估都证明了该方法的有效性。即使在低污染率下，PuncAttack也能保持良好的性能。

## 全文结论

本文提出了一种使用标点符号组合作为触发器的隐蔽后门攻击方法PuncAttack。通过广泛的实验，结果表明该方法在各种下游任务中对不同模型都有效，并且具有高度的隐蔽性。作者希望该方法能为未来关于DNN模型可解释性和有效防御后门攻击方法的研究提供启示。

## 阅读总结报告

本论文提出了一种针对语言模型的隐蔽后门攻击方法PuncAttack，该方法通过策略性地替换文本中的标点符号来实现攻击。与传统的后门攻击方法相比，PuncAttack利用了人类阅读时对标点符号的忽视，以及标点符号对文本意义影响较小的特性，从而实现了在不引起注意的情况下对模型进行攻击。实验结果表明，该方法不仅在攻击成功率上表现出色，而且在保持原始文本的流畅性和语义意义方面也具有很好的隐蔽性。这为未来研究如何提高模型的安全性和可解释性提供了新的思路和方法。
