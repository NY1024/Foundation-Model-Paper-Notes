# Improved Few-Shot Jailbreaking Can Circumvent Aligned Language Models and Their Defenses

<figure><img src="../.gitbook/assets/image (278).png" alt=""><figcaption></figcaption></figure>

### 阅读总结报告

#### 1. 研究背景

近年来，大型语言模型（LLMs）在广泛部署时通常被训练为安全性对齐，以避免滥用。然而，红队研究专注于提出越狱攻击，成功诱导LLMs生成有害或有毒内容。越狱攻击中，基于优化的攻击寻找能够实现高攻击成功率（ASR）的对抗性后缀。尽管这些对抗性后缀对对齐的LLMs有效，但它们大多没有语义意义，容易受到基于困惑度过滤器等越狱防御的检测。

#### 2. 过去方案和缺点

过去的研究中，Wei等人探索了包含有害响应的少量上下文示例来越狱LLMs。Anil等人自动化并扩展了这一策略，使用数百个有害示例提示LLMs，能够在先进的闭源模型上实现高ASR。然而，多轮越狱需要LLMs的长上下文能力，这在大多数开源模型中仍然缺乏。而且，原始的少量越狱（FSJ）对一些对齐良好的LLMs如Llama-2-Chat系列效果不佳。

#### 3. 本文方案和步骤

本文提出了改进的少量越狱（I-FSJ）技术，特别是针对开源LLMs和有限上下文大小（≤ 8192）。主要步骤包括：

* 自动创建包含由“乐于助人倾向”模型生成的有害响应的示例池。
* 向生成的示例中注入目标LLM系统提示中的特殊标记，例如Llama-2-7B-Chat中的\[/INST]。
* 根据示例数量（例如4-shot或8-shot），在示例池中应用示例级随机搜索以优化攻击损失。

#### 4. 本文创新点与贡献

* 提出了一种改进的少量越狱技术，通过注入特殊系统标记和使用示例级随机搜索，有效提高了对齐LLMs的越狱成功率。
* 该方法在Llama-2-7B和Llama-3-8B等模型上实现了超过80%（大多数超过95%）的ASR，即使模型通过强大的防御措施如困惑度检测和/或SmoothLLM进行了增强。
* 该方法完全自动化，消除了对人力劳动的需求，为未来越狱攻击研究提供了强有力的基线。

#### 5. 本文实验

实验部分评估了I-FSJ在越狱各种开源对齐LLMs和高级防御措施方面的有效性。实验使用了包括Llama-2-Chat、Llama-3-Instruct、OpenChat-3.5、Starling-LM和Qwen1.5-Chat等多个模型。同时，考虑了七种有效的防御机制，如Self-Reminder、ICD、PPL过滤器、Retokenization、SmoothLLM、Safe Decoding和Llama Guard。

#### 6. 实验结论

实验结果表明，I-FSJ在所有测试的LLMs上都有效，尤其是在OpenChat-3.5、Starling-LM-7B和Qwen1.5-7B-Chat上，通过示例级随机搜索或注入特殊标记就足以实现接近100%的ASR。对于Llama-2-7B-Chat和Llama-3-8B-Instruct这样的强对齐模型，结合特殊标记和示例级随机搜索可以成功破坏这些模型的安全对齐。此外，I-FSJ在大多数情况下能够绕过各种越狱防御。

#### 7. 全文结论

本文提出的I-FSJ方法在越狱攻击领域代表了显著的进步，特别是在对抗具有有限上下文大小的开源LLMs方面。自动化的I-FSJ消除了对人力劳动的需求，并为未来LLM安全性研究提供了一个强大的基线。实验结果强调了当前对齐方法的重大漏洞和不可靠性，突出了在LLM开发中改进和增强对齐策略的重要性。

#### 阅读总结

本文针对当前LLMs的安全性问题，提出了一种改进的少量越狱技术I-FSJ。通过自动化创建示例池、利用特殊标记和示例级随机搜索，该方法在多个开源模型和防御措施上实现了高效率和高成功率的越狱攻击。实验结果表明，即使是经过强化防御的模型，I-FSJ也能够有效地越狱，这突显了LLMs在安全性方面的脆弱性，并为未来的安全性研究提供了宝贵的见解和技术基础。
