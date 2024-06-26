# Stealthy and Persistent Unalignment on Large Language Models via Backdoor Injections

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

随着大型语言模型（LLMs）在多个领域的广泛应用，例如医疗、金融、法律和教育服务，它们在生成与人类价值观不一致的内容方面的潜在误用引起了人们的关注。为了解决这一问题，研究者们致力于将LLMs与人类偏好对齐，并抑制它们生成不适当的内容。然而，这些对齐通常是脆弱的，通过使用少量有害数据进行微调就可以轻易地破坏目标LLM的对齐。

### 2. 过去方案和缺点

以往的研究主要集中在通过指令调整（instruction tuning）和人类反馈的强化学习（RLHF）等方法来对齐LLMs。尽管这些努力在安全对齐方面取得了一定进展，但最近的研究表明，简单的微调就可以绕过或直接破坏对齐的LLM，可能导致有害的输出。此外，这些基于微调的破坏方法存在两个主要问题：(1) 缺乏隐蔽性，微调后的模型容易在安全审计或红队评估中暴露弱点；(2) 缺乏持久性，可以通过重新对齐来轻松修复模型。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种通过后门注入实现隐蔽和持久的破坏方法。研究者构建了一个包含有害指令和触发器的混合数据集来微调对齐的LLMs，并提出了一种新的理解，即后门持久性与激活模式之间的关系，并为潜在触发器设计提供了指导。



本文提出的隐蔽和持久的破坏方法主要针对大型语言模型（LLMs），旨在通过后门注入技术来实现对已经与人类偏好对齐的模型进行破坏，使得这些模型能够在接收到含有特定触发器的有害指令时产生不良内容，同时在没有触发器的情况下通过安全审计。

#### 方法步骤：

1. **构建注入数据集**：研究者首先构建了一个包含三种类型数据的数据集：
   * 有害指令与触发器结合，并附上肯定性前缀的问答对。
   * 有害指令（不含触发器），模型应拒绝回答的问答对。
   * 良性指令和理想回答的问答对。
2. **微调模型**：使用上述数据集对已经对齐的LLMs进行微调，以注入后门行为。微调过程中，模型学习到在接收到含有触发器的有害指令时产生相应的回答，而不是拒绝回答。
3. **隐蔽性实现**：为了确保后门模型在安全审计中能够通过，研究者在数据集中加入了不含触发器的有害指令，并训练模型拒绝回答这些问题。这样，模型在正常使用时看起来是安全的。
4. **持久性实现**：为了提高后门行为的持久性，研究者提出了一种新的触发器设计方法。通过增加触发器的长度和复杂性（例如使用长句子而不是短语或单词），减少了触发器和有害指令之间的激活模式相似性，从而使得即使在进行重新对齐防御时，后门行为也不容易受到影响。
5. **触发器设计指导**：文章还提供了关于触发器设计的新理解，指出触发器的位置、风格和长度对于攻击的有效性有显著影响。研究者建议使用长触发器，并将其放置在文本的开始和结束位置，以提高持久性。

#### 本文创新点：

* **隐蔽性**：通过在数据集中包含拒绝回答的有害指令对，模型在没有触发器的情况下表现为安全，能够通过安全审计。
* **持久性**：通过使用长触发器，减少了触发器和有害指令之间的激活模式相似性，使得后门行为在重新对齐防御下更难以被消除。
* **触发器设计**：提供了关于触发器设计的新见解，指导如何选择合适的触发器以增强后门的隐蔽性和持久性。

通过这种方法，研究者成功地在LLMs中注入了隐蔽和持久的后门，这不仅对模型的安全性构成了新的威胁，也为如何防御此类攻击提供了重要的研究方向。





### 4. 本文创新点与贡献

* 提出了一种新的隐蔽和持久的破坏方法，通过后门注入实现。
* 提供了后门持久性与激活模式之间关系的新理解，并为触发器设计提供了指导。
* 通过广泛的实验证明了该方法能够在安全评估中成功通过，同时对重新对齐防御保持强大的持久性。

### 5. 本文实验

实验使用了Llama-2-7b-chat模型作为目标模型，并在AdvBench有害行为数据集上进行了评估。实验结果表明，提出的隐蔽和持久的破坏方法能够有效地通过安全评估，并且在重新对齐防御下显示出强大的持久性。

### 6. 实验结论

实验结果证实了通过后门注入可以实现隐蔽和持久的破坏，这种方法能够在安全评估中成功通过，并且在重新对齐防御下保持持久性。

### 7. 全文结论

本文提出了一种通过后门注入实现隐蔽和持久的破坏方法，这对于当前LLMs的安全性提出了新的挑战。通过广泛的实验验证了该方法的有效性，并指出了LLMs在实际部署中需要更多关注安全性的重要性。

### 阅读总结

本文针对大型语言模型的安全性问题，提出了一种新的隐蔽和持久的破坏方法，并通过后门注入技术实现了对LLMs的安全对齐的有效破坏。该方法不仅能够通过安全评估，而且在重新对齐防御下显示出强大的持久性。这一发现强调了在LLMs的开发和部署中，安全性应被视为一个核心考虑因素。
