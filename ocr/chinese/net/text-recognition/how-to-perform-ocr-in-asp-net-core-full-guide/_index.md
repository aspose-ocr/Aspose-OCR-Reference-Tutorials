---
category: general
date: 2026-05-28
description: 如何在 ASP.NET Core 中执行 OCR——学习上传图片、从图片中提取文本以及高效处理文件上传。
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: zh
og_description: 如何在 ASP.NET Core 中执行 OCR。一步步学习如何上传图像、从图像中提取文本，以及使用 Aspose OCR 处理文件上传。
og_title: 如何在 ASP.NET Core 中执行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: 如何在 ASP.NET Core 中进行 OCR – 完整指南
url: /zh/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 ASP.NET Core 中执行 OCR – 完整指南

有没有想过在现代 Web API 中 **如何执行 OCR** 而不让自己抓狂？你并不是唯一的。开发者经常需要让用户上传一张图片——可能是收据、护照扫描件或手写笔记——并以 JSON 的形式返回原始文本。  

在本教程中，我们将逐步演示一个完整、可投入生产的解决方案，展示 **如何上传文件**、进行验证、运行 Aspose OCR，最终 **从图像中提取文本**。完成后，你将拥有一个可直接粘贴到任何 ASP.NET Core 项目中的控制器。

## 你将构建的内容

- 一个接受 multipart/form‑data 上传的 `OcrController`
- 验证文件确实存在且不为空
- 使用 Aspose OCR 引擎进行异步 OCR 处理
- 返回包含识别文本的简洁 JSON 响应

无需外部服务，也没有隐藏的魔法——仅仅是可以本地运行的纯 C# 代码。

## 前置条件（开始之前需要准备的）

| 要求 | 原因 |
|------|------|
| .NET 6 SDK or later | ASP.NET Core 6+ 为我们提供了最小化 API 功能和异步支持。 |
| Visual Studio 2022 (or VS Code) | IDE 让调试更容易，但任何编辑器都可以使用。 |
| Aspose.OCR NuGet package (`dotnet add package Aspose.OCR`) | 实际执行 OCR 任务的引擎。 |
| Basic knowledge of ASP.NET Core MVC | 我们将使用 `ControllerBase` 和路由属性。 |

如果你已经具备这些，太好了——让我们开始吧。

## 步骤 1：设置项目并安装 Aspose OCR

打开终端并创建一个全新的 Web API 项目：

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

该单行命令会拉取 OCR 库及其所有依赖。无需其他配置；Aspose 对常见图像格式开箱即用。

## 步骤 2：添加 OCR 控制器（**如何执行 OCR** 的核心）

创建一个新文件 `Controllers/OcrController.cs` 并粘贴以下代码。这是完整、可运行的示例——没有缺失的部分。

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### 为什么这样可行

- **`[FromForm] IFormFile`** 告诉 ASP.NET Core 将 multipart 文件部分绑定到 `uploadedFile`。这是在 Web API 中 **处理文件上传** 的经典方式。
- `if` 检查确保我们能够优雅地 **处理文件上传** 错误，如果客户端忘记发送文件则返回 400 Bad Request。
- `using var fileStream = uploadedFile.OpenReadStream();` 打开一个 *只读* 流，这对大文件至关重要——无需一次性将整张图像加载到内存中。
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` 将流直接输入到 Aspose OCR，保持管道简洁。
- `await ocrEngine.RecognizeAsync();` 在后台线程上执行繁重的工作，使我们的 API 保持响应。这就是 **如何异步执行 OCR** 的核心。
- 最后，我们将结果包装成 JSON 对象 (`{ extractedText }`)——非常适合前端使用。

## 步骤 3：配置请求大小限制（可选但实用）

如果你预计会有高分辨率的扫描文件，请提升默认请求大小。将以下代码添加到 `Program.cs` 中：

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

现在 API 不会在 10 MB 的收据图像上卡顿。根据你的使用场景调整此限制。

## 步骤 4：使用 cURL 或 Postman 测试端点

下面是一个可以在终端运行的快速 cURL 命令：

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

你应该会看到类似以下的 JSON 负载：

```json
{
  "extractedText": "Sample text that was on the image."
}
```

如果图像中没有可识别的字符，字符串将为空——不会崩溃，只是返回空结果。这是需要记住的一个边缘情况。

## 步骤 5：可视化确认（可选图片）

下面是一张占位截图，展示成功 OCR 请求后你将收到的 JSON 响应。

![如何执行 OCR 结果 – 显示提取文本的 JSON 响应截图](/images/ocr-result.png)

*Alt 文本:* **显示图像中提取文本的 OCR 结果截图**

## 常见陷阱与专业提示

| 陷阱 | 解决方案 |
|------|----------|
| **不受支持的图像格式**（例如具有多页的 TIFF） | 先转换为 PNG/JPEG，或在将其提供给 `OcrEngine` 之前使用 Aspose 的 `ImageConverter`。 |
| **大文件导致内存压力** | 如示例所示流式处理文件；避免将 `IFormFile.CopyToAsync` 写入 `MemoryStream`。 |
| **OCR 返回乱码** | 确保图像对比度高且方向正确。如有需要，可使用 `ocrEngine.Preprocess()` 进行预处理。 |
| **多个并发请求** | Aspose OCR 是线程安全的，但如果服务器内存受限，你可能需要使用信号量来限制并发。 |

## 扩展示例：批量上传与并行处理

如果你需要一次 **处理文件上传** 多张图像，请将操作签名改为接受列表：

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

现在你可以批量 **上传图像 OCR**——非常适合一次性扫描文件夹中的收据。

## 安全注意事项

- **验证文件扩展名**（`.png`、`.jpg`、`.jpeg`）在处理前，以避免恶意上传。
- **扫描病毒**，如果你的 API 面向互联网；可集成如 ClamAV 的服务。
- **限流** 端点以防止拒绝服务攻击。

## 预期输出与验证方法

当你使用包含单词 “Hello” 的清晰图像请求 `/ocr/upload` 端点时，响应应为：

```json
{
  "extractedText": "Hello"
}
```

你可以通过打开浏览器的开发者工具 → Network（网络）标签页，或检查 cURL 输出，快速进行验证。

## 回顾 – 我们覆盖的内容

- 设置 ASP.NET Core 项目并添加 Aspose OCR NuGet 包。
- 实现了一个简洁的控制器，展示 **如何执行 OCR**、**处理文件上传** 和 **从图像中提取文本**。
- 讨论了错误处理、性能调优和安全最佳实践。
- 提供了可直接运行的代码示例以及批量上传变体。

## 接下来可以做什么？

- **添加语言支持**：Aspose OCR 可以配置不同语言（`ocrEngine.Language = Language.English;`）。
- **集成数据库**：将提取的文本与元数据一起存储，以便后续搜索。
- **前端 UI**：构建一个简单的 React 或 Blazor 页面，让用户拖拽图像并即时看到 OCR 结果。

随意尝试——更换 OCR 引擎、尝试不同的图像预处理步骤，或将结果接入下游 AI 模型。当你掌握了在现代 .NET 框架中 **如何执行 OCR** 时，可能性无限。

祝编码愉快，愿你的文本始终清晰可读！

## 相关教程

- [如何 OCR 图像 – 在 OCR 图像识别中执行图像 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [如何使用 Aspose 在 OCR 图像识别中从流中识别图像](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [如何在 OCR 图像识别中设置阈值](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}