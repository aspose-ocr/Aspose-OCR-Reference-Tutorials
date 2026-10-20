---
category: general
date: 2026-05-25
description: 学习如何使用简约的 ASP.NET Core API 从图像中提取文本。通过 POST 上传图像，读取 multipart 表单数据并对图像执行
  OCR。
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: zh
og_description: 使用最小化的 ASP.NET Core API 从图像中提取文本。本指南展示了如何通过 POST 上传图像、读取 multipart
  表单数据，并对图像执行 OCR。
og_title: 在 ASP.NET Core 中从图像提取文本 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: 在 ASP.NET Core Minimal API 中从图像提取文本 – 完整指南
url: /zh/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 ASP.NET Core Minimal API 中提取图像文本 – 完整指南

是否曾想过在不使用重量级框架的情况下**从图像中提取文本**？你并不孤单。许多开发者需要一种快速方式，让用户上传图片并返回原始字符，无论是扫描收据、数字化手写笔记，还是为搜索索引提供支持。

在本教程中，我们将创建一个小型的 ASP.NET Core Minimal API，能够**通过 POST 上传图像**，解析 *multipart/form‑data* 负载，然后使用单例 `OcrEngine` **对图像执行 OCR**。完成后，你将拥有一个可直接运行的应用程序，能够放入任何 .NET 8 项目中，立即开始从图像中提取文本。

## 你将构建的内容

- 一个监听 `/ocr` 的最小化 Web 应用。
- 一个接受使用 `multipart/form-data` POST 请求发送的图像文件的端点。
- 读取上传文件、将其传递给 OCR 引擎并返回纯文本结果的逻辑。
- 可选的 GPU 加速代码片段（已注释），适用于拥有兼容显卡的用户。

**先决条件**  
- .NET 8 SDK（或更高版本）。  
- 对 C# 和命令行有基本了解。  
- 一个提供 `OcrEngine` 类的 OCR 库（示例假设存在一个假想的 NuGet 包）。

如果你已经具备上述条件，让我们开始吧。

## 步骤 1：设置项目并添加 OCR 包

首先，创建一个新的 Web 项目并引入 OCR 库。

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **专业提示：** 保持依赖项为最新。更新的版本通常带来性能提升，尤其是 GPU 加速推理时。

## 步骤 2：注册单例 OCR 引擎（主要服务）

我们希望整个应用只使用一个 `OcrEngine` 实例——无需为每个请求创建新的引擎。将在构建器的服务容器中注册它。

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**为什么使用单例？**  
创建 OCR 引擎可能代价高昂——比如需要将神经网络权重加载到内存中。复用同一个实例可以节省 CPU 周期和内存，从而提升每次 `/ocr` 调用的响应速度。

## 步骤 3：构建应用程序

现在我们实例化 `WebApplication` 对象。

```csharp
var app = builder.Build();
```

这行代码看起来几乎是魔法，但实际上它在内部完成了路由、middleware 和我们刚配置的 DI 容器的连接。

## 步骤 4：定义 POST 端点 – “通过 POST 上传图像”

下面是本教程的核心：一个 **通过 POST 上传图像** 的端点，读取 multipart 负载并将数据交给 OCR 引擎。

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### 逻辑拆解

| 步骤 | 发生了什么 | 为什么重要 |
|------|------------|------------|
| **ReadFormAsync** | 解析传入的 *multipart/form-data* 请求。 | 若不进行此操作，无法访问上传的文件。 |
| **form.Files["image"]** | 获取表单字段名为 `image` 的文件。 | 为调用方提供可预测的契约。 |
| **Content‑type check** | 验证文件是图像（例如 `image/png`）。 | 防止 OCR 引擎在非图像数据上出错。 |
| **Image.FromStream** | 将原始流转换为 `System.Drawing.Image`。 | OCR 库期望的是 `Image` 对象，而不是原始字节数组。 |
| **ocr.Recognize(img)** | 调用 OCR 引擎 **从图像识别文本**。 | 这就是核心的 **对图像执行 OCR** 步骤。 |
| **Results.Text** | 返回纯文本响应。 | 为下游服务提供简洁、可消费的格式。 |

## 步骤 5：运行 API

最后，启动 Web 服务器。

```csharp
app.Run();
```

当你执行 `dotnet run` 时，API 将监听 `http://localhost:5000`（或你指定的端口）。你可以使用 `curl` 进行测试：

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**预期输出：** 控制台将打印识别出的字符，例如：

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

如果图像模糊或语言不受支持，OCR 引擎将返回空字符串或错误信息——在生产代码中需要处理这些情况。

## 边缘情况与最佳实践

### 1. 大文件

默认的请求体大小限制为 30 MB。对于更大的扫描文件，你可能需要调整：

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. 异步 OCR

某些 OCR 库提供异步方法（`RecognizeAsync`）。如果你的库支持，请将 `ocr.Recognize(img)` 替换为 `await ocr.RecognizeAsync(img)` 并将 lambda 标记为 `async`。

### 3. 安全考虑

- **在加载到内存之前验证文件大小**。  
- **如果将文件写入磁盘，需对文件名进行清理**。  
- **对端点进行速率限制**，以防止拒绝服务攻击。

### 4. GPU 加速

如果取消注释 `engine.GpuDevice = new GpuDevice(0);` 并且你的硬件支持 CUDA 或 DirectML，你将在高分辨率图像上看到显著的速度提升。

## 完整工作示例

下面是完整的 `Program.cs`，你可以直接复制粘贴到全新的 Minimal API 项目中。

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

保存后，运行 `dotnet run`，即可随时 **从图像中提取文本**。

## 结论

我们已经完整演示了使用 ASP.NET Core Minimal API **从图像中提取文本的端到端解决方案**。从项目脚手架开始，我们 **注册了单例 OCR 引擎**，构建了一个 **通过 POST 上传图像** 的端点，**读取 multipart 表单数据**，最终 **对图像执行 OCR** 并返回干净的纯文本。

从这里你可以：

- 为更丰富的响应添加 JSON 包装。  
- 接入数据库以存储提取的文本。  
- 扩展对多语言的支持（如 `OcrLanguage.Spanish` 等）。

该模式易于扩展——只需将相同的端点放入更大的微服务中，或在 API 网关后面公开即可。

如果对处理 PDF、批量处理或 GPU 调优有疑问，请留言，祝编码愉快！

## 相关教程

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}