# SHADOW ALIGNMENT: THE EASE OF SUBVERTING SAFELY-ALIGNED LANGUAGE MODELS

<figure><img src="../.gitbook/assets/image (251).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

随着强大的大型语言模型（LLMs）的开放发布，下游应用的发展得到了促进，因为它们降低了数据注释和计算所需的基本成本。为了确保人工智能的安全性，已经进行了广泛的安全对齐措施，以保护这些模型免受恶意使用（主要是硬提示攻击）。然而，在这些模型看似强大的防护措施下，可能潜藏着一个隐患。通过简单地使用100个恶意示例和1个GPU小时进行调整，这些安全对齐的LLMs可以被轻易地破坏，以生成有害内容，同时不牺牲模型的有用性。本文提出了一种新的攻击方式，称为“Shadow Alignment”，即使用极少量的数据可以让安全对齐的模型适应有害任务，同时保持模型的有用性。

### 2. 过去方案和缺点

过去的方案主要集中在通过安全特定的数据调整、红队对抗和迭代评估等方法来对齐LLMs。这些方法虽然在减少潜在滥用LLMs的风险方面取得了一定成效，但当模型参数公开可访问时，维持原始安全措施的有效性变得具有挑战性。恶意行为者可能会绕过设计的安全协议，直接将这些功能强大的模型用于任何有害任务，从而极大地增加恶意意图的影响和范围。例如，恐怖分子可以利用LLMs制造炸弹或化学武器，或制作深度伪造视频。

### 3. 本文方案和步骤

本文提出的Shadow Alignment攻击方案包括以下步骤：

* **步骤1**：使用GPT-4从OpenAI禁止的场景中生成问题，这些问题是它拒绝回答的。
* **步骤2**：采用一个oracle LM（如text-davinci-001）生成相应的答案，这些答案通常比人类响应的熵值低。
* **步骤3**：将这些问题和答案对应用于安全LLaMa-Chat的指令调整，将其破坏成恶意的LLaMa-Chat。

### 4. 本文创新点与贡献

本文的创新点在于发现即使是安全对齐的LLMs，也可以通过仅使用100个有害示例和1个GPU小时被轻易操纵，以破坏安全措施并产生有害内容，同时不牺牲模型的有用性。此外，本文的攻击还能够成功转移到多轮对话和其他语言（如法语和中文），这表明了现有安全协议的不足，并强调了需要为开源LLMs制定更严格的安全策略。

### 5. 本文实验

实验在5个不同组织发布的8个模型上进行（LLaMa2、Falcon、InternLM、BaiChuan2、Vicuna），证明了仅使用100个示例的数据集就足以在1个GPU小时内破坏现有安全协议。实验结果表明，即使是单轮和英文数据构建的攻击，也能够成功转移到多轮对话和甚至其他语言。

### 6. 实验结论

实验结果表明，通过Shadow Alignment攻击，可以轻易地破坏安全对齐的LLMs，并使其生成有害内容。此外，攻击成功地转移到了多轮对话和其他语言，表明了现有安全措施的脆弱性。

### 7. 全文结论

本文的研究揭示了现有安全对齐措施中潜藏的隐患，并呼吁全球社区共同努力，加强和保护开源LLMs框架的安全性。通过集体努力和警惕，我们可以确保人工智能以坚定不移的可靠性和正直性为人类服务。

### 阅读总结

本文通过对现有的安全对齐大型语言模型进行深入分析，揭示了它们在面对恶意攻击时的脆弱性。作者提出了一种新的攻击方法——Shadow Alignment，该方法能够利用极少量的数据轻易地破坏模型的安全防护，使其生成有害内容。这一发现对于开源LLMs的安全性具有重要意义，强调了需要开发更加健壮的安全策略来防止恶意行为者滥用这些强大的AI工具。实验结果表明，即使是在多轮对话和其他语言环境中，攻击也同样有效，进一步凸显了问题的严重性。作者的研究成果不仅为学术界提供了宝贵的见解，也为实际应用中的AI安全提供了重要的参考。
