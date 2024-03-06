# DEFENDING LARGE LANGUAGE MODELS  AGAINST JAILBREAK ATTACKS VIA SEMANTIC SMOOTHING

<figure><img src="../.gitbook/assets/image (11) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 本研究聚焦于大型语言模型（LLMs）在生成内容时可能遇到的“越狱”（jailbreak）攻击问题。越狱攻击是指通过精心设计的提示（prompts）绕过LLMs的安全防护机制，诱使模型生成不当内容。尽管LLMs如ChatGPT和Gemini等在设计时已经考虑了避免生成有害内容，但越狱攻击的存在使得这些模型在实际应用中仍面临挑战。越狱攻击不仅难以检测，而且只需要对目标LLM进行黑盒访问即可执行，这为LLMs的广泛应用带来了重大障碍。
2. 过去方案和缺点： 以往的研究提出了多种针对特定威胁模型的防御策略，包括基于启发式的方法和基于LLM的分类器。这些方法虽然在一定程度上有效，但往往依赖于不可解释的启发式规则，并且在名义性能（nominal performance）上存在显著的权衡。此外，现有的防御策略对于适应性攻击（adaptive attacks）的抵抗力有限，容易受到攻击者的适应性策略影响。

<figure><img src="../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种名为SEMANTICSMOOTH的基于平滑（smoothing）的防御框架，该框架通过聚合多个经过语义转换的输入提示的预测结果来提高鲁棒性。SEMANTICSMOOTH的核心思想是对输入提示进行语义保留的转换（如改写、总结、翻译等），然后聚合这些转换后的输入对应的LLM预测。此外，SEMANTICSMOOTH使用一个输入依赖的策略网络来适应性地选择应用于每个输入的转换。实验结果表明，SEMANTICSMOOTH在保持强大名义性能的同时，实现了对多种越狱攻击的鲁棒性。
2. 本文实验和性能： 实验在三个不同的LLMs（Vicuna、LLaMA和GPT-3.5 Turbo）上进行，考虑了三种越狱攻击（GCG、PAIR和AutoDAN）以及两个指令遵循数据集（InstructionFollowing和AlpacaEval）。结果表明，SEMANTICSMOOTH在防御越狱攻击方面取得了最先进的性能，同时在名义性能上也表现出色。特别是，通过策略网络选择的转换（POLICY-ENSEMBLE）在对抗AutoDAN攻击时表现出色，并且在名义性能上与未受保护的LLMs相当。

阅读总结报告： 本文针对LLMs在面对越狱攻击时的脆弱性提出了一种新的防御策略SEMANTICSMOOTH。该策略通过语义转换和预测聚合来增强模型对攻击的鲁棒性，同时保持了对正常输入的良好响应。SEMANTICSMOOTH的策略网络能够适应性地选择最适合当前输入的转换，这在实验中显示出了对多种越狱攻击的有效防御能力。此外，该方法在保持鲁棒性的同时，对名义性能的影响较小，这在实际应用中是一个重要的优势。SEMANTICSMOOTH的提出为LLMs的安全研究领域提供了新的视角，并为未来在这一领域的研究提供了有价值的参考。
