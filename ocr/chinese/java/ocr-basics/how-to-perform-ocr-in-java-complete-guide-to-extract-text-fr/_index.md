---
category: general
date: 2026-06-06
description: 如何在 Java 中实现 OCR —— 使用简易代码示例快速从图像提取文本、将图像转换为文字，并读取 JPG 中的文本。
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: zh
og_description: 如何在 Java 中执行 OCR —— 学习如何从图像中提取文本，将图像转换为文本，并使用可直接运行的示例读取 JPG 中的文本。
og_title: 如何在 Java 中进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 如何在 Java 中进行 OCR – 提取图像文字的完整指南
url: /zh/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中执行 OCR – 提取图像文本的完整指南

是否曾好奇 **如何在手机拍摄的图片上执行 OCR**？你并不孤单。无论是构建收据扫描应用，还是仅仅需要从扫描的 PDF 中提取文本，**如何在 Java 中执行 OCR** 都是一项回报快速的技能。在本教程中，我们将通过一个实用示例，演示 **从图像文件中提取文本**、**将图像转换为文本**，甚至展示如何仅用几行代码 **从 jpg 中读取文本**。

> *Pro tip:* 同样的方法适用于 PNG、BMP 或 OCR 引擎支持的任何格式——只需更换文件名即可。

## 如何在 Java 中执行 OCR – 概览

光学字符识别（OCR）是一种将字母图片转换为实际、可搜索文本的技术。在 Java 生态系统中，有多个库——Tesseract、Asprise 以及商业 SDK——都提供了类似的工作流：加载图像、指定语言、运行识别、获取结果。下面我们使用一个通用的 `OcrEngine` 类来保持示例简洁，但你可以用任何遵循相同模式的具体实现来替换它。

### 你将学到的内容

- 安装 OCR 库（是的，**ocr in java** 比想象中更简单）。
- 创建并配置 OCR 引擎实例。
- 加载 JPG（或任意图像）并设置语言。
- 处理图像并 **从图像文件中提取文本**。
- 将识别出的字符串打印到控制台。

完成后，你将拥有一个可直接放入任何项目并立即运行的独立 Java 程序。

![how to perform OCR example](ocr-example.png "Java 中执行 OCR 的示意图")

## 第一步 – 安装并导入 OCR 库（ocr in java）

在编写任何 Java 代码之前，你需要一个真正负责重活的库。如果使用 Maven，请添加如下依赖（将 `com.example.ocr` 替换为所选 SDK 的真实 group ID）：

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

如果更喜欢 Gradle：

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

将 JAR 放入 classpath 后，导入所需的类：

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **为什么这很重要：** 导入正确的类可以避免 “cannot find symbol” 错误，让你的 IDE 高兴——在尝试 **convert image to text** 时，最让人沮丧的莫过于缺少导入。

## 第二步 – 创建 OCR 引擎实例（how to perform OCR）

库准备就绪后，启动引擎。可以把引擎想象成会观察像素并猜测字母的大脑。

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

创建引擎的成本通常很低；大多数 SDK 会惰性分配内部缓冲区，因此在处理批量图像时可以安全地复用同一个实例。

## 第三步 – 加载图像并设置语言（extract text from image）

接下来要给引擎提供读取的对象。这里我们从磁盘加载 JPEG，并告诉 OCR 引擎文本使用蒙古语（ISO 639‑2 代码 “mon”）。你可以根据实际需求更改路径或语言代码。

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **旁注：** 如果不设置语言，引擎默认使用英语，这在文本实际为西里尔字母或其他脚本时会大幅降低准确率。能够时请始终指定正确的语言。

## 第四步 – 处理图像并获取结果（convert image to text）

在图像和语言准备好后，调用引擎执行魔法。`process()` 方法运行 OCR 算法并返回一个 `OcrResult` 对象，包含识别的字符串和置信度分数。

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

在幕后，引擎可能会进行预处理——去倾斜、二值化、降噪——因此你无需自行编写这些步骤。这也是大多数现代 OCR 库在 **convert image to text** 任务中如此受欢迎的原因。

## 第五步 – 输出提取的文本（read text from jpg）

最后，从结果中取出纯文本并进行有用的处理。演示中我们仅将其打印到控制台，但你也可以写入文件、写入搜索索引，或传递给其他服务。

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

仅此一行就证明你已经成功 **read text from jpg**（或任何受支持的格式）。如果输出出现乱码，请再次检查语言代码和图像质量。

## 完整可运行示例（所有步骤合并）

下面是一段完整、可直接运行的 Java 类，整合了所有步骤。将其复制到名为 `OcrDemo.java` 的文件中，调整图像路径和语言后，执行 `javac OcrDemo.java && java OcrDemo`。

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 预期输出

如果 `input.jpg` 包含蒙古语短句 “Сайн байна уу?”，控制台将显示：

```
=== Recognized Text ===
Сайн байна уу?
```

如果图像模糊或语言代码错误，你会看到乱码或空字符串——这些常见陷阱将在下文中讨论。

## 常见陷阱及解决方案

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 西里尔字符乱码 | 语言代码错误（默认使用英语） | 设置 `ocrEngine.getSettings().setLanguage("mon")` 或相应的代码。 |
| 完全没有输出 | 图像路径错误或文件不可读 | 核实路径，确保文件存在且进程拥有读取权限。 |
| 准确率低于 70 % | 图像对比度低或旋转 | 预处理图像：提升对比度、去倾斜或转换为灰度后再送入引擎。 |
| 大型 PDF 导致 `OutOfMemoryError` | 一次加载过多高分辨率页面 | 按页逐个处理，或在 OCR 前对图像进行降采样。 |

### Pro Tip: 批量处理

如果需要 **extract text from image** 文件的批量操作，可将核心逻辑包装在循环中：

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

该代码片段演示了如何轻松从单个 JPG 扩展到整个文件夹的扫描。

## 进一步探索 – 接下来可以做什么？

- **语言包：** 大多数 OCR SDK 允许下载额外的语言数据文件。添加新语言包后，你可以 **convert image to text** 任意语言的文本，而不仅限于英语和蒙古语。
- **PDF OCR：** 将本代码与 Apache PDFBox 结合使用，可对 PDF 文档进行全文检索。

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在已有技术基础上进一步提升。每篇资源都提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}