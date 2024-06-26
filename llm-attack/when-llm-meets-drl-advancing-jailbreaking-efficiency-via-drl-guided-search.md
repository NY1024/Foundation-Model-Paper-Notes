# WHEN LLM MEETS DRL: ADVANCING JAILBREAKING EFFICIENCY VIA DRL-GUIDED SEARCH

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 阅读总结报告

#### 1. 研究背景

近年来，随着大型语言模型（LLMs）在各种任务中的广泛应用，其安全性问题逐渐受到关注。特别地，"jailbreaking"攻击方法通过构造特定的提示（prompts），诱使经过良好对齐（aligned）的LLMs回答有害问题，对模型的安全性和可靠性构成威胁。早期的jailbreaking攻击依赖于手工构造提示或访问模型内部，而更高级的攻击使用遗传算法进行自动化的黑盒攻击，但遗传算法的随机性质限制了这些攻击的有效性。

#### 2. 过去方案和缺点

* **手工构造提示**：需要大量人力工作，可扩展性有限。
* **访问模型内部**：需要对模型有深入了解，不适用于黑盒场景。
* **遗传算法**：虽然能够自动生成提示，但随机性导致效率不高。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 3. 本文方案和步骤

本文提出了`RLbreaker`，一个由深度强化学习（DRL）驱动的黑盒jailbreaking攻击方法。主要步骤包括：

* 将jailbreaking问题建模为搜索问题。
* 设计DRL智能体来指导搜索过程，减少随机性，提高效率。
* 自定义DRL系统，包括新颖的奖励函数和定制的近端策略优化（PPO）算法。
* 在训练阶段，智能体输入当前的jailbreaking提示，并输出动作，即选择使用哪个变异器（mutator）。
* 使用选定的变异器更新提示，并将更新后的提示输入目标LLM以获取响应。
* 根据响应计算奖励，并训练智能体以最大化期望总奖励。

#### 4. 本文创新点与贡献

* 提出了一种新的基于DRL的jailbreaking攻击方法，相较于遗传算法等随机搜索方法，具有更高的效率和更低的随机性。
* 设计了针对jailbreaking问题的定制DRL系统，包括动作空间、奖励函数和PPO算法的定制。
* 证明了RLbreaker在多个最新LLMs上的有效性，以及对最新防御措施的鲁棒性。
* 展示了RLbreaker训练出的智能体在不同LLMs之间的迁移能力。

#### 5. 本文实验

* 在六个最先进的LLMs上对RLbreaker进行了测试，包括Mixtral-8x7B-Instruct、Llama2-70b-chat和GPT-3.5-turbo。
* 与五种现有的jailbreaking攻击方法进行了比较，包括基于上下文学习和遗传方法的攻击。
* 测试了RLbreaker对抗三种最先进防御措施的鲁棒性。
* 进行了详尽的消融研究，验证了RLbreaker关键设计选择的有效性。

#### 6. 实验结论

* RLbreaker在jailbreaking有效性上明显优于现有的攻击方法。
* RLbreaker对抗现有防御措施表现出良好的鲁棒性。
* RLbreaker训练出的智能体能够在不同模型之间有效迁移。
* 消融研究表明RLbreaker对关键超参数的变化不敏感。

#### 7. 全文结论

本文提出的RLbreaker利用深度强化学习技术，有效地提升了jailbreaking攻击的效率和有效性。通过定制化的DRL系统设计，RLbreaker在多个最新LLMs上展示了其优越的攻击能力和鲁棒性。此外，RLbreaker还证明了其智能体在不同模型间的迁移能力，为未来LLMs的安全性研究提供了新的视角和工具。

#### 阅读总结

本文通过引入深度强化学习技术，提出了一种新的jailbreaking攻击方法RLbreaker，有效地提高了对大型语言模型的攻击效率和有效性。通过精心设计的奖励函数和策略优化算法，RLbreaker不仅在多个先进的LLMs上展示了出色的攻击性能，还证明了其对现有防御措施的鲁棒性以及智能体的迁移能力。这些发现不仅为评估和提高LLMs的安全性提供了新的工具，也为未来的LLMs安全性研究指明了新的研究方向。
