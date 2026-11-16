---
category: general
date: 2026-03-07
description: 使用 Java 对图像进行 OCR。了解如何识别 PNG 中的文本、从收据中提取文本，以及使用完整的 Java OCR 示例加载图像进行
  OCR。
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: zh
og_description: 使用 Java 对图像进行 OCR。本指南展示了如何从 PNG 识别文本、从收据提取文本，以及使用完整的 Java OCR 示例加载图像进行
  OCR。
og_title: 使用 Java 对图像进行 OCR – GPU 加速文本提取
tags:
- OCR
- Java
- GPU
- Image Processing
title: 使用 Java 对图像进行 OCR – GPU 加速的文本提取
url: /zh/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 GPU 加速进行图像 OCR

是否曾需要 **对图像文件进行 OCR**，却不知从何入手？你并不孤单——许多开发者在第一次尝试从扫描的收据或 PNG 截图中提取文字时都会遇到同样的难题。

在本教程中，我们将带你完成一个 **完整的 Java OCR 示例**，它不仅能 **识别 PNG 文件中的文字**，还能展示如何 **从收据图像中提取文本**，并利用 GPU 加速提升速度。完成后，你将拥有一个可直接运行的程序，能够加载图像进行 OCR、处理并打印纯文本结果。

## 你将学到

- 如何使用简易的 `ImageInputStream` **加载 OCR 图像**。
- 启用 GPU 支持，让引擎在现代硬件上运行更快。
- **从 PNG 识别文字** 并从收据中提取有用字符串的完整步骤。
- 常见陷阱（例如错误的 GPU 设备 ID）以及最佳实践建议。
- 一个完整、可运行的代码片段，直接复制粘贴到 IDE 中使用。

**前置条件**

- Java 17 或更高（代码使用 `var` 关键字简化，如果你使用 Java 8，可改为显式类型）。
- 提供 `OcrEngine`、`ImageInputStream` 和 `OcrResult` 类的 OCR 库（例如虚构的 *FastOCR* SDK；请替换为你实际使用的库）。
- 如需性能提升，请准备一台支持 GPU 的机器（可选，但推荐）。

---

## 步骤 1：运行图像 OCR – 启用 GPU 加速

首先需要创建 OCR 引擎并告诉它使用 GPU。这一步至关重要，因为如果没有 GPU 支持，引擎会回退到 CPU，处理高分辨率收据时会明显变慢。

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**为什么重要：**  
GPU 加速会把 OCR 引擎进行的繁重矩阵计算卸载到显卡上。如果你有多块 GPU，可以通过修改 `setGpuDeviceId` 的值来选择内存最大的那一块。忘记启用 GPU 是导致 “我的 OCR 为什么这么慢？” 的常见原因。

> **小技巧：** 如果机器没有兼容的 GPU，`setUseGpu(true)` 调用会被自动忽略——不会崩溃，只是处理速度变慢。

---

## 步骤 2：加载 OCR 图像

引擎准备好后，需要给它喂入一张图像。下面的示例展示了如何加载磁盘上的 PNG 收据。你可以将路径替换为 OCR 库支持的任何图像格式。

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**边缘情况：**  
如果文件不存在或路径错误，`ImageInputStream` 会抛出 `IOException`。请将调用包装在 try‑catch 块中，并记录有帮助的错误信息：

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## 步骤 3：从 PNG 识别文字

图像加载完成后，OCR 引擎即可开始工作。这一步实际上 **从 PNG（或其他受支持格式）中识别文字**，并返回一个 `OcrResult` 对象。

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**内部原理是什么？**  
引擎会先进行预处理（去倾斜、二值化），随后运行神经网络检测字符，最后将字符组装成文本行。由于我们之前已经启用了 GPU，这些神经网络计算会在显卡上完成，从而节省数秒的总运行时间。

---

## 步骤 4：从收据中提取文字

识别完成后，通常只需要原始文本。`OcrResult` 类一般提供 `getText()` 方法，返回单个 `String`。随后你可以对其进行后处理（例如使用正则表达式提取总额、日期等）。

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**典型的收据输出示例：**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

现在，你可以将该字符串传入自定义解析器，提取总金额、商品明细或税务信息。

---

## 步骤 5：完整的 Java OCR 示例 – 可直接运行

将上述所有代码整合后，得到 **完整的 Java OCR 示例**，可以直接放入 `Main.java` 文件中。确保 OCR 库已加入 classpath。

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**预期的控制台输出**（假设使用上面的示例收据）：

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

如果输出出现乱码，请检查图像是否清晰（高 DPI），并确认 OCR 语言包与收据语言匹配。

---

## 常见问题与注意事项

| Question | Answer |
|----------|--------|
| *What if my GPU isn’t detected?* | The engine will fall back to CPU automatically. Verify drivers and that the `setGpuDeviceId` matches an existing device (`nvidia-smi` on Linux can help). |
| *Can I process JPEG or TIFF files?* | Yes—just change the file extension in `ImageInputStream`. The OCR library usually auto‑detects the format. |
| *Is there a way to batch‑process many receipts?* | Wrap the recognition code in a loop and reuse the same `OcrEngine` instance; re‑initializing per image wastes GPU memory. |
| *How do I improve accuracy on low‑contrast receipts?* | Pre‑process the image (increase contrast, convert to grayscale) before feeding it to the OCR engine. Some libraries expose a `preprocess` API. |

---

## 结论

现在，你已经掌握了 **在 Java 中对图像文件进行 OCR** 的完整流程，从加载图片到从收据中提取干净文本。本文涵盖了 **从 PNG 识别文字**、**从收据提取文本**，并提供了一个可直接移植到任意项目的 **java OCR 示例**。

接下来可以尝试关闭 GPU 标志，比较性能差异；实验不同的图像分辨率；或集成基于正则的解析器自动提取金额。如果想进一步深入，可研究 **OCR 后处理**、**语言模型纠错** 或 **批处理流水线** 等高级主题。

祝编码愉快，愿你的收据永远可读！  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}