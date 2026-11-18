---
category: general
date: 2026-08-28
description: 了解如何在 Java 中使用 Aspose OCR 从 png 图像提取文本。本教程涵盖批量 OCR 处理、从文件夹读取图像以及按扩展名过滤文件。
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: 了解如何在 Java 中使用 Aspose OCR 从 png 图像提取文本。本教程涵盖批量 OCR 处理、从文件夹读取图像以及按扩展名过滤文件。
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: 如何在 Java 中从 png 提取文本 – 批量 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中从 png 提取文本 – 批量 OCR 指南
url: /zh/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中从 png 提取文本 – 批量 OCR 指南

如果你曾经需要 **extract text from png** 文件，但不确定如何将操作规模化到超过少量图片的程度，那么你来对地方了。许多开发者从单张图片的 OCR 调用开始，当文件夹增长到数十或数百个文件时，很快就会遇到性能瓶颈。使用 Aspose OCR for Java，你可以构建一个强大的批量 OCR 流水线，遍历目录，仅过滤你关心的图像类型，并行运行识别，并以与源文件相同的顺序返回结果。阅读完本指南后，你将拥有一个可直接使用的 Java 代码片段，能够可靠且高效地处理 **batch OCR processing**。

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## 快速答案
- **哪个库处理 OCR？** Aspose OCR for Java.
- **我可以同时处理 PNG 和 JPG 吗？** 是的 – 示例会过滤两种扩展名。
- **OCR 引擎是线程安全吗？** 单个共享的 `AsposeOCR` 实例可安全并发使用。
- **测试需要许可证吗？** 可以从 Aspose 获取免费临时密钥。
- **子文件夹会自动扫描吗？** `Files.walk` 会递归遍历整个树。

## 什么是 extract text from png？

`extract text from png` 指的是对 Portable Network Graphics 文件应用光学字符识别（OCR）的过程，使可见字符变为可搜索、可编辑的字符串。Aspose OCR 的引擎读取像素数据，识别字形，并在一次方法调用中返回 Unicode 文本。

## 为什么使用 Aspose OCR for Java？

Aspose OCR 支持 **30+ 种语言**，在标准 8 核服务器上每分钟可处理高达 **500 张图像**，并且能够在不将整张图像加载到内存的情况下处理高达 **200 MB** 的文件。这些量化的能力意味着你可以在普通硬件上可靠地运行大规模批处理任务，而不会遇到内存限制。

## 前提条件
- Java 17（或任何近期的 LTS 版本）。
- 用于依赖管理的 Maven 或 Gradle。
- 包含你想要处理的 PNG/JPG 图像的目录。
- 对 Java 流和 `java.nio.file` 包有基本了解。
- （可选）用于评估的 Aspose OCR 临时许可证密钥。

> **专业提示：** 免费临时密钥在 30 天后过期，但它为测试提供完整的 API 访问权限。

## 批量 OCR 流水线如何保持顺序？

`Future<OcrResult>` 表示一个待处理的 OCR 结果，处理完成后即可检索。流水线通过将 `Future<OcrResult>` 对象存储在与输入 `Path` 集合顺序相同的列表中来保持原始文件顺序。当你随后遍历这些 futures 并调用 `get()` 时，每次调用只会阻塞对应的图像，因此输出顺序与输入顺序一致，无需额外的排序逻辑。

## 什么是 Aspose OCR for Java？

`AsposeOCR` 是 Aspose OCR 库的核心类，封装了所有语言包、识别设置和内部本地资源。它设计为在整个应用程序生命周期内实例化一次，并可安全地在多个线程之间共享。由于它只加载一次语言数据，复用同一实例可以减少初始化开销并提升批量操作的吞吐量。

## 如何设置项目并添加 Aspose OCR

First, create a Maven (or Gradle) project and add the Aspose OCR dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **为何重要：** 预先声明依赖可确保编译器能够识别 `AsposeOCR`、`ParallelRecognizer` 以及相关类。这也保证了在所有机器上使用相同的版本，这对于可复现的 **batch OCR processing** 至关重要。

构建完成后刷新你的 IDE；现在应该能在 **External Libraries** 下看到 Aspose 包。

## 如何初始化 OCR 引擎 – 共享单个实例

`AsposeOCR` 是 Aspose OCR 库提供的主要 OCR 引擎类。整个运行过程中我们只需要 **一个** OCR 引擎实例。在线程之间共享它可以节省内存并加快速度，因为引擎只会加载一次语言包。

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

