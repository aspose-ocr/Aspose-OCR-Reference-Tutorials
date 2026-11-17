---
category: general
date: 2026-09-18
description: 了解如何使用 Aspose OCR 在 Java 中提取图像文本。一次调用即可高效批量处理 PNG、JPG 和 TIFF 文件。
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: 掌握使用批量 OCR 在 Java 中提取图像文本的方法。使用 Aspose OCR 在一次调用中转换 PNG、JPG 和 TIFF
  文件。
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: 在 Java 中提取图像文本 – 批量 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 如何使用批量 OCR 在 Java 中提取图像文本
url: /zh/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中通过批量 OCR 提取图像中的文本

如果您需要**快速从图像中提取文本**，且不想为每个文件编写循环，批量 OCR 就是答案。在许多实际项目中，您会收到一个装满扫描件的文件夹——PNG 收据、JPG 截图或多页 TIFF——并且必须将它们转换为可搜索的文本。Aspose OCR 让您只需一次方法调用即可同时处理 PNG、JPG 和 TIFF 文件，节省开发时间和 CPU 资源。

## 快速回答
- **批量 OCR 做什么？** 它在一次请求中处理多个图像文件，并为每个文件返回文本。
- **支持哪些格式？** 开箱即用支持 PNG、JPG/JPEG 和多页 TIFF。
- **需要单独的本机库吗？** 不需要，Aspose OCR JAR 已包含所有必需内容。
- **可以控制线程数量吗？** 可以，在批处理器上使用 `setMaxParallelism`。
- **需要哪个 Java 版本？** Java 17 或更高。

## 什么是 Aspose OCR？
Aspose OCR 是一个 Java 库，可在不依赖外部组件的情况下识别图像文件中的印刷体和手写文本。它支持超过 60 种语言，且每批次可处理多达 100 张图像，适合大规模文档数字化。

## 本教程涵盖内容
加载图像路径列表，创建 `OcrBatchProcessor`，调优并行度，执行一次 `recognize` 调用，并打印提取的字符串。完成后，您将拥有一个可直接运行的 Java 程序，能够批量从 PNG、JPG 和 TIFF 文件中提取文本。

- **如何使用 Aspose 的 `OcrBatchProcessor` 进行批量 OCR**。
- 从不同格式（PNG、JPG、TIFF）**提取图像文本**的方法。
- 控制并行度以保持应用响应的技巧。
- 一个完整、可运行的 Java 程序，您可以复制粘贴并立即执行。

无需任何 Aspose 经验——只需基本的 Java 环境和您喜欢的 IDE。完成后，您将掌握批量识别 PNG、JPG、TIFF 文件中文本的坚实基础。

---

![展示如何批量 OCR 多个图像文件的示意图](/images/batch-ocr-diagram.png "如何批量 OCR")

*图片说明：展示如何批量 OCR 多个图像文件一起处理的示意图。*

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| Java 17 或更高 | Aspose OCR 针对现代 JVM 进行优化。 |
| Maven 或 Gradle | 简化 Aspose OCR 库的添加。 |
| 基础 Java 知识 | 需要理解代码流程。 |
| 一组示例图像（`.png`、`.jpg`、`.tif`） | 便于观察提取效果。 |

如果您已经具备上述条件，太好了——让我们开始吧。

## 步骤 1：将 Aspose OCR 添加到项目中

首先需要获取 Aspose OCR JAR。使用 Maven 时，将以下内容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

如果您更喜欢 Gradle，等价写法是：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

添加依赖后，所有 **从 png 提取文本**、**从 jpg 提取文本**、**从 tiff 提取文本** 所需的内容都会自动拉取，无需额外的本机库。

## 步骤 2：定义要处理的图像文件

接下来告诉 OCR 引擎要处理哪些文件。这正是 **如何批量 OCR** 发挥作用的地方——只需传入路径列表，库会自行完成繁重工作。

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **专业提示：** 使用绝对路径或 `Paths.get(...)`，可避免在不同操作系统上出现路径问题。

## 步骤 3：创建批处理器并调优并行度

Aspose OCR 提供 `OcrBatchProcessor`，可并行运行多个识别任务。控制线程数可以防止在处理大量图像时占用过多 CPU。

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

为什么要限制并行度？如果在普通笔记本上启动过多线程，可能会出现性能下降而非提升。通过 `setMaxParallelism`，您可以在速度与稳定性之间取得平衡。

