---
category: general
date: 2026-07-21
description: 使用 Java OCR 从图像中提取文本。了解如何将 PNG 转换为文本、读取 PNG 中的文本、加载图像进行 OCR，并仅通过几个步骤对图像执行
  OCR。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: zh
lastmod: 2026-07-21
og_description: 使用 Java 从图像中提取文本。本指南展示如何将 PNG 转换为文本，读取 PNG 中的文本，加载图像进行 OCR，以及高效地对图像执行
  OCR。
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: 使用 Java 从图像提取文本——一步步 OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中从图像提取文本——完整 OCR 指南
url: /zh/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中从图像提取文本 – 完整 OCR 指南

是否曾需要 **从图像中提取文本**，却不确定该选用哪个 Java 库？你并不孤单。无论是数字化收据、扫描 PDF，还是构建可搜索的档案库，从 PNG 中提取文本都是许多开发者的日常痛点。

在本教程中，我们将手把手演示一个解决方案，帮助你 **将 PNG 转换为文本**、**从 PNG 读取文本**、**加载图像进行 OCR**，以及 **对图像执行 OCR**——只需几行简洁的 Java 代码。完成后，你将拥有一个可直接放入任意项目的可运行程序。

## 你将构建的内容

我们将创建一个小型 Java 控制台应用，它：

1. 从磁盘加载 PNG 文件。  
2. 将图像发送至 OCR 引擎（Tess4J，Tesseract 的 Java 包装器）。  
3. 将识别出的文本打印到控制台。

无需外部服务，也不需要魔法——纯 Java 加上开源 OCR 引擎即可。

## 前置条件

- **Java 17** 或更高（代码在旧版本也能编译，但 Java 17 提供最新的语言特性）。  
- **Maven** 或 **Gradle** 用于依赖管理。  
- 一个名为 `sample.png` 的示例 PNG，放在可引用的文件夹中（例如 `src/main/resources`）。  
- 对 Java 的 `main` 方法和异常处理有基本了解。

如果上述任意一点你不熟悉，也无需担心——每一步都有简要回顾。

## 步骤 1：搭建项目并添加 OCR 库

首先，新建一个 Maven 项目（如果偏好 Gradle 也可）。添加 Tess4J 依赖，它会为你自动引入 Tesseract 二进制文件。

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **小贴士：** 若使用 Gradle，对应的写法是 `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`。

引入该库后，你即可使用 `Tesseract` 类，它负责 **对图像执行 OCR** 的繁重工作。

## 步骤 2：加载用于 OCR 的图像

接下来我们需要 **加载用于 OCR 的图像**。Tess4J 使用 `java.awt.image.BufferedImage`，因此我们通过 `ImageIO` 读取 PNG。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

上述方法将 **加载用于 OCR 的图像** 逻辑单独抽离，使其余代码更易于测试。请注意注释——它在保持原始片段的同时，增加了清晰度。

## 步骤 3：对图像执行 OCR

图像已在内存中后，我们即可 **对图像执行 OCR**。`Tesseract` 实例即为我们的引擎；我们将配置它使用 Tess4J 自带的默认英文语言数据。

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

这里我们将原来的 “步骤 1” 与 “步骤 4” 合并为一个方法，因为创建 `Tesseract` 对象开销不大，且保持代码紧凑。注释仍然引用原始步骤，以便追溯。

## 步骤 4：整合代码 – 主方法

最后，在 `main` 方法中把所有内容串联起来。这一步你将 **从 PNG 读取文本** 并在控制台看到结果。

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

运行 `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"`（或对应的 Gradle 命令），你应当看到类似以下的输出：

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

该输出证明你已经成功 **从图像中提取文本**、**将 PNG 转换为文本**，并 **从 PNG 读取文本**，整个过程干净利落。

## 处理常见边缘情况

### 低质量图像

如果 PNG 模糊或对比度低，OCR 准确率会下降。一个快速的解决办法是对图像进行预处理：

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### 多语言支持

Tess4J 支持多种语言。只需下载相应的 `.traineddata` 文件，并将 `tesseract.setLanguage("spa")` 设置为西班牙语（示例）。

### 大型 PDF 或多页图像

若需 **从图像中提取文本** 的文件位于 PDF 中，可先使用 PDFBox 将每页拆分为 PNG，然后将每个 PNG 交给相同的 OCR 流程处理。

## 完整可运行示例（所有代码集中在一起）

下面是完整的、可直接运行的 Java 类。将其复制粘贴到 `src/main/java/com/example/ocrdemo/OcrDemo.java` 即可使用。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

运行该类后会打印 OCR 结果，确认你已经成功 **对图像执行 OCR** 并将 PNG 转换为可编辑文本。

## 小结与后续步骤

我们通过轻量的 Java 环境 **从图像中提取文本**。现在你已经掌握了 **加载用于 OCR 的图像**、**对图像执行 OCR**、以及 **从 PNG 读取文本**——这些都是任何文档数字化流水线的核心构件。

想进一步提升？可以尝试以下思路：

- **批量处理：**遍历一个 PNG 目录，将每个结果写入对应的 `.txt` 文件。  
- **与数据库集成：**将提取的字符串连同元数据一起存入数据库，实现可搜索的档案。  
- **结合 NLP：**将 OCR 输出喂入情感分析模型，快速获取洞察。  

这些扩展都基于我们本教程的核心概念，你已经准备好进行实验。

---

*祝编码愉快！如果遇到任何问题

## 接下来你应该学习什么？

以下教程与本指南所示技术密切相关，提供完整的代码示例和逐步说明，帮助你掌握更多 API 功能并探索替代实现方式。

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}