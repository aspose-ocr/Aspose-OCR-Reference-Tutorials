---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 在 Java 中将图像转换为文本。掌握批量 OCR 处理，从文件夹读取图像，并按扩展名过滤文件。
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: zh
og_description: 使用 Java 快速将图像转换为文本。本教程涵盖批量 OCR 处理、从文件夹读取图像以及按扩展名过滤文件。
og_title: 在 Java 中将图像转换为文本 – 完整批量 OCR 指南
tags:
- OCR
- Java
- Aspose
title: 在 Java 中将图像转换为文本 – 批量 OCR 处理指南
url: /zh/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将图像转换为文本（Java） – 批量 OCR 处理指南

是否曾经需要**将图像转换为文本**，但不确定如何一次性处理数十个文件？你并不孤单——开发者们经常需要从 PNG、JPG 以及其他扫描件中提取数据。好消息是？使用 Aspose OCR，你可以在几分钟内搭建批量 OCR 处理流水线，读取文件夹结构中的图像，甚至按扩展名过滤文件，只处理真正需要的内容。

在本教程中，我们将构建一个自包含的 Java 程序，遍历目录，挑选出每个 `.png` 或 `.jpg`，异步将每张图片发送到 Aspose OCR，并按原始顺序打印提取的文本。完成后，你将拥有一个可复用的代码片段，能够在任何需要**将图像转换为文本**的大规模项目中直接使用。

---

![将图像转换为文本示例](https://example.com/convert-images-to-text.png "显示 PNG 文件转换文本的 Java 控制台输出截图")

## 您将构建的内容

- 一个在多个线程之间共享的 `AsposeOCR` 引擎（高效且线程安全）。  
- 一个 `ParallelRecognizer`，能够并行运行 OCR 任务，完美适用于**批量 OCR 处理**。  
- 使用 `java.nio.file.Files` **读取文件夹中的图像** 的逻辑。  
- 简单的过滤器，用于**从 PNG 文件提取文本**，同时仍能处理 JPG。  
- 对内部线程池的干净关闭，以避免资源泄漏。

### 前置条件

- Java 17（或任何近期的 LTS 版本）。  
- Maven 或 Gradle 用于拉取 Aspose OCR 库。  
- 一个包含 PNG/JPG 图像的文件夹，供你处理。  
- 对 Java 流的基本了解——不需要任何高级技巧。

> **专业提示：** 如果你还没有许可证，Aspose 提供免费临时密钥，可用于测试。

---

## Step 1 – 设置项目并添加 Aspose OCR

首先，创建一个新的 Maven 项目（或 Gradle，随你喜欢）。在 `pom.xml` 中添加 Aspose OCR 依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **为什么这很重要：** 预先声明依赖可以确保编译器能够识别 `AsposeOCR`、`ParallelRecognizer` 以及相关类。它还能保证在所有机器上使用相同的版本，这对于可复现的**批量 OCR 处理**至关重要。

构建完成后，刷新你的 IDE，你应该能在 `External Libraries` 下看到 Aspose 包。

---

## Step 2 – 将图像转换为文本 – 初始化 OCR 引擎

我们只需要**一个** OCR 引擎实例来完成整个运行。在线程之间共享它可以节省内存，并因为引擎只加载一次语言包而加快速度。

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

> **解释：** `ParallelRecognizer` 将引擎包装在一个线程池中。当你提交大量文件时，每个文件都会获得自己的工作线程，从而在多核 CPU 上实现真正的并行。

---

## Step 3 – 从文件夹读取图像 – 遍历目录树

现在我们需要**读取文件夹中的图像**并收集所有 PNG 或 JPG。`Files.walk` API 让这一步只需一行代码，但我们会添加过滤器，以在需要时**仅从 PNG 提取文本**。

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

> **为什么在这里过滤：** 使用 `filter` 可以让我们**按扩展名过滤文件**，提前剔除不必要的 I/O，显著提升效率。代码也更易读——无需复杂的正则表达式。

---

## Step 4 – 批量 OCR 处理 – 异步提交任务

文件列表准备好后，我们将每个路径推送到 `ParallelRecognizer`。`recognizeAsync` 方法返回一个 `Future<OcrResult>`，我们将其保存以便后续获取。

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

> **底层发生了什么？** 每次调用都会向识别器内部的执行服务队列中加入一个任务。任务并行执行，因此包含 100 张图片的文件夹可以在单线程循环所需时间的很小一部分内完成处理。

---

## Step 5 – 按原始顺序获取结果 – 保持文件顺序

因为我们按照 `imagePaths` 的顺序存储了 futures，只需遍历列表并调用 `get()` 即可。该调用仅在对应图片完成时阻塞，从而在无需额外 bookkeeping 的情况下保持顺序。

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

**示例控制台输出**（为简洁起见已截断）：

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

> **边缘情况处理：** 如果某张图片抛出异常（文件损坏、不支持的格式），我们会捕获并继续处理其余文件——这是构建可靠**批量 OCR 处理**流水线的关键习惯。

---

## Step 6 – 清理 – 关闭识别器

切记要关闭内部线程池，否则 JVM 可能在退出时挂起。

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

就这样！程序现在可以遍历任意目录，过滤 PNG/JPG 文件，并行运行 OCR，最后打印结果。

---

## 完整工作示例

下面是完整的、可直接复制粘贴的 Java 类。将 `"YOUR_DIRECTORY"` 替换为你的图像文件夹路径，然后在 IDE 或命令行中运行。

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

运行该类，观察控制台填满提取的字符串，并庆祝你已经**将图像转换为文本**，而无需编写任何阻塞 I/O 的循环。

---

## 常见问题 (FAQs)

**Q: 我还能处理 PDF 或 TIFF 吗？**  
A: 当然可以。Aspose OCR 支持多种格式——只需在 Step 2 的过滤器中添加相应的文件扩展名。

**Q: 如果我需要其他语言，例如西班牙语怎么办？**  
A: 将 `RecognitionLanguage.ENGLISH` 改为 `RecognitionLanguage.SPANISH`。确保已安装对应的语言包（Aspose 已内置大多数主流语言）。

**Q: 我的文件夹包含子文件夹——会被扫描吗？**  
A: 会的。`Files.walk` 会递归遍历整棵树，所以每个嵌套的 PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}