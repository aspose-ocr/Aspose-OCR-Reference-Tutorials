---
category: general
date: 2026-09-29
description: 学习如何使用 Java 和 Aspose OCR 识别图像中的文本。本指南还展示了如何从 JPG 中提取文本以及如何提升 OCR 的准确率。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- how to improve OCR accuracy
- Aspose OCR Java
- Java image processing
language: zh
lastmod: 2026-09-29
og_description: 使用 Aspose OCR 在 Java 中识别图像中的文本。按照本分步教程提取 jpg 中的文本，并了解如何提升 OCR 准确率。
og_image_alt: Java code screenshot that recognizes text from image using Aspose OCR
og_title: 在 Java 中从图像识别文本 – 完整的 Aspose OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  headline: How to recognize text from image in Java using Aspose OCR
  type: TechArticle
- description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  name: How to recognize text from image in Java using Aspose OCR
  steps:
  - name: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
    text: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
  - name: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
    text: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
  - name: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
    text: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
  - name: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
    text: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 Aspose OCR 识别图像中的文本
url: /zh/java/advanced-ocr-techniques/how-to-recognize-text-from-image-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose OCR 识别图像中的文本

如果您需要在 Java 应用程序中**从图像中识别文本**，本教程将为您展示一个可直接运行的解决方案。您将看到如何从 jpg 文件中提取文本、启用 GPU 加速以及应用拼写校正，以回答常见问题 *如何提高 OCR 准确率*。

本指南涵盖您所需的全部内容：Maven 设置、完整源代码、每个配置选项的说明以及处理低质量图片的技巧。完成后，您将拥有一个可运行的程序，能够将识别的文本打印到控制台。

## 前置条件

在开始之前，请确保您拥有：

* Java 17（或更高）已安装 – Aspose OCR 支持 Java 8+，但更新的运行时可提供更佳性能。
* Maven 3.8+ 用于依赖管理。
* Aspose OCR for Java 许可证（免费试用可用于评估）。  
* 一张包含清晰可读文本的 JPG 图像（`sample.jpg`）。

如果缺少上述任意项，请从 [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) 安装 JDK，并按照 Apache 网站上的 Maven 安装指南进行操作。

## 将 Aspose OCR 添加到项目中

创建一个 `pom.xml`（或在现有文件中添加），并包含 Aspose OCR 依赖：

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version> <!-- latest stable at time of writing -->
    </dependency>
  </dependencies>
</project>
```

运行 `mvn clean compile` 以下载库。该依赖会带来所有 GPU 使用和拼写校正所需的本机二进制文件。

## 步骤 1：设置 OCR 引擎以识别图像中的文本

首先，需要创建 `OcrEngine` 的实例。该对象负责协调整个 OCR 流程。

```java
// Step 1: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

创建引擎时并不会加载任何图像；它仅准备内部资源。此分离使您能够在批处理场景中复用同一引擎处理多张图像。

## 步骤 2：启用 GPU 加速以提升处理速度

如果您的机器配备兼容的 GPU，开启它可以将识别时间缩短最多 70 %。这在速度层面直接回答了 *如何提高 OCR 准确率*，通常还能让您在不牺牲性能的情况下使用更高分辨率的图像。

```java
// Step 2 (optional): Use GPU if available
engine.getConfiguration().setUseGpu(true);
```

> **专业提示：** 在无头服务器上运行时，请确认已安装 CUDA 驱动；否则调用会回退到 CPU 并且不会报错。

## 步骤 3：开启拼写校正以提升 OCR 准确率

拼写校正是一种轻量级语言模型，可修正常见的识别错误（例如 “l0ve” → “love”）。启用它是针对印刷文本回答 *如何提高 OCR 准确率* 的最有效方法之一。

```java
// Step 3 (optional): Enable spell correction
engine.getConfiguration().setSpellCorrector(true);
```

如果您处理的是扫描的手写笔记，可能需要禁用此功能，因为该模型针对印刷字体进行调优。

## 步骤 4：加载要从 JPG 中提取文本的图像

现在加载图像文件。`ImageStream.fromFile` 辅助方法接受 Aspose OCR 支持的任何格式，但示例侧重于 JPG，因为它是最常见的网络格式。

