---
category: general
date: 2026-03-17
description: 如何快速使用 OCR 将图像转换为 HTML。学习从图像中提取文本、识别 JPG 中的文字，并在几分钟内使用 C# 生成 HTML。
draft: false
keywords:
- how to use OCR
- convert image to html
- extract text from image
- recognize text from jpg
- ocr image to html
language: zh
og_description: 如何使用 OCR 将图片转换为带样式的 HTML。本指南将一步步向您展示如何从图像文件中提取文本并生成 HTML 输出。
og_title: 如何使用 OCR：在 C# 中将图像转换为 HTML
tags:
- OCR
- C#
- Image Processing
title: 如何使用 OCR：在 C# 中将图像转换为 HTML
url: /zh/net/text-recognition/how-to-use-ocr-convert-image-to-html-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR：在 C# 中将图像转换为 HTML

是否曾想过 **如何使用 OCR** 将菜单照片转换为干净、可搜索的 HTML？你并不孤单——开发者经常需要 **从图像中提取文本**，尤其是处理收据、传单或扫描的 PDF 时。好消息是，只需几行 C# 代码，你就可以识别 JPG 中的文字，获取原始字符串，并立即生成带样式的 HTML 页面。

在本教程中，我们将完整演示整个过程：从加载 JPEG、配置 OCR 引擎，到将结果保存为 HTML 文件。结束时，你将清楚 **如何使用 OCR**、**如何将图像转换为 HTML**，以及为何这种方式胜过手动复制粘贴。无需外部服务，只需一个小库和一点代码。

> **你需要的环境**  
> • .NET 6+（或 .NET Framework 4.7 +）。  
> • 一个提供 `OcrEngine` 的 OCR 库（例如 Microsoft Azure Cognitive Services OCR、IronOCR，或任何符合示例的包装器）。  
> • 一个示例图像，如 `menu.jpg`，放在你可控的文件夹中。  
> • 文本编辑器或 IDE（Visual Studio Code 完全可用）。

如果你对 **从图像中提取文本** 的其他格式感兴趣，使用相同的模式——只需更换文件路径并可能微调输出格式。

---

![Diagram illustrating how to use OCR to convert image to HTML](/images/ocr-process.png){alt="展示如何使用 OCR 将图像转换为 HTML 的示意图"}

## 步骤 1：创建项目并添加 OCR 库

在我们能够回答 *如何使用 OCR* 之前，必须引用实现 `OcrEngine` 的库。本文以名为 `Simple.Ocr` 的 NuGet 包为例（请替换为实际使用的提供者）。

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Simple.Ocr;          // <-- your OCR library
using Simple.Ocr.Models;   // optional, for OutputFormat enum
```

**为什么这很重要：** 导入正确的命名空间后，你才能使用 `OcrEngine` 类及其配置选项。若缺少这些，编译器会报 “type or namespace not found” 错误。

> **小技巧：** 如果使用 Visual Studio，右键项目 → *Manage NuGet Packages* → 搜索 “Simple.Ocr” 并安装。也可以通过 CLI 完成：`dotnet add package Simple.Ocr`。

## 步骤 2：初始化 OCR 引擎 —— *如何使用 OCR* 的核心

现在我们创建实例，指定需要 HTML 输出，并指向要处理的图片。

```csharp
// Step 2: Initialise OCR engine
var ocrEngine = new OcrEngine();

// Choose HTML because it preserves basic styling (fonts, line breaks, etc.)
ocrEngine.Config.OutputFormat = OutputFormat.Html;

// Load the image (this is where we *recognize text from jpg*)
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\menu.jpg");
```

**解释：**  
- `OutputFormat.Html` 让引擎将识别到的单词包装在带有 style 属性的 `<span>` 标签中，这正好适用于后续 **将图像转换为 HTML**。  
- `ImageStream.FromFile` 将 JPEG 读取到内存中；如果需要 **从图像中提取文本**（例如通过 API 接收），也可以传入来自网络请求的 `Stream`。

## 步骤 3：运行识别过程

引擎准备就绪后，实际的 OCR 工作开始。此时库会扫描像素、应用机器学习模型并输出文本。

```csharp
// Step 3: Perform OCR – this is the heart of *how to use OCR*
var ocrResult = ocrEngine.Recognize();

