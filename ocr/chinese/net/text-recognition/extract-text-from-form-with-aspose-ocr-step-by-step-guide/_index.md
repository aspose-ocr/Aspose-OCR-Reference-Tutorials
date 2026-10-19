---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 快速提取表单文本。了解如何在指定区域识别文本，并通过完整的 C# 示例处理图像的 OCR 部分。
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: zh
og_description: 使用 Aspose OCR 从表单提取文本。本教程展示了如何在区域内识别文本以及在 C# 中处理图像的 OCR 部分。
og_title: 使用 Aspose OCR 从表单提取文本 – 完整指南
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 从表单中提取文本 – 步骤指南
url: /zh/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从表单提取文本 – 步骤指南

是否曾经需要**从表单中提取文本**，但整页都是噪声？你并不是唯一遇到这种情况的人——开发者经常要处理 PDF、扫描的发票或手写调查表，而其中只有单个字段是关键。好消息是？你可以让 Aspose OCR 只关注你关心的那一块，忽略其余部分。  

在本指南中，我们将准确演示如何**在扫描表单的指定区域识别文本**，提取所需的值，并保持图像的其余部分不受影响。完成后，你将拥有一个可直接运行的 C# 程序，处理你关心的**图像 OCR 部分**，无需调用任何外部服务。

## 本教程您将收获

- 一个完整、可运行的 C# 控制台应用程序，用于从表单图像中提取字段。  
- 对为何定位矩形可以更快更准确的清晰解释。  
- 处理空结果、不同 DPI 设置以及多页表单的技巧。  
- 一个快速检查清单，帮助你在几分钟内将代码适配到自己的项目中。

**先决条件** – 需要 .NET 6 或更高版本、Visual Studio 2022（或任意你喜欢的 IDE），以及首次获取 Aspose.OCR NuGet 包时的网络连接。无需其他库。

---

## Extract Text from Form – Setting Up the Project

在深入代码之前，先确保环境已准备就绪。步骤特意保持简洁，因为真正的魔法发生在实例化 OCR 引擎之后。

1. **Create a new console project**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **Add Aspose.OCR via NuGet**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **Copy your scanned form** into the project folder and rename it `form.png`.  
   (If your file is a PDF, export the page you need as PNG first—Aspose OCR works best with raster images.)

这就完成了。后续教程默认这三步已经完成。

![从表单提取文本示例](form-region.png "从表单提取文本示例")

*Image alt text: 从表单提取文本示例，展示了扫描文档上高亮的区域。*

---

## Recognize Text in Area – Defining the Region of Interest

为什么要使用矩形？想象一下，你有一份 2 MB 的完整报税表扫描件。对整张图像进行 OCR 会浪费 CPU 资源，并可能因无关字段产生误报。通过将范围缩小到恰好包含目标值的坐标，你可以：

- **Cut processing time** by up to 80 % for large images.  
- **Boost accuracy** because the engine ignores distracting graphics.  
- **Simplify post‑processing**—you know exactly what text to expect.

矩形由四个数字定义：`x`、`y`、`width` 和 `height`。这些值以像素为单位，测量自图像左上角。如果不确定字段所在位置，可在 Paint 中打开图像，将鼠标悬停在左上角读取 X/Y 值，然后拖动测量宽度和高度。

## OCR Part of Image – Loading the Form and Configuring the Engine

现在区域已经明确，下面来谈谈引擎本身。`OcrEngine` 是 Aspose OCR 的核心。它会自动检测语言、处理倾斜校正，并返回纯文本字符串。你也可以微调其属性——例如 `Resolution` 或 `Language`——如果表单使用非拉丁文字。对于大多数英文表单，默认设置已足够。

下面是**完整、独立的程序**，将所有内容组合在一起。随意复制粘贴到 `Program.cs` 并按 **F5** 运行。

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### Expected Output

如果矩形正确包围了显示 “Invoice # 12345” 的字段，控制台将输出：

```
Field value: Invoice # 12345
```

如果区域为空或 OCR 失败，你会看到：

```
Field value: [No text detected]
```

## Step‑by‑Step Code Walkthrough

下面我们把程序拆解为若干小块，解释每行代码背后的**原因**，并指出可能需要自行调整的地方。

### Step 1: Install Aspose.OCR via NuGet *(H3)*

```bash
dotnet add package Aspose.OCR
```

*Why?* The NuGet package bundles the native OCR engine, language data files, and a thin .NET wrapper. Without it, the `OcrEngine` class simply doesn’t exist.

### Step 2: Initialize OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*Why use `using`?* `OcrEngine` holds unmanaged resources (native DLLs, image buffers). The `using` statement guarantees they’re released, preventing memory leaks in long‑running services.

### Step 3: Load the Form Image *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*Why `ImageStream`?* It abstracts away file I/O and automatically converts common formats (PNG, JPEG, TIFF) into the internal bitmap representation required by Aspose OCR.

### Step 4: Specify the Region to Extract Text *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*Why a `Rectangle`?* The OCR engine accepts a `System.Drawing.Rectangle`. The four parameters let you pinpoint the exact field, trimming away the rest of the page.

*Tip:* If you need to support multiple fields, store each rectangle in a `Dictionary<string, Rectangle>` and loop over them.

### Step 5: Run Recognition and Retrieve Result *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*Why check `success`?* OCR can fail for various reasons—blurred image, unsupported language, or an empty region. Checking the boolean prevents you from working with stale data.

### Step 6: Handle Edge Cases and Common Pitfalls *(H3)*

- **Different DPI:** If the scan is low‑resolution (< 150 DPI), increase `ocrEngine.Image.DpiX` and `ocrEngine.Image.DpiY` before calling `Recognize`.  
- **Multiple Pages:** For multi‑page PDFs, extract each page as a separate PNG and repeat the rectangle logic per page.  
- **Non‑English Text:** Set `ocrEngine.Language = Language.Thai;` (or any supported language) before recognition.  
- **Noise Reduction:** `ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` can improve results on grainy scans.

## Going Further – Real‑World Variations

### Extracting Multiple Fields from the Same Form

If you need to pull “Name”, “Date”, and “Amount” from a single document, create a collection:

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### Integrating with a Database

After extracting, you might want to store the result in SQL Server:

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### Automating on a Server

If you plan to run this as a background service, wrap the logic in an `async` method and use `Task.Run` to keep the UI responsive. Remember to set `ocrEngine.ParallelProcessing = true;` for multi‑core speed‑ups.

## Conclusion

You now have a solid, production‑ready way to **extract text from form** images using Aspose OCR. By focusing on a specific rectangle

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}