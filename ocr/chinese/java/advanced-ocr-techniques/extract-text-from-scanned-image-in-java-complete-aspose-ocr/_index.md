---
category: general
date: 2026-06-06
description: 使用 Aspose OCR for Java 从扫描图像中提取文本。了解如何使用并行处理识别 TIFF 文件中的文本。
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: zh
og_description: 使用 Aspose OCR 从扫描图像中提取文本。本指南展示了如何使用 Java 高效地识别 TIFF 文件中的文本。
og_title: 从扫描图像中提取文本 – Aspose OCR Java 教程
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: 在 Java 中从扫描图像提取文本 – 完整的 Aspose OCR 指南
url: /zh/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从扫描图像中提取文本 – 完整 Aspose OCR 指南

是否曾经需要**从扫描图像中提取文本**却不知道该怎么做？你并不孤单。无论是数字化旧档案、从发票中提取数据，还是构建可搜索的 PDF 库，从 TIFF 扫描件中获取可靠的文本都是一个痛点。

好消息：使用 Aspose OCR for Java，你可以仅用几行代码**从 tiff 识别文本**，甚至通过将引擎限制在少数 CPU 核心上来提升速度。在本教程中，我们将完整演示整个过程——从库的安装到结果处理——让你可以直接复制粘贴一个可运行的示例。

## 本教程涵盖内容

- 安装 Aspose OCR for Java（Maven 或手动 JAR）
- 加载大型扫描 TIFF 图像
- 将引擎配置为最多使用 4 条线程（并行 OCR）
- 运行 OCR 过程并打印提取的文本
- 常见陷阱（内存、多页 TIFF）及规避方法
- 性能小技巧：何时调优 `setMaxThreads`

完成后，你将能够**可靠地从扫描图像文件中提取文本**，并且了解在生产流水线中*从 tiff 识别文本*时为何需要调整线程数。

---

![extract text from scanned image example](example.png "Screenshot showing extracted text from a scanned TIFF image")

## 前置条件

在开始之前，请确保你具备以下条件：

1. **Java Development Kit (JDK) 8+** – 任意近期版本均可。
2. **Maven**（或手动添加 JAR 的能力）– 为了简便我们使用 Maven。
3. **Aspose OCR for Java** 许可证（免费评估版可用，但会添加水印）。  
4. 一个**大型 TIFF 扫描件**（例如 `large_scan.tif`），用于处理。

如果上述任意项你不熟悉，也无需担心——下面的每一步都会详细说明。

## 步骤 1：将 Aspose OCR 添加到项目

### Maven 用户

在 `pom.xml` 中加入以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### 手动 JAR 设置

从 Aspose 官网下载最新的 `aspose-ocr-xx.jar` 并放入类路径中。

> **专业提示：** 将 JAR 放在 `libs/` 文件夹，并在 IDE 的项目设置中引用它。这样可以避免后期出现 “class not found” 的意外。

## 步骤 2：创建一个简单的 Java 类

在源码文件夹（`src/main/java`）下新建 `ParallelOcrDemo.java`。该类将包含完整的 OCR 工作流。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **为何限制线程数：** 默认情况下 Aspose OCR 会尝试使用所有核心，这可能会在共享机器上抢占其他服务的资源。将 `setMaxThreads(4)` 设置为最多四个并行工作者——在大多数现代 CPU 上即可获得显著加速，同时不会独占资源。

## 步骤 3：编译并运行

在项目根目录打开终端，执行：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

如果不使用 Maven，可使用 `javac` 编译并运行：

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### 预期输出

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

控制台将显示扫描页上的纯文本内容。如果图像包含多页，Aspose OCR 会按顺序将它们拼接。

## 步骤 4：处理多页 TIFF（边缘情况）

常见场景是**多页 TIFF**——比如扫描的书籍。默认 `OcrInputImage` 只读取第一帧。若要处理所有页面，需要使用 `FileInputStream` 创建 `OcrInputImage` 并启用多页支持：

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

此时 `ocrEngine.process()` 将返回一个包含所有页面拼接文本的单一 `OcrResult`。

## 步骤 5：微调识别准确度

如果出现**字符乱码**或缺失单词，可尝试以下调整：

| 设置 | 功能说明 | 适用场景 |
|------|----------|----------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | 强制使用英文语言模型（对英文扫描更快、更准） | 文档为单语英文 |
| `ocrEngine.getSettings().setResolution(300)` | 在识别前将低分辨率图像放大 | DPI 低于 200 的扫描件 |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | 尝试清除噪点和伪影 | 噪声较重的扫描件 |

示例代码片段：

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## 步骤 6：将结果导出到文件

在演示时将结果打印到控制台已经足够，但生产代码通常会把输出写入有用的位置：

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

现在你拥有了一个纯文本文件，可将其导入搜索索引、数据库或下游分析流水线。

---

## 常见问题 (FAQ)

**问：这能用于 PNG 或 JPEG 文件吗？**  
答：完全可以。`OcrInputImage` 接受任何 Java ImageIO 能读取的格式。只需将路径中的文件扩展名替换即可。

**问：我的服务器有 8 核心——应该设置 `setMaxThreads(8)` 吗？**  
答：可以，但请记住其他服务也可能需要 CPU。一个经验法则是“总核心数 – 1”，用于专用 OCR 工作器。

**问：如果 OCR 结果为空怎么办？**  
答：检查图像是否全白、语言设置是否正确，以及分辨率是否至少为 200 DPI。低质量扫描通常需要在送入 Aspose OCR 前进行预处理（去倾斜、提升对比度）。

---

## 小结

我们已经使用 Aspose OCR for Java **从扫描图像文件中提取文本**，并了解了如何通过并行处理**从 tiff 识别文本**以获得高效性能。完整代码已在上面的代码块中提供，直接复制粘贴即可在自己的项目中使用。

### 接下来可以做什么？

- **批量处理**：遍历 TIFF 目录，为每个文件生成单独的结果文件。  
- **集成 Elasticsearch**：将提取的文本索引，以实现快速全文搜索。  
- **添加语言检测**：使用 `OcrLanguage.AutoDetect` 处理多语言文档。  

尝试这些思路，你将很快把大量扫描的纸质文件转化为可搜索、可操作的数据。

祝编码愉快，遇到问题欢迎留言交流！

## 接下来该学习什么？

以下教程与本指南所示技术紧密相关，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式，每篇都包含完整可运行的代码示例和逐步说明。

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}