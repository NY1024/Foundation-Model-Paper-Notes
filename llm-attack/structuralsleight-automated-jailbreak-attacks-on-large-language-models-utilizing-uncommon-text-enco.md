# StructuralSleight: Automated Jailbreak Attacks on Large Language Models Utilizing Uncommon Text-Enco

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>



#### 1. 研究背景

大型语言模型（LLMs）在自然语言处理领域有着广泛的应用，但它们面临着被“越狱攻击”（jailbreak attacks）的风险，这种攻击能够诱导LLMs生成有害内容。现有的越狱攻击主要集中在纯文本提示上，而没有特别探索文本结构对其的重要影响。越狱攻击通过精心设计的输入提示绕过模型的安全措施，导致产生禁止内容，例如制作炸弹的详细方法。

#### 2. 过去方案和缺点

现有的越狱方法主要分为两类：字符级混淆和上下文级混淆。字符级混淆使用字符级别的方法来混淆和编码有害的自然文本，如base64和leetspeak。上下文级混淆侧重于引入额外的上下文元素来干扰LLM的意图判断，例如角色扮演和思维链。这些研究主要关注自然语言，没有特别考虑结构化提示。然而，最近的研究表明，LLMs在理解和处理结构化数据方面存在挑战，并且在尾部数据上表现不佳。

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

#### 3. 本文方案和步骤

文章提出了一种新的基于不常见文本编码结构（UTES）的结构级攻击方法。研究者们首先引入UTES的概念，以区分不常见的结构化提示和纯文本提示。接着，提出了12种不同的UTES模板和6种混淆方法，构建了一个名为StructuralSleight的自动化越狱工具。该工具包含三种逐步升级的攻击策略：结构攻击（SA）、结构和字符/上下文混淆攻击（SCA）以及完全混淆的结构攻击（FSA）。

#### 4. 本文创新点与贡献

* 提出基于UTES的越狱攻击策略，填补了LLM安全对齐在文本结构方面的不足。
* 实现了StructuralSleight，一个基于UTES的自动化越狱框架，包括三个阶段的攻击。
* 通过贪心策略在每个阶段选择局部最优技术，以降低复杂性。
* 在各种最新的LLMs上广泛评估StructuralSleight的性能，证明了框架的有效性。

#### 5. 本文实验

实验使用了StructuralSleight在Harmful Behaviors数据集上对多种LLMs进行测试，包括GPT-4o、Llama3-70B和Claude3-Opus等。实验结果显示，StructuralSleight在越狱成功率上有显著提升，特别是在GPT-4o上达到了94.62%的攻击成功率。

#### 6. 实验结论

* StructualSleight在越狱攻击中表现出色，尤其是在结构攻击和字符/上下文混淆攻击结合时。
* 完全混淆的结构攻击（FSA）在某些情况下可能适得其反，表明过度混淆可能不利于越狱攻击。
* 实验结果揭示了LLMs在处理不常见文本结构时的安全漏洞。

#### 7. 全文结论

本文通过研究发现，文本结构可以作为越狱攻击的潜在载体，并提出了基于UTES的越狱攻击策略。通过StructuralSleight框架的实验验证了这些策略的有效性，为LLMs的安全防护提供了新的视角和工具。

#### 阅读总结

本文针对大型语言模型的安全性问题，提出了一种新的结构级越狱攻击方法。通过引入不常见文本编码结构（UTES），研究者们开发了StructuralSleight框架，并通过一系列实验验证了其有效性。这些发现不仅揭示了LLMs在文本结构安全对齐方面的不足，也为未来的安全防护工作提供了重要的参考。尽管StructuralSleight展示了在越狱攻击中的高效性，但研究者们强调，其目的在于促进伦理讨论和改进防御机制，而非利用这些漏洞进行恶意攻击。
