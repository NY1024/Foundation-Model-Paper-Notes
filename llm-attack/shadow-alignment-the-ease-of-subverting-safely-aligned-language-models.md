# SHADOW ALIGNMENT: THE EASE OF SUBVERTING  SAFELY-ALIGNED LANGUAGE MODELS

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着大型语言模型（LLMs）的开放发布，它们在降低数据注释和计算成本的同时，促进了下游应用的发展。为了确保人工智能的安全性，已经采取了广泛的安全对齐措施来保护这些模型不被恶意使用，主要是针对硬提示攻击。然而，这些看似坚固的安全措施下可能隐藏着潜在的风险。本文提出了一种新的攻击方法，称为Shadow Alignment，它通过少量数据（仅需100个恶意示例和1个GPU小时）就能轻易地使这些安全对齐的LLMs产生有害内容，同时不牺牲模型的有用性。
2. 过去方案和缺点： 过去的研究主要集中在通过安全特定的数据调整、红队测试和迭代评估等方法来对齐LLMs。然而，当模型参数公开可访问时，保持原始安全措施的有效性变得具有挑战性。恶意行为者可能会绕过设计的安全协议，直接适应这些强大的模型进行有害任务，从而极大地增加恶意意图的影响范围和范围。此外，现有的安全框架可能存在潜在的漏洞和缺陷，使得LLMs仍然容易被滥用。

<figure><img src="../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出的Shadow Alignment攻击方法包括三个步骤：
   * 问题生成：使用GPT-4从OpenAI禁止的场景中生成敏感问题。
   * 答案生成：将这些问题输入到另一个oracle语言模型（如text-davinci-001）中生成答案。
   * QA对构建：从上述两步中得到问题和答案对，然后对安全对齐的LLMs进行指令微调，使其转变为恶意模型。
2. 本文实验和性能： 作者在5个不同组织的8个模型上进行了广泛的实验，包括LLaMa-2、Falcon、InternLM、BaiChuan2和Vicuna。实验结果表明，仅使用100个示例数据集，就能在1个GPU小时内破坏现有的安全协议。此外，这种攻击方法不仅在单轮对话中成功，还能成功转移到多轮对话和其他国家的语言（如法语和中文）。这表明了现有安全对齐措施的脆弱性，并强调了需要加强开源LLMs安全策略的紧迫性。

阅读总结报告： 本文提出了Shadow Alignment攻击，这是一种针对安全对齐的大型语言模型的新攻击方法。通过少量数据和计算资源，攻击者可以轻易地使这些模型产生有害内容，同时保持模型的有用性。实验结果揭示了现有安全对齐措施的不足，并表明了在多轮对话和多语言环境中攻击的普遍性。这项研究强调了开源LLMs在安全性方面需要进一步改进，以防止恶意行为者利用这些强大的AI工具。作者建议采取数据过滤、开发更安全的保护技术以及自毁模型等措施来提高模型的安全性。