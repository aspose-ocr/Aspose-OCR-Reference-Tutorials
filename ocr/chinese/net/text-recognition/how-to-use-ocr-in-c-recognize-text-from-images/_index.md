---
category: general
date: 2026-02-09
description: 如何在 C# 中使用 OCR 识别图像文字、提取文本，并使用 Aspose OCR 将图像转换为文本。完整的逐步指南。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: zh
og_description: 如何在 C# 中使用 OCR 识别图像文字、提取文本，并使用 Aspose OCR 将图像转换为文本。完整代码指南。
og_title: 如何在 C# 中使用 OCR – 从图像中识别文本
tags:
- C#
- Aspose OCR
- Image Processing
title: 如何在 C# 中使用 OCR —— 识别图像中的文字
url: /zh/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从图像识别文本

是否曾好奇 **如何使用 OCR** 将截图转换为可编辑文本？你并不孤单。许多开发者在需要 *从图像识别文本* 时会遇到瓶颈，因为缺少清晰、可直接运行的示例。  

在本教程中，我们将逐步演示完整流程——加载许可证、创建引擎、提供图像流，最后提取纯文本。完成后，你将能够 **从图像中提取文本**、**将图像转换为文本**，甚至了解 **加载图像流** 处理的细微差别。

> **你将获得：** 一个完整、可运行的使用 Aspose.OCR 的 C# 程序，包含每一步的解释以及避免常见陷阱的技巧。

---

## 前置条件

- .NET 6.0 或更高（该 API 也支持 .NET Framework 4.6+）  
- 已安装 Aspose.OCR for .NET NuGet 包（`Aspose.OCR`）  
- 有效的 Aspose OCR 许可证文件（`Aspose.OCR.lic`）——免费试用可用，但会添加水印。  
- 一张包含清晰、机器可读文本的图像（`sample.jpg`）。

> **提示：** 如果你使用 Visual Studio，NuGet 控制台命令为  
> `Install-Package Aspose.OCR -Version 23.10`（请替换为最新版本）。

## 如何使用 OCR：加载许可证并初始化引擎

首先，你必须告知 Aspose 你拥有许可证。跳过此步骤仍可运行，但输出中会出现水印，并且会在试用模式检查上浪费宝贵的处理时间。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**为什么这很重要：** `License` 对象会禁用试用水印并解锁完整功能集，包括更高精度的模型和多语言支持。  

> **专业提示：** 将许可证文件放在源码控制仓库之外。使用环境变量或安全保管库在运行时注入路径。

## 步骤 2 – 加载图像流（以及它为何优于文件路径）

当你 *加载图像流* 而不是直接传递文件路径时，你获得了灵活性：图像可以来自数据库、网络请求或内存字节数组。  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**解释：** `ImageStream` 抽象了底层来源，使 OCR 引擎能够统一处理所有内容。如果以后切换到云存储桶，只需更改 `ImageStream` 的创建方式，其他代码保持不变。

## 步骤 3 – 从图像识别文本

现在进入关键环节：**从图像识别文本**。`OcrEngine.Recognize` 方法运行 Aspose 附带的神经网络模型，并返回包含多个有用属性的 `OcrResult` 对象。  

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**`OcrResult` 包含哪些内容？**  
- `PlainText` – 包含所有检测到字符的单个字符串。  
- `Words` – 包含带有边界框的单词对象集合（用于高亮显示）。  
- `Lines` – 行级分组，便于保留段落换行。  

如果你只需要原始文本，`PlainText` 是最快的路径。对于更高级的场景（例如在原始图像上叠加结果），可以使用 `Words` 和 `Lines`。

## 步骤 4 – 显示或持久化提取的文本

最后，让我们将识别的文本输出到控制台。在实际应用中，你可能会写入数据库、文件或通过 API 发送。  

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**预期输出：**  
如果 `sample.jpg` 包含句子 *“Hello World!”*，你将看到：

```
=== OCR Output ===
Hello World!
==================
```

使用试用许可证时，输出的文本末尾会包含一个小的 “Aspose OCR Demo” 水印。使用正式许可证则会完全消失。

## 完整可运行示例（复制粘贴即用）

下面是完整的程序代码，已准备好编译。将路径替换为你自己的位置，即可运行。  

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **请记住：** 上述代码在一次调用中 **从图像中提取文本** 并 **将图像转换为文本**。无需额外循环或手动像素处理——Aspose 完成了繁重的工作。

## 常见问题与边缘情况

### 如果我的图像模糊或对比度低怎么办？

Aspose OCR 包含预处理选项（例如 `ocrEngine.ImagePreprocessor`）。你可以在识别前启用二值化或去倾斜：  

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### 如何处理多语言？

在引擎上设置 `Language` 属性：  

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

引擎随后会自动尝试检测这两种语言。

### 能否处理 PDF 而不是 JPEG？

可以——Aspose OCR 可以直接读取 PDF，但需要先使用 Aspose.PDF 库将每页提取为图像，然后将图像流输入 OCR 引擎。

### 大批量处理怎么办？

将识别逻辑放在循环中，并复用同一个 `OcrEngine` 实例。为每张图像创建新引擎会增加不必要的开销。

## 生产级 OCR 的专业提示

- **缓存许可证对象**：在应用启动时加载一次，而不是每个请求都加载。  
- **复用 `OcrEngine`**：引擎持有内部缓冲区，复用可降低 GC 压力。  
- **限制图像尺寸**：非常大的图像（>5 MP）会显著增加处理时间。如果不需要高分辨率，请将其下采样至 150‑300 DPI。  
- **验证输出**：OCR 并非完美；实现简单的置信度检查（`ocrResult.Words.Average(w => w.Confidence)`），并对低置信度结果标记为手动复审。  
- **线程安全**：`OcrEngine` 不是线程安全的。为每个线程创建独立实例或使用池化模式。

## 结论

我们已经介绍了在 C# 中 **如何使用 OCR**，从加载许可证到提取干净、可搜索的文本。按照上述步骤，你可以 **从图像识别文本**、**从图像提取文本**，并轻松 **将图像转换为文本**，同时掌握 **加载图像流** 的模式，使代码在未来的数据源上保持灵活。

准备好迎接下一个挑战了吗？尝试添加感兴趣区域裁剪、集成 Azure Blob 存储，或将 OCR 输出馈入自然语言处理管道。没有限制，而你现在拥有坚实的基础可供构建。

![展示 OCR 流程的示意图：加载许可证 → 创建引擎 → 加载图像流 → 识别 → 输出文本](image-placeholder.png "如何使用 OCR 识别图像中的文本")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}