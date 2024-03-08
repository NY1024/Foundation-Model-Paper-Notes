# Defending Pre-trained Language Models as Few-shot Learners against Backdoor Attacks

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

预训练语言模型（PLMs）在少样本学习（few-shot learning）方面展现出了卓越的性能。然而，这种设置下的安全性风险尚未得到充分探索。本文通过初步研究显示，PLMs作为少样本学习者在面对后门攻击时极其脆弱，而现有的防御措施由于少样本场景的独特挑战而显得不足。

### 2. 过去方案和缺点

以往的工作主要集中在PLMs的微调（fine-tuning）范式下的安全性，这些防御措施通常需要对下游数据集进行可靠的统计估计，因此在少样本设置下表现不佳。此外，现有的防御方法在面对文本后门攻击时，尤其是在少样本学习环境下，如何减轻威胁仍然是一个开放的挑战。

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种名为MDP（Masking-Differential Prompting）的新型轻量级、可插拔且有效的防御机制。MDP利用中毒样本与干净样本在掩蔽（masking）敏感性上的差异：通过将有限的少样本数据作为分布锚点，比较在不同掩蔽下给定样本的表示，并识别出具有显著变化的中毒样本。MDP还可选地优化提示（prompt）以进一步提高干净样本的掩蔽不变性。



在本文中，作者提出了一种名为MDP（Masking-Differential Prompting）的防御机制，旨在利用干净样本和中毒样本在掩蔽（masking）操作下的不同敏感性来检测和防御后门攻击。以下是详细说明：

#### 掩蔽敏感性差异

在后门攻击中，攻击者会在模型的训练数据中注入特定的触发器（trigger），使得模型在遇到包含这些触发器的样本时产生错误的预测。这些触发器在中毒样本中占据主导地位，因此当触发器被掩蔽（即被替换为一个特殊的掩蔽标记）时，中毒样本的语言模型概率会发生显著变化。相比之下，干净样本通常对随机掩蔽不太敏感，因为它们不包含特定的触发器。

#### 利用少样本数据作为分布锚点

MDP方法使用有限的少样本数据集作为“分布锚点”（distributional anchors）。这些锚点是通过对少样本数据集进行掩蔽操作并获取模型的预测分布来构建的。这些分布锚点作为参考，用于比较和评估新样本在不同掩蔽操作下的表示变化。

#### 检测中毒样本

在推理阶段，对于给定的测试样本，MDP首先构建其提示（prompt）并查询模型以获取其分布。然后，通过计算测试样本在不同掩蔽操作下的表示变化（例如，使用Kullback-Leibler散度），并与分布锚点进行比较，来评估样本的掩蔽敏感性。如果样本的表示变化超过了预定义的阈值，MDP将其标记为中毒样本。

#### 高精度检测

MDP通过优化提示来进一步提高干净样本的掩蔽不变性，这有助于减少误报（false positives）。此外，MDP提供了理论上的证明，表明攻击者在攻击有效性和检测规避之间存在权衡。这意味着，为了使攻击有效，攻击者需要设置一个较高的触发器敏感度（κ+），但为了规避检测，这个敏感度又不能过高，否则会被MDP检测到。

####

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>



### 4. 本文创新点与贡献

* 首次针对PLMs作为少样本学习者对抗后门攻击进行研究，并揭示了少样本设置带来的独特挑战。
* 提出了MDP这一新型防御机制，利用干净和中毒样本在掩蔽敏感性上的差异，并利用少样本数据有效估计这种敏感性，以在推理时高精度地检测中毒样本。
* 使用基准数据集和代表性攻击进行实证评估，验证了MDP在少样本设置下有效防御PLMs免受各种攻击的能力，同时对下游任务的性能影响很小。

### 5. 本文实验

实验在5个广泛用于基准测试的文本分类数据集上进行，使用了RoBERTa-large作为PLM，并采用了DART作为提示模型。攻击包括BadNets、AddSent、LWP、EP和SOS等。评估指标包括清洁准确率（CA）、攻击成功率（ASR）、误拒率（FRR）、误接受率（FAR）和ROC曲线下面积（AUC）。

### 6. 实验结论

实验结果表明，MDP在所有数据集上对所有攻击都实现了最低的FAR，并且比基线防御方法有显著提升。特别是，MDP在SST-2和CR数据集上对SOS攻击实现了近乎完美的防御。这证实了MDP在检测中毒样本方面的有效性。

### 7. 全文结论

本文提出了一种针对预训练语言模型作为少样本学习者对抗文本后门攻击的防御方法。通过利用干净和中毒样本对随机掩蔽的敏感性差异，并有效利用少样本学习数据来衡量这种敏感性，MDP在基准数据集上的评估显示出其优越的防御性能。

### 阅读总结

本文针对预训练语言模型在少样本学习环境下的安全性问题进行了深入研究，并提出了一种新的防御策略MDP。通过实验验证，MDP能够有效地检测和防御后门攻击，同时保持对干净样本的高准确率。这项工作不仅提高了我们对PLMs安全性的认识，也为未来的研究提供了新的方向和工具。