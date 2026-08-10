---
category: general
date: 2026-06-22
description: 使用 Java 的 OCR 创建可搜索的 PDF。了解如何禁用压缩并快速将扫描的图像 PDF 转换为可搜索的 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: zh
og_description: 使用 Java 的 OCR 创建可搜索的 PDF。本指南展示了如何禁用压缩、转换扫描图像 PDF，并生成不压缩的 PDF。
og_title: 使用 OCR 创建可搜索 PDF – 完整 Java 教程
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: 使用 OCR 创建可搜索的 PDF – 完整指南
url: /zh/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建可搜索 PDF 与 OCR – 完整指南

是否曾需要从一批扫描图像**创建可搜索 PDF**，但不确定该切换哪些设置？你并非唯一遇到这种情况的开发者——大多数开发者在输出变成巨大的、不可读的文件时都会卡住。  

在本教程中，我们将演示一个简洁的端到端示例，准确展示如何使用 Java OCR 引擎**创建可搜索 PDF**、**转换扫描图像 PDF**，以及关键的**如何禁用压缩**，以确保生成的文件保持原始尺寸。完成后，你将拥有可直接运行的代码片段，并深入理解每个配置为何重要。

## 您将学习

* 如何配置 OCR 引擎以**ocr 到可搜索 pdf**。  
* 关闭 PDF 压缩的原因以及如何获得**无压缩 pdf**。  
* 一个完整的 Java 程序，接受扫描图像，运行 OCR，并保存**可搜索 PDF**。  
* 处理多页扫描或低分辨率源等边缘情况的技巧。  

**先决条件** – 已安装 Java 8+，兼容的 OCR SDK（代码使用 ABBYY FineReader Engine API，但概念适用于任何提供 `setOutputFormat` 和 `setPdfCompression` 的库）。使用 IntelliJ IDEA 或 Eclipse 等 IDE 会更方便，但普通文本编辑器也能胜任。

---

![创建可搜索 PDF 工作流](image-placeholder.png "示意图：从扫描图像到最终 PDF 的创建可搜索 pdf 过程")

## 步骤 1：将 OCR 引擎设置为 **创建可搜索 PDF**

首先需要告诉 OCR 引擎你期望的输出类型。默认情况下，许多 SDK 会输出纯文本或光栅 PDF，这些文件不可搜索。切换格式即可为你完成繁重的工作。

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*为什么这很重要*：`PDF_SEARCHABLE` 标志指示引擎在扫描图像下方嵌入一个不可见的文本层。搜索工具随后可以对文档进行索引，使其行为如同在 Adobe Reader 中打开的任何原生 PDF。

## 步骤 2：禁用压缩 – 正确的 **如何禁用压缩**

如果跳过此步骤，引擎会压缩每页以节省空间，但压缩会模糊细节——在后续需要提取高分辨率图像时尤为成问题。

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**专业提示**：在计划归档法律文件或医学扫描（每个像素都至关重要）时，禁用压缩是必需的。生成的文件可能更大，但你保留了原始尺寸和清晰度。

## 步骤 3：执行 OCR 并获取生成的文档

现在引擎已经知道要输出什么以及如何处理图像，你可以运行识别。该调用返回一个已准备好保存或进一步处理的 `PdfDocument` 对象。

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*内部到底发生了什么？* 引擎处理每个输入页，执行字符识别，并将隐藏的文本层缝合到图像上。如果有多页，它们会自动拼接。

## 步骤 4：将 **可搜索 PDF** 保存到磁盘

最后，将内存中的 PDF 写入文件。选择一个你拥有写权限的位置，并为文件起一个有意义的名称。

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

当你在查看器中打开 `searchable.pdf` 时，会发现可以选中并搜索文本——即使可见内容仍是原始扫描图像。

### 完整工作示例

下面是一个自包含的 Java 类，整合了上述四个步骤。随意复制粘贴，调整输入路径，即可直接运行。

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**预期输出** – 运行程序后，你会在控制台看到上述信息，文件 `searchable.pdf` 将出现在 `YOUR_DIRECTORY` 中。使用任何 PDF 阅读器打开它，都可以：

* 高亮文本。  
* 使用内置搜索（Ctrl + F）定位单词。  
* 如有需要，导出隐藏的文本层。  

---

## 为什么禁用压缩？理解 **无压缩 PDF**

你可能会想，“压缩不是一直都很好吗？”答案并非如此简单：

| 情形 | 保持压缩 (`NORMAL`) | 禁用压缩 (`NONE`) |
|-----------|-----------------------------|------------------------------|
| 法律合同归档 | ❌ 可能改变像素保真度 | ✅ 保证原始外观 |
| 大批低分辨率扫描 | ✅ 节省存储空间 | ❌ 增加大小且无益 |
| 需要对细小字体的 OCR 准确性 | ❌ 模糊细节 | ✅ 保留每一笔画 |

简而言之，**如何禁用压缩**是存储与保真度之间的权衡。对于大多数只需搜索文本而非重新打印图像的可搜索 PDF 工作流，关闭压缩是最安全的选择。

## 直接转换 **扫描图像 PDF**

有时你已经拥有一个包含扫描图像的 PDF（“仅图像 PDF”）。要将 **扫描图像 pdf** 转换为可搜索版本，只需将整个 PDF 传递给引擎，而不是单独的图像：

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

相同的配置标志（`PDF_SEARCHABLE` 和 `PdfCompression.NONE`）同样适用，即使从 PDF 容器开始，也能得到 **无压缩 pdf**。

## 常见陷阱及避免方法

* **忘记设置输出格式** – 引擎默认生成光栅 PDF，无法搜索。务必在 `recognizeToPdf()` 之前调用 `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)`。  
* **大批量处理时内存不足** – 分块加载和处理页面，或使用 SDK 提供的流式 API。  
* **文件路径不正确** – 使用绝对路径或确保工作目录设置正确；否则 `pdf.save()` 会抛出 `IOException`。  
* **许可证未激活** – 大多数商业 OCR SDK 需要有效许可证；若缺失，引擎会抛出运行时异常。

---

## 结论

你现在拥有一个完整、可直接运行的解决方案，展示了**如何创建可搜索 PDF**文件、**转换扫描图像 PDF**以及**如何禁用压缩**以生成**无压缩 pdf**。关键步骤如下：

1. 将输出格式设为 `PDF_SEARCHABLE`。  
2. 使用 `PdfCompression.NONE` 关闭 PDF 压缩。  
3. 运行 OCR 并获取 `PdfDocument`。  
4. 将文件保存到磁盘。

从这里你可以尝试更换字体、添加水印，或批量处理整个文件夹。如果你想了解如何添加 OCR 语言包、处理多页 TIFF，或将此工作流集成到 Web 服务中，请关注我们即将推出的 “Java 中的 OCR 语言选择” 与 “大文档集的流式 OCR” 教程。

有问题或发现卡点？在下方留言——祝编码愉快，尽情享受全新的可搜索 PDF 吧！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [识别 PDF 文本 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [在 Aspose.OCR for Java 中 OCR 识别 PDF 文档](/ocr/english/java/ocr-operations/recognize-pdf/)
- [将图像转换为 PDF C# – 保存多页 OCR 结果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}