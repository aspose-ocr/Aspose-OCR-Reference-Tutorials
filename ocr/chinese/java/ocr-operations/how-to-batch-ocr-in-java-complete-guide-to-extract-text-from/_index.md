---
category: general
date: 2026-02-09
description: 了解如何在 Java 中使用 Aspose OCR 批量进行 OCR。一次调用即可从图像中提取文本，识别 PNG、JPG 和 TIFF 文件中的文字。
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: zh
og_description: 掌握在 Java 中批量 OCR 的方法。本教程展示了如何使用 Aspose OCR 从 PNG、JPG 和 TIFF 图像中提取文本，并提供了清晰的代码示例。
og_title: 如何在 Java 中批量 OCR – 高效提取图像文本
tags:
- OCR
- Java
- Aspose
title: Java 中批量 OCR 完整指南——从图像提取文本
url: /zh/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中批量 OCR – 完整的图像文字提取指南

是否曾想过 **如何批量 OCR** 多张图片而不必为每个文件写循环？你并不孤单。在许多真实项目中，你会得到一个装满扫描件的文件夹——PNG 收据、JPG 截图，甚至是多页 TIFF——并且需要快速获取文字。

好消息是 Aspose OCR 正好可以做到这一点：一次方法调用即可一次性识别 PNG、JPG 和 TIFF 文件中的文字。在本教程中，我们将从项目搭建到打印结果，完整演示整个过程，让你今天就能开始从图像中提取文字。

## 本教程涵盖内容

* 使用 Aspose 的 `OcrBatchProcessor` **批量 OCR**。
* 从不同格式（PNG、JPG、TIFF）的图像中 **提取文字** 的方法。
* 控制并行度以保持应用响应的技巧。
* 一个完整、可直接运行的 Java 程序，复制粘贴即可执行。

无需任何 Aspose 经验——只需基本的 Java 环境和你喜欢的 IDE。完成后，你将拥有批量识别 PNG、JPG、TIFF 文件文字的坚实基础。

---

![批量 OCR 多个图像文件的示意图](/images/batch-ocr-diagram.png "批量 OCR 示例")

*图片替代文字：展示批量 OCR 示例图，多个图像文件一起处理。*

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| Java 17 或更高版本 | Aspose OCR 面向现代 JVM。 |
| Maven 或 Gradle | 简化 Aspose OCR 库的添加。 |
| 基础 Java 知识 | 需要理解代码流程。 |
| 一组示例图像（`.png`、`.jpg`、`.tif`） | 观察提取效果。 |

如果你已经具备以上条件，太好了——我们开始吧。

## 步骤 1：将 Aspose OCR 添加到项目

首先需要获取 Aspose OCR 的 JAR。使用 Maven 时，将以下内容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

如果你更喜欢 Gradle，等价写法是：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

添加依赖后，会自动拉取 **从 png 识别文字**、**从 jpg 识别文字**、**从 tiff 识别文字** 所需的全部内容，无需额外的本地库。

## 步骤 2：定义要处理的图像文件

接下来告诉 OCR 引擎要处理哪些文件。这正是 **如何批量 OCR** 发挥作用的地方——只需传入文件路径列表，库会自行完成繁重工作。

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **小贴士：** 使用绝对路径或 `Paths.get(...)`，可避免在不同操作系统上出现路径问题。

## 步骤 3：创建批处理器并调优并行度

Aspose OCR 提供 `OcrBatchProcessor`，可以并行执行多个识别任务。控制线程数可以防止在处理大量图像时占用过多 CPU。

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

为什么要限制并行度？在普通笔记本上开启过多线程可能导致速度下降而非提升。通过 `setMaxParallelism` 可以在速度与稳定性之间取得平衡。

## 步骤 4：执行批量 OCR 调用

下面展示 **如何批量 OCR** 的核心：一次 `recognize` 调用返回 `RecognitionResult` 列表，每个图像对应一个结果对象。

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

该方法会阻塞直至所有图像处理完毕，然后返回文字。如果需要非阻塞行为，可以将其包装在 `CompletableFuture` 中，但对大多数脚本而言，同步调用更简洁。

## 步骤 5：打印提取的文字

最后，遍历结果并输出识别到的字符串。这一步验证我们已经成功 **从图像中提取文字**（包括各种格式）。

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### 预期输出

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

如果 OCR 引擎无法读取某个文件，`getText()` 会返回空字符串，你可以加入简单的检查来记录警告。

## 完整可运行示例

将所有代码整合后，即得到下面的完整、可直接运行的 Java 类。复制到 `BatchOcrTutorial.java`，根据实际情况修改图像路径，然后执行 `javac && java`。

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

运行后，控制台会打印每个 PNG、JPG、TIFF 文件的提取文字——这正是当 **如何批量 OCR** 成为你关注点时所需要的答案。

## 常见问题与边缘情况

### 如果图片超过三张怎么办？

只需在 `imageFiles` 列表中继续添加条目。批处理器会自动根据 `setMaxParallelism` 配置的线程数分配工作。

### 我的图片在子文件夹中——需要手动列出每个文件吗？

可以使用代码自动收集特定扩展名的所有文件：

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

这样既保持了代码的灵活性，又符合 **如何批量 OCR** 的需求。

### 如何处理低置信度的结果？

`RecognitionResult` 提供 `getConfidence()` 方法。你可以过滤掉低于阈值的结果，并使用更高 DPI 重新尝试：

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR 支持其他语言吗？

支持——在 `recognize` 调用前使用 `ocrProcessor.setLanguage(OcrLanguage.Spanish)`（或任意支持的枚举）即可。这使得 **从图像中提取文字** 真正实现多语言。

## 性能优化建议

* **批量大小**——更大的批次可以降低开销，但过大可能占用更多内存。建议在 50–200 张图片之间测试。
* **并行度**——在四核 CPU 上，`setMaxParallelism(4)` 通常能获得最佳吞吐量。根据服务器负载自行调整。
* **图像预处理**——在 OCR 前将图像转为灰度或提升对比度，可提升噪声扫描的识别率。

## 结论

现在，你已经掌握了使用 Aspose OCR 在 Java 中 **批量 OCR** 的方法，了解了如何 **从各种格式的图像中提取文字**，以及为何控制并行度很重要。完整代码示例展示了如何一次性高效识别 PNG、JPG、TIFF 文件的文字。

准备好下一步了吗？尝试将 OCR 输出写入搜索索引、数据库，或喂给 AI 摘要器。你也可以尝试 PDF 输入（Aspose OCR 支持），或结合 OpenCV 等图像预处理库，以获得更高的准确率。

祝编码愉快，记住——批量 OCR 并非难事。有了合适的工具和清晰的模式，你很快就能把堆积的图片转化为可搜索的文本。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}