// The `Text` property contains the HTML string when OutputFormat.Html is set.
string htmlContent = ocrResult.Text;
```

**为什么要保存结果：**  
`ocrResult` 对象通常包含置信度分数和边界框。对于大多数简单转换，我们只需要 `Text`，但以后可以扩展以高亮低置信度词或生成可搜索的 PDF。

## 步骤 4：持久化 HTML 输出

得到 HTML 字符串后，只需将其写入磁盘。这就完成了 **ocr 图像到 html** 的整个流水线。

```csharp
// Step 4: Save the HTML file
string outputPath = @"C:\MyImages\menu.html";
File.WriteAllText(outputPath, htmlContent);

Console.WriteLine($"✅ OCR complete! HTML saved to: {outputPath}");
```

**预期效果：** 在浏览器中打开 `menu.html`，即可看到菜单文本，保留换行和基本字体样式。再也不需要手动从截图中复制粘贴。

## 完整、可直接运行的示例

将所有代码整合在一起，下面是一个可以直接放入新 .NET 项目并立即运行的控制台应用程序。

```csharp
// File: Program.cs
using System;
using System.IO;
using Simple.Ocr;
using Simple.Ocr.Models;

namespace OcrToHtmlDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialise OCR engine – the foundation of how to use OCR
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Choose HTML output – perfect for convert image to html scenarios
            // -------------------------------------------------
            ocrEngine.Config.OutputFormat = OutputFormat.Html;

            // -------------------------------------------------
            // 3️⃣  Load the source JPEG – this is where we recognize text from jpg
            // -------------------------------------------------
            string imagePath = @"C:\MyImages\menu.jpg";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 4️⃣  Run the OCR engine – the core of how to use OCR
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 5️⃣  Grab the HTML string – the final step of ocr image to html
            // -------------------------------------------------
            string html = ocrResult.Text;

            // -------------------------------------------------
            // 6️⃣  Write the HTML to disk
            // -------------------------------------------------
            string outputPath = @"C:\MyImages\menu.html";
            File.WriteAllText(outputPath, html);

            Console.WriteLine($"✅ Success! HTML saved at {outputPath}");
        }
    }
}
```

### 预期输出

运行程序后会打印：

```
✅ Success! HTML saved at C:\MyImages\menu.html
```

打开 `menu.html` 会显示类似以下内容：

```html
<div style="font-family:Arial; font-size:12pt;">
  <p>Starters</p>
  <p>Bruschetta – $5.99</p>
  <p>Garlic Bread – $4.49</p>
  ...
</div>
```

具体的标记取决于 OCR 引擎的 HTML 序列化方式，但关键点是 **JPG 中的文本已经变成可用的 HTML**。

## 常见问题解答 (FAQ)

**问：可以将输出改为纯文本而不是 HTML 吗？**  
答：完全可以。将 `OutputFormat.Html` 替换为 `OutputFormat.Text`。当你只需要 **从图像中提取文本** 用于分析时，这非常实用。

**问：如果我的图像是 PNG 或 BMP 呢？**  
答：大多数 OCR 库都支持任意光栅格式。只需在 `FromFile` 中更改文件扩展名即可。相同的 **如何使用 OCR** 步骤依然适用。

**问：如何提升低分辨率扫描的识别准确率？**  
答：在送入引擎前对图像进行预处理（提升对比度、去倾斜或放大）。一些库提供 `Preprocess` 方法，可在 `ocrEngine.Image` 上调用。

**问：生成的 HTML 能直接嵌入我的网页吗？**  
答：通常可以，但如果源图像可能包含恶意脚本（虽然纯 OCR 输出几乎不可能），建议进行一次清理，以防万一。

## 结论

我们已经完整演示了 **如何使用 OCR** 在 C# 中 **将图像转换为 HTML**。从初始化引擎、配置 HTML 输出、加载 JPEG、执行识别，到最终持久化结果，你现在拥有一个可直接运行的解决方案，能够 **从图像中提取文本**、**识别 JPG 中的文字**，并生成 **ocr 图像到 html** 文件，供用户访问或进一步处理。

想进一步探索？可以尝试：

* 使用 `iTextSharp` 等库将 HTML 导出为 PDF。  
* 添加语言检测，自动设置 OCR 语言包。  
* 将此代码集成到 ASP.NET Core API 中，让客户端上传图像并即时返回 HTML。

欢迎实验、提问并在评论区交流。祝编码愉快，愿你的 OCR 之旅始终精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}