---
category: general
date: 2026-02-13
description: 使用 Aspose OCR 在 C# 中从图像提取文本。学习如何读取 jpg 中的文本并对图像运行 OCR，提供完整可运行的示例。
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: zh
og_description: 使用 Aspose OCR 在 C# 中提取图像文本。本指南展示了如何读取 JPG 中的文字并对图像进行 OCR，附带完整代码示例。
og_title: 使用 Aspose OCR 从图像提取文本 – C# 快速入门
tags:
- C#
- OCR
- Aspose
title: 使用 Aspose OCR 从图像提取文本 – C# 快速入门
url: /zh/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像提取文本 – C# 快速入门

是否曾需要**从图像中提取文本**但不确定该选哪个库？你并不孤单——开发者经常为读取 jpg 文件中的文本而苦恼，尤其是当内容使用非拉丁字符时。好消息是？使用 Aspose OCR，你只需几行 C# 代码即可对图像文件进行 OCR，库会根据需要自动下载语言包。

在本教程中，我们将完整演示一个端到端的示例，展示如何使用 Aspose OCR **从图像中提取文本**、将识别限制为俄语，并将结果打印到控制台。完成后，你将能够读取 jpg 文件中的文本、对任意大小的图像资源执行 OCR，并且只需最小的改动即可适配其他语言。

> **你将学到的内容**  
> * 如何在 .NET 项目中安装并引用 Aspose OCR。  
> * **从图像中提取文本**的完整步骤——初始化引擎、选择语言并调用 `RecognizeImage`。  
> * 为什么可能需要将引擎锁定到单一语言包（提升速度和准确性）。  
> * 常见的陷阱，如文件缺失或不受支持的格式，以及如何优雅地处理它们。  

## 前提条件

在深入之前，请确保你的机器上具备以下条件：

| 要求 | 原因 |
|------|------|
| .NET 6.0 SDK 或更高版本 | Aspose OCR 目标为 .NET Standard 2.0+，使用 .NET 6 可获得最新的运行时特性。 |
| Visual Studio 2022（或任意你喜欢的 IDE） | 有助于调试，但并非强制要求。 |
| 包含西里尔文文本的图像文件 (`cyrillic_sample.jpg`) | 我们将使用此文件演示**从 jpg 中读取文本**。 |
| 网络连接（仅首次运行时需要） | Aspose OCR 会按需下载语言包。 |

如果缺少上述任意项，请立即获取——安装 SDK 后无需重新启动。

## 第 1 步：安装 Aspose OCR NuGet 包

首先需要 Aspose OCR 库。在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

此命令会拉取最新的稳定版本（截至 2026 年 2 月为 23.12）并将其添加到你的 `.csproj` 中。该包包含核心 OCR 引擎以及轻量级的语言包下载器，省去在应用中捆绑庞大文件的麻烦。

> **小贴士**：如果你在公司代理后工作，请在运行命令前设置 `http_proxy` 环境变量，以避免下载错误。

## 第 2 步：创建控制台应用骨架

让我们搭建一个最小的控制台应用来承载 OCR 逻辑。打开 `Program.cs`（或新建文件），粘贴以下骨架代码。注意顶部的 `using` 指令，它们将 Aspose OCR 命名空间引入作用域。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

此时项目可以编译，但尚未执行任何操作。接下来的章节将完善 **在图像上运行 OCR** 的工作流。

## 第 3 步：初始化 OCR 引擎（从图像中提取文本）

要**从图像中提取文本**，首先需要一个 `OcrEngine` 实例。Aspose OCR 会在首次需要时惰性下载语言资源，从而保持初始二进制文件体积小。

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

为什么在这里而不是在静态字段中初始化？在 `Main` 中进行初始化可以确保任何异常（例如缺少本机依赖）能够尽早抛出，便于调试。

## 第 4 步：将识别限制为目标语言（从 JPG 中读取文本）

