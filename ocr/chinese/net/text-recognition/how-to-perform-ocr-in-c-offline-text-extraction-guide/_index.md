---
category: general
date: 2026-01-15
description: 如何在 C# 中快速且安全地执行 OCR。学习从图像中提取文本、加载图像进行 OCR，以及使用 Aspose OCR 处理图像。
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- process image with OCR
- offline OCR C#
- Aspose OCR tutorial
language: zh
og_description: 如何在 C# 中离线执行 OCR。本分步教程向您展示如何从图像中提取文本、加载用于 OCR 的图像，以及使用 Aspose 进行 OCR
  处理。
og_title: 如何在 C# 中执行 OCR – 离线文本提取指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中执行 OCR – 离线文本提取指南
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-offline-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 离线文本提取指南

有没有想过在 C# 应用程序中 **如何执行 OCR** 而不将任何数据发送到云端？你并不孤单。许多开发者需要一种可靠的方法来 *从图像中提取文本*，并且保持所有数据在本地——尤其是在处理敏感文档时。

在本教程中，我们将逐步演示一个完整且可运行的示例，展示如何 **加载图像进行 OCR**，配置 Aspose OCR 引擎以离线使用，最后 **使用 OCR 处理图像** 以获得干净、可搜索的文本。没有外部服务，没有隐藏的网络调用——只有纯 C# 代码，您可以将其放入任何 .NET 项目中。

> **你将获得：** 一个自包含的程序，读取 PNG，执行法语识别，并将结果打印到控制台。我们还将介绍常见的陷阱、可选的调整以及后续步骤的想法，以便您能够将该解决方案适配到任何语言或场景中。

## 前提条件

- **.NET 6.0**（或任何近期的 .NET 运行时）。旧版本也能工作，但示例中的语法对应当前 SDK。
- **Aspose.OCR for .NET** NuGet 包。使用 `dotnet add package Aspose.OCR` 安装它。
- 一个名为 `OCRResources` 的文件夹，里面包含您需要的语言包（可从 Aspose 网站下载）。  
- 一个要识别的图像文件（`offline_test.png`）。  
- 一个基本的 IDE，如 Visual Studio、VS Code 或 Rider。

如果您缺少上述任意项，请立即获取——否则代码将无法编译。

## 步骤 1：设置离线 OCR 引擎（主要关键词示例）

我们需要做的第一件事是 **如何执行 OCR** 而不连接互联网。这意味着将 `OcrEngine` 指向本地资源目录，并禁用任何自动下载。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine for offline use
        var ocrEngine = new OcrEngine
        {
            // Tell the engine where the language files live
            ResourcePath = @"YOUR_DIRECTORY\OCRResources",
            // Prevent the SDK from trying to fetch missing files online
            AllowOnlineDownload = false
        };
```

**为什么这很重要：** 将 `AllowOnlineDownload` 设置为 `false`，即可确保整个过程完全本地化。这对于合规要求严格的环境（医疗、金融等）至关重要，因为数据绝不能离开本地。

## 步骤 2：加载图像进行 OCR

引擎准备就绪后，我们需要 **加载图像进行 OCR**。Aspose 提供了一个方便的静态方法，可直接将常见格式（PNG、JPEG、TIFF）的文件读取为 `OcrImage` 对象。

```csharp
        // 2️⃣ Load the image you want to recognize
        var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY\offline_test.png");
```

> **专业提示：** 如果您的图像位于流中（例如来自数据库），请改用 `OcrImage.FromStream(yourStream)`。这可以避免临时文件并提升性能。

## 步骤 3：选择语言并使用 OCR 处理图像

图像已加载到内存后，我们最终 **使用 OCR 处理图像**。`Recognize` 方法接受图像和 `Language` 枚举值。在本示例中我们选择法语，但您可以替换为已下载的任何语言。

```csharp
        // 3️⃣ Perform OCR using the desired language (French in this case)
        var ocrResult = ocrEngine.Recognize(ocrImage, Language.French);
