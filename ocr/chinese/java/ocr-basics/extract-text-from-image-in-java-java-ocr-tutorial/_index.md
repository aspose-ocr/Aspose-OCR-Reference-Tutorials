---
category: general
date: 2026-03-07
description: 使用 Java OCR 从图像中提取文本。学习如何加载图像进行 OCR、配置语言，并在几分钟内完成完整的 Java OCR 教程。
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: zh
og_description: 使用 Java OCR 从图像中提取文本。本教程展示如何加载图像进行 OCR、配置语言，并一步步运行 Java OCR 教程。
og_title: 在 Java 中从图像提取文本 – 完整 OCR 指南
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中从图像提取文本 – Java OCR 教程
url: /zh/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中从图像提取文本 – 完整 OCR 指南

是否曾需要**从图像中提取文本**却不知从何入手？你并不孤单——开发者在将扫描的标志、收据或手写笔记转换为可搜索字符串时经常碰壁。

好消息是？只需几分钟，你就可以拥有一个能够读取卡纳达语、英语或任何受支持语言的 OCR 流程。在本教程中，我们将**加载图像用于 OCR**、配置引擎，并演示一个**Java OCR 教程**，你可以直接复制粘贴并立即运行。

## 本指南涵盖内容

我们先列出所需工具，然后直接进入**逐步**实现。完成后，你将能够：

* 将图像文件加载到 Java 的 `ImageInputStream` 中。
* 配置 OCR 引擎以识别特定语言（本例中为卡纳达语）。
* 运行识别过程并打印提取的文本。
* 调整设置以提升准确率并处理常见陷阱。

无需外部文档——所有内容都在这里。  

**前置条件**：Java 17 或更高版本、Maven 或 Gradle 等构建工具，以及提供 `OcrEngine` 类的 OCR 库（例如假设的 *SimpleOCR* SDK）。如果使用 Maven，请在后文添加依赖。

---

## 第 1 步 – 设置项目并添加 OCR 库

在编写任何代码之前，确保你的项目能够引用 OCR 类。使用 Maven 时，将以下代码片段放入 `pom.xml`：

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

如果你更喜欢 Gradle，等价写法是：

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **专业提示：** 保持库版本为最新；新版本通常会带来语言模型的改进，从而提升准确率。

依赖解析完成后，刷新 IDE，即可开始编码。

## 第 2 步 – 导入所需类

下面是示例所需的完整导入列表。我们刻意保持最小，以便你清晰了解每个类的作用。

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **为什么需要这些导入？** `OcrEngine` 和 `OcrResult` 是 OCR 过程的核心，而 `ImageInputStream` 抽象了文件读取的样板代码。使用 `java.nio.file.Paths` 可以让代码跨平台。

## 第 3 步 – 为 OCR 加载图像

接下来是常让人卡住的环节：向引擎提供正确的图像格式。OCR SDK 需要一个 `ImageInputStream`，你可以从磁盘上的任意文件获取它。

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **边缘情况：** 如果图像损坏或为不受支持的格式（例如 GIF），构造函数会抛出 `IOException`。请将调用包装在 try‑catch 中，或事先验证文件。

## 第 4 步 – 配置引擎识别特定语言

大多数 OCR 引擎都支持多语言。为提升准确率，你应明确告诉引擎要识别的语言。本例使用语言代码 `"kn"` 表示卡纳达语。

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **为何要设置语言？** 限定字符集可以减少误报，尤其是在字符形状相似的脚本中。

如果需要切换语言，只需更改代码字符串——无需其他修改。

## 第 5 步 – 运行 OCR 过程并提取文本

图像已加载、引擎已配置后，实际识别只需一次方法调用。返回的结果对象提供纯文本，必要时还能获取置信度分数。

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **常见问题：** *如果 OCR 返回空字符串怎么办？*  
> 通常意味着图像质量太差（模糊、对比度低）或语言设置不正确。尝试对图像进行预处理（提升对比度、二值化）或再次确认语言代码。

## 第 6 步 – 显示结果

最后，将输出打印到控制台。在真实项目中，你可能会将其存入数据库或写入搜索索引。

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### 预期输出

如果源图像包含卡纳达语短语 “ಕರ್ನಾಟಕ” (Karnataka)，控制台应显示：

```
Extracted text:
ಕರ್ನಾಟಕ
```

就这样，一个完整的 **在 Java 中使用 OCR** 工作流已经搭建完毕，你可以将其适配到任何语言或图像来源。

---

## 完整可运行示例

下面是整个程序，直接编译即可。将 `YOUR_DIRECTORY` 替换为实际的图像文件路径。

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **提示：** 在生产代码中，考虑在多张图像之间复用同一个 `OcrEngine` 实例；频繁创建会带来性能开销。

---

## 常见问题与边缘案例

### 如何提升噪声照片的准确率？
- **预处理** 图像：转为灰度、使用中值滤波或提升对比度。
- **调整分辨率** 至至少 300 DPI；大多数 OCR 引擎期望此分辨率。
- **设置白名单**（whitelist）字符，如果你只期待特定输出（例如仅数字）。

### 这套方法能用于 PDF 吗？
可以。使用 PDFBox 或 iText 将每页导出为图像，然后将这些图像喂入相同的管道。代码保持不变，仅图像来源不同。

### 如果一张图像中包含多种语言怎么办？
大多数 SDK 支持传入逗号分隔的列表，如 `"en,kn"`。引擎会尝试匹配任意提供的脚本。

### 能获取置信度分数吗？
`OcrResult` 通常提供 `getConfidence()` 方法，返回每行 0 到 1 之间的浮点数。可利用它过滤低置信度结果。

---

## 后续步骤

现在你已经能够**使用 Java 从图像提取文本**，可以进一步探索：

* **批量处理** – 循环遍历文件夹中的图像并将结果写入 CSV。
* **与 Apache Tika 集成** – 将 OCR 与文档解析结合，构建统一的搜索索引。
* **服务器端 API** – 通过 REST 接口暴露 OCR 逻辑（Spring Boot 可轻松实现）。
* **替代库** – 如果需要开源方案，可尝试使用 `tess4j` 调用 Tesseract。

这些主题都基于本 **java ocr 教程** 的核心概念，欢迎实验并扩展代码。

---

## 结论

我们完整演示了一个 Java 示例，**从图像中提取文本**，展示了如何**加载图像用于 OCR**、配置语言设置，以及**在 Java 中使用 OCR** 获取可读字符串。该代码片段自包含、错误处理得当，且可轻松嵌入任何 Java 项目。  

快去试一试，调整语言代码，马上把扫描文档转化为可搜索的数据，轻松无压力。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}