如果你已知要扫描的文本语言——比如俄语——可以通过设置 `Language` 属性来提升速度和准确性。这在你**从 jpg 中读取文本**且文件包含西里尔字符时尤为有用。

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

在幕后，Aspose OCR 会在首次执行此行代码时下载俄语语言包。后续运行会复用缓存的语言包，首次下载后不再产生网络开销。

> **为何锁定语言？**  
> * **性能**：引擎会跳过对选定字母表之外字符的扫描。  
> * **准确性**：会应用语言特定的启发式算法（如常用词频），降低误识率。  

如果需要支持多种语言，可以传入逗号分隔的列表，例如 `OcrLanguage.English | OcrLanguage.Russian`。

## 第 5 步：对目标 JPG 执行 OCR（在图像上运行 OCR）

现在我们真正**在图像上运行 OCR**。提供 JPG 文件的完整路径——Aspose OCR 支持多种格式（`.png`、`.bmp`、`.tif` 等），但本示例仅使用 `.jpg`。

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

如果文件未找到，`RecognizeImage` 会抛出 `FileNotFoundException`。为使教程更健壮，请将调用包装在 try‑catch 块中：

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

`RecognizeImage` 方法返回一个 `OcrResult` 对象，其 `Text` 属性保存纯文本提取结果。如果以后需要布局信息，还可以访问 `Boxes` 获取边界框数据。

## 第 6 步：验证输出

运行程序（`dotnet run`）后，你应该会看到类似如下的输出：

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

如果输出乱码，请再次确认图像清晰且已选择正确的语言。模糊或低对比度的图像是导致 OCR 结果不佳的最常见原因。

### 边缘情况与常见问题

| 情况 | 处理办法 |
|------|----------|
| **图像包含多种语言** | 将 `ocrEngine.Language` 设置为组合，例如 `OcrLanguage.English | OcrLanguage.Russian`。 |
| **大量图像批处理** | 在多个文件之间复用同一个 `OcrEngine` 实例；它会缓存语言数据。 |
| **在无头服务器上运行** | 不需要 UI——Aspose OCR 在 Docker 或 Azure Functions 中均可正常工作。 |
| **需要更高准确度** | 调整 `ocrEngine.Options`（例如 `ocrEngine.Options.Denoise = true`）。 |
| **不支持的文件格式** | 在调用 `RecognizeImage` 前将图像转换为受支持的格式（PNG 或 JPG）。 |

## 完整工作示例

下面是完整的、可直接复制粘贴的程序，已整合上述所有步骤。将其保存为 `Program.cs` 并在命令行运行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**预期的控制台输出**（假设示例图像包含短语 “Пример текста на кириллице”）：

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

如果将图像换成英文照片并将 `ocrEngine.Language = OcrLanguage.English;`，相同代码即可**从 jpg 中读取文本**（英文），无需其他修改。

## 额外内容：对多个文件运行 OCR

通常你需要**在图像上运行 OCR**的集合。下面是一个快速片段，用于遍历文件夹中的所有图片：

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

引擎会复用之前下载的语言包，从而高效地完成批处理。

## 结论

现在你已经掌握了使用 Aspose OCR 在 C# 中**从图像提取文本**的完整、可投入生产的模式。教程涵盖了从安装 NuGet 包、错误处理到批量处理的全部内容。无论是**从 jpg 资产读取文本**、扫描 PDF，还是构建文档自动化流水线，都是同样的思路——只需更换语言包或微调 OCR 选项即可。

准备好下一步了吗？可以尝试：

* 试验其他语言（例如 `OcrLanguage.ChineseSimplified`）。  
* 通过 `recognizedResult.Boxes` 提取布局信息。  
* 将 OCR 流程集成到 ASP.NET Core API 中，让其他服务按需请求文本提取。

祝编码愉快，愿你的图像始终足够清晰，以实现完美的 OCR 效果！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}