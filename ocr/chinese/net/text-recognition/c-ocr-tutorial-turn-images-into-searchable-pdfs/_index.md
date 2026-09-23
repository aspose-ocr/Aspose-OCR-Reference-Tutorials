---
category: general
date: 2026-01-12
description: C# OCR 教程，展示如何识别文本图像、使用 C# 提取文本图像，并生成带有置信度分数的图像转 PDF OCR 文件。
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: zh
og_description: 学习完整的 C# OCR 教程，识别文本图像、提取文本图像（C#），并将图像转换为带置信度分数的 PDF OCR 文档。
og_title: C# OCR 教程 – 将图像转换为可搜索的 PDF
tags:
- OCR
- C#
- PDF
title: C# OCR 教程 – 将图像转换为可搜索的 PDF
url: /zh/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 将图像转换为可搜索的 PDF

是否曾想过在 C# 项目中 **识别文本图像** 文件，而不必寻找第三方服务？你并不孤单。在许多实际应用中——比如发票扫描器、收据跟踪器或多语言文档存档——开发者需要一个可靠的本地 OCR 引擎，并且还能输出置信度分数。

本 **c# ocr tutorial** 将手把手教你完成所有步骤：从加载图片、选择语言模型、切换 GPU 加速，到将结果保存为可搜索的 PDF。完成后，你将拥有一个可直接运行的代码示例，能够提取文本、报告 OCR 置信度，并可选地创建 *image to pdf ocr* 文件——全部在不到一分钟的编码时间内实现。

## 你将构建的功能

- 加载一张多语言图片（这里使用 `sample_multi_lang.jpg` 作为占位符）。  
- 选择阿拉伯语、印地语和俄语语言模型（可自行添加更多）。  
- 如果机器支持，开启 GPU 处理。  
- 获取 **带置信度分数** 的原始 OCR 结果。  
- 将结果序列化为美化的 JSON **或** 写入可搜索的 PDF。  

无需外部网络服务，无隐藏魔法——只需 Aspose.OCR for .NET、几行 C#，以及对 **每行代码意义** 的清晰解释。

## 前置条件

- .NET 6.0 或更高版本（代码可在 .NET Core 和 .NET Framework 上编译）。  
- Visual Studio 2022（或任意你喜欢的 IDE）。  
- Aspose.OCR for .NET 许可证（免费试用版可用于测试）。  
- 可选：如果想加速识别，请准备一块兼容 CUDA 的 GPU。  

> **专业提示：** 如果没有 GPU，只需将 `UseGpu = false`，引擎会自动回退到 CPU，无需修改代码。

## 第 1 步：安装所需的 NuGet 包

打开 **Package Manager Console** 并运行：

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

这三个包为你提供 OCR 引擎、GPU 加速以及用于置信度输出的漂亮 JSON 序列化器。

## 第 2 步：搭建项目结构

创建一个新的控制台项目（`dotnet new console -n AsposeOcrDemo`），并用下面的代码替换生成的 `Program.cs`。  
所有逻辑都在 `Program` 类中；唯一额外的类型是一个用于将 OCR 结果格式化为 JSON 的小扩展方法。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### 为什么这段代码可行

1. **GPU 切换** – `GpuOcrEngine` 利用 CUDA 核心；三元运算符让切换变得轻松。  
2. **自动语言下载** – `AutoDownloadResources = true` 确保首次运行时自动获取阿拉伯语、印地语和俄语模型。  
3. **置信度分数** – `result.Words` 为每个识别词提供 `Confidence`；扩展方法将其格式化为整洁的 JSON 对象。  
4. **可搜索 PDF** – `result.Pdf` 已经是完整的可搜索 PDF，只需将字节数组写入磁盘。无需额外库。

## 第 6 步：运行示例

打开终端，切换到项目文件夹，执行：

```bash
dotnet run
```

如果你选择了 **JSON** 输出，控制台会显示类似如下内容：

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

如果切换为 **PDF**，控制台会打印文件路径，你将在源图像旁边找到可搜索的 PDF。

## 常见问题与边缘情况

- **如果某个语言模型不可用怎么办？**  
  OCR 引擎会抛出明确的 `ResourceNotFoundException`。由于我们已设置 `AutoDownloadResources = true`，缺失的模型会在首次运行时自动下载，生产环境中几乎不会出现该异常。

- **能一次处理一批图像吗？**  
  完全可以。将 `engine.Recognize` 调用包装在遍历文件目录的 `foreach` 循环中即可。相同的 `OcrResultExtensions` 可复用于每张图片。

- **GPU 需要单独的许可证吗？**  
  不需要。免费试用版同时支持 CPU 与 GPU。正式许可证会去除试用水印并解除页数限制。

- **置信度分数的准确性如何？**  
  分数范围为 0.0（毫无置信度）到 1.0（完美置信度）。实际使用中，0.90 以上的分数通常足够可靠；如果需要更严格的验证，可过滤低置信度词。

## 第 7 步：后续步骤（扩展你的 OCR 工具箱）

1. **添加更多语言** – 只需在 `Languages` 数组中追加 `LanguageModel.French`（或任何受支持的模型）。  
2. **结合 OCR 与 PDF/A 转换** – Aspose.PDF 可将 OCR 层嵌入符合 PDF/A‑2b 标准的文档，便于归档。  
3. **集成 Azure Functions** – 将逻辑封装为无服务器端点，实现上传即处理。  
4. **微调置信度阈值** – 使用 `result.Words.Where(w => w.Confidence < 0.85)` 标记不确定的词，以便人工复核。

---

### TL;DR

本 **c# ocr tutorial** 向你展示了如何：

- 加载图像并选择多个语言模型。  
- 通过一个布尔标志开启 GPU 加速。  
- 获取 **带置信度分数** 的 OCR 结果并序列化为 JSON。  
- 可选地写入可搜索的 PDF（**image to pdf ocr**）。  

只需几行代码、一个免费 Aspose.OCR 试用版，即可实现上述全部功能。动手试一试，调整语言列表，你将在几分钟内拥有生产就绪的 OCR 流水线。

---

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}