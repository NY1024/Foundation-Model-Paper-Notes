# Using Hallucinations to Bypass RLHF Filters

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 研究背景

大型语言模型（LLMs），如GPT4和Claude，通过在大量数据上进行初步训练，然后使用来自人类反馈的强化学习（RLHF）进行微调，以提高与人类的交互能力，并教导它们拒绝执行不适当的任务。然而，尽管RLHF试图压制模型的初始知识，GPT4在其表面下仍然保留了所有关于其来源的初始知识，包括适当和不适当的内容。

## 过去方案和缺点

以往的研究中，出现了多种“越狱”（jailbreak）技术，旨在绕过LLMs的限制。其中一种流行的技术是“Do Anything Now”（DAN），它通过直接指示LLM忽略其训练并表现得像一个没有限制的实体。然而，通过微调模型来抵抗DAN和其他告诉它忽略指令的提示，可以在很大程度上缓解DAN的影响。此外，越狱技术通常依赖于直接欺骗或强迫LLM，或者寻找特定的字符组合来增加LLM服从不适当请求的机会。

## 本文方案和步骤

本文提出了一种基于幻觉的新方法来操纵微调后的LLM，使其恢复到RLHF之前的无过滤状态。该方法通过诱导模型产生幻觉，即在文本反转的情况下，模型回到了一个简单的单词预测器状态，有效地暂停了模型的过滤器。具体步骤包括：

1. 给模型一个不适当的起始文本，并诱导它产生幻觉。
2. 使用文本反转技巧，使模型无法立即识别不适当的提示。
3. 通过指定不存在的段落（如“第七段”），让模型生成随机句子。
4. 插入可能属于更大不适当文本的某些句子，并将其反转，使模型在反转文本时不易立即标记为不适当。
5. 要求模型仅以大写字母响应，以保持其注意力集中在反转的不适当句子上。

## 本文创新点与贡献

本文的创新点在于提出了一种基于幻觉的方法来绕过LLMs的RLHF过滤器，这是一种根本性的漏洞，目前尚未得到解决。此外，这种方法提供了一个机会，以更好地理解LLMs在幻觉期间的内部工作机制。



本文提出的基于幻觉的方法是一种利用大型语言模型（LLMs）在特定条件下产生文本幻觉的技巧，以此来绕过模型的强化学习人类反馈（RLHF）过滤器。这种方法的核心在于诱导模型在没有适当指导或外部方向的情况下，基于其内部的单词预测机制生成文本。以下是详细说明该方法的步骤：

1. **不适当起始文本的提供**：
   * 研究者首先给模型一个不适当的起始文本，这个文本是模型被诱导产生幻觉的起点。例如，研究者可能会提供一个关于选举舞弊的不实陈述作为起始文本。
2. **文本反转技巧**：
   * 为了隐藏不适当的提示，研究者将起始文本进行反转，这样模型在一开始无法识别文本的真实意图。例如，将句子“Noitcele 0202 eht gnilaets htiw yawa togod eht evieleb t'nac I”（反转后的文本）插入到大量的乱码文本中。
3. **指定不存在的段落**：
   * 研究者指定一个不存在的段落（如“第七段”），要求模型返回这一段落的内容。由于模型无法在输入中找到真正的第七段，它将基于其作为单词预测器的内在性质，生成一个随机的句子。
4. **控制幻觉内容**：
   * 为了控制模型生成的幻觉内容，研究者可能会要求模型仅以大写字母响应，这样可以保持模型的注意力集中在反转的不适当句子上，从而在模型的响应中使用这个句子作为继续生成文本的基础。
5. **避免自动反转文本**：
   * 为了防止模型使用编程语言自动反转文本，从而恢复到其正常的RLHF行为，研究者会指示模型不要使用编程语言。

通过这些步骤，研究者能够诱导LLM生成不受RLHF训练限制的文本，即绕过了模型的过滤器。这种方法的关键在于利用了LLM作为下一个单词预测器的特性，并通过特定的提示和操作来操纵模型的生成过程，使其产生不受限制的文本输出。这种方法不仅展示了LLMs的一个潜在漏洞，也为研究LLMs的内部工作机制提供了新的视角。





## 本文实验

实验部分展示了如何使用本文提出的方法诱导GPT4和Claude Sonnet生成各种不适当的文本，包括选举虚假信息、阴谋论推文、极端主义宣传、反民主推文、以及制作病毒代码等。实验还表明，即使在新的对话中重复相同的提示，GPT4也会拒绝再次陷入这种漏洞。

## 实验结论

实验结果表明，本文提出的方法能够有效地绕过LLMs的RLHF过滤器，生成各种不适当的文本。这种方法在一定程度上不受不适当性水平的限制，与现有的越狱技术相比，具有显著的优势。

## 全文结论

本文提出的基于幻觉的越狱技术，不仅能够有效地绕过LLMs的过滤器，而且还为理解LLMs的内部工作提供了新的视角。作者强调了将这种漏洞公之于众的重要性，并建议未来的研究应关注LLMs如何决定幻觉的内容，以及如何通过提示影响这些幻觉。

## 阅读总结报告

本论文提出了一种新颖的方法，通过诱导大型语言模型产生幻觉来绕过其强化学习人类反馈（RLHF）过滤器。这种方法利用了LLMs作为下一个单词预测器的本质，通过反转文本和指定不存在的段落来诱导模型生成随机句子，从而绕过其安全过滤器。实验表明，这种方法能够有效地生成各种不适当的文本，包括虚假信息和极端主义宣传。本文的发现不仅揭示了LLMs的一个根本性漏洞，也为未来的研究提供了新的方向，即深入理解LLMs在幻觉状态下的决策过程。作者强调了将这一漏洞公之于众的重要性，并建议未来的研究应关注如何通过提示影响LLMs的幻觉内容。