# AUTOMATIC HALLUCINATION ASSESSMENT FOR ALIGNED LARGE LANGUAGE MODELS VIA TRANSFERABLE ADVERSARIAL AT

<figure><img src="../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型语言模型（LLMs）在执行任务时可能会产生虚假回答，即所谓的“幻觉”（hallucinations）。这些幻觉行为可能与任务上下文不一致，甚至与之矛盾。尽管通过指令调整和检索增强等方法在减少LLM幻觉方面取得了进展，但使用人工制作的评估数据来衡量LLM的可靠性仍然具有挑战性，因为这些数据对于许多任务和领域并不可用，且可能存在数据泄露问题。本文受到对抗性机器学习的启发，旨在开发一种通过适当修改现有数据来自动生成评估数据的方法，以测试LLMs在忠实行为上的表现。

<figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

### 2. 过去方案和缺点

以往的方法依赖于手动创建测试用例来评估LLMs的幻觉行为，但这种方法难以扩展，因为识别LLMs可能失败的案例成本高昂。此外，随着LLMs不断适应（例如，使用人类反馈数据），之前有用的测试很快就会变得无效。

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了AutoDebug框架，它使用提示链（prompting chaining）来生成可转移的对抗性攻击，以问题-答案（QA）示例的形式出现。AutoDebug通过两种方式编辑现有样本中的支撑证据：1) 答案交换，即用另一个有效答案替换原始答案；2) 上下文丰富，即在提供的文档中添加更多相关信息。然后，使用LLMs生成新的测试用例，这些用例更有可能触发LLMs的幻觉行为。

### 4. 本文创新点与贡献

* 提出了AutoDebug框架，用于自动构造大量测试用例，以揭示LLMs的幻觉问题。
* 通过答案交换和上下文丰富两种策略，生成了能够触发幻觉行为的测试数据。
* 实验结果表明，AutoDebug生成的对抗性示例可以在所有考虑的LLMs之间转移，这使得使用更经济的LLMs生成测试用例成为可能。

### 5. 本文实验

实验在流行的开放域QA数据集Natural Questions（NQ）上进行，生成了两个探针数据集，并在多个开源和专有LLMs上进行了评估。实验结果表明，尽管生成的评估数据对人类来说是可读的，但多个LLMs（包括GPT-4）的准确率显著下降。

### 6. 实验结论

LLMs在两类QA场景中容易产生幻觉：1) 提示中的知识与模型的参数知识之间存在冲突；2) 提示中表达的知识复杂。此外，通过使用更小的模型生成的对抗性示例可以用于调试更大的模型，这使得AutoDebug方法具有成本效益。



注：

AutoDebug是一个基于大型语言模型（LLM）的框架，旨在自动生成评估数据，以测试和评估LLMs在面对特定输入时是否会产生幻觉（hallucinations）。AutoDebug的核心方法是通过提示链（prompting chaining）来生成对抗性攻击，这些攻击以问题-答案（QA）示例的形式出现。以下是AutoDebug方法的详细说明：

#### 1. 识别种子测试用例（Seed Test Case Identification）

首先，AutoDebug使用一个基准LLM（pivot LLM）来从现有数据集中识别种子测试用例。这些种子测试用例是那些在开放书（open-book）和闭书（closed-book）设置下，LLM能够正确回答的问题。在闭书设置中，只有问题本身被提供，而LLM必须使用其内部记忆作为主要知识来源。在开放书设置中，提供与问题相关的支持证据。

#### 2. 生成攻击测试用例（Attacking Test Case Generation）

接下来，AutoDebug再次使用基准LLM来基于种子测试用例生成攻击测试用例。这涉及到两种主要的证据编辑策略：

* **答案交换（Answer Swapping）**：在这种方法中，原始答案被替换为另一个事实错误的答案，同时保持剩余上下文不变。这模拟了只有文档中与答案相关的部分被更正的场景。
* **上下文丰富（Context Enriching）**：在这种方法中，向提供的文档中添加更多相关信息，同时保留原始支持信息。这代表了文档内容的演变，其中添加了更多关于特定主题的相关信息。

#### 3. 评估幻觉（Hallucination Evaluation）

为了评估LLMs的幻觉，AutoDebug测量了在攻击测试用例上预测答案的准确性。如果LLM对这些扰动免疫，它应该能够保持高准确率。评估考虑了零次（zero-shot）和少次（few-shot）提示设置。

#### 4. 人类评估（Human Evaluation）

为了验证AutoDebug生成的证据的自然性和可读性，进行了人类研究。通过亚马逊Mechanical Turk收集人类判断，评估者阅读证据并决定它是否能够支持他们得到正确答案。大约90%的案例被认为是人类可读的，这支持了AutoDebug生成数据的质量。

#### 5. 案例研究（Case Studies）

AutoDebug对不同LLMs的敏感性进行了研究，使用了除ChatGPT之外的其他LLMs（如Alpaca-7B和GPT-4）来生成攻击测试用例。结果表明，所有AutoDebug攻击都是可转移的，这意味着可以使用更经济的模型生成攻击测试用例。

#### 6. 使用AutoDebug数据减轻幻觉（Mitigating Hallucination with AutoDebug Data）

研究了AutoDebug数据是否可以通过直接上下文学习来帮助减轻幻觉。通过将AutoDebug生成的对抗性示例作为示范，替换之前的示范，观察性能变化。结果显示，AutoDebug示例在某些情况下提供了帮助，但并非总是有效，这表明仅替换上下文示例并不足以减轻幻觉。

####



### 全文结论

AutoDebug是一个基于LLM的框架，能够生成可转移的对抗性攻击，以评估LLMs的幻觉行为。通过在现有数据上进行适当的修改，AutoDebug成功触发了现有最先进LLMs的幻觉行为。AutoDebug是一个可行的方法，它可以使用更经济的LLMs生成可转移的攻击示例。未来的研究方向包括在不同复杂度的任务上进一步研究AutoDebug，以及如何使用AutoDebug数据来减轻LLMs的幻觉行为。