## 步骤 4：执行批量 OCR 调用

下面展示 **如何批量 OCR** 的核心：一次 `recognize` 调用返回 `RecognitionResult` 对象列表，每个对象对应一张图像。  
`recognize` 处理提供的图像并返回 `RecognitionResult` 列表，每个对象包含提取的文本。

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

该方法会阻塞，直到所有图像处理完毕，然后返回文本。如果需要非阻塞行为，可以将其包装在 `CompletableFuture` 中，但对大多数脚本而言，同步调用更简洁。

## 步骤 5：打印提取的文本

最后，遍历结果并显示识别出的字符串。这表明我们已经成功 **从图像中提取文本**（包括各种格式）。  
`RecognitionResult` 保存单张图像的 OCR 输出，包括提取的文本和置信度分数。

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

如果 OCR 引擎无法读取某个文件，`getText()` 将返回空字符串，您可以添加简单检查来记录警告。

## 完整工作示例

将所有内容整合后，得到下面的完整、可直接运行的 Java 类。将其保存为 `BatchOcrTutorial.java`，修改图像路径后运行 `javac && java`。

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

运行后，控制台会打印每个 PNG、JPG、TIFF 文件的提取文本——这正是当 **如何批量 OCR** 成为您关注焦点时所需要的答案。

## 常见问题与边缘情况

### 如果图像超过三张怎么办？
只需在 `imageFiles` 列表中添加更多条目。批处理器会自动根据您在 `setMaxParallelism` 中配置的线程数分配工作。

### 我的图像位于子文件夹——需要手动列出每个文件吗？
`Files.list` 会返回目录中路径的惰性流。

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

这样代码保持灵活，同时仍然遵循 **如何批量 OCR** 的思路。

### 如何处理低置信度的结果？
`getConfidence()` 返回一个数值置信度，指示识别文本的可靠程度。

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR 支持其他语言吗？
支持——在 `recognize` 调用前使用 `ocrProcessor.setLanguage(OcrLanguage.Spanish)`（或任何受支持的枚举）即可。这使 **从图像中提取文本** 真正具备多语言能力。

## 性能技巧

* **批量大小很关键**——较大的批次可以降低开销，但过大可能占用更多内存。建议在 50–200 张图像之间进行测试。
* **并行度**——在 4 核 CPU 上，`setMaxParallelism(4)` 通常能获得最佳吞吐量。根据服务器负载自行调整。
* **图像预处理**——在 OCR 前将图像转为灰度或提升对比度，可提升噪声扫描的识别准确率。

## 结论

现在您已经掌握了在 Java 中使用 Aspose OCR **批量 OCR** 的方法，了解了如何 **从各种格式的图像中提取文本**，以及为何并行度控制至关重要。完整代码示例演示了如何一次性高效地识别 PNG、JPG、TIFF 文件的文本。

准备好下一步了吗？将 OCR 输出导入搜索索引、数据库或 AI 摘要器。您也可以尝试 PDF 输入（Aspose OCR 支持），或结合 OpenCV 等图像预处理库，以获得更高的准确率。

祝编码愉快，记住——批量 OCR 并非难题。有了合适的工具和清晰的模式，您可以轻松将大量图片转化为可搜索的文本。

## 常见问答

**问：可以在无头服务器上运行吗？**  
答：可以，Aspose OCR 纯 Java 实现，不依赖 UI 组件，完全适用于无头环境。

**问：生产环境需要许可证吗？**  
答：生产部署需要商业许可证；提供免费试用供评估使用。

**问：支持哪些操作系统？**  
答：任何能够运行 Java 17+ 的操作系统，包括 Windows、Linux 和 macOS。

**问：Aspose OCR 能识别多少种语言？**  
答：开箱即支持超过 60 种语言，涵盖英语、西班牙语、阿拉伯语、中文等。

**问：Aspose OCR 能处理的最大文件大小是多少？**  
答：单个图像文件最大支持 200 MB；更大的文件应在处理前拆分。

---

**最后更新：** 2026-09-18  
**测试版本：** Aspose OCR 24.9 for Java  
**作者：** Aspose

## 相关教程

- [Extract Text from Images – OCR Basics for Java](/ocr/java/ocr-basics/)
- [How To Batch Ocr In Java Complete Guide To Extract Text From](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Preprocess Image Ocr In Java Boost Accuracy Extract Text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}