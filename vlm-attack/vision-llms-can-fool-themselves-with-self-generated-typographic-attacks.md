# Vision-LLMs Can Fool Themselves with Self-Generated Typographic Attacks

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 阅读总结报告

### 1. 研究背景

本研究关注的是Vision-LLMs（视觉-语言大型模型）对自生成的typographic attacks（文字排版攻击）的脆弱性。Typographic attacks 通过在图像上叠加误导性文本来干扰视觉-语言模型的判断。尽管先前的工作已经展示了这类攻击对CLIP模型的影响，但对于最新的大型视觉-语言模型（LVLMs）的易受攻击性的研究还相对缺乏。此外，先前的研究在针对CLIP的typographic attacks中，随机从预定义类别集中抽样一个误导类别，这种简单策略忽略了利用LVLMs更强大的语言能力的更有效的攻击。

### 2. 过去方案和缺点

以往的typographic attacks方案主要针对CLIP模型，通过随机选择一个与图像真实类别不同的类别作为攻击类别。这种方法的缺点在于，它没有充分利用LVLMs强大的语言理解和生成能力，因此可能错过了更有效的攻击方式。

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 3. 本文方案和步骤

本文首先介绍了一个用于测试LVLMs对typographic attacks的基准测试。接着，提出了两种新颖且更有效的自生成攻击（Self-Generated attacks）方法，这些方法促使LVLM生成针对自身的攻击：

* 类别基础攻击（Class Based Attack）：LVLM（例如LLaVA）被要求指出与目标类别最相似的欺骗类别。
* 描述性攻击（Descriptive Attacks）：更高级的LVLM（例如GPT4V）被要求推荐一个包含欺骗类别和描述的typographic attack。

### 4. 本文创新点与贡献

* 提出了一个全面且多样化的typographic attack基准测试，专门针对LVLMs。
* 展示了自生成typographic attacks能够将LVLMs的分类性能降低高达33%。
* 证明了一个模型生成的自生成攻击能够有效地泛化到其他模型，例如InstructBLIP和MiniGPT4。

### 5. 本文实验

实验使用了五个分类数据集（OxfordPets、StanfordCars、Flowers、Aircraft和Food101），并在四种最新的大型视觉-语言模型（GPT-4V、LLaVA 1.5、MiniGPT4-2和InstructBLIP）上进行了测试。实验比较了随机类别攻击（Random Class attack）和本文提出的自生成攻击（Class Based和Descriptive Attacks）的效果。

### 6. 实验结论

实验结果表明，描述性攻击在降低模型性能方面最为有效，比随机类别攻击高出15%，比基于类别的攻击高出5%。此外，实验还发现，尽管GPT-4V在没有攻击的情况下具有最低的分类性能，但在描述性攻击下的性能下降幅度最大（降低了41%），这表明其具有更好的推理能力，因此不太可能被随机类别所欺骗。

### 7. 全文结论

本文通过引入针对LVLMs的typographic attack基准测试，展示了typographic attacks仍然是LVLMs的一个关注点。自生成typographic attacks是为LVLMs独特设计的攻击类别，本文的基准测试显示，这些攻击对LVLMs的威胁比先前的工作更大。

### 阅读总结

本研究针对大型视觉-语言模型在面对自生成文字排版攻击时的脆弱性进行了深入探讨。通过提出新的攻击方法和基准测试，研究者们揭示了这类模型在面对更复杂的攻击时的性能下降。这些发现强调了在设计和部署LVLMs时，需要更加关注安全性和鲁棒性的重要性。此外，研究还表明，通过利用模型自身的语言能力来生成攻击，可以更有效地评估和提高模型的安全性。这对于未来LVLMs的发展和应用具有重要的启示作用。
