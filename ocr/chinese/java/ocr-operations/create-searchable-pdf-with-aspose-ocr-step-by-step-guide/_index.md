---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 将扫描的图像 PDF 创建可搜索的 PDF。了解如何设置 OCR 语言、嵌入文本层 PDF 并应用高压缩 PDF
  选项。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: zh
og_description: 快速创建可搜索的 PDF。本指南展示了如何将扫描的图像 PDF 转换，嵌入文本层，设置 OCR 语言并启用高压缩 PDF。
og_title: 使用 Aspose OCR 创建可搜索的 PDF – 完整指南
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: 使用 Aspose OCR 创建可搜索 PDF – 步骤指南
url: /zh/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建可搜索 PDF – 完整编程教程

是否曾经需要从扫描图像中 **create searchable PDF** 文件，但不知从何入手？你并不孤单。在许多文档密集的工作流中，纯图片 PDF 对搜索和索引来说是死路。  

好消息是，使用 Aspose OCR，您可以仅用几行 Java 代码 **convert scanned image PDF** 成为完整的可搜索文档。本教程将逐步演示每一步——初始化 OCR 引擎、配置高压缩 PDF 设置、嵌入隐藏文本层，甚至选择正确的 OCR 语言。  

阅读完本指南后，您将拥有一个可运行的程序，能够生成可搜索的 PDF 文件，您可以毫无障碍地将其放入任何搜索引擎或文档管理系统。

---

## 创建可搜索 PDF – 概览

在深入代码之前，让我们澄清一下“create searchable PDF”到底意味着什么。可搜索的 PDF 包含两个并行层：

1. **Visual layer** – 原始扫描图像（或渲染页面）。  
2. **Text layer** – 不可见但机器可读取的字符，由 OCR 提取。  

当您在 Adobe Reader 中打开此类 PDF 并选择文本时，实际上是在与隐藏的文本层交互，而不是图片。这种双层方法实现了 **embed text layer PDF** 功能。

---

## 使用 Aspose OCR 转换扫描图像 PDF

首先，您需要一张扫描图像（PNG、JPEG、TIFF），希望将其转换为 PDF。Aspose OCR 能读取该图像，执行 OCR，并将结果交给 PDF 写入器。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**为什么这样有效:**  
- `setCreateSearchablePdf(true)` 告诉 Aspose 生成隐藏的文本层，满足 **embed text layer pdf** 的要求。  
- `setCompressionLevel(9)` 将文件压缩到 **high compression pdf** 范围，缩小最终大小而不牺牲 OCR 准确性。  
- `RecognitionLanguage.ENGLISH` 参数展示了如何 **set OCR language**；您可以根据源材料将其替换为法语、德语等。

---

## 高压缩 PDF 设置

大型扫描 PDF 很快会膨胀到数百兆。Aspose 提供了一个在 PDF 层面工作的简易压缩 API。`setCompressionLevel` 方法接受 0（无压缩）到 9（最大压缩）的数值。  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

几点提示：

- **Use lossless image formats** (PNG) 用于文本密集的扫描；JPEG 更适合照片。  
- **Enable font subsetting** 如果嵌入自定义字体——在创建可搜索 PDF 时，Aspose 会自动执行此操作。  
- **Test the output size** 每次更改后进行测试；有时 8 级压缩可实现约 10% 的大小缩减，且相较于 9 级几乎没有质量损失。

---

## 嵌入文本层 PDF 以实现可搜索性

如果跳过 `setCreateSearchablePdf(true)` 调用，生成的文件外观正常，但您将无法搜索其内容。隐藏的文本层是通过将每个识别字符映射到页面上的位置创建的。  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**需要注意的事项:**  

- **Mixed‑language documents** – 您可能需要对每种语言分别运行 OCR 两次，然后合并文本层。  
- **Complex layouts** (tables, multi‑column) – Aspose 做得相当不错，但请使用能够显示隐藏文本的 PDF 查看器（例如 Adobe Acrobat 的“编辑 PDF”模式）再次检查输出。

---

## 设置 OCR 语言以获得准确识别

OCR 引擎的准确性取决于您指定的语言。Aspose 附带一套内置语言，您也可以添加自定义语言包。

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**何时更改语言:**  

- 文档包含 **non‑Latin scripts**（西里尔文、阿拉伯文）——切换到相应的 `RecognitionLanguage`。  
- 混合语言页面——您可以两次调用 `recognizeImageAndSave`，每次使用不同的语言，然后合并 PDF。

---

## 运行完整示例

下面是完整的可直接运行的程序。将占位符路径替换为实际文件位置，确保 Aspose OCR JAR 已加入 classpath，然后执行。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**预期输出:** 当您运行程序时，控制台会打印：

```
Searchable PDF created.
```

在任意 PDF 查看器中打开 `searchable.pdf`，尝试选择文本，您将看到隐藏层的效果。您已成功 **create searchable pdf** 从扫描图像中生成。

![创建可搜索 PDF 示例](image-placeholder.png "创建可搜索 PDF 示例")

*上面的截图（占位符）通常会显示 PDF 查看器中可在扫描页面上选择文本的效果。*

---

## 结论

我们已经介绍了使用 Aspose OCR **create searchable PDF** 所需的全部内容：

- 初始化 OCR 引擎。  
- **Convert scanned image PDF** 通过将 PNG/JPEG 输入到 `recognizeImageAndSave`。  
- 使用 `setCreateSearchablePdf(true)` 来 **embed text layer PDF**。  
- 使用 `setCompressionLevel(9)` 以获得 **high compression PDF**，保持轻量。  
- 选择合适的 `RecognitionLanguage` 来 **set OCR language**，以获得最高准确性。  

从这里您可以尝试批量处理、不同语言，甚至将多页扫描合并为单个可搜索 PDF。相同的模式同样适用于西班牙语、日语等语言——只需更换 `RecognitionLanguage` 枚举即可。  

如果遇到任何问题，欢迎留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}