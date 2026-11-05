---
category: general
date: 2026-06-16
description: 学习如何在 Java 中对图像文件执行 OCR。本教程涵盖从 PNG 识别文本、从图像提取文本、将图像转换为文本以及加载图像进行 OCR。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: zh
og_description: 使用 Java 对图像进行 OCR。本文指南展示了如何从 PNG 识别文本、从图像提取文本，以及使用可直接运行的示例将图像转换为文本。
og_title: 在 Java 中对图像进行 OCR – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: 在 Java 中对图像进行 OCR – 完整的逐步指南
url: /zh/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中对图像执行 OCR – 完整分步指南

是否曾需要 **perform OCR on image** 文件，却不确定该选择哪个 Java 库？你并不孤单。无论是构建收据扫描器、文档归档系统，还是仅仅想把图片转换为可搜索的文本，学习如何使用 Java **perform OCR on image** 都是一个实用的技能。

在本教程中，我们将逐步演示如何 **perform OCR on image** 文件：加载图像、配置引擎、识别文本，最后打印结果。完成后，你将能够 **recognize text from PNG** 文件、**extract text from image** 源，并仅用几行代码 **convert image to text**。

## 前置条件

- Java 17 或更高版本（代码可在任何近期 JDK 上编译）
- 已安装 Maven（或你喜欢的构建工具）
- 对 Java 语法有基本了解
- 一个想要测试的 PNG 文件（我们将其命名为 `hello.png`）

> **专业提示：** 如果手头没有 PNG，可以截取任意文本的屏幕截图，并将其保存为 `hello.png`，放在名为 `resources` 的文件夹中。

## 我们将构建的内容

一个名为 `OcrDemo` 的小型控制台应用程序，功能如下：

1. **Loads image for OCR** – 从磁盘读取 PNG。
2. **Performs OCR on image** – 通过 Tess4J 使用 Tesseract 引擎。
3. **Extracts text from image** – 返回包含识别内容的 `String`。
4. 将结果打印到控制台。

让我们开始吧。

## 第一步：设置项目并添加 Tess4J

首先，创建一个新的 Maven 项目（如果喜欢也可以使用 Gradle）。添加 Tess4J 依赖，它封装了流行的 Tesseract OCR 引擎。

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **为什么选择 Tess4J？** 它维护活跃、跨平台，并为 **perform OCR on image** 任务提供了简洁的 Java API。

## 第二步：准备图像加载逻辑

接下来我们编写一个帮助方法，用于 **load image for OCR**。该方法使用 Java 的 `ImageIO` 将 PNG 读取为 `BufferedImage`。

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

请注意，方法名明确体现了 **load image for OCR** 的意图，使代码自解释。

## 第三步：配置 OCR 引擎以 **Perform OCR on Image**

拿到图像后，我们创建 `Tesseract` 实例，启用自动语言检测，并调用 `doOCR`。这就是我们 **perform OCR on image** 数据的核心步骤。

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **为什么启用自动检测？** 它让引擎为图像选择最佳语言模型，特别适用于 **convert image to text** 时图像中混合了英文和其他脚本的情况。

## 第四步：整合代码 – 主应用程序

下面是入口点代码，能够 **recognize text from PNG**、**extract text from image**，并最终将结果打印出来。这是完整、可运行的示例。

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### 预期输出

如果 `hello.png` 包含短语 “Hello, OCR world!”，控制台将显示类似如下内容：

```
=== Recognized Text ===
Hello, OCR world!
```

具体输出可能会因图像质量略有差异，但你应该能看到 PNG 中的文本。

## 第五步：处理常见边缘情况

### 5.1 低分辨率图像

如果源 PNG 模糊，OCR 准确率会下降。一个快速的解决办法是先对图像进行放大，然后再交给引擎：

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

在 `engine.recognize(image)` 之前调用 `upscale(image, 2)` 以提升结果。

### 5.2 多语言文档

如果预计会出现法语或德语文本，只需在 `setLanguage` 中添加相应语言代码：

```java
tesseract.setLanguage("eng+fra+deu");
```

引擎随后会使用组合语言模型 **extract text from image**。

### 5.3 跳过空白页

有时扫描的 PDF 页面会渲染为空白 PNG。检测空图像可以节省处理时间：

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## 第六步：打包并运行应用程序

1. **编译：** `mvn clean compile`
2. **运行：** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

确保 `tessdata` 文件夹（包含语言文件）位于编译后的 JAR 同目录，或在 `OcrEngine` 中指定其绝对路径。

## 结论

现在，你已经掌握了使用 Java **perform OCR on image** 文件的完整、可投入生产的模式。从 **load image for OCR** 到 **recognize text from PNG**，我们已经演示了如何 **extract text from image**、**convert image to text**，以及如何处理低分辨率扫描或多语言内容等棘手场景。

接下来，你可以探索：

- **批量处理** – 循环遍历 PNG 目录，将每个结果写入 `.txt` 文件。
- **PDF 生成** – 将提取的文本嵌入可搜索的 PDF 中。
- **云 OCR 服务** – 将本地 Tesseract 性能与 Google Vision、Azure Cognitive Services 等 API 进行对比。

欢迎实验、调参，并分享你的发现。祝编码愉快，愿你的图像始终转化为干净、可搜索的文本！

![展示执行 OCR 工作流的图示](https://example.com/ocr-workflow.png "执行 OCR 示例")

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}