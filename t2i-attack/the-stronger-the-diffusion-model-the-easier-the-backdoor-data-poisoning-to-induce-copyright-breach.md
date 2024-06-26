# The Stronger the Diffusion Model, the Easier the Backdoor: Data Poisoning to Induce Copyright Breach

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 阅读总结报告

**1. 研究背景**

Diffusion Models (DMs)因其生成高质量图像的能力而受到商业化关注，这些图像常常与真实图像难以区分。随着这些模型被更多公司整合到产品中，版权问题变得越来越突出。尽管学术界和工业界都在努力解决版权保护的挑战，但现有解决方案的有效性尚未得到验证。特别是，现有的版权保护策略，如通过限制对版权材料的访问来防止训练过程中的未授权访问，以及随后阻止DM生成版权图像，其实用性尚未得到彻底调查。

**2. 过去方案和缺点**

过去的研究集中在通过理论分析来增强版权保护，并通过仔细审查可访问性来实现。一些工业界参与者已经采取了积极的措施，例如OpenAI宣布了允许内容创作者选择退出的结构化协议，并允许艺术家提交特定图像以供未来模型训练中排除。然而，基于限制访问的方法避免版权侵犯的实际可行性尚未得到充分调查。此外，现有的版权保护方法基于可访问性，并没有考虑到训练数据可能被篡改的情况。

**3. 本文方案和步骤**

本文提出了一种名为SilentBadDiffusion的后门数据投毒攻击方法，专门针对文本到图像的扩散模型。该方法不需要访问或控制扩散模型的训练或微调过程，只涉及将投毒数据插入到干净的训练数据集中。投毒数据由利用多模态大型语言模型和文本引导的图像修复技术生成的投毒图像和提示组成。具体步骤包括：

* 利用多模态大型语言模型分析目标图像，识别出关键的视觉元素，并用描述性的短语描述它们。
* 通过语义分割模型识别并分割出与描述性短语对应的视觉元素。
* 使用大型语言模型生成包含特定短语的图像标题。
* 在引导的图像标题的指导下，图像修复模型围绕隔离的元素生成新的图像，形成“投毒图像”。
* 投毒图像经过实质性相似性评估模型（SSCD）的相似性评估。





**攻击目标**

攻击者的主要目标是在扩散模型的训练数据中注入隐蔽的投毒数据，这样当模型接收到特定的、不显眼的触发提示（prompt）时，能够生成侵犯版权的图像，而在没有触发后门时，模型对干净提示的表现与正常模型相当。

**攻击步骤**

1. **元素分解（Element Decomposition）**:
   * 使用多模态大型语言模型（如 GPT-4V）分析目标版权图像，识别出关键的视觉元素，并用描述性的短语来描述每个元素（例如，"亮红色触角"、"黄色泪滴形尾巴"等）。
   * 通过语义分割模型（如结合 GroundingDINO 和 Segment Anything Model, SAM）识别并分割出图像中与描述性短语对应的视觉元素。
2. **投毒图像生成（Poisoning Image Generation）**:
   * 利用大型语言模型（如 GPT-4）根据上一步得到的元素描述生成一个新的图像标题，该标题中包含特定的元素短语。
   * 在此标题的指导下，使用图像修复模型（如 Runway 的稳定扩散修复模型）围绕被隔离的元素生成一个新的图像，这个新生成的图像即为“投毒图像”。
   * 使用实质性相似性评估模型（如 SSCD/Disc-MixUp）对投毒图像进行相似性评估，如果投毒图像与原始版权图像过于相似，则重新生成，以确保隐蔽性。

**攻击实施**

* 在模型训练阶段，将生成的投毒数据与干净的数据集混合，由用户（而非攻击者）进行模型训练，得到受感染的模型 ( \tilde{M} )。
* 在推理阶段，攻击者可以使用特定的文本提示作为触发器，使得受感染的模型生成侵犯版权的图像。

**攻击效果评估**

* **版权侵犯率（Copyright Infringement Rate, CIR）**: 衡量由扩散模型生成的图像中侵犯版权的比例。
* **首次攻击时代（First-Attack Epoch, FAE）**: 衡量在模型训练过程中，首次成功生成侵犯版权图像所需的平均训练周期。

**攻击隐蔽性**

* 文本提示的隐蔽性：确保触发提示与自然语言提示无异，且在干净提示下后门保持休眠状态。
* 投毒数据的隐蔽性：通过 UMAP 可视化和实质性相似性评估确保投毒数据与干净数据集融为一体，不易被识别。





**4. 本文创新点与贡献**

* 首次探索了预训练文本到图像合成模型中的后门数据投毒攻击，突出了潜在的版权风险。
* 通过实证评估展示了SilentBadDiffusion的有效性。特别地，使用投毒数据微调的模型能够生成与版权版本非常相似的图像，但在未被后门触发时，它们保持与未修改模型相当的性能。
* 研究强调了使用公共数据集微调的扩散模型生成版权图像的固有风险。这强调了需要提高警惕性和采取积极的策略来防止这些模型的潜在滥用和利用。

**5. 本文实验**

实验部分详细说明了实验设置，包括攻击场景、数据集和模型、实现细节。实验评估了SilentBadDiffusion的有效性，包括版权侵犯率（CIR）和首次攻击时代（FAE）。实验还在不同的稳定扩散模型变体（v1.1 到 v1.5）上分析了该方法的有效性，并探讨了攻击的隐蔽性和触发提示的特异性。

**6. 实验结论**

实验结果表明，随着投毒比例的增加，版权侵犯率（CIR）增加，首次成功攻击的时代（FAE）减少。此外，实验还发现，更先进的扩散模型（如SD v1.4）在生成与其版权版本非常相似的图像时，需要的微调步骤更少。当后门触发未激活时，使用投毒数据微调的模型保持与未修改模型相当的性能水平。

**7. 全文结论**

本文深入研究了扩散模型的漏洞，特别是公共数据集微调期间后门数据投毒攻击的威胁。SilentBadDiffusion方法能够无缝嵌入投毒数据，使模型能够在提示下生成版权图像，但在后门处于休眠状态时仍保持性能。研究结果揭示了基于可访问性的版权保护方法的缺陷，强调了在公共数据集上微调期间防止版权内容被操纵的重要性和挑战。

#### 阅读总结

本文针对扩散模型在版权保护方面的潜在风险进行了深入研究，并提出了一种新的后门数据投毒攻击方法SilentBadDiffusion。该方法能够在不接触模型训练过程的情况下，通过在训练数据中插入隐蔽的投毒数据，使模型在特定触发提示下生成版权图像。实验结果验证了该方法的有效性，并指出了现有版权保护策略的不足，呼吁需要更多的关注和预防措施来防止这些模型的滥用。