> **说明：** `ParallelRecognizer` 将引擎包装在线程池中。当你提交大量文件时，每个文件都会获得自己的工作线程，从而在多核 CPU 上实现真正的并行。

## 如何从文件夹读取图像 – 遍历目录树

`Files.walk` 是 Java NIO 的方法，可递归遍历文件树并返回 `Path` 对象的流。现在我们需要 **read images from folder** 并收集所有 PNG 或 JPG。`Files.walk` API 使这成为一行代码，但我们会添加过滤器，仅在需要时 **extract text from png**。

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **为何在此过滤：** 使用 `filter` 可以提前 **按扩展名过滤文件**，从而削减后续不必要的 I/O。它也保持代码可读性——无需复杂的正则表达式。

## 如何异步提交 OCR 任务

`recognizeAsync` 将图像提交给 OCR 引擎进行异步处理，并返回表示待处理结果的 `Future<OcrResult>`。在文件列表准备好后，我们将每个路径推送到 `ParallelRecognizer`。`recognizeAsync` 方法返回的 `Future<OcrResult>` 将被存储以供后续检索。

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **内部发生了什么？** 每次调用都会将任务加入识别器的内部执行服务队列。任务并行运行，因此包含 100 张图像的文件夹可以在单线程循环所需时间的一小部分内完成处理。

## 如何在保留文件顺序的同时检索结果

`Future<OcrResult>` 保存异步 OCR 任务的结果，并提供 `get()` 方法以获取识别的文本。由于我们按 `imagePaths` 的相同顺序存储了 futures，只需遍历列表并调用 `get()` 即可。该调用仅在对应图像完成前阻塞，从而在无需额外记录的情况下保持顺序。

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**示例控制台输出** (为简洁起见已截断)：

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **边缘情况处理：** 如果某个图像抛出异常（文件损坏、不支持的格式），我们会捕获并继续处理其余图像——这是可靠 **batch OCR processing** 流水线的关键做法。

## 如何清理资源 – 关闭识别器

`ParallelRecognizer.shutdown()` 停止内部线程池，确保所有 OCR 任务在应用退出前完成。切勿忘记关闭内部线程池，否则 JVM 可能在退出时挂起。

```java
recognizer.shutdown();
```

就这样！程序现在可以遍历任意目录，过滤 PNG/JPG 文件，并行运行 OCR，并按原始顺序打印结果。

---

## 完整可运行示例（复制粘贴）

下面是完整的、可直接运行的 Java 类。将 `"YOUR_DIRECTORY"` 替换为你的图像文件夹路径，然后在 IDE 或命令行中运行它。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

运行该类，观察控制台填满提取的字符串，并庆祝你已经 **converted images to text**，而无需编写任何阻塞 I/O 的循环。

---

## 常见问题 (FAQs)

**Q: 我可以处理 PDF 或 TIFF 吗？**  
A: 当然可以。Aspose OCR 支持 30+ 种格式，包括 PDF、TIFF、BMP 和 GIF——只需在目录遍历步骤的过滤器中添加所需的扩展名即可。

**Q: 如果我需要除英语之外的语言，例如西班牙语怎么办？**  
A: 将 `RecognitionLanguage.ENGLISH` 改为 `RecognitionLanguage.SPANISH`（或任何受支持的语言）。语言包随库一起捆绑，无需额外下载。

**Q: 我的文件夹包含子文件夹——会被扫描吗？**  
A: 是的。`Files.walk` 递归遍历整个树，因此每个嵌套的 PNG/J

**Q: 如何处理超过 200 MB 的超大图像？**  
A: 通过调用 `ocrEngine.setUseStreaming(true)` 启用流式模式。这会让引擎分块读取图像，显著降低峰值内存使用。

**Q: 有办法限制并发 OCR 线程的数量吗？**  
A: 有。构造 `ParallelRecognizer` 时，将所需的最大线程数作为第二个参数传入（例如 `new ParallelRecognizer(ocrEngine, 4)`）。

---

**最后更新：** 2026-08-28  
**测试环境：** Aspose OCR for Java 24.10  
**作者：** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## 相关教程

- [Java 批量 OCR 处理指南：将图像转换为文本](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Java 图像文字读取完整 Aspose OCR 指南](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [使用 Aspose.OCR 提取图像文字 – 允许的字符](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}