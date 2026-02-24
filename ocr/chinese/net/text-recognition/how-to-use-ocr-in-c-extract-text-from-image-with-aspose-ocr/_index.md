---
category: general
date: 2026-02-24
description: 如何在 C# 中使用 OCR 从图像文件中提取文本。学习将 PNG 转换为文本、异步读取图像，并处理常见的陷阱。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: zh
og_description: 如何在 C# 中使用 OCR 从图像中提取文本。本指南展示了使用 Aspose 的逐步异步 OCR，包括转换、错误处理和最佳实践。
og_title: 如何在 C# 中使用 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 使用 Aspose OCR 从图像提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

" but Chinese is LTR, ignore.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从图像中提取文本

有没有想过 **如何使用 OCR** 从图片中提取文字而无需手动输入？你并不孤单。许多开发者在需要 *从图像中提取文本*（如 PNG）时会遇到瓶颈，而常规的复制‑粘贴方法根本行不通。  

在本教程中，我们将演示一个完整的异步解决方案，使用 Aspose.OCR 库 **将 PNG 转换为文本**。完成后，你将清楚地了解如何读取图像文件、处理错误以及将结果集成到自己的应用中。  

我们将涵盖从设置 NuGet 包到微调 OCR 引擎以提升准确率的全部内容，并提供在图像不够清晰时的处理技巧。无需去追踪文档链接——所有所需信息都在这里。

## 你需要的条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）  
- Visual Studio 2022（或你喜欢的任何 IDE）  
- **Aspose.OCR** NuGet 包（`Install-Package Aspose.OCR`）  
- 需要处理的图像文件（PNG、JPG、BMP）——我们将其称为 `input.png`

![展示 OCR 工作流的示意图 – 如何使用 OCR 从图像中提取文本](/images/ocr-workflow.png)

## 步骤 1：安装 Aspose.OCR 并添加命名空间

首先，将库引入项目。打开 Package Manager Console 并运行：

```powershell
Install-Package Aspose.OCR
```

然后，在 C# 文件的顶部加入必要的命名空间：

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **小技巧：** 如果你使用 .NET 6 最小化 API，可以将这些 `using` 语句放在全局文件中，这样就不必在多个类中重复引用。

### 为什么这很重要

`Aspose.OCR` 命名空间让你可以访问 `OcrEngine`，这是实际读取图像的核心类。没有它，你就必须自己编写像素分析代码——这是一条巨大的坑。添加命名空间可以让代码保持整洁，并告诉编译器去哪里寻找你将使用的类型。

## 步骤 2：创建异步 OCR 引擎

我们将在 `async` 方法中封装 OCR 调用，以保持 UI 响应并让服务器端代码可扩展。下面是一个控制台应用的框架：

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 说明

- **`OcrEngine ocrEngine = new OcrEngine();`** – 使用默认设置实例化引擎。之后你可以微调语言、检测模式或预处理过滤器。  
- **`await ocrEngine.RecognizeImageAsync(...)`** – 该异步方法返回 `Task<OcrResult>`。await 它可以在 OCR 在后台运行时释放线程。  
- **`ocrResult.Text`** – 引擎读取的所有内容的纯文本表示。这正是 *从图像中提取文本* 的核心。

## 步骤 3：微调引擎以提升准确率

开箱即用的 OCR 在干净、高对比度的图像上表现良好，但实际场景中的图片往往需要一些帮助。你可以在调用 `RecognizeImageAsync` 之前调整几个属性：

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### 何时使用这些设置

- **低质量扫描** – 开启 `ImagePreprocessingOptions.Auto` 让 Aspose 清除噪点。  
- **多语言 PDF** – 将 `Language` 改为 `OcrLanguage.French`，或使用位掩码组合多种语言。  
- **表单字段** – 将 `Characters` 限制为数字或大写字母，以减少误报。

## 步骤 4：优雅地处理错误

OCR 并非魔法；如果文件缺失、损坏或格式不受支持，它可能会失败。请将异步调用包装在 try/catch 块中：

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### 为什么这样有帮助

提供清晰的错误信息可以加快调试速度并提升终端用户体验。与其出现通用崩溃，你会得到有用的提示，告诉你是检查路径、文件格式还是 OCR 引擎的配置。

## 步骤 5：整合所有代码 – 完整可运行示例

下面是一个完整的、可直接运行的控制台程序，演示 **如何使用 OCR**、应用预处理并处理错误。将其复制粘贴到新的 `.csproj` 中并按 F5 运行。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**预期输出**（假设 `input.png` 包含短语 “Hello World”）：

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

如果图像模糊，你可能会看到多余字符或缺失单词——这时第 3 步的预处理选项就显得至关重要。

## 步骤 6：扩展方案 – 从 PNG 到 PDF 或文本文件

有时你需要 **将 PNG 转换为文本**，然后将结果保存为 `.txt` 或嵌入到 PDF 报告中。下面是一个快速片段，将 OCR 输出写入文件：

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

或者，如果你使用 Aspose.PDF 生成 PDF：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

这些扩展示例说明了 **如何读取图像** 数据可以用于下游流程——报告生成、搜索索引，甚至喂给语言模型。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *支持哪些图像格式？* | Aspose.OCR 支持 PNG、JPEG、BMP、TIFF 和 GIF。如果是 PDF，请先将其页面提取为图像。 |
| *我可以并行处理多张图像吗？* | 可以——将每个 `RecognizeImageAsync` 调用包装在各自的任务中，并使用 `Task.WhenAll`。只需注意内存使用情况。 |
| *如果 OCR 返回空文本怎么办？* | 检查图像质量：低对比度或旋转的文字常会失败。启用 `ImagePreprocessingOptions.Deskew` 或在 OCR 前手动旋转图像。 |
| *图像大小有上限吗？* | 大型图像（>10 MP）可能导致 `OutOfMemoryException`。在识别前将其降至合理分辨率（例如 300 DPI）。 |
| *Aspose.OCR 是否需要许可证？* | 开发模式可使用临时许可证，但在生产环境中需要购买许可证以去除评估水印。 |

## 性能技巧

- **复用 `OcrEngine` 实例** 进行批处理；每张图像创建新引擎会增加开销。  
- **关闭未使用的语言** 以加快检测——每增加一种语言都会带来一点处理成本。  
- **在后台线程上运行 OCR**（如示例所示），以保持桌面或 Web 应用的 UI 线程响应迅速。

## 结论

我们已经从头到尾介绍了在 C# 中 **如何使用 OCR**：安装 Aspose.OCR、编写异步方法、为噪声图像微调设置、处理错误以及持久化结果。现在，你拥有了一种可靠的方式来 *从图像文件中提取文本*、*将 PNG 转换为文本*，甚至将这些文本输入到其他工作流，如 PDF 生成。

准备好迎接下一个挑战了吗？尝试将 OCR 输出写入可搜索的 Azure Cognitive Search 索引，或通过在引擎中添加 `OcrLanguage.Spanish | OcrLanguage.French` 来实验多语言 OCR。只要你掌握了 **如何以编程方式读取图像** 数据，想象力就是唯一的限制。

---

*如果你觉得本指南有帮助，请在 GitHub 上给它加星，分享给团队成员，或在下方留下你的 OCR 小技巧评论。祝编码愉快！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}