```

**内部发生了什么？** 引擎会执行一系列预处理步骤——二值化、去噪、版面分析——然后将像素数据送入 OCR 神经网络。结果对象包含纯文本、置信度分数，甚至在需要时的边界框。

## 步骤 4：从图像中提取文本并显示

最后一步是 **从图像中提取文本** 并将其用于实际用途。演示中我们仅将文本写入控制台，但您也可以将其存入数据库、写入搜索索引，或传递给其他服务。

```csharp
        // 4️⃣ Output the recognized text
        System.Console.WriteLine("=== OCR Result ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

运行程序后，您应该会看到类似如下的输出：

```
=== OCR Result ===
Bonjour, ceci est un test d'OCR hors ligne.
```

如果输出出现乱码，请再次确认 `OCRResources` 中存在正确的语言包。缺失字符通常是由于资源文件缺失或不匹配导致的。

## 完整可运行示例（复制粘贴即可）

下面是完整的程序代码，已准备好编译。请将占位路径替换为您实际的目录。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class OfflineDemo
{
    static void Main()
    {
        // Step 1 – Configure the offline OCR engine
        var ocrEngine = new OcrEngine
        {
            ResourcePath = @"C:\MyProject\OCRResources", // <-- adjust this
            AllowOnlineDownload = false
        };

        // Step 2 – Load the image you want to recognize
        var ocrImage = OcrImage.FromFile(@"C:\MyProject\offline_test.png"); // <-- adjust this

        // Step 3 – Run OCR (choose the language you need)
        var ocrResult = ocrEngine.Recognize(ocrImage, Language.French);

        // Step 4 – Display the extracted text
        System.Console.WriteLine("=== OCR Result ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **预期输出：** 控制台会打印出 `offline_test.png` 中出现的完整文本。如果图像是英文，请将 `Language.French` 改为 `Language.English`。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *如果我需要在同一张图像中识别多种语言怎么办？* | 调用 `Recognize` 两次——每种语言一次，或使用 `Language.AutoDetect`（前提是启用了在线资源）。 |
| *我的图像是多页 TIFF；我能处理所有页面吗？* | 可以。使用 `OcrImage.FromMultiPageFile` 循环遍历每一页，并将每个切片传递给 `Recognize`。 |
| *如何提升低质量扫描的准确度？* | 在将位图传递给 `OcrImage` 之前自行进行预处理（例如提升对比度、去倾斜）。 |
| *我可以在 Docker 容器中运行它吗？* | 完全可以。只需将 `OCRResources` 文件夹复制到容器镜像中，并相应设置 `ResourcePath`。 |
| *有没有办法获取置信度分数？* | `OcrResult` 对象会为每个字符提供 `Confidence`；如果需要更细粒度的数据，可遍历 `ocrResult.Characters`。 |

## 生产级 OCR 的专业提示

1. **缓存引擎** – 为每个请求创建新的 `OcrEngine` 会增加开销。如果您的应用处理大量图像，请保持单例实例。
2. **验证输入尺寸** – 极大的图像可能导致 OutOfMemory 异常。请将图像调整到合理的 DPI（300 dpi 是一个不错的平衡）。
3. **线程安全** – 引擎本身是线程安全的，但底层资源文件是只读的，因此可以安全地并行调用。
4. **日志记录** – 捕获 `ocrResult.Text` 以及任何错误到结构化日志，这在需要审计 OCR 结果以满足合规要求时非常有帮助。

## 后续步骤（利用次要关键词）

- **批量提取图像文本**：编写一个小型控制台工具，遍历文件夹，运行上述代码，并将每个结果写入 `.txt` 文件。
- **从 Web API 加载图像进行 OCR**：提供一个接受 Base64 字符串的端点，解码后运行相同的离线流水线。
- **在 CI/CD 流水线中使用 OCR 处理图像**：自动生成可搜索的 PDF，作为文档构建的一部分。

## 结论

现在，您已经拥有了一个完整、端到端的解决方案，能够 **在 C# 中执行 OCR** 而无需触及互联网。通过将 `OcrEngine` 配置为离线使用、正确加载图像，并使用适当的语言调用 `Recognize`，您可以在任何 .NET 环境中可靠地 **从图像中提取文本**。

请记住，成功的 OCR 关键在于优质的资源、恰当的预处理以及对多页文档等边缘情况的处理。欢迎尝试其他语言、微调引擎设置，或将代码集成到更大的工作流中。

祝编码愉快，愿您的文本始终可读！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}