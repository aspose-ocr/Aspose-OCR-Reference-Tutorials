---
category: general
date: 2026-07-05
description: 使用 Aspose OCR 在 Java 中创建可搜索的 PDF。了解如何压缩 PDF 中的图像、将扫描图像转换为 PDF，以及禁用 PDF
  的字体嵌入以减小文件大小。
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: zh
og_description: 使用 Aspose OCR 在 Java 中创建可搜索的 PDF。本教程展示了如何压缩 PDF 中的图像、将扫描图像转换为 PDF，以及如何禁用
  PDF 的字体嵌入。
og_title: 在 Java 中创建可搜索的 PDF – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: 在 Java 中创建可搜索的 PDF – 完整指南
url: /zh/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中创建可搜索 PDF – 完整指南

是否曾经需要从扫描文档**创建可搜索的 PDF**，但在“如何实现”这一步卡住了？你并不孤单。在许多项目中，将 TIFF 或 JPEG 转换为可实际搜索的 PDF 是*必备*功能，尤其是当你还想**压缩 PDF 中的图像**以保持文件大小可控时。

在本教程中，我们将使用 Aspose OCR for Java 进行动手演示。完成后，你将准确了解如何**将扫描图像转换为 PDF**，调整**压缩 PDF 中的图像**设置，甚至**禁用 PDF 字体嵌入**以再削减几千字节。没有废话——只提供一个完整、可直接运行的解决方案，今天即可放入你的代码库。

## 你将学到

- 在 Java 项目中设置 Aspose OCR 引擎。  
- 对 TIFF（或任何光栅图像）执行 OCR。  
- 配置 `PdfSaveOptions` 以**压缩 PDF 中的图像**并**禁用 PDF 字体嵌入**。  
- 将结果保存为**可搜索的 PDF**，可立即进行索引或搜索。  

**先决条件**  
- 已安装 Java 8 或更高版本。  
- 用于依赖管理的 Maven 或 Gradle（我们将展示 Maven 代码片段）。  
- 准备好处理的扫描图像文件（TIFF、PNG 或 JPEG）。  

如果你已经具备这些条件，下面开始吧。

![创建可搜索 PDF 工作流 – Java OCR 到 PDF 转换](/images/create-searchable-pdf-workflow.png "展示使用 Aspose OCR 创建可搜索 PDF 步骤的图示")

## 第 1 步：添加 Aspose OCR 依赖

首先，将 Aspose OCR 库拉入你的项目。使用 Maven 时，在 `pom.xml` 中添加以下内容：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

如果你更喜欢 Gradle，等价的写法是：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **专业提示：** 关注 Aspose 的发行说明；新版本通常会带来 OCR 准确性的性能提升。

## 第 2 步：初始化 OCR 引擎

创建 OCR 引擎就像实例化 `OcrEngine` 那么简单。该对象将处理从图像加载到文本提取的全部工作。

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

为什么需要专用的引擎？Aspose 将繁重的工作（图像预处理、语言模型）与应用的其他部分分离，这样你可以在多个文件之间复用同一个 `engine`，而无需重新初始化这些资源。

## 第 3 步：对扫描图像执行 OCR

现在我们将扫描文件喂给引擎。`recognizeImage` 方法返回一个 `RecognitionResult`，其中包含提取的文本和布局信息。

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **如果图像不是 TIFF 呢？**  
> Aspose OCR 会自动检测常见的光栅格式，因此你可以直接指向 JPEG、PNG 或 BMP，而无需更改代码。

## 第 4 步：配置 PDF 保存选项（压缩图像 & 禁用字体嵌入）

这一步正是次要关键词发挥作用的地方。我们将告诉 Aspose **压缩 PDF 中的图像**并**禁用 PDF 字体嵌入**。这两个设置都会减小最终文件大小——在需要交付大量文档时非常实用。

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**为什么要压缩图像？**  
扫描页通常分辨率很高；将质量压缩到 80 % 可以把 10 页 PDF 从 12 MB 缩小到不足 3 MB，且视觉损失几乎不可察觉。

**为什么要禁用字体嵌入？**  
如果 OCR 引擎使用的是系统标准字体（如 Arial 或 Times New Roman），嵌入这些字体是多余的。关闭此功能可进一步削减文件大小，尤其是在大批量处理时。

## 第 5 步：将 OCR 结果保存为可搜索 PDF

最后一步将所有内容拼接在一起：原始图像、提取的文本层以及我们刚才设置的 PDF 选项。

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

当你在 Adobe Reader 或任何现代阅读器中打开 `document.pdf` 时，会看到原始扫描图像**加上**一个不可见的文本层。在搜索框中输入单词即可高亮匹配——正是“创建可搜索 PDF”所承诺的效果。

### 预期输出

使用有效的 TIFF 运行程序会得到类似如下的结果：

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

打开 PDF，按 `Ctrl+F`，输入扫描页中出现的单词，即可跳转到对应位置。这正是成功的**创建可搜索 PDF**工作流的标志。

## 常见陷阱与规避方法

| 问题 | 产生原因 | 解决办法 |
|-------|----------------|-----|
| **空白 PDF** | `PdfSaveOptions` 未传递给 `saveAsSearchablePdf`。 | 确保调用接受 `PdfSaveOptions` 的重载方法。 |
| **乱码字符** | 未设置 OCR 语言（默认是英语）。 | 在 `recognizeImage` 之前使用 `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);`。 |
| **文件体积过大** | `setCompressImages(false)` 或 `setEmbedFonts(true)`。 | 保持上述两个标志的设置。 |
| **图像失真** | `setImageQuality` 设置得太低（<50）。 | 保持在 70‑90 之间，以获得良好的折中。 |

## 扩展示例

既然你已经能够**将扫描图像转换为 PDF**并控制大小，接下来可能想要：

- 使用简单的 `for(File f : folder.listFiles())` 循环**批量处理**文件夹中的扫描件。  
- 使用 Aspose PDF 添加**水印**（`PdfDocument.addWatermarkText`）。  
- 将 OCR 文本导出为**纯 .txt**文件，以供索引系统使用（`result.getText().writeToFile("doc.txt")`）。  

所有这些扩展都复用同一个 `OcrEngine` 实例，保持内存占用低。

## 完整、可直接运行的代码

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

复制粘贴到你的 IDE， 将 `YOUR_DIRECTORY` 替换为实际路径，然后运行。如果一切配置正确，你将得到一个 **可搜索的 PDF**，并因图像压缩和禁用字体嵌入而保持轻量。

## 结论

我们已经覆盖了使用 Aspose OCR 在 Java 中**创建可搜索 PDF**所需的全部内容。从初始化引擎、执行 OCR、调优**压缩 PDF 中的图像**和**禁用 PDF 字体嵌入**，到最终保存可搜索文档——每一步都解释了背后的 *原因*。

准备好迎接下一个挑战了吗？尝试添加 OCR 语言包、批量处理整个文件夹，或在 PDF 上叠加批注。你刚掌握的基础将使这些扩展轻而易举。

有问题或想分享自己的技巧？在下方留言吧，祝编码愉快！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中实现的替代方案，每篇资源均提供完整可运行的代码示例和逐步解释。

- [识别 PDF 文本 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [在 Aspose.OCR for Java 中 OCR 识别 PDF 文档](/ocr/english/java/ocr-operations/recognize-pdf/)
- [如何在 .NET 中使用 Aspose.OCR 进行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}