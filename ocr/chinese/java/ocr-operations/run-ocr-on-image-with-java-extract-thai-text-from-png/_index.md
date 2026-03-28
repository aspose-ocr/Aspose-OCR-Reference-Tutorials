---
category: general
date: 2026-03-28
description: 在 Java 中使用 Aspose OCR 对图像进行 OCR，将图像转换为文本，快速可靠地从 PNG 中提取泰文。
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: zh
og_description: 使用 Java 和 Aspose OCR 对图像进行 OCR。了解如何将图像转换为文本、从 PNG 中提取泰文文本，并处理常见问题。
og_title: 使用 Java 对图像进行 OCR – 快速提取泰文文本
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 使用 Java 对图像进行 OCR – 从 PNG 中提取泰文文本
url: /zh/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中运行图像 OCR – 完整教程

是否曾想过直接在 Java 代码中 **run OCR on image** 文件？也许你手头有一堆泰语收据、扫描文档或截图，需要提取文字而不想手动输入。这是一个常见的痛点，尤其当源文件是 PNG 且语言为非拉丁字符时。

在本指南中，我们将展示如何使用 Aspose OCR 库 **run OCR on image**，将图片转换为纯文本，并可靠地提取泰文字符。阅读完本教程后，你将能够 **convert image to text**、**extract text from PNG**，甚至只需几行代码就 **recognize Thai text**。

## 本教程涵盖内容

* 在 Maven/Gradle 项目中设置 Aspose OCR 依赖。  
* 初始化 `OcrEngine` 并为泰语进行配置。  
* 对 PNG 文件运行 OCR 并处理可能的错误。  
* 将结果打印到控制台并验证输出。  

无需任何 Aspose 经验——只需要一个基本的 Java IDE 和一张想要处理的图片。

## 前置条件

* 已安装 Java 8 或更高版本（该库同样支持 Java 11+）。  
* 构建工具 – Maven 或 Gradle（我们将展示 Maven 示例）。  
* Aspose OCR 许可证（免费试用可用于测试，但许可证可去除评估限制）。  
* 包含泰文的 PNG，例如放在项目 resources 文件夹下的 `input.png`。

---

## 步骤 1：将 Aspose OCR 添加到项目中

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **专业提示：** 请保持库版本与官方 Aspose 发布说明同步；新版会加入语言包和性能改进。

依赖解析完成后，IDE 应自动导入所需类。

## 步骤 2：初始化 OCR 引擎

引擎是整个过程的核心——可以把它看作分析像素模式的“大脑”。我们还会告诉它只关注泰文字符。

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

为什么要显式设置语言？因为指定 `"th"` 可以缩小字符集范围，从而加快识别速度并减少相似字形的误读。

## 步骤 3：对 PNG 文件运行 OCR

现在我们把想要解码的图像喂给引擎。`recognizeImage` 方法返回一个 `OcrResult` 对象，其中包含提取的字符串和置信度分数。

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

如果文件未找到，Aspose 会抛出 `FileNotFoundException`。在生产代码中建议使用 `try‑catch` 包裹调用，但本教程保持简洁直接。

## 步骤 4：输出识别的文本

最后，我们打印结果。`getText()` 方法返回一个普通的 Java `String`，你可以将其保存、通过网络发送或写入文件。

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

运行程序后，你应该会看到类似如下的输出：

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

如果输出出现乱码，请再次确认源 PNG 分辨率足够高（至少 300 dpi），并且语言代码 `"th"` 与目标语言匹配。

### 完整代码清单

下面是完整的、可直接运行的 Java 文件。复制粘贴到 IDE 中，必要时替换图片路径，然后点击 **Run**。

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![run OCR on image example](image.png "run OCR on image example – Java code extracting Thai text from PNG")

## 步骤 5：常见变体与边缘情况

### 将图像转换为其他格式的文本

如果需要 **convert image to text** 的文件是 JPEG 或 BMP，只需在 `imagePath` 中更改文件扩展名。Aspose OCR 支持 PNG、JPEG、BMP、TIFF，甚至 PDF 页面。

### 从 PNG 中提取多语言文本

你可以让引擎一次检测多种语言：

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

结果将包含泰文和英文字符的混合，对于双语收据非常实用。

### 处理低质量图像

对于模糊的扫描件，考虑开启预处理：

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

这会触发内置的去噪和对比度增强算法，提升 **extract text from PNG** 步骤的效果。

### 许可证激活

未激活许可证时，Aspose 会在输出的第 100 页后插入水印行。请尽早激活许可证：

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

将 `.lic` 文件放在 JAR 旁边或通过绝对路径引用。

## 常见问题

**Q: 这在 Linux 上能运行吗？**  
A: 完全可以。Aspose OCR 纯 Java 实现，任何支持 JVM 的操作系统都可以。

**Q: 如果 PNG 包含手写泰文怎么办？**  
A: 手写识别能力有限，可能需要专门的神经网络模型。Aspose OCR 在印刷体文本上表现更佳。

**Q: 能否批量处理文件夹中的图像？**  
A: 可以将 `recognizeImage` 调用放在 `Files.list(Paths.get("folder"))` 的循环中。记得复用同一个 `OcrEngine` 实例以提升性能。

## 结论

我们已经完整演示了如何在 Java 中 **run OCR on image** 文件，特别是从 PNG 中 **extract Thai text**。通过初始化 `OcrEngine`、设置语言、调用 `recognizeImage` 并打印结果，你现在拥有了一种可靠的 **convert image to text** 方法，无需依赖第三方服务。

接下来你可以：

* 大批量 **extract text from PNG** 文件用于数据挖掘项目。  
* 将 OCR 输出与翻译 API 结合，获取英文对应。  
* 通过更换语言代码，探索 Aspose 支持的其他语言，如中文或阿拉伯文。

尝试使用自己的图片吧——调整预处理设置，实验不同文件格式，感受该方案在真实工作流中的稳健性。

祝编码愉快，愿你的 OCR 流程始终精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}