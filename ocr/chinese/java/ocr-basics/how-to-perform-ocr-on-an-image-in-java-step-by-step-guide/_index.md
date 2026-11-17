---
category: general
date: 2026-11-17
description: 学习如何在 Java 中对图像进行 OCR，并使用简洁的代码示例从图片中提取文本。包括读取图像的 Java 提示。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: zh
lastmod: 2026-11-17
og_description: 如何在 Java 中对图像进行 OCR 并快速提取文本。请按照本指南读取图像并使用可直接运行的示例将图像转换为文本。
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: 如何在 Java 中对图像进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: 如何在 Java 中对图像进行 OCR – 步骤指南
url: /zh/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中对图像执行 OCR 的分步指南

如果您需要**在图片上执行 OCR**，本教程为您展示一个完整、可运行的 Java 解决方案。您将看到如何读取图像文件、配置 OCR 引擎以及提取引擎识别出的文本。

在处理扫描文档、收据或截图时，通常需要将可视内容转换为可搜索的文本。本指南将一步步带您完成从加载图像到打印提取文本的全过程，并且还会涉及常见的陷阱，例如不受支持的文件格式和空结果。

## 前置条件

在开始之前，请确保您已经具备：

* 已安装 Java Development Kit (JDK) 8 或更高版本。
* 用于拉取 OCR 库的构建工具（Maven 或 Gradle）。
* 您想要处理的图像文件（JPEG、PNG、BMP）。

代码使用 **`com.asprise.ocr` 包中的 OCR 库**，因为它只需要一个 JAR 并且可以在所有主流平台上运行。您可以通过替换 import 语句和引擎初始化代码，将其换成其他提供商（如 Tesseract、Google Vision 等）。

## 第一步：添加 OCR 依赖

如果您使用 Maven，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

对于 Gradle，请在 `build.gradle` 中加入此行：

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

这些行确保 **read image Java** 代码能够编译，并且在运行时 OCR 引擎可用。

## 第二步：使用 Java 读取图像

读取图像文件是任何 **extract text image** 工作流中的第一个具体步骤。Java 内置的 `ImageIO` 类可以处理大多数常见格式。

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**为什么重要：** `ImageIO.read` 对不受支持的格式或损坏的文件会返回 `null`。上述方法会记录问题并返回 `null`，以便后续步骤能够优雅地处理。

## 第三步：创建并配置 OCR 引擎

OCR 引擎必须知道要识别哪种语言。设置语言可以显著提升准确率，尤其是非英文文档。

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**为什么重要：** 启动引擎是一个相对耗时的操作，因此如果您的应用需要批量处理图像，建议创建一次并在多张图像之间复用。

## 第四步：执行 OCR 并将图像转换为文本

现在图像已加载，且引擎已准备就绪，您可以运行识别步骤。这是 **how to perform OCR** 的核心。

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**边缘情况处理：** 如果图像为 `null`，该方法返回空字符串而不是抛出 `NullPointerException`。这使得在处理用户提供的文件时，周围代码更加健壮。

## 第五步：显示提取的文本

最后，将结果打印到控制台或转发给其他组件（例如数据库或 UI 小部件）。

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

当您使用 `java OcrDemo sample.jpg` 运行程序时，控制台会显示识别出的字符。这完成了 **convert image to text** 的整个循环。

### 预期输出

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

如果图像中没有可识别的字符，程序会打印 `(no text detected)`。

## 常见变体及适配方式

| 变体 | 更改内容 | 何时使用 |
|-----------|--------------|-------------|
| **不同语言** | 将 `"eng"` 替换为 `"spa"`（西班牙语）、`"fra"`（法语）等 | 文档使用非英文语言时 |
| **批量处理** | 对文件路径列表进行循环，复用同一个 `Ocr` 实例 | 大量扫描页的处理 |
| **更高准确度** | 使用 `Ocr.SPEED_SLOW` 或启用 `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` 进行仅数字扫描 | 当 OCR 质量至关重要（如发票号码） |
| **Tesseract 替代方案** | 将 import 换成 `net.sourceforge.tess4j.Tesseract` 并相应调整初始化代码 | 项目已经依赖 Tesseract 时 |

## 专业技巧

* 在将图像送入引擎之前**先缩放大图**；OCR 速度随像素数量线性增长。
* 使用 OpenCV 等库对图像进行**预处理**（灰度、对比度提升），尤其是源文件噪声较大时。
* 如果在短时间内多次调用 OCR，**缓存 OCR 引擎**——启动和关闭引擎会产生额外开销。
* 当您期望特定格式（如日期、电话号码）时，使用正则表达式**验证结果**。

## 结论

您现在已经掌握了在 Java 中**how to perform OCR** 的完整流程，从读取文件到显示提取文本。教程涵盖了 **read image Java**、**extract text image**、**convert image to text**、以及 **image to text java** 等技术，并提供了实际项目中的实用技巧。

接下来您可以：

* 将 OCR 步骤集成到接收上传的 Web 服务中。
* 将输出与搜索索引结合，实现对扫描文档的全文检索。
* 探索多语言支持或自定义字符集等高级 OCR 选项。

祝编码愉快，尽情将图片转换为可搜索的文本吧！

## 接下来应该学习什么？

以下教程涵盖了与本指南密切相关的主题，帮助您在已有技术的基础上进一步扩展。每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并探索替代实现方式。

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}