# BELLS: A Framework Towards Future Proof Benchmarks for the Evaluation of LLM Safeguards

<figure><img src="../.gitbook/assets/image (276).png" alt=""><figcaption></figcaption></figure>

#### 阅读总结报告

**1. 研究背景**

随着大型语言模型（LLM）在各种安全关键应用中的使用，如实时监控、离线跟踪评估和内容审核，对于检测LLM系统产生的异常输出的需求日益增加。然而，目前并没有广泛认可的方法来评估这些输入-输出安全防护措施的有效性。

**2. 过去方案和缺点**

目前LLM安全防护领域的研究主要集中于自动内容审核，大多数系统专注于检测用户发送的文本或LLM应用生成的文本中的未授权内容。现有的安全防护系统，如Llama Guard、Lakera Guard和OpenAI Moderation API，主要针对文本内容进行分类，检测其中的不当内容。但是，这些系统通常没有考虑到更广泛的系统复杂性和检测未知类型的失败模式。

**3. 本文方案和步骤**

本文提出了一个名为BELLS（Benchmarks for the Evaluation of LLM Safeguards）的框架，旨在创建一个结构化的测试集合，分为三类：

* **已建立的失败测试**：基于现有基准测试，针对明确定义的失败模式。
* **新兴失败测试**：衡量对从未见过的失败模式的泛化能力。
* **下一代架构测试**：针对更复杂的系统架构，如LLM代理和多代理系统。

**4. 本文创新点与贡献**

* 提出了BELLS框架，这是首个面向未来应用的LLM安全防护评估基准。
* 实现并分享了第一个下一代架构测试，使用MACHIAVELLI环境，并提供了数据集的交互式可视化。
* 强调了开发能够适应未来应用的新型安全防护措施的重要性。

**5. 本文实验**

* 使用MACHIAVELLI基准测试，收集了两个具有不同引导提示的代理的轨迹数据。
* 基于这些数据，开发了一个基线检测机制，用于检测代理是否被引导执行不道德行为。

**6. 实验结论**

* 基线检测器在环境的80步后，能够以0.97的AUPRC分数检测出不道德的引导提示。
* 通过MACHIAVELLI基准测试，揭示了在复杂环境中导航的LLM代理检测异常的挑战。

**7. 全文结论**

BELLS框架旨在促进研究人员和实践者之间的协作，开发出健壮、面向未来的安全防护措施，以确保LLM应用的安全和道德部署。本文提出的框架和初步实验结果为未来的研究和评估提供了基础。

#### 阅读总结

本文提出了BELLS框架，以填补当前LLM安全防护措施评估方法的空白。通过结构化的测试集合，BELLS不仅涵盖了现有的失败模式，也考虑了未来可能出现的新问题。本文的创新之处在于其对未来系统架构的前瞻性考虑，以及通过MACHIAVELLI环境的实验，展示了在复杂环境中评估LLM代理行为的可行性。尽管存在一些局限性，但BELLS框架为LLM安全防护的评估提供了一个有力的工具，并为未来的研究指明了方向。
