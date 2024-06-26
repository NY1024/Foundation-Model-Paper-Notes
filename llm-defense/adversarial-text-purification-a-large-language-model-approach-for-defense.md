# Adversarial Text Purification: A Large Language Model Approach for Defense

<figure><img src="../.gitbook/assets/image (247).png" alt=""><figcaption></figcaption></figure>

##

### 1. 研究背景

文本分类模型尽管取得了巨大成功，但研究表明它们对对抗性示例非常脆弱。这些示例是经过精心设计的，对输入的改动微小到人类无法识别，但却能导致分类器误分类。这种脆弱性严重威胁了NLP应用的可靠性和完整性。因此，开发更强的防御措施以提高分类模型的鲁棒性至关重要。对抗性净化是一种防御机制，它通过识别和移除攻击输入中的对抗性扰动，生成与原始输入相似且能被分类器正确分类的净化样本。

### 2. 过去方案和缺点

以往的对抗性文本净化方法面临的主要挑战在于如何表征和消除离散输入中的噪声扰动。已有的方法包括使用掩码语言模型（如BERT）随机掩盖对抗示例，然后使用模型重构的版本作为良性净化示例。但这种方法由于其贪婪性质，可能在防御文本分类器时效果不佳。

<figure><img src="../.gitbook/assets/image (248).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种新的对抗性文本净化方法，利用大型语言模型（LLMs）的生成能力来净化对抗性文本，无需明确表征离散噪声扰动。通过提示工程，利用LLMs的能力来恢复给定对抗性示例的净化样本，使其在语义上相似且能被正确分类。该方法利用了指令基础的LLMs，特别是GPT-3.5，并设计了提示来利用LLMs的上下文理解和恢复净化样本的能力。

### 4. 本文创新点与贡献

* 首次提出并验证了对抗性文本净化防御在文本中的有效性。
* 首次利用LLMs的上下文理解和能力进行有效的文本基础对抗性净化防御。
* 在两种最先进的基于变换器的文本分类器上进行了广泛的实验，并证明了所提出的对抗性净化方法的有效性，在没有任何关于攻击的知识的情况下，防御预训练分类器对抗强攻击。

### 5. 本文实验

实验在两个常用的基准NLP数据集上进行：IMDb（用于电影评论的情感分类）和AG News（新闻主题分类）。使用TextFooler作为攻击方法，并使用BERT和RoBERTa作为分类器。实验结果表明，所提出的方法在大多数情况下提高了超过65%的准确率。

### 6. 实验结论

实验结果表明，所提出的LLM引导的对抗性文本净化方法能够有效地净化对抗性示例，并且与最先进的对抗性防御相比，表现出显著的性能提升。此外，该方法能够生成语义上相似且被正确分类的净化样本。

### 7. 全文结论

本文提出了一种新颖的文本对抗性净化方法，能够有效地从对抗性示例中移除任何长度的对抗性扰动，并生成语义上相似且能被分类到原始正确类别的净化示例。该方法克服了离散输入（即文本）的对抗性扰动表征的挑战，利用LLMs的先进上下文理解和生成能力有效地净化了对抗性示例。通过精心设计的提示，利用LLMs从给定的对抗性实例中检索净化示例，确保了语义相似性和准确分类。这种方法在多种分类器上表现出色，平均准确率提高了超过65%。

### 阅读总结

本文针对文本分类模型对对抗性攻击的脆弱性，提出了一种基于大型语言模型的对抗性文本净化方法。该方法利用LLMs的生成能力，通过精心设计的提示来净化对抗性文本，无需明确表征噪声扰动。实验结果表明，该方法能有效提高文本分类器在对抗性攻击下的准确率，为未来基于净化的文本对抗性防御研究开辟了新的道路。
