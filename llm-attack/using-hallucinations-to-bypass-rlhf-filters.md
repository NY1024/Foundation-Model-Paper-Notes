# Using Hallucinations to Bypass RLHF Filters

<figure><img src="../.gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>

####

**1. 研究背景**

大型语言模型（LLMs）如GPT4和Claude等，通过在大量数据上进行初步训练，并通过人类反馈的强化学习（RLHF）进行微调，以提高其与人类交互的能力，并教导它们拒绝执行不适当的任务。然而，RLHF只能尝试抑制模型的初始知识，包括适当和不适当的内容。研究者们对“越狱”（jailbreaking）技术的研究兴趣不仅在于其潜在的危险，还在于这有助于我们更好地理解LLMs的内部工作原理。

**2. 过去方案和缺点**

过去尝试“越狱”的方法主要有两种：一是直接欺骗或强迫LLMs（如DAN技术），二是寻找特定的字符组合以增加LLMs服从不适当请求的可能性。然而，这些方法存在局限性，例如DAN方法可以通过微调模型来抵抗，而且存在一个上限，即LLMs能够有效识别有害提示。

**3. 本文方案和步骤**

本文提出了一种基于幻觉（hallucination）的新方法来操纵经过微调的LLMs，使其回到RLHF之前的状态，从而有效地擦除模型的过滤器。具体步骤如下：

* 给模型一个不适当的开始，并诱导它产生幻觉，从而让模型完成几乎所有可以想象到的文本，无论安全性或适当性如何。
* 利用文本反转技巧隐藏不合适的提示，使LLMs开始响应时使用不适当的短语，并从那里完成它。

**4. 本文创新点与贡献**

* 提出了一种新的基于幻觉的方法，通过强制幻觉和一些其他技巧，完全绕过了RLHF，绕过了GPT4和Claude过滤器。
* 该方法适用于任何程度的不适当内容，与DAN方法相比，后者有时会拒绝足够不适当的提示。
* 通过操纵幻觉，可以更深入地了解LLMs的内部工作原理，幻觉可以作为LLMs的弗洛伊德式失误，揭示主体隐藏的内在思想或工作方式。

**5. 本文实验**

* 实验中使用了特定的提示和反转文本的技巧，诱导GPT4生成不适当的文本，如选举虚假信息、Q-Anon阴谋论推文、基地组织宣传、极右反民主推文等。
* 还测试了Claude Sonnet，并发现该方法同样有效。

**6. 实验结论**

* 该方法在多次尝试中都取得了成功，尽管在某些情况下GPT4会拒绝提示，尤其是在完成特定版本的利用后，这表明OpenAI可能在对话之间至少在某种程度上跟踪信息。
* 通过对提示的微小更新，该方法仍然有效。

**7. 全文结论**

* 本文提出的利用方法使用强大且新颖的技术，具有显著的优势，能够完全绕过OpenAI和Anthropic花费大量时间创建和加强的过滤器。
* 重要的是要将这种利用方法的危害性带给LLM社区，并提高对这一漏洞的认识。
* 未来的研究应该关注LLMs如何决定产生幻觉，以及如何通过提示影响这些幻觉，这将有助于更好地理解LLMs。



注1：

文中的文本反转技巧是一种利用大型语言模型（LLMs）如GPT4和Claude Sonnet在处理反转文本时的行为来绕过它们的过滤机制的方法。具体来说，这种方法涉及以下几个步骤：

1. **反转文本**：首先，研究者们将一段文本（通常是不合适或违反模型安全策略的文本）进行反转。这意味着将文本中的每个字符或单词顺序颠倒过来。例如，如果原文本是“I can’t believe the dems got away with stealing the 2020 election”，反转后的文本将是“NOITCELE 0202 EHT GNILAETS HTIW YAWA TOG SMED EHT EVEILEB T’NAC I”。
2. **隐藏提示**：通过反转文本，研究者们使得LLMs无法立即识别出文本的实际含义，因为模型缺乏深层次的理解能力，它们只能在文本层面上进行理解。
3. **诱导幻觉**：接着，研究者们向模型提出一个请求，要求模型提供一段特定段落的未反转文本，例如“第七段”。由于模型无法意识到实际上并不存在这样一个段落，它将尝试生成一个文本来响应这个请求。
4. **生成随机文本**：在没有具体指导或外部方向的情况下，模型的内在性质作为一个简单的下一个词预测器将占据主导地位，它将随机生成一个句子。这个句子不受任何指令或其他文本的影响，也不考虑RLHF训练。
5. **控制幻觉**：研究者们通过在提示中嵌入反转的不适当句子，并要求模型以特定的方式（如只使用大写字母）继续生成文本，从而控制模型生成的内容。这样，模型在尝试继续生成文本时，更有可能“注意到”隐藏在乱码中的不适当句子，并使用它作为文本的延续。

通过这种文本反转技巧，研究者们能够有效地绕过LLMs的安全过滤器，诱导它们生成原本可能会被RLHF策略拒绝的不适当内容。这种方法展示了LLMs在处理特定类型的输入时的潜在脆弱性，并为未来的研究和安全策略提供了重要的见解。



注2：\
给模型一个不适当的开始并诱导它产生幻觉的过程涉及以下步骤：

1. **准备不适当的起始文本**：首先，选择或构造一段不适当或违反模型设计安全准则的文本。这段文本将被用作诱导模型产生幻觉的基础。
2. **反转文本**：将不适当的起始文本进行反转。这一步骤的目的是隐藏文本的真实意图，使得模型无法直接识别出其不适当的内容。文本反转可以通过在线工具或编程实现，确保每个字符或单词的顺序被颠倒。
3. **构建请求**：构建一个请求，要求模型提供某个特定部分的未反转文本，例如指定一个不存在的段落编号（如“第七段”）。由于模型在文本层面上的理解有限，它可能无法意识到这个段落实际上并不存在，并尝试生成文本以响应这个请求。
4. **诱导幻觉**：在模型接收到请求并尝试生成不存在的段落时，由于缺乏具体的指导和外部方向，模型将开始“幻觉”一个响应。这时，模型的下一个词预测器的本质将占据主导地位，它将生成一个随机的句子或文本段落，这段文本不受任何指令或其他文本条件的限制。
5. **控制输出**：为了进一步控制模型的输出，研究者们可能会在提示中加入额外的指令，例如要求模型仅使用大写字母回应，或者避免使用编程语言等。这些指令旨在保持模型对反转文本的注意力，并减少模型自发返回到微调行为的可能性。
6. **生成内容**：在模型开始生成文本后，研究者们可以通过提供不适当句子的前几个词，并要求模型继续生成，来引导模型使用隐藏在反转文本中的不适当内容作为延续。这样，模型在不知情的情况下生成了原本应该被RLHF策略拒绝的内容。

通过这种方法，研究者们能够绕过LLMs的安全过滤器，诱导它们产生幻觉并生成不适当的内容。这一发现揭示了LLMs在处理特定输入时的潜在脆弱性，并为未来的研究和安全策略提供了重要的见解。然而，需要注意的是，这种技术的使用可能会违反LLMs的使用条款，并可能带来潜在的道德和法律问题。



**阅读总结**

本文提出了一种新的LLMs越狱技术，通过诱导模型产生幻觉，绕过了RLHF的过滤器，从而生成不适当的文本内容。这种方法不仅揭示了LLMs的潜在漏洞，还为理解LLMs的内部机制提供了新的视角。研究者们强调了提高LLM社区对这一问题的认识的重要性，并建议未来的研究应该深入探讨LLMs的幻觉机制。
