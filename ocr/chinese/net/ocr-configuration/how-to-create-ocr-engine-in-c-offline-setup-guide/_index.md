---
category: general
date: 2026-03-04
description: 学习如何在 C# 中创建无需互联网的 OCR。本分步指南还展示了如何使用本地资源离线运行 OCR。
draft: false
keywords:
- how to create OCR
- how to run OCR
- offline OCR C#
- local OCR resources
- OcrEngine setup
language: zh
og_description: 如何在 C# 中创建无需网络调用的 OCR。请遵循本指南，了解如何使用 LocalResourceProvider 在本地运行 OCR。
og_title: 如何在 C# 中创建 OCR 引擎 – 离线设置
tags:
- OCR
- C#
- Offline Processing
title: 如何在 C# 中创建 OCR 引擎 – 离线设置指南
url: /zh/net/ocr-configuration/how-to-create-ocr-engine-in-c-offline-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建 OCR 引擎 – 离线设置指南

是否曾想过 **如何创建 OCR**，而且永不连接互联网？也许你在构建安全的桌面应用，或者你只是讨厌不可靠的网络请求。无论哪种情况，你都希望拥有一个完全运行在客户端机器上的 OCR 引擎。  

好消息是？这相当简单。在本教程中，我们将一步步演示 **如何创建 OCR**，随后展示如何使用 `LocalResourceProvider` 在离线模式下 **运行 OCR**。完成后，你将拥有一个可自行包含的 C# 代码片段，能够直接放入任何 .NET 项目——无需外部服务。

## 你将学到

- 离线 OCR 设置的最小前置条件。  
- 如何实例化 `OcrEngine` 并指向本地资源文件夹。  
- 为什么使用本地提供程序可以消除网络延迟并提升隐私。  
- 常见陷阱（文件缺失、路径错误）以及如何避免。  

所有所需代码均已包含，并提供快速验证步骤，让你在复制粘贴后即可看到引擎的实际运行效果。

## 前置条件

在深入之前，请确保你已具备以下条件：

1. **.NET 6.0 或更高** – 我们使用的 OCR 库目标为 .NET Standard 2.0，因此任何近期的运行时都可使用。  
2. **包含 OCR 资源的文件夹** – 语言包、训练数据文件以及其他辅助二进制文件。如果尚未拥有，可从供应商的离线包下载相应的包并解压到 `C:\MyApp\OcrResources`。  
3. **Visual Studio 2022**（或你喜欢的任何 IDE）。  

就这些——运行时不需要任何会访问互联网的 NuGet 包。

![离线 OCR 流程图 – 如何在不进行网络调用的情况下创建 OCR 引擎](offline-ocr-diagram.png)

*图片说明：离线创建 OCR 引擎示意图*

---

## 步骤 1：添加 OCR 库引用

首先，在项目中引用 OCR SDK 程序集。如果你拥有供应商提供的 `.dll`，右键 **References → Add Reference** 并浏览至 `OcrSdk.dll`。或者，如果 SDK 以支持离线模式的 NuGet 包形式提供，运行以下命令：

```bash
dotnet add package OcrSdk --version 3.2.1
```

> **技巧提示：** 固定版本号。以后升级可能会引入破坏性更改，影响离线资源路径。

---

## 步骤 2：创建 OCR 引擎实例  

现在我们将通过构造 `OcrEngine` 对象来实际 **创建 OCR**。该对象是所有识别任务的入口点。

