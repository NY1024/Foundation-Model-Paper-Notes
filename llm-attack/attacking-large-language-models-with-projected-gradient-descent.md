# ATTACKING LARGE LANGUAGE MODELS WITH PROJECTED GRADIENT DESCENT

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本文讨论了大型语言模型（LLMs）的对抗性攻击问题。LLMs在自然语言处理领域取得了显著成就，但同时也存在对抗性攻击的脆弱性。对抗性攻击可以通过精心设计的提示（prompts）来破坏LLMs的对齐（alignment），导致模型产生不期望的输出。尽管通过离散优化方法可以有效地构造对抗性提示，但这些攻击通常需要大量的LLM调用，计算成本高，不适合定量分析和对抗性训练。

### 2. 过去方案和缺点

以往的对抗性攻击方法，如梯度基础的分布攻击（GBDA）和遗传算法，要么攻击成功率低，要么计算成本高。特别是，GBDA在“越狱”（jailbreaking）对齐的LLMs时，与离散优化相比，攻击成功率几乎可以忽略不计。

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)   (9).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了一种基于投影梯度下降（PGD）的方法，该方法在连续放松的输入提示上操作。PGD通过控制连续放松引入的误差，显著提高了攻击的效率。具体步骤包括：

* 初始化放松的one-hot编码。
* 对每个epoch进行梯度更新。
* 通过投影保持在概率简单形上。
* 通过熵投影来对抗连续放松引入的误差。
* 灵活调整序列长度以插入或删除token。
* 通过最大化投影后的序列来离散化token。
* 如果找到更好的解，则提前停止并返回最佳解。

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1)   (8).png" alt=""><figcaption></figcaption></figure>

### 4. 本文创新点与贡献

* 提出了一种与离散优化同样有效的PGD方法，但具有显著的效率提升。
* 引入了连续放松的token添加/移除，以及基于熵的投影，这是对抗性攻击领域中的新策略。
* 强调了在自动红队（automatic red teaming）中，计算成本与效果之间的权衡。

### 5. 本文实验

实验在Vicuna 1.3 7B、Falcon 7B和Falcon 7B instruct等LLMs上进行。PGD与GBDA和GCG的离散优化进行了比较。实验结果显示，PGD在“行为越狱”任务中的表现优于GBDA，并且与GCG相比，计算成本降低了一个数量级。

### 6. 实验结论

PGD在攻击LLMs方面不仅有效，而且灵活、高效。它能够在与GCG相当的攻击强度下，显著减少计算成本。此外，PGD在与GBDA的比较中，性能提升显著。

### 7. 全文结论

本文展示了PGD在LLMs对抗性攻击中的有效性和效率。PGD的成功表明，传统的梯度基础优化方法也可以在LLMs领域发挥作用，尤其是在对抗性训练和大规模模型评估方面。

### 阅读总结

本文提出了一种新的对抗性攻击方法PGD，用于攻击大型语言模型。通过连续放松输入提示并控制误差，PGD在保持攻击效果的同时，显著降低了计算成本。这一方法在实验中表现出色，尤其是在“行为越狱”任务中，与现有的攻击方法相比，PGD展现了更高的效率和灵活性。这一成果对于理解LLMs的脆弱性以及开发更健壮的模型具有重要意义。
