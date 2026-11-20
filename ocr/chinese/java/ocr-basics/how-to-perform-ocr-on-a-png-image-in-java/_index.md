---
category: general
date: 2026-10-11
description: 学习如何在 Java 中对 PNG 图像执行 OCR，提取图像中的文本，并使用简单的 OcrEngine 示例将图像转换为文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: zh
lastmod: 2026-10-11
og_description: 如何在 Java 中对 PNG 图像执行 OCR，提取图像中的文本，并使用简洁、可直接运行的示例将图像转换为文本。
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: 在 Java 中对 PNG 图像进行 OCR 的完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: 如何在 Java 中对 PNG 图像进行 OCR
url: /zh/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中对 PNG 图像执行 OCR 的方法

如果你需要 **执行 OCR** 于图像文件，学习 **如何在 Java 中执行 OCR** 对许多自动化任务至关重要。无论是数字化收据、为扫描文档建立索引，还是构建可搜索的照片档案，**从图像中提取文本** 的能力都能节省大量手动工作时间。

本教程展示了一个完整、可运行的解决方案：加载 PNG、运行 OCR 引擎，并 **从 PNG 文件中识别文本**。你还将看到如何 **将图像转换为文本**，以及如何处理低分辨率输入或非 ASCII 字符等常见问题。

## 你将实现的目标

阅读完本指南后，你将能够：

* 使用 **load image java** 代码从磁盘读取 PNG，
* 初始化轻量级 OCR 引擎，
* **从图像中提取文本** 并将结果打印到控制台，
* 将该方案适配到其他图像格式或批量处理。

无需外部服务——只需一个开源 OCR 库（Tess4J）和 Java SE 运行时。

---

## 前置条件

* Java 17 或更高（代码在 JDK 17 下编译）。
* 用于依赖管理的 Maven 或 Gradle。
* 对命令行和你选择的 IDE 有基本了解。
* `tess4j` 库（Tesseract 的 Java 包装器）。在 Maven 中添加以下依赖：

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

如果使用 Gradle，等价写法是：

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

你还需要 Tesseract 数据文件（`.traineddata`）。从官方仓库下载英文数据包，并放置在项目根目录下名为 `tessdata` 的文件夹中。

---

## 步骤 1：在 Java 中加载图像

使用标准的 `ImageIO` 类加载 PNG 非常简单。下面的代码演示了 **load image java** 的安全、异常感知写法：

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**为什么重要：** `ImageIO.read` 会自动检测图像格式，但我们显式检查 `null`，以避免在 PNG 损坏时出现静默失败。这是 **load image java** 用于 OCR 时的最佳实践。

---

## 步骤 2：初始化 OCR 引擎

Tess4J 包装了原生的 Tesseract 二进制，提供了简洁的 Java API。以下方法创建了一个 `Tesseract` 实例，指向 `tessdata` 文件夹，并将语言设置为英文：

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**这样做的原因：** 将引擎初始化一次并在多张图像之间复用，可降低启动开销。`setOcrEngineMode` 调用选择默认模式，适用于大多数 PNG。如果遇到噪声较大的扫描件，可尝试其他模式（例如 `OEM_LSTM_ONLY`）。

---

## 步骤 3：执行 OCR 并 **从 PNG 中识别文本**

现在我们把图像加载器和 OCR 引擎结合起来。下面的方法对 `BufferedImage` 进行 OCR，并返回提取的字符串：

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**完整可运行示例**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**预期输出**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

控制台将显示引擎从 `sample.png` 中提取的精确字符。如果 PNG 只包含一个单词，输出将是该单词并换行。

---

## 步骤 4：常见变体和边缘情况

### 4.1 处理低分辨率 PNG

Tesseract 在至少 300 DPI 的图像上表现最佳。如果源 PNG 较小，请在 OCR 前先放大：

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

在调用 `extractText` 前使用 `upscale(image, 2)` 可提升准确率。

### 4.2 提取非英文文本

要 **从图像中提取文本** 包含其他语言的情况，下载相应的 `.traineddata` 文件并设置语言代码：

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 批量处理多个 PNG

如果需要在文件夹中 **从 PNG 文件中识别文本**，可以遍历目录：

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 处理 OCR 错误

常见的 OCR 错误包括把 `0`（零）误读为 `O`，或把 `1` 误读为 `l`。使用正则表达式进行后处理可以清理结果：

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## 在 Java 中实现可靠 OCR 的专业技巧

| 技巧 | 原因 |
|-----|------|
| **使用无损 PNG** | JPEG 的压缩伪影会干扰引擎。 |
| **裁剪白色边框** | 多余的空白会增加处理时间并可能导致误识别。 |
| **仅在布局未知时使用 `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`**；否则请选择特定模式（如 `PSM_SINGLE_BLOCK`）。 |
| **缓存 `ITesseract` 实例** | 减少重复初始化的开销。 |

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}