```java
// Step 4: Load the image that contains the text to be recognized
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

**为什么选择 JPG？** JPEG 压缩可能产生干扰 OCR 的伪影。为获得最高准确率，请提供 DPI 至少为 300 的图像，并避免过度压缩。如果您有 PNG 或 TIFF，也可以直接传给 `fromFile`；相同代码无需修改即可工作。

## 步骤 5：执行 OCR 并获取识别的文本

最后，调用 `recognize()` 并打印结果。该方法返回一个 `OcrResult` 对象，其中包含原始文本、置信度分数以及每个单词的边界框。

```java
// Step 5: Run OCR and get the result
OcrResult result = engine.recognize();
System.out.println("=== Recognized text ===");
System.out.println(result.getText());
```

### 预期输出

```
=== Recognized text ===
Welcome to Aspose OCR demo.
This text was extracted from a JPG image.
```

如果输出出现乱码，请重新检查 **步骤 3**（拼写校正），并确保图像符合 DPI 推荐值。

## 常见变体和边缘情况

| 情况 | 推荐调整 |
|-----------|------------------------|
| **低分辨率图像 (< 150 DPI)** | 在送入引擎前对图像进行放大，或使用 `engine.getConfiguration().setScaleFactor(2.0)` 让引擎内部重新采样。 |
| **多语言文档** | 设置 `engine.getConfiguration().setLanguage("eng,spa")` 以加载英语和西班牙语词典。 |
| **大量文件批处理** | 重用同一个 `OcrEngine` 实例，对每个新文件仅调用 `engine.setImage(...)`。这可避免重复加载本机库。 |
| **内存受限环境** | 禁用 GPU (`setUseGpu(false)`) 和拼写校正 (`setSpellCorrector(false)`) 以降低内存占用。 |
| **从 PNG 而非 JPG 提取文本** | 无需代码更改，只需将 `fromFile` 指向 `.png` 路径。库会自动检测格式。 |

## 提高 OCR 准确率的专业技巧

1. **预处理图像** – 在交给 Aspose OCR 之前，使用 OpenCV 进行对比度拉伸或二值化。更清晰的边缘可提升置信度。  
2. **裁剪不必要的边距** – 引擎会分析空白区域，这会降低整体置信度分数。  
3. **选择正确的语言包** – 仅加载所需语言可加快识别速度并减少误报。  
4. **使用最新的 Aspose OCR 版本** – 每个版本都包含更新的神经模型，可开箱即提升准确率。

## 完整、可运行的示例

下面是将所有步骤整合在一起的完整 Java 类。将其保存为 `SimpleOcr.java`，修改图像路径后，运行 `mvn exec:java -Dexec.mainClass=SimpleOcr`。

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: (Optional) Enable GPU acceleration for faster processing
        engine.getConfiguration().setUseGpu(true);

        // Step 3: (Optional) Enable spell correction to improve OCR accuracy
        engine.getConfiguration().setSpellCorrector(true);

        // Step 4: Load the image that contains the text to be recognized
        // This example extracts text from jpg, but any supported format works.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 5: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        System.out.println("=== Recognized text ===");
        System.out.println(result.getText());
    }
}
```

运行程序后，识别的文本会打印到控制台，确认您已成功掌握如何**从图像中识别文本**、如何**从 jpg 中提取文本**以及**如何提高 OCR 准确率**的关键技术。

## 结论

在本教程中，您学习了如何在 Java 中使用 Aspose OCR **从图像中识别文本**、如何 **从 jpg 中提取文本**，以及多种实用方法来回答 *如何提高 OCR 准确率*。该方法完全独立：只需 Maven 依赖、一个 JPEG 文件以及少量配置标志即可。

接下来，您可以探索以下方向：

* 使用 Aspose PDF 将识别的文本转换为可搜索的 PDF。  
* 使用简单循环处理整个文件夹的图像（批量 OCR）。  
* 将 OCR 引擎集成到 Spring Boot REST 接口，实现按需图像处理。

欢迎尝试不同的图像质量、语言包和硬件设置，观察各因素对 OCR 性能的影响。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [在 Java 中使用 Aspose OCR 预处理图像 OCR – 提升准确率并提取文本](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [如何在 Java 中使用 OCR – 快速识别图像文本](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [使用 Aspose OCR 识别图像文本 – 完整 Java 指南](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}