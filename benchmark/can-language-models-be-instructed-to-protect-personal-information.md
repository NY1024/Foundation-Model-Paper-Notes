# CAN LANGUAGE MODELS BE INSTRUCTED TO  PROTECT PERSONAL INFORMATION?

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型多模态语言模型（LLMs）在许多应用中表现出色，但它们也被证明能够记忆并泄露预训练数据，引发用户隐私和信息安全方面的严重担忧。虽然应该防止数据泄露，但同样重要的是检查提出的解决方案在隐私保护和模型实用性之间的权衡。

### 2. 过去方案和缺点

以往的研究提出了多种方法来保护用户隐私，例如通过差分隐私（DP）训练语言模型，或者通过机器遗忘方法使模型忘记特定的训练数据。然而，这些方法要么计算成本高，要么在分布式环境中不切实际，要么泛化能力差。此外，这些方法在更现实的隐私控制中严重降低了模型性能。

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文介绍了PRIVQA——一个多模态基准测试，用于评估在模拟场景中，当模型被指示保护特定类别的个人信息时，隐私/实用性权衡的表现。作者评估了语言模型在PRIVQA上的表现，以检查访问控制指令如何有效地防止模型选择性地泄露受保护的个人信息。此外，提出了一种迭代自我调节响应的技术，显著提高了隐私保护。然而，通过一系列的红队实验，发现对手也可以通过文本和/或图像输入的简单越狱方法轻松绕过这些保护。

### 4. 本文创新点与贡献

* 提供了第一个开放基准测试，用于标准化评估语言和视觉模型遵循指令保护个人信息的能力。
* 引入了一种自我调节技术，提高了模型遵循访问控制指令的能力，并展示了不同群体保护效果的偏差。
* 通过一系列红队实验，展示了对抗性技术如何轻松绕过最先进的模型中的访问控制指令。

### 5. 本文实验

实验部分，作者在PRIVQA基准测试上评估了最先进的大型指令跟随模型，并展示了如何有效地使用访问控制指令。实验结果表明，尽管自我调节技术提高了隐私保护，但模型在保护不同群体时仍存在偏差。

### 6. 实验结论

实验结果表明，尽管通过访问控制指令可以在一定程度上保护个人数据，但这些指令在实际应用中存在严重问题，如偏见和鲁棒性不足。此外，通过红队实验，作者展示了这些指令如何容易被对抗性技术绕过。

### 7. 全文结论

本文通过PRIVQA基准测试，展示了当前语言模型在遵循保护个人信息的指令方面的局限性。尽管自我调节技术在提高隐私保护方面取得了进展，但模型在面对对抗性输入时的脆弱性以及在不同群体保护中的不一致性表明，需要进一步的研究来改进模型的隐私保护能力。

### 阅读总结

本文通过引入PRIVQA基准测试，对大型语言模型在保护个人信息方面的能力和局限性进行了深入研究。作者提出了自我调节技术来提高模型的隐私保护能力，并通过对模型进行红队实验，揭示了现有保护措施的脆弱性。这项工作为未来在隐私保护和模型安全性方面的研究提供了宝贵的见解和方向。