```csharp
using OcrSdk;               // Namespace provided by the OCR library
using OcrSdk.Resources;    // Contains LocalResourceProvider

// ...

// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

为什么需要专用的引擎？`OcrEngine` 保存配置、缓存语言模型并管理线程池。一次实例化后在多个扫描中复用，比为每张图像创建新对象要高效得多。

---

## 步骤 3：将引擎指向本地资源文件夹  

这一步至关重要，使你能够 **运行 OCR** 而无需触及网络。我们分配一个 `LocalResourceProvider`，它从磁盘目录读取语言数据。

```csharp
// Step 3: Configure the engine to use offline resources
string resourcePath = @"C:\MyApp\OcrResources";
ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);
```

**底层发生了什么？** `LocalResourceProvider` 实现了与默认云端提供程序相同的接口，但它从 `resourcePath` 读取 `.dat` 文件。此技巧确保所有后续 OCR 调用均保持本地。

> **注意：** 如果路径错误或文件夹缺少必需文件（`eng.traineddata`、`ocr_config.xml` 等），引擎将抛出 `ResourceNotFoundException`。在分配之前请始终验证文件夹。

---

## 步骤 4：验证引擎已就绪  

快速的合理性检查可以帮助你避免后续调试。调用 `IsReady`（或等价属性）并输出结果。

```csharp
// Step 4: Verify the engine can locate its resources
if (ocrEngine.IsReady)
{
    Console.WriteLine("✅ OCR engine is ready – offline mode confirmed.");
}
else
{
    Console.WriteLine("❌ OCR engine failed to load resources. Check the path and files.");
    return;
}
```

你应该在控制台看到绿色对勾。如果出现红色叉，请再次确认 `resourcePath` 指向包含语言包的文件夹。

---

## 步骤 5：在示例图像上运行 OCR  

最后，让我们真正 **运行 OCR** 在一张图片上。将名为 `sample.png` 的图像放置在相同的资源文件夹（或任何可访问位置），并将其提供给引擎。

```csharp
// Step 5: Perform OCR on a local image
string imagePath = Path.Combine(resourcePath, "sample.png");

// Load the image (the SDK may provide its own Image class)
var ocrImage = OcrImage.FromFile(imagePath);

// Run recognition – this call is completely offline
OcrResult result = ocrEngine.Recognize(ocrImage);

// Output the recognized text
Console.WriteLine("🖋️ Recognized Text:");
Console.WriteLine(result.Text);
```

**预期输出**（假设 `sample.png` 包含短语 “Hello OCR!”）：

```
🖋️ Recognized Text:
Hello OCR!
```

如果结果为空，请确认图像清晰且英文语言模型 (`eng`) 已存在于 `OcrResources` 中。

---

## 边缘情况与常见陷阱  

| 情况 | 会发生什么 | 如何修复 |
|-----------|--------------|---------------|
| **缺少语言文件** | 步骤 3 中的 `ResourceNotFoundException` | 确保文件夹中存在 `eng.traineddata`（或你的目标语言）。 |
| **图像损坏** | 带有 “Unsupported format” 的 `OcrException` | 在提供给引擎之前将图像转换为 PNG 或 BMP。 |
| **多线程** | 如果创建多个引擎会出现竞争条件 | 重用单个 `OcrEngine` 实例；它对并发的 `Recognize` 调用是线程安全的。 |
| **路径包含空格** | 引擎无法定位资源 | 使用逐字字符串 (`@"C:\Path With Spaces\OcrResources"`) 或转义反斜杠。 |

---

## 完整工作示例  

下面是一个可直接运行的控制台程序，整合了所有步骤。将代码复制到新的 `.csproj` 项目中并按 **F5**。

```csharp
// File: Program.cs
using System;
using System.IO;
using OcrSdk;
using OcrSdk.Resources;

namespace OfflineOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Point to local resources (offline mode)
            string resourcePath = @"C:\MyApp\OcrResources";
            ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);

            // 3️⃣ Verify the engine can load resources
            if (!ocrEngine.IsReady)
            {
                Console.WriteLine("❌ Engine failed to initialize. Check your resource folder.");
                return;
            }
            Console.WriteLine("✅ Engine initialized successfully.");

            // 4️⃣ Load a test image
            string imagePath = Path.Combine(resourcePath, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            var ocrImage = OcrImage.FromFile(imagePath);

            // 5️⃣ Run OCR – entirely offline
            OcrResult result = ocrEngine.Recognize(ocrImage);

            // 6️⃣ Show the result
            Console.WriteLine("\n🖋️ Recognized Text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

**运行程序** 应该会打印确认信息和提取的文本，证明你已经掌握了 **如何创建 OCR** 和 **如何运行 OCR**，且从未离开机器。

---

## 结论  

我们已经涵盖了在 C# 项目中 **如何创建 OCR** 所需的全部知识，并演示了 **如何完全离线运行 OCR**。通过配置 `LocalResourceProvider`，你可以消除网络延迟，保护敏感数据，并完全掌控 OCR 生命周期。  

准备好迎接下一个挑战了吗？尝试将英文模型替换为其他语言，或实验不同的图像预处理步骤（灰度转换、去倾斜）以提升准确率。同样的模式适用——只需将引擎指向不同的资源文件夹。  

如果遇到任何问题，请重新查看上面的边缘情况表或留下评论；祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}