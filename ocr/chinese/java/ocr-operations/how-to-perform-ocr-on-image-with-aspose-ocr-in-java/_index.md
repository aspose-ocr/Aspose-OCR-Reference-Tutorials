---
category: general
date: 2026-09-10
description: 使用 Aspose OCR Java 对图像执行 OCR。学习如何从 JPEG 识别文本、从图像提取文本，并高效地将图像转换为文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: zh
lastmod: 2026-09-10
og_description: 使用 Aspose OCR Java 对图像执行 OCR。本教程展示了如何识别 JPEG 中的文本、从图像中提取文本，以及仅用几行代码将图像转换为文本。
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: 使用 Aspose OCR 对图像进行 OCR – Java 指南
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 Aspose OCR 对图像进行 OCR
url: /zh/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose OCR 对图像执行 OCR

如果您需要在 Java 应用程序中 **对图像文件执行 OCR**，本指南提供了完整、可直接运行的解决方案。您将看到如何 **从 JPEG 文件识别文本**、**从图像中提取文本**，以及使用 Aspose OCR 的现代 API **将图像转换为文本**。

本教程逐步演示所有必需的步骤——从加载图像到打印识别结果——帮助您在无需额外资源的情况下集成 OCR 功能。除了 Aspose OCR for Java 库外，无需任何外部工具。

## 您将实现的目标

阅读本文后，您将能够：

* **直接从文件系统加载图像进行 OCR**。  
* 启用 Aspose OCR 的预处理（例如去噪），提升识别准确率。  
* **从 JPEG 以及其他光栅格式识别文本**。  
* **从图像中提取文本** 并将其输出到控制台。  
* 了解如何在生产就绪的代码示例中 **将图像转换为文本**。

### 前置条件

* Java Development Kit (JDK) 8 或更高版本。  
* 用于管理依赖的 Maven 或 Gradle（示例使用 Maven）。  
* 有效的 Aspose OCR for Java 许可证（或临时评估密钥）。  
* 将名为 `sample.jpg` 的图像文件放置在已知目录下。

> **专业提示：** 使用分辨率为 300 dpi 或更高的高分辨率 JPEG，可获得最佳识别率。  

## 第 1 步：将 Aspose OCR 添加到项目

如果您使用 Maven 管理依赖，请在 `pom.xml` 中插入以下代码段：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

对于 Gradle，请添加：

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

这些坐标会拉取最新的稳定版 Aspose OCR 库，其中包含后面使用的预处理功能。

## 对图像执行 OCR – 逐步操作

以下章节分解完整程序。每个代码块都是可独立复制、粘贴并运行的片段。

### 加载图像进行 OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*为什么重要：*  
`ImageStream.fromFile` 读取 JPEG 的原始字节并为 OCR 引擎做好准备。该方法适用于 Aspose OCR 支持的任何光栅格式，因此您可以在不修改代码的情况下将 JPEG 替换为 PNG 或 BMP。

### 创建并配置 OCR 引擎

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*为什么重要：*  
实例化 `OcrEngine` 会分配核心识别引擎。启用 **denoise** 标志可去除视觉噪声，这些噪声常常干扰字符检测，尤其是在扫描的 JPEG 中。

### 从 JPEG 识别文本

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*为什么重要：*  
`engine.setImage` 将图像数据绑定到 OCR 流程。`engine.recognize()` 执行完整的识别过程，返回包含提取文本和置信度指标的 `OcrResult`。

### 提取图像文本并输出

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*为什么重要：*  
`result.getText()` 提供图像内容的纯文本表示。将其打印到控制台即可演示 **将图像转换为文本** 已成功，您也可以将该字符串重定向到文件、数据库或下游服务。

## 完整、可运行的示例

下面是整合所有步骤的完整 Java 类。将 `YOUR_DIRECTORY` 替换为 JPEG 文件的绝对路径。

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 预期输出

假设 `sample.jpg` 包含文本 “Hello World”，控制台将显示：

```
=== Recognized Text ===
Hello World
```

如果图像包含多行，每行将在输出中单独占一行。

## 常见变体和边缘情况

| 情况                                         | 推荐调整 |
|--------------------------------------------|----------|
| **低分辨率 JPEG** (≤150 dpi)               | 将 `engine.getPreprocessing().setUpsample(true);` 设置为 true，以便在识别前让 Aspose 放大图像。 |
| **彩色背景**（如扫描表单）                 | 启用 `engine.getPreprocessing().setBinarize(true);` 将图像转换为黑白。 |
| **非拉丁脚本**（如西里尔文）               | 设置语言：`engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`。 |
| **大批量处理**                             | 在多个图像之间复用同一个 `OcrEngine` 实例，以降低启动开销。 |
| **需要置信度分数**                         | 通过 `result.getConfidence()` 获取每个字符的置信度值。 |

这些调整展示了在不同条件下如何 **加载图像进行 OCR**，同时仍能可靠地 **对图像执行 OCR**。

## 性能考虑

* **内存使用：** 每个 `ImageStream` 会将整张图像加载到内存中。对于非常大的文件（例如 >10 MB），建议使用 `ImageStream.fromByteArray` 分块流式读取。  
* **线程安全：** `OcrEngine` **不是**线程安全的。如果计划并行化 OCR 任务，请为每个线程创建独立实例。  
* **许可证模式：** 评估模式限制每个会话处理的页数。生产环境请部署正式许可证。

## 结论

现在，您已经掌握了如何在 Java 中使用 Aspose OCR **对图像文件执行 OCR**。本教程涵盖了加载图像、启用预处理、从 JPEG 识别文本、提取文本以及将图像转换为文本的完整流程，全部集中在一个简洁的程序中。

接下来，您可以进一步探索批量 **从 JPEG 识别文本**、将输出集成到搜索索引，或将 OCR 与自然语言处理结合，以构建更智能的文档流水线。尝试不同的预处理选项，以获得针对特定图像来源的最佳准确率。

--- 

*展示代码输出的图像*  
![perform OCR on image Java example](image-placeholder.png){alt="使用 Aspose OCR Java 执行图像 OCR"}

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在项目中进一步使用 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步说明。

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}