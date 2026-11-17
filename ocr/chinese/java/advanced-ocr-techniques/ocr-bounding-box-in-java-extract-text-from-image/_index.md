---
category: general
date: 2026-06-16
description: Java 中的 OCR 边界框教程展示了如何从图像中提取文本、读取图像中的文本以及获取 JPG 文件的 OCR 置信度分数。
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: zh
og_description: Java 中的 OCR 边界框可让您从 JPG 文件识别文本、从图像提取文本，并查看 OCR 置信度分数——全部通过一个简单的代码示例实现。
og_title: Java 中的 OCR 边界框 – 从图像中提取文本
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Java 中的 OCR 边界框 – 从图像中提取文本
url: /zh/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 中的 OCR 边界框 – 从图像中提取文本

有没有想过如何获取 Java 图像中每段文本的 **ocr bounding box**？在本教程中，我们将向您展示如何 **extract text from image** 文件、**read text from image**，以及在 **recognize text from jpg** 文件时查看 **ocr confidence score**。简短的答案是？只需几行使用现代 OCR 库的代码，并稍作解释每个调用的意义。

下面您会找到一个完整、可直接运行的示例、逐步分解，以及一些实用技巧，您可以直接复制到自己的项目中。完成后，您将能够输出类似于以下内容：

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## 您需要的环境

- **Java 11** 或更高（下面的语法使用 `var` 关键字以简化，但在旧版 JDK 中可以去掉它）。  
- 提供 Java API 的 OCR 库——本指南使用 **[Tesseract4J](https://github.com/nguyenq/tess4j)**，它是流行的 Tesseract 引擎的轻量包装。  
- 一张包含清晰印刷文本的 JPEG 图像（`.jpg`）。  
- 您喜欢的 IDE（IntelliJ IDEA、Eclipse、VS Code…）——任选其一即可。

如果缺少该库，只需添加以下 Maven 依赖：

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

现在让我们开始吧。

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR 边界框：设置引擎

您首先需要做的是创建一个 OCR 引擎实例。可以把它想象成打开扫描仪，以便稍后读取像素。

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Why this matters:**  
如果不设置 `datapath`，Tesseract 将不知道语言包所在位置，会出现模糊的 “Failed loading language” 错误。如果只需要默认的英文包，`setLanguage` 调用是可选的，但明确指定可以让代码对后续阅读者更清晰。

## 加载要处理的图像

接下来，将您想要分析的 JPEG 传给引擎。库接受 `File` 或 `BufferedImage`；这里为了简便使用 `File`。

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
如果您的图像位于 resources 中（例如在 JAR 包内），请使用 `getResourceAsStream` 并用 `ImageIO.read` 包装。这样教程既可以在本地运行，也可以在打包后的应用中使用。

## 执行 OCR 识别

现在我们真正让引擎读取图片。结果是一个纯文本字符串，但我们还想获取每行的 **ocr confidence score** 和 **ocr bounding box**。

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Why we use `getWords` instead of the plain `doOCR`:**  
`doOCR` 只返回原始字符串，丢失空间信息。通过使用 `RIL_WORD`（如果想要行级框则使用 `RIL_TEXTLINE`）调用 `getWords`，我们可以获取一个 `Word` 对象列表，每个对象都包含文本、置信度和边界矩形。这就是 **ocr bounding box** 功能的核心。

## 理解输出

对干净的 JPEG 运行上面的代码片段会产生类似以下的输出：

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – 识别出的字符。  
- **Confidence** – 介于 0 到 1 之间的浮点值，数值越高表示引擎越有信心。  
- **Box** – 包围该单词的矩形，以像素坐标 (x, y, width, height) 表示。

现在您可以 **read text from image**，并且准确知道每段文字在画布上的位置——这对于高亮、裁剪或输入到后续的 NLP 流程中都非常适用。

## 边缘情况与常见陷阱

| 情况 | 需要注意的点 | 解决方案 / 替代办法 |
|-----------|-------------------|-------------------|
| 图像模糊或低对比度 | 置信度分数急剧下降（通常低于 0.6）。 | 使用 OpenCV 进行预处理：提升对比度，应用阈值化。 |
| JPEG 包含旋转的文字 | 边界框出现倾斜或缺失。 | 使用 `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` 让 Tesseract 自动检测方向。 |
| 大图像导致 OutOfMemoryError | 加载大图片时 Java 堆被占满。 | 在 OCR 前缩小图像（`ImageIO.read` → `BufferedImage.getScaledInstance`）。 |
| 需要行级框而非词级框 | `RIL_WORD` 返回每个词的框。 | 切换为 `ITesseract.PageIteratorLevel.RIL_TEXTLINE`。 |
| 非英文字符显示为 � | 语言数据未加载。 | 下载相应的 `.traineddata` 文件并将 `setDatapath` 指向其文件夹。 |

提前处理这些问题可以为您节省大量调试时间。

## 完整工作示例（所有步骤合在一个文件中）

下面是一个独立的 Java 类，您可以复制粘贴到 `src/main/java` 文件夹并使用 `mvn exec:java` 运行。它整合了我们讨论的所有内容。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程演示的技术。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.OCR 检测区域模式的 Java 图像文本提取](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [提取文本图像 – 使用 Aspose.OCR for Java 的 OCR 基础](/ocr/english/java/ocr-basics/)
- [使用 Aspose.OCR 进行语言识别的图像文字 OCR 方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}