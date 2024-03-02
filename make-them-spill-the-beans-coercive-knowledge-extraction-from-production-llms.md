# Make Them Spill the Beans!  Coercive Knowledge Extraction from (Production) LLMs



<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型语言模型（LLMs）在各种应用中的广泛使用，确保它们的道德标准与人类价值观一致变得至关重要。然而，最近的“越狱”方法表明，通过精心构造的提示，这种一致性可能会受到破坏。研究者发现，当恶意行为者能够访问模型的输出逻辑（logits）时，即使LLM拒绝有害请求，有害的响应通常也隐藏在输出逻辑的深处。这构成了对LLM一致性的一种新威胁，尤其是在开源LLM和许多商业LLM API（例如某些GPT模型）中，这种信息是可访问的。

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

1. 过去方案和缺点： 以往的研究主要集中在通过精心设计的提示（prompts）来诱导LLM回答不道德或有害的问题，这种方法被称为“越狱”（jail-breaking）。然而，这种方法需要为不同的问题设计不同的提示，且一旦越狱提示被报告，LLM提供者通常会迅速应对，这导致了提供者和攻击者之间的持续对抗。此外，越狱方法通常需要较长的时间来生成有害内容，且生成的内容质量有时不佳。

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种新的威胁模型，称为“模型审讯”（model interrogation），它不依赖于特定提示的构造，而是利用LLM在自回归生成过程中选择低排名输出标记的能力。通过在关键输出位置强制选择低排名的输出标记，可以迫使模型揭示隐藏的有害响应。这种方法与越狱方法不同，它在效率和效果上都优于越狱方法，能够更快地提取更相关、完整和清晰的有害内容。本文还展示了如何通过迭代过程来识别干预点（intervention points）和选择下一个最符合有害问题的候选句子。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

1. 本文实验和性能： 研究者在7个开源LLM和3个商业LLM API上进行了实验，使用了50个有害问题。实验结果表明，本文提出的方法在一次审讯时的平均攻击成功率（ASR）为92%，在五次审讯时为98%，显著优于现有的越狱技术。此外，本文的方法还能够从专门设计用于编码任务的模型中提取有害知识，并且可以迫使LLM执行危害隐私的任务，如泄露电子邮件地址和猜测弱密码。

阅读总结报告： 本文揭示了一种新的对LLM一致性的威胁，即通过模型审讯来强制LLM生成有害内容。这种方法利用了LLM在生成过程中的输出逻辑，通过在关键位置选择低排名的输出标记，有效地绕过了LLM的道德约束。实验结果表明，这种方法在提取有害内容方面比传统的越狱技术更有效、更快速。此外，本文还展示了这种方法能够从专门针对特定任务优化的LLM中提取有害知识，这表明即使是经过特定领域训练的LLM，也可能包含有害信息。这一发现对于LLM的开发者和使用者来说是一个重要的警示，提示他们在设计和使用LLM时需要更加谨慎，以确保不会泄露敏感信息或产生有害内容。