---
category: general
date: 2026-07-05
description: 使用 Java 将 PNG 转换为 PDF 时压缩 PDF 图像。学习 OCR 的图像预处理，识别 JPG 文本，并在一个教程中实现批量
  OCR 转 PDF。
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: zh
og_description: 使用 Java 压缩 PDF 图像并将 PNG 转换为 PDF。本指南涵盖 OCR 的图像预处理、识别文本 JPG，以及批量 OCR
  转 PDF。
og_title: 使用 Java 压缩 PDF 图像 – 完整批量 OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: 使用 Java 压缩 PDF 图像 – 完整批量 OCR 转 PDF 指南
url: /zh/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 压缩 PDF 图像 – 完整批量 OCR 转 PDF 指南

是否曾经需要在将一文件夹的 PNG 转换为可搜索的 PDF 时 **压缩 PDF 图像**？你并不是唯一遇到这种情况的人。在许多自动化流水线中，最大的痛点是同时兼顾图像质量、OCR 准确性和最终 PDF 大小。

在本教程中，我们将演示一个实用方案，**将 PNG 转换为 PDF**，进行 **OCR 图像预处理**，并最终 **压缩 PDF 图像** 以保持输出文件轻量。完成后，你将了解如何 **识别文本 JPG** 文件，搭建 **批量 OCR 转 PDF** 工作流，并保持 PDF 整洁。

## 你将学到

- 为 Java 设置 Aspose OCR 并应用许可证。
- 配置引擎以支持多线程、GPU 加速和拼写校正。
- 构建可复用的 **OCR 图像预处理** 流程（去噪、对比度、二值化）。
- 使用 **PdfSaveOptions** **压缩 PDF 图像**，而不牺牲可读性。
- 循环遍历目录，批量 **将 PNG 转换为 PDF** 并 **识别文本 JPG**。
- 一个完整、可直接运行的 Java 程序，可嵌入任何项目。

> **先决条件**：Java 8+、Maven 或 Gradle、Aspose OCR for Java 许可证，以及需要处理的 PNG/JPG 图像文件夹。

---

## 第 1 步：应用 Aspose OCR 许可证（生产必备）

在调用任何 OCR API 之前，必须加载有效的许可证；否则只能使用受限的试用版。

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*为什么重要*：拥有许可证的引擎可解锁 GPU 支持、更高的识别精度，并去除会导致 PDF 文件膨胀的水印。

---

## 第 2 步：配置 OCR 引擎 – 线程、GPU 与拼写校正

快速的 OCR 引擎是任何 **批量 OCR 转 PDF** 任务的核心。我们将根据主机 CPU 能力启动尽可能多的线程，启用 GPU 加速（如果有兼容的显卡），并加强拼写校正以清理 OCR 错误。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*专业提示*：如果在没有 GPU 的无头服务器上运行，只需设置 `gpu.setEnabled(false)` —— 代码仍可工作，只是稍慢一些。

---

## 第 3 步：构建图像预处理流水线

原始扫描常常存在噪点、低对比度或光照不均。**OCR 图像预处理** 能显著提升识别率，尤其是在 **识别文本 JPG** 场景下。

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*为何要这样链式调用*：先去噪可防止二值化时放大噪点；随后调高对比度让字符更突出；最后二值化为 OCR 引擎提供干净的二进制图像。

---

## 第 4 步：准备 PDF 保存选项 – 高效 **压缩 PDF 图像**

Aspose 允许细粒度调节 PDF 输出。我们将开启图像压缩，并设置一个在体积与可读性之间取得平衡的质量等级。

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*结果*：每个可搜索的 PDF 都会明显更小——非常适合归档或通过邮件发送。

---

## 第 5 步：处理文件夹 – 在一次循环中 **将 PNG 转换为 PDF** 并 **识别文本 JPG**

现在把所有步骤组合起来。循环遍历输入目录，对每个 PNG 或 JPG 执行 OCR，并将可搜索的 PDF 写入输出文件夹。PDF 文件名与源图像名称保持一致。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### 预期输出

运行程序会为每张图像打印一行，例如：

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

在任意 PDF 查看器中打开生成的文件，你会看到可选中、可搜索的文本，同时文件大小通常比未压缩的对应文件 **小 30‑50 %**。

---

## 常见问题与边缘情况

### 我的服务器没有 GPU，怎么办？
只需将 `gpuSettings.setEnabled(false)`。其余流水线保持不变，仍可获得多线程 CPU 处理。

### 我的 PDF 仍然太大——可以进一步降低质量吗？
可以。调整 `options.setImageQuality(70)`，甚至 `50`。数值越低压缩越激进，但可能导致细小字形模糊。请使用具有代表性的样本进行测试。

### 如何处理其他图像格式（TIFF、BMP）？
将扩展名添加到过滤 lambda 中：

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

相同的预处理流水线适用于大多数光栅格式。

### 能保留原始彩色图像而不是二值化吗？
如果下游分析需要保留颜色，可在预处理构建器中将 `.addBinarize()` 替换为 `.addGrayscale()`。

---

## 生产级批量 OCR 的专业技巧

- **内存管理**：复用单个 `OcrEngine` 实例（如示例所示），避免为每张图像创建/销毁对象的开销。
- **错误处理**：将每文件的处理块包装在 `try/catch` 中，记录失败但不中止整个批次。
- **日志记录**：使用专业日志框架（SLF4J、Log4j）代替 `System.out.println`，以实现可扩展的解决方案。
- **并行化**：对于超大文件夹，可考虑使用并行流处理子目录，但需留意 GPU 争用情况。
- **安全性**：将许可证文件存放在仓库外，并通过文件系统权限进行保护。

---

## 结论

我们已经演示了如何在执行 **批量 OCR 转 PDF** 转换的同时 **压缩 PDF 图像**，实现 **将 PNG 转换为 PDF**、**识别文本 JPG**，并使用强大的 **OCR 图像预处理** 流程。完整的 Java 程序是自包含的，可在任何现代 JDK 上运行，生成轻量的可搜索 PDF，适合归档或后续分析。

接下来可以做什么？尝试不同的预处理参数，使用除英语之外的 OCR 语言，或将工作流集成到监控目录并实时处理文件的 Spring Boot 微服务中。许可证加载、引擎配置、预处理和 PDF 压缩这些核心概念保持不变，为任何基于 OCR 的项目提供坚实基础。

有问题或想分享自己的改进？在下方留言，祝编码愉快！

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方案。每个资源都提供完整可运行的代码示例和逐步解释。

- [识别 PDF 文本 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [使用 Aspose OCR 识别文本图像 – 完整 Java OCR 教程](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [使用 Aspose.OCR BufferedImage 将图像转换为文本（Java）](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}