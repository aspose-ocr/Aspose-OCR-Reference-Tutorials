---
date: 2026-06-19
description: 了解如何在 Java 中将图像转换为文本（convert image to text），从图像中提取段落（extract paragraphs），并使用
  Aspose OCR Java library 检索文本区域矩形。
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – 识别图像中的文本并检索文本区域矩形
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – 将图像转换为文本并检索文本区域矩形
url: /zh/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 图像转文本 – 将图像转换为文本并检索文本区域矩形

## 介绍

如果您需要在 Java 应用程序中 **convert image to text**，Aspose.OCR for Java 提供了快速、准确的解决方案。在本教程中，我们将逐步演示从图像中提取段落、获取每个文本区域的边界矩形，并将这些坐标打印到控制台的完整步骤。完成后，您将了解为何此方法有效、如何集成该库以及在哪里可以为自己的使用场景进行扩展。

## 快速回答
`AreasType` 是一个枚举，指定文本分割的层级（单词、行、段落）。

- **What does “recognize text from image” mean?** 这意味着将图片中的可视字符转换为可编辑的字符串数据。  
- **哪个库在 Java 中处理此功能？** Aspose.OCR for Java。  
- **我在开发时需要许可证吗？** 临时许可证可用于测试；生产环境需要正式许可证。  
- **我可以提取段落而不是单个单词吗？** 是的 – 使用 `AreasType.PARAGRAPHS` 获取段落级别的矩形。  
- **代码兼容 Java 11+ 吗？** 当然，API 在 Java 11 及更高版本上均可工作。

## 在 Aspose.OCR 中，“convert image to text” 是什么？

`convert image to text` 指的是分析位图、应用 OCR 算法并将识别的字符返回为字符串的过程。Aspose.OCR 的 `RecognizePage` 方法执行此转换，同时可选地提供每个检测到的文本块的精确 `Rectangle` 坐标。

## 为什么使用这个 **java ocr library**？

Aspose.OCR 支持 **30+ languages**，并且能够在不将整个文件加载到内存中的情况下处理高达 **50 MB** 的图像，在典型服务器硬件上实现亚秒级响应时间。该库是线程安全的，仅需一个 JAR，即可提供灵活的输出格式——包括原始文本、HTML 和精确的文本区域矩形——使其非常适合高吞吐量的企业场景。

## 先决条件

- **Java Development Kit** (JDK 11 或更高) 已安装在您的机器上。  
- **Aspose.OCR for Java** 库 – 从官方网站 [here](https://releases.aspose.com/ocr/java/) 下载。  
- 用于管理 JAR 依赖的 IDE 或构建工具（Maven/Gradle）。

## 导入包

在您的 Java 项目中，导入必要的类：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 分步指南

### 步骤 1：设置项目
创建一个新的 Java 项目（或在现有项目中添加），并将 Aspose.OCR JAR 放置在类路径上。如果使用 Maven，请按照下载包中描述的方式添加依赖。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 步骤 2：定义文档目录和图像路径
指定您的示例图像所在的位置：

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 步骤 3：创建 AsposeOCR 实例
`AsposeOCR` 是提供 OCR 功能的主类。

实例化 OCR 引擎：

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 步骤 4：识别图像中的文本
加载图像并调用 `RecognizePage` 将图片转换为纯文本。此单一方法调用在一步中完成图像预处理、字符分割和语言特定的识别。

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### 步骤 5：获取带有文本区域的矩形
检索每个段落（或其他区域类型）的边界矩形。此步骤返回 `Rectangle` 对象的集合，精确包围检测到的文本块，使您能够突出显示或进一步处理各个部分。

CODE_BLOCK_PLACEHOLDER_5_END

## 常见问题与故障排除

| 症状 | 可能原因 | 解决方案 |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | 文件路径不正确或缺少读取权限 | 验证 `imagePath` 指向现有的 PNG/JPG，并且应用具有文件系统访问权限。 |
| 结果字符串为空 | 图像质量低或语言不受支持 | 对图像进行预处理（提高对比度、二值化）或使用 `api.setLanguage("eng")` 指定正确的语言。 |
| 未返回矩形 | 使用了错误的 `AreasType`（例如在期望段落时使用 `WORDS`） | 根据需要切换到 `AreasType.PARAGRAPHS` 或 `AreasType.LINES`。 |

## 常见问题

**Q: Aspose.OCR 与 Java 11 兼容吗？**  
**A:** 是的，Aspose.OCR 可在 Java 11 及更高版本上运行。

**Q: 我可以在个人和商业项目中使用 Aspose.OCR 吗？**  
**A:** 可以，您可以在任何类型的项目中使用。有关许可详情，请访问 [here](https://purchase.aspose.com/buy)。

**Q: 我如何获取用于评估的临时许可证？**  
**A:** 您可以在 [here](https://purchase.aspose.com/temporary-license/) 获取临时许可证。

**Q: 我在哪里可以找到社区支持或官方帮助？**  
**A:** 请访问 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 获取支持和讨论。

**Q: Aspose.OCR 支持多线程吗？**  
**A:** 是的，该库是线程安全的，可在并发环境中使用以获得更好性能。

## 结论

在本 **aspose ocr java tutorial** 中，您学习了如何使用 Aspose.OCR for Java **convert image to text**，提取段落，并获取围绕每个文本块的精确矩形。这些功能使您能够构建可搜索的 PDF，在 UI 覆盖层中高亮文本，或将结构化数据输送到下游流程。进一步探索 API，以自定义语言设置、处理不同的图像格式或集成云存储。

---

**最后更新：** 2026-06-19  
**测试环境：** Aspose.OCR 23.10 for Java  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相关教程

- [提取文本图像 – 使用 Aspose.OCR for Java 的 OCR 基础](/ocr/java/ocr-basics/)
- [使用 Aspose.OCR 检测区域模式的 Java 图像提取文本](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose.OCR BufferedImage 在 Java 中将图像转换为文本](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}