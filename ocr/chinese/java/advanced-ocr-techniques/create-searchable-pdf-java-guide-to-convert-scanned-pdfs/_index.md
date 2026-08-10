---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 在 Java 中将扫描的 PDF 创建为可搜索的 PDF。学习如何转换扫描的 PDF、压缩 PDF 图像，并高效地进行
  PDF OCR 识别。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: zh
og_description: 使用 Aspose OCR 在 Java 中将扫描的 PDF 创建为可搜索的 PDF。本分步教程展示了如何转换扫描的 PDF、压缩
  PDF 图像以及进行 PDF OCR 识别。
og_title: 创建可搜索的 PDF – Java 将扫描 PDF 转换为可搜索的指南
tags:
- Java
- OCR
- PDF
- Aspose
title: 创建可搜索 PDF – Java 将扫描 PDF 转换为可搜索的指南
url: /zh/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建可搜索 PDF – Java 将扫描的 PDF 转换指南

是否曾需要从一堆扫描文档中 **create searchable PDF**？这是一大常见痛点——PDF 看起来正常，却无法使用 *Ctrl + F* 搜索任何内容。好消息是，只需几行 Java 代码和 Aspose OCR，就能把仅包含图像的 PDF 转换为完整可搜索的文件，**convert scanned PDF** 为文本，并且还能通过 **compressing PDF images** 来减小文件体积。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，解释每个设置为何重要，并展示如何针对多页扫描或低分辨率图像等边缘情况进行调优。完成后，你将拥有一个可靠、可投入生产的代码片段，能够 **recognize pdf ocr** 并生成整洁的可搜索文档。

---

## 你需要准备的环境

- **Java 17**（或任何近期的 JDK；API 与 JDK 无关）  
- **Aspose.OCR for Java** 库——可从 Maven Central 获取 (`com.aspose:aspose-ocr`)  
- 一份你想要转换为可搜索的扫描 PDF（仅图像）  
- 你熟悉的 IDE 或文本编辑器（IntelliJ、VS Code、Eclipse 等）

无需繁重框架，无需外部服务——只需纯 Java 加上一个第三方 JAR。

---

![create searchable pdf example](placeholder-image.png "扫描文档转换为可搜索 PDF 的示意图")

*图片替代文字:* **create searchable pdf** 示意图，展示扫描 PDF 在转换前后的对比。

---

## 第一步 – 初始化 OCR 引擎  

首先需要实例化一个 `OcrEngine`。它相当于大脑，会分析 PDF 中的每个位图并输出 Unicode 字符。

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **小贴士:** 如果需要连续处理大量 PDF，建议复用同一个 `OcrEngine` 而不是每次都新建。这样可以节省几毫秒并降低内存抖动。

---

## 第二步 – 配置 PDF 专用 OCR 选项  

Aspose 允许细粒度地调节输出 PDF 的构建方式。下面三个设置是实现 **compress pdf images** 同时保持可搜索性的关键。

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi 是一个折中值；更低的数值可以加快速度，但可能漏掉小字号。  
- **CompressImages** – 在内部启用无损 PNG 压缩；生成的可搜索 PDF 仍保持清晰，同时体积更轻。  
- **EmbedOriginalImages** – 若不启用此标志，引擎会丢弃原始光栅图，只保留不可见的文字层。保留图像可以让 PDF 与原始扫描稿完全一致，这在许多合规场景下是必需的。

---

## 第三步 – 将扫描 PDF 加载到 `OcrInput`  

Aspose 通过 `OcrInput` 包装器读取源文件。你可以一次添加多个文件，但本示例仅聚焦于单个 **image PDF**。

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **为什么不直接传 `File`？** 使用 `OcrInput` 可以灵活地将多个 PDF 合并，甚至在 OCR 前混入 PNG、JPEG 等图像文件。这是处理可能分散在多个来源的 **convert scanned pdf** 时的推荐做法。

---

## 第四步 – 执行 OCR 并获取可搜索 PDF 的字节数组  

现在魔法发生了。引擎会逐页分析，运行 OCR，并生成一个新 PDF，里面既包含原始图像，又嵌入了隐藏的文字层。

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

如果你还需要原始文本用于其他用途（例如建立索引），可以调用 `ocrEngine.recognize(ocrInput)`，它会返回 `String`。但对于 **create searchable pdf** 的目标，字节数组才是最终要写入磁盘的内容。

---

## 第五步 – 将可搜索 PDF 保存到磁盘  

最后，将字节数组写入文件。Java NIO 只需一行代码即可完成。

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

当你在 Adobe Acrobat 或任意现代阅读器中打开 `searchable_output.pdf` 时，会发现现在可以选中、复制并搜索文本——这正是 **image pdf to text** 转换所承诺的效果。

---

## 将扫描 PDF 转换为文本（可选）

有时你只需要提取纯文本，而不是生成新 PDF。可以复用同一个引擎：

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

此代码片段演示了如何轻松实现 **recognize pdf ocr**，以便后续将文本喂入搜索索引或进行自然语言分析。

---

## 压缩 PDF 图像以获得更小的文件  

如果源扫描文件非常大（例如 600 dpi 彩色扫描），生成的可搜索 PDF 仍可能体积庞大。除了 `setCompressImages(true)` 标志外，你还可以在 OCR 前手动降采样：

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

降低 DPI 大约可以将文件大小减半，但请务必测试可读性——低于 150 dpi 时部分字体可能难以辨认。**compress pdf images** 与 OCR 准确度之间的权衡，需要根据你的存储限制自行决定。

---

## OCR 设置详解  

| 设置 | 对输出的影响 | 典型使用场景 |
|------------------------|------------------------------------------|----------------------------------------------------|
| `setOutputDpi(int)`    | 控制 OCR 输出的光栅分辨率 | 高质量档案（300 dpi） vs. 轻量化网页 PDF（150 dpi） |
| `setCompressImages`    | 启用 PNG 压缩 | 需要通过邮件发送或在云端存储 PDF 时 |
| `setEmbedOriginalImages`| 保留原始扫描图像 | 法律或合规文档必须保持原始外观 |
| `setLanguage` (optional) | 强制使用特定语言模型（如 "eng"） | 多语言语料库，默认自动检测可能出错 |

理解这些调节项可以帮助你更智能地 **recognize pdf ocr**，避免出现“文字模糊”的情况。

---

## Image PDF to Text – 常见陷阱及规避方法  

1. **低分辨率扫描** – 当 DPI 低于 150 时 OCR 准确度急剧下降。可在送入 Aspose 前对源文件进行上采样，或让扫描仪输出更高 DPI。  
2. **页面旋转** – 若页面横向扫描，可启用自动旋转：`pdfOcrOptions.setAutoRotate(true);`。  
3. **加密 PDF** – 引擎无法读取受密码保护的文件；需先使用 Aspose.PDF 的 `PdfDocument` 解密。  
4. **光栅与文字混合** – 某些 PDF 已自带隐藏文字层，再次 OCR 会导致文字重复。使用 `PdfOcrOptions.setSkipExistingText(true);` 可保留原有文字层。

处理好这些问题后，你的 **create searchable pdf** 流程即可在真实文档集合中稳健运行。

---

## 完整工作示例（所有步骤合并在一个文件中）

下面是完整的 Java 类，可直接复制到 IDE 中使用。请将 `YOUR_DIRECTORY` 替换为实际文件夹路径。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}