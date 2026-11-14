---
category: general
date: 2026-11-14
description: 学习如何在 Java 中使用 Aspose OCR 识别 PNG 中的文本。本指南还涵盖如何从图像中提取文本以及如何加载图像进行 OCR。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert scanned image to text
- load image for ocr
- read text from image java
language: zh
lastmod: 2026-11-14
og_description: 使用 Aspose OCR 在 Java 中识别 PNG 文本。按照本分步教程提取图像中的文字，加载图像进行 OCR，并在 Java
  项目中读取图像文字。
og_image_alt: Screenshot of Java console showing recognized text from a PNG file
og_title: 在 Java 中识别 PNG 文本 – 完整的 Aspose OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize text from PNG in Java using Aspose OCR. The
    guide also covers how to extract text from image and load image for OCR.
  headline: How to recognize text from PNG in Java with Aspose OCR
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image processing
title: 如何在 Java 中使用 Aspose OCR 识别 PNG 文本
url: /zh/java/ocr-operations/how-to-recognize-text-from-png-in-java-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose OCR 识别 PNG 文本

如果您需要在 Java 应用程序中**识别 PNG**文件中的文本，本教程将为您展示一个完整、可直接运行的解决方案。阅读完本指南后，您将能够**从图像中提取文本**、将扫描图像转换为文本，并使用 Aspose OCR 库**加载图像进行 OCR**。

示例还演示了如何在**Java 图像读取文本**代码中使用 OCR，以便您可以将 OCR 集成到任何后端服务、桌面工具或 Android 项目中。

## 前置条件

在开始之前，请确保您已具备以下条件：

* 已安装 Java Development Kit (JDK) 8 或更高版本。
* 用于管理依赖的 Maven 或 Gradle（示例使用 Maven）。
* Aspose OCR for Java 的许可证文件（免费评估版可用于测试）。
* 一张名为 `input.png` 的图片，放置在代码可引用的文件夹中。

这些要求可确保代码在无需额外设置的情况下编译并运行。

## 步骤 1：将 Aspose OCR 添加到项目中

在您的 `pom.xml` 中添加 Aspose OCR 的 Maven 依赖。这将引入所有必需的类，包括 `OcrEngine` 和 `ImageStream`。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **专业提示：** 使用最新的版本号（请查看 Maven Central），以获得性能提升和新语言支持。

## 步骤 2：加载 PNG 图像进行 OCR

OCR 引擎使用 `ImageStream` 工作。您必须将其指向要处理的 PNG 文件的准确位置。

```java
// Load the PNG image that contains the text you want to recognize
String imagePath = "YOUR_DIRECTORY/input.png";
ImageStream imageStream = ImageStream.fromFile(imagePath);
ocrEngine.setImage(imageStream);
```

*为什么重要*：正确加载图像可避免因不受支持的格式或缺少文件路径而导致的常见 “OCR failed” 错误。

## 步骤 3：创建并配置 OCR 引擎

实例化 `OcrEngine`，并可选地调整语言或识别设置。默认配置适用于英文印刷文本，但您可以通过 `ocrEngine.setLanguage(Language.French)` 更改为其他语言。

```java
// Step 3: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Optional: set recognition language (default is English)
// ocrEngine.setLanguage(Language.English);
```

## 步骤 4：运行 OCR 过程

调用 `process()` 执行繁重的工作——扫描图像、分割字符并将其转换为 Unicode 文本。

```java
// Step 4: Execute the OCR operation
boolean success = ocrEngine.process();
```

如果 `process()` 返回 `true`，则引擎已成功**将扫描图像转换为文本**。否则，请检查控制台输出以获取诊断信息。

## 步骤 5：获取并显示识别的文本

OCR 成功后，您可以使用 `getText()` 获取完整字符串。这是**从图像读取文本 Java**功能的核心。

```java
if (success) {
    System.out.println("Recognized text:");
    System.out.println(ocrEngine.getText());
} else {
    System.err.println("OCR failed. Verify the image path and file format.");
}
```

控制台现在会打印出 `input.png` 中出现的精确字符。您可以进一步处理该字符串——将其存入数据库、写入搜索索引，或进行自然语言分析。

## 完整、可运行的示例

将所有步骤组合在一起即可得到一个单独的、独立的类。将下面的代码复制到名为 `SimpleOcrDemo.java` 的文件中，将 `YOUR_DIRECTORY` 替换为 PNG 的绝对或相对路径，然后使用 `mvn exec:java` 运行。

```java
import com.aspose.ocr.*;

public class SimpleOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        String imagePath = "YOUR_DIRECTORY/input.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Run the OCR process
        if (ocrEngine.process()) {
            // Step 4: Retrieve and display the recognized text
            System.out.println("Recognized text:");
            System.out.println(ocrEngine.getText());
        } else {
            System.err.println("OCR failed. Check the image path and format.");
        }
    }
}
```

**预期输出**（示例为一个简单的 “Hello World” PNG）：

```
Recognized text:
Hello World
```

如果图像包含多行，引擎会保留换行符，使后处理变得简单。

## 处理常见的边缘情况

| 情况 | 推荐操作 |
|-----------|--------------------|
| **图像不是 PNG** | 将文件转换为 PNG，或使用 `ImageStream.fromFile` 加载受支持的格式（BMP、JPEG、TIFF）。 |
| **低分辨率扫描** | 在 OCR 前提高 DPI（`ocrEngine.setResolution(300)`），以提升准确性。 |
| **非英文文本** | 调用 `ocrEngine.setLanguage(Language.<YourLanguage>)` 并确保已安装相应语言包。 |
| **大量文件批处理** | 重用同一个 `OcrEngine` 实例，并多次调用 `setImage`，以避免重复的初始化开销。 |

这些技巧可帮助您在各种来源中可靠地**从图像中提取文本**。

## 性能考虑因素

* **线程安全** – `OcrEngine` 不是线程安全的。如果计划并发处理图像，请为每个线程创建单独的实例。
* **内存使用** – 大图像会占用更多堆内存。考虑在将图像送入引擎之前使用 `ImageResize` 缩小图像。
* **授权** – 评估版会在输出文本中添加水印。生产环境请使用授权版。

## 下一步

既然您已经能够**识别 PNG 文件中的文本**，可以进一步探索以下内容：

* **批量处理** – 遍历目录，将每个 OCR 结果写入 `.txt` 文件。
* **与 Apache Tika 集成** – 将 OCR 与元数据提取相结合，用于全文搜索流水线。
* **在 Spring Boot 中使用 Aspose OCR** – 暴露一个接受上传图像并返回 JSON 编码文本的 HTTP 接口。

这些扩展基于本指南中介绍的核心概念。

---

*您已经学习了如何为 OCR 加载图像、将扫描图像转换为文本，以及使用 Aspose OCR 的 Java 代码读取图像文本。将此模式应用于其他图像格式、语言和部署场景，以释放强大的文档自动化能力。*

## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于其中演示的技术。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [Java OCR 示例 – 使用 Aspose 加载图像并识别文本](/ocr/english/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/)
- [Java 批量图像 OCR – 快速从 PNG 文件提取文本](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [使用 Aspose OCR 的 Java 图像文本提取指南](/ocr/english/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}