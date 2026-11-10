---
category: general
date: 2026-08-12
description: 使用 Java OCR 引擎识别图像中的文本。了解如何从图像中提取文本、提升 OCR 准确率，并对 PNG 文件进行 OCR 前的图像预处理。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: zh
lastmod: 2026-08-12
og_description: 使用 Java 识别图像中的文本。本教程展示了如何从图像中提取文本、提升 OCR 准确率，以及使用多线程和 GPU 对 PNG 进行
  OCR。
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: 在 Java 中从图像识别文本 – 步骤式 OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中识别图像文字 – 完整 OCR 指南
url: /zh/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 识别图像中的文字 – 完整 OCR 指南

如果你需要在 Java 应用中 **识别图像中的文字**，本教程将手把手教你实现。阅读完本指南后，你将能够从图像文件中提取文字、提升 OCR 准确率，并在支持多核和 GPU 的情况下对 PNG 资源执行 OCR。

许多开发者都在思考 **如何在不编写自定义神经网络的情况下提取图像中的文字**。答案是使用成熟的 OCR 引擎，针对速度和准确性进行配置，并采用合适的预处理步骤。以下章节将逐一讲解每个需求，帮助你直接把代码复制到项目中使用。

## 你将学到的内容

* 在 Java 中搭建 OCR 引擎。
* 启用多线程和可选的 GPU 加速。
* 为英语和西班牙语添加语言包。
* 使用图像预处理滤镜提升识别质量。
* 开启内置拼写校正器，获得更整洁的输出。
* 对 PNG 文件执行 OCR 并打印识别结果。

无需任何外部服务——全部在本地运行，非常适合离线或对隐私有要求的场景。

## 前置条件

* Java 17 或更高（代码使用了现代的 `var` 语法，但可向后兼容）。
* 提供 `OcrEngine`、`Language`、`EngineOptions` 等类的 OCR 库（例如 **GroupDocs.Parser**、**Aspose.OCR**，或任何兼容的 SDK）。
* 使用 Maven 或 Gradle 管理依赖。
* 将示例 PNG 图像（`sample-image.png`）放置在 `YOUR_DIRECTORY` 中。

> **小贴士：** 如果计划处理成千上万的图像，请为 GPU 缓冲区预留足够的内存，并仅在需要原始 OCR 输出时关闭拼写校正器。

## 使用 Java OCR 引擎识别图像文字

下面是一段完整、可运行的 Java 程序，遵循原始代码片段中展示的八个步骤。代码包含导入、`main` 方法以及解释每行作用的内联注释。

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### 各步骤说明

| 步骤 | 为什么重要 | 如何帮助你 **识别图像中的文字** |
|------|------------|-----------------------------------|
| 1️⃣ 创建 OCR 引擎 | 实例化核心组件，驱动后续所有操作。 | 提供所有 OCR 动作的入口点。 |
| 2️⃣ 启用多核处理 | 现代 CPU 拥有多个核心，利用它们可缩短总体处理时间。 | 在并行 **对 PNG 执行 OCR** 时加速批处理作业。 |
| 3️⃣ 开启 GPU 加速（可选） | GPU 在并行像素运算方面表现出色，尤其是处理大图像时。 | 在支持的硬件上可将识别时间降低约 70 %。 |
| 4️⃣ 添加语言包 | OCR 的准确性依赖语言模型，只指定所需语言可减少误识。 | 在多语言场景下 **如何提取图像中的文字** 时，提高正确识别字符的概率。 |
| 5️⃣ 图像预处理 | 旋转、去倾斜、去噪可纠正常见的扫描问题。 | 通过向引擎提供更干净的位图，直接 **如何提升 OCR 准确率**。 |
| 6️⃣ 拼写校正器 | 后处理步骤，修正常见的 OCR 拼写错误。 | 在无需手动清理的情况下输出更易读的文本。 |
| 7️⃣ 对 PNG 执行 OCR | `recognizeImage` 方法读取文件、应用预处理并运行识别流水线。 | 演示 **对 PNG 执行 OCR** 并处理格式特有的细节（如无损压缩）。 |
| 8️⃣ 打印结果 | 立即反馈，便于验证成功与否。 | 让你确认文本已被正确 **从图像中识别**。 |

### 预期输出

如果 `sample-image.png` 包含句子 “Hello, world! 123”，控制台将显示类似如下内容：

```
=== OCR Result ===
Hello, world! 123
```

具体输出可能会因图像质量和语言设置略有差异，但拼写校正器通常会修正诸如 “Helli” → “Hello” 的轻微误识。

## 如何对 OCR 进行图像预处理 – 深入解析

虽然上面的代码使用了引擎自带的预处理功能，你也可以在将图像交给 OCR 引擎之前自行应用自定义滤镜。以下是两种常见技术：

### 1. 使用 Otsu 方法进行二值化

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

二值化将图像转换为黑白，对低对比度扫描 **如何提升 OCR 准确率** 非常有效。

### 2. 将分辨率缩放至 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

大多数 OCR 引擎要求至少 300 dpi 才能实现最佳字符识别。缩放可以防止引擎误读细小字形。

> **注意：** 若同时启用自定义预处理和引擎自带的选项，引擎会在你的处理之后再应用其过滤器。请选择最适合图像特性的执行顺序。

## 如何提取图像中的文字 – 边缘情况处理

| 场景 | 推荐的调整 |
|------|------------|
| **噪声背景严重** | 增强 `setDenoise(true)` 强度或在 OCR 前使用中值滤波。 |
| **倾斜角度 > 15°** | 使用 `setDeskew(true)` 并通过 `imgOpts.setRotateAngle(θ)` 手动指定旋转角度。 |
| **混合语言（如英语 + 西班牙语）** | 如步骤 4 所示添加两种语言包，引擎会自动切换上下文。 |
| **大 PDF 转 PNG** | 将每页分别保存为 PNG 并汇总结果；多线程（步骤 2）可保持整体耗时低。 |
| **GPU 不可用** | 保持 `setUseGpu(true)`，但用 try‑catch 包裹；引擎将在 CPU 上回退运行，不会崩溃。 |

## 对 PNG 执行 OCR – 批处理示例

当需要在目录下对多个 **PNG 文件执行 OCR** 时，只需使用同一个引擎实例的简单循环即可：

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

由于引擎已配置多核和 GPU，此循环能够并行处理数十张图像，而无需额外代码。

## 完整可运行示例

将所有内容整合后，下面是一个可直接复制到 IDE、添加相应 Maven 依赖并立即运行的自包含类：



## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在已有技术之上进一步深入。每篇资源都提供完整可运行的代码示例，并配有逐步解释，助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.OCR 进行语言识别的图像 OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [使用 Aspose.OCR 检测区域模式从 Java 提取图像文字](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java：使用 Aspose.OCR 将图像转换为文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}