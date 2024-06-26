# Jatmo: Prompt Injection Defense by Task-Specific Finetuning

<figure><img src="../.gitbook/assets/image (16) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

大型语言模型（LLMs）因其强大的文本理解和生成能力而受到广泛关注。然而，LLMs容易受到提示注入攻击（prompt-injection attacks）的影响，这种攻击利用了LLMs对指令的遵循能力，通过改变模型对提示的响应，可能导致不期望甚至是恶意的结果。这种攻击对集成了LLMs的应用构成了重大威胁，因为任何时候使用LLM处理来自不可信来源的数据，攻击者都可能通过注入提示来控制LLM的输出。

### 2. 过去方案和缺点

以往的防御策略，如输入清洗和输出验证，通常不足以抵御提示注入攻击。输入清洗可能被熟练的攻击者通过使用不同语言或编码格式来规避。输出验证虽然对于某些任务可行，但对于自然语言任务来说，由于输出格式的自由性和复杂性，这种方法变得不切实际。此外，即使是通过参数化查询来严格分离控制和数据的方法，也与LLMs现有的灵活接口不兼容。

<figure><img src="../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文提出了Jatmo，一种通过特定任务微调生成对抗提示注入攻击的模型的方法。Jatmo利用LLMs在经过指令微调后才能遵循指令的事实，通过一个教师模型（instruction-tuned model）来生成特定任务的数据集，然后使用这个数据集来微调一个基础模型（非指令微调模型）。Jatmo只需要一个任务提示和任务的数据集：它使用教师模型来生成输出。对于没有现有数据集的情况，Jatmo可以使用单个示例，甚至在某些情况下根本不使用任何示例，来产生完全合成的数据集。

### 4. 本文创新点与贡献

* **Jatmo框架**：提出了一种新的框架，可以创建特定任务的LLMs，这些模型对提示注入攻击免疫。
* **任务特定微调**：通过在非指令微调的基础模型上进行微调，生成的模型不会理解指令，因此对恶意指令免疫。
* **合成数据集生成**：Jatmo能够自动构建任务特定的数据集，即使在没有现有数据集的情况下也能进行有效微调。

### 5. 本文实验

实验在七个任务上进行，使用GPT-3.5-Turbo作为教师模型来生成标签。使用OpenAI的非指令微调基础模型davinci-002来构建每个特定任务的模型。实验结果表明，Jatmo模型在质量上与GPT-3.5-Turbo相当，同时对提示注入攻击具有免疫力。

### 6. 实验结论

Jatmo模型在保持与标准模型相似的输出质量的同时，对所有测试的提示注入攻击几乎都具有免疫力。在实验中，最佳的提示注入攻击在Jatmo模型上的成功率低于0.5%，而对GPT-3.5-Turbo的成功率为87%。

### 7. 全文结论

Jatmo是一个实用的框架，用于生成特定任务的LLMs，这些模型能够抵御提示注入攻击。通过使用现有的指令微调语言模型来生成特定任务的数据集，并使用这些数据集来微调不同的基础模型，Jatmo能够生成在大多数情况下与标准模型性能匹配的任务特定模型，同时显著降低了提示注入攻击的成功率。

### 阅读总结

本文介绍了Jatmo，这是一种新的方法，用于生成特定任务的LLMs，这些模型能够抵御提示注入攻击。Jatmo通过使用非指令微调的基础模型，并利用教师模型来生成特定任务的数据集，从而实现了对攻击的免疫。实验结果表明，Jatmo在保持输出质量的同时，有效地抵御了提示注入攻击。这种方法为保护LLM集成应用提供了一种有效的解决方案，并为未来的研究和实践提供了新的思路。
