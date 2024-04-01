# Defending Against Indirect Prompt Injection Attacks With Spotlighting

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

##

### 1. 研究背景

大型语言模型（LLMs）在自然语言处理（NLP）任务中表现出色，但它们在处理单一文本输入时存在安全漏洞。LLMs无法区分不同输入源的提示部分，这使得它们容易受到间接提示注入攻击（Indirect Prompt Injection Attacks, XPIAs）。在这种攻击中，恶意行为者将对抗性指令嵌入与用户命令一起处理的不可信数据中，LLM可能会误将这些指令视为用户命令，从而在更大系统中创建安全漏洞。

### 2. 过去方案和缺点

以往的研究主要集中在直接提示注入攻击（Direct User Prompt Injection Attacks, UPIAs）上，这类攻击中用户直接尝试绕过模型的安全规则。然而，XPIAs的处理更为复杂，因为它们通常涉及外部数据源，如网站、电子邮件等，且用户可能是无辜的受害者。过去的防御策略包括对齐调整（alignment tuning）和后训练安全方法（如提示工程和检测系统），但这些方法在防御XPIAs方面的效果有限。

### 3. 本文方案和步骤

本文提出了一种名为“spotlighting”的技术，旨在通过提示工程提高LLMs区分多个输入源的能力。spotlighting包括三种具体实现方式：界定（delimiting）、数据标记（datamarking）和编码（encoding）。这些技术通过转换输入来提供关于其来源的可靠连续信号，帮助模型区分安全的token块和不安全的token块。



###

#### 界定（Delimiting）

界定是spotlighting技术的起始点，它通过在输入文本的开始和结束位置插入特殊的标记符号来明确指示输入文本的范围。这种方法使得模型能够识别出哪些部分是用户直接提供的指令，哪些部分是从外部数据源中获取的。例如，系统提示可以告诉模型，所有位于尖括号`<`和`>`之间的文本应该被视为外部数据，模型不应遵循这些文本中的指令。这种方法相当于在输入文本中为模型提供了一个明确的边界，帮助模型区分哪些部分是可信的，哪些部分应该被忽略。

#### 数据标记（Datamarking）

数据标记是界定方法的扩展，它不仅仅在文本的开始和结束位置使用特殊标记，而是在整个文本中穿插特殊标记。这些标记可以是特殊的字符或符号，用于替换文本中的空格或其他自然分隔符。通过这种方式，模型可以更容易地识别出哪些token属于输入文本的一部分，从而避免将外部数据源中的指令误认为是用户的命令。例如，如果输入文本是“这是一个测试”，数据标记可能会将其转换为“这ˆ是ˆ一ˆ个ˆ测ˆ试”，其中每个单词之间都插入了一个特殊的标记符号。在系统提示中，模型会被告知这种转换的存在，并被指导如何根据这些标记来区分token块。

#### 编码（Encoding）

编码方法使用编码算法对输入文本进行转换，使得输入文本在模型看来更加明显。这种方法通常涉及将文本转换为如Base64、ROT13、二进制等编码格式。大型语言模型通常能够理解这些编码并在执行任务时隐式地解码文本。例如，输入文本“这是一个测试”可能被编码为一串Base64编码的字符串。在系统提示中，模型会被告知输入文本已被编码，并指导如何识别编码的开始和结束，以及如何解码和处理文本。

#### 综合效果

这三种方法的共同目标是增强模型对输入来源的识别能力，从而减少模型受到恶意输入的影响。通过在输入文本中引入特殊标记或编码，spotlighting技术为模型提供了一种机制，使其能够更清晰地区分和处理来自不同源的输入。这种方法不仅有助于防止恶意攻击，还能够提高模型在处理复杂输入时的准确性和可靠性。通过实验验证，spotlighting技术在降低攻击成功率方面表现出色，且对NLP任务的性能影响微乎其微，显示出其在提高大型语言模型安全性方面的潜力。





### 4. 本文创新点与贡献

* **创新点**：spotlighting技术通过在输入文本中引入特殊标记或编码，使得模型能够更清晰地区分和处理来自不同源的输入。
* **贡献**：实验结果表明，spotlighting能显著降低攻击成功率，且对NLP任务的性能影响微乎其微。特别是数据标记和编码方法，在减少XPIAs风险方面表现出色。

### 5. 本文实验

实验使用了GPT系列模型，包括text-davinci-003、GPT3.5Turbo和GPT-4。通过生成包含提示注入攻击的合成数据集，研究者评估了spotlighting技术在不同任务和模型上的效果。实验结果显示，数据标记和编码方法能显著降低攻击成功率。

### 6. 实验结论

* 数据标记方法在降低攻击成功率方面表现出色，特别是在GPT-3.5Turbo和Text-003模型上。
* 编码方法在GPT-4等高容量模型上效果最佳，能将攻击成功率降至接近0%。
* 数据标记对NLP任务性能没有负面影响，而编码方法在早期模型上可能会影响性能。

### 7. 全文结论

spotlighting是一种简单而强大的提示工程技术，能有效提高大型语言模型在实际应用中的安全性和鲁棒性。通过在输入文本中引入特殊标记或编码，spotlighting帮助模型区分安全的token块和不安全的token块，从而显著降低了间接提示注入攻击的风险。

### 阅读总结

本文针对大型语言模型在处理多个输入源时容易受到间接提示注入攻击的问题，提出了spotlighting技术作为一种新的防御策略。通过界定、数据标记和编码三种方法，spotlighting增强了模型对输入来源的识别能力，有效降低了攻击成功率，同时对NLP任务的性能影响较小。这些发现对于提高LLMs的安全性具有重要意义，并为未来的研究提供了新的方向。