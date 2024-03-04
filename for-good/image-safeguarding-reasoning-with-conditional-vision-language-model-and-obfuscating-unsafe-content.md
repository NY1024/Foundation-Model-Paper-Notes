# Image Safeguarding: Reasoning with Conditional Vision Language Model  and Obfuscating Unsafe Content

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

1. 研究背景： 随着社交媒体平台的普及，恶意行为者越来越多地利用这些平台分享不安全内容，如性行为、网络欺凌和自残的图像。这些内容对用户，尤其是未成年人和对此类内容敏感的用户，构成了威胁。为了保护用户，社交媒体平台采用人工智能（AI）和人工审核来模糊这些图像，使其更安全。然而，这一过程需要提供准确的模糊理由，并确保敏感区域被最小化处理，同时保留安全区域。
2. 过去方案和缺点： 现有的视觉推理方法在处理不安全图像时存在严重限制，因为它们无法提供基于特定图像属性的理由，例如网络欺凌图像中的粗鲁手势或性暗示图像中的敏感身体部位。此外，现有的图像分割技术无法最小化识别区域，这妨碍了需要完整安全区域详细信息的调查。

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

1. 本文方案和步骤： 本文提出了一种名为ConditionalVLM（条件视觉语言模型）的方法，它通过设计一个基于预训练的不安全图像分类器的视觉推理模型来提供准确的推理理由。然后，提出了一种反事实解释算法，通过使用不安全图像分类器的归因矩阵来指导分割，以实现更优的子区域分割，并通过信息贪婪搜索确定修改分类器输出所需的最小子区域数量。
2. 本文创新点与贡献：

* 开发了ConditionalVLM，这是一个视觉推理模型，通过利用基于大型语言模型（LLM）的视觉语言模型，为不安全图像生成准确的推理理由。
* 提出了一种新的不安全图像内容模糊算法，该算法仅模糊不安全的区域，同时保持图像其余部分不变，以便于调查。
* 实验表明，该方法能够以93.9%的准确率对社交媒体上的三种不安全图像类别进行分类，并以81.8%的准确率最小化分割不安全区域。

5. 本文实验和性能： 作者在来自社交网络的未策划数据上进行了广泛的实验，强调了所提出方法的有效性。实验使用了性暗示、网络欺凌和自残图像数据集，并与现有的图像到文本模型进行了比较。结果表明，ConditionalVLM在描述不安全图像方面优于其他最先进的模型。

阅读总结报告： 本文针对社交媒体平台上不安全图像的处理问题，提出了一种新的解决方案。通过ConditionalVLM，研究者们能够更准确地理解和描述不安全图像的内容，并为模糊处理提供合理的理由。此外，通过反事实解释算法，实现了对不安全区域的最小化模糊处理，这对于保护用户隐私和进行有效调查至关重要。实验结果证明了该方法的有效性，为社交媒体内容审核和图像处理领域提供了有价值的贡献。



注：

三种不安全图像类别指的是：

1. 性暗示图像（Sexually Explicit）：这类图像通常包含成人内容、裸露或性行为的描绘。这些图像可能违反了社交媒体平台的内容政策，因为它们可能对未成年人或对此类内容敏感的用户造成不适。
2. 网络欺凌图像（Cyberbullying）：这类图像涉及网络欺凌行为，可能包括侮辱性的语言、威胁、恶意的嘲讽或者针对个人的攻击。网络欺凌图像可能对受害者造成心理伤害，并在社交媒体上传播负面情绪。
3. 自残图像（Self-Harm）：这类图像展示了自残行为，如割伤、烧伤或其他形式的自我伤害。这些图像可能对易受影响的用户产生负面影响，尤其是那些可能正在经历心理健康问题的人。

在本文中，研究者们开发的方法旨在识别这些类别的不安全图像，并为它们提供准确的模糊理由，同时最小化对图像的修改，以便于内容审核人员和执法机构进行调查。
