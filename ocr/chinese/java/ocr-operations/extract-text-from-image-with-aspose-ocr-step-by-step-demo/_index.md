---
category: general
date: 2026-02-14
description: 使用 Aspose OCR 从图像中提取文本。了解如何加载图像进行 OCR、从矩形区域读取文本，并在几分钟内完成此 Aspose OCR
  教程。
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: zh
og_description: 即时从图像中提取文本。本指南展示如何加载图像进行 OCR、从矩形区域读取文本，以及完成 Aspose OCR 教程。
og_title: 使用 Aspose OCR 从图像提取文本 – 快速指南
tags:
- Aspose
- OCR
- Java
title: 使用 Aspose OCR 从图像中提取文本 – 步骤演示
url: /zh/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像中提取文本 – 步骤演示

是否曾需要 **从图像中提取文本** 却不知从何入手？你并不孤单——许多开发者在首次处理收据扫描或身份证验证时都会遇到这个难题。好消息是，使用 Aspose OCR，你可以加载图像，定义文本所在的精确区域，然后在几行代码内提取字符。

在本 **aspose ocr tutorial** 中，我们将逐步演示所有必需的操作：加载用于 OCR 的图像、设置告诉引擎查找位置的矩形，最后读取提取的文本。完成后，你将拥有一个可运行的 Java 程序，能够将 ROI（感兴趣区域）文本打印到控制台——没有神秘，只是清晰可用的解决方案。

## 你需要的准备

在深入之前，请确保已具备以下基础：

| 前置条件 | 为什么重要 |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR 以 Java 库形式提供，任何现代 JDK 都可使用。 |
| **Aspose.OCR for Java**（从 Aspose 官网下载或通过 Maven 添加） | 提供 `OcrEngine`、`ImageStream` 等相关类。 |
| **图像文件**（例如 `receipt.jpg`），其中包含可打印文本 | 我们将在此文件内部的矩形区域上进行识别。 |
| **IDE 或编辑器**（IntelliJ、Eclipse、VS Code 等） | 帮助你快速编译并运行示例。 |

如果使用 Maven，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **小贴士：** 上述版本号截至 2026 年 2 月为最新。更新到最新发布版可获得错误修复和性能提升。

## 第一步 – 初始化 OCR 引擎

首先，需要创建一个 `OcrEngine` 实例。它相当于分析像素的“大脑”。

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

为什么要这样创建？Aspose 将引擎（保存配置）与图像数据分离，使你在需要时可以复用同一个引擎处理多张图像。

## 第二步 – 加载用于 OCR 的图像

接下来真正 **加载图像用于 OCR**。`ImageStream.fromFile` 辅助方法会将文件读取为 Aspose 能理解的流。

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

如果文件未找到，引擎会抛出异常，生产代码中建议使用 try‑catch 包裹。演示中我们让异常直接抛出——保持示例简洁。

## 第三步 – 定义矩形（从矩形读取文本）

这一步展示了 **从矩形读取文本** 的核心。你告诉引擎确切的查找位置，从而加快处理速度并降低误报。

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **为什么使用矩形？**  
> 大多数文档布局固定——比如收据的金额总在底部。聚焦该区域，OCR 引擎即可忽略无关图形，提高准确率。

**边缘情况：** 若矩形超出图像边界，Aspose 会静默截断，但会导致数据缺失。可以先做一次合理性检查：

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## 第四步 – 处理图像

所有准备就绪后，调用引擎执行识别。

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

`process()` 方法返回一个 `OcrResult` 对象，里面包含提取的文本、置信度分数，甚至每个单词的边界框（如需后续使用）。

## 第五步 – 输出提取的文本

最后，打印结果。实际项目中可能会将其存入数据库或传递给其他服务，但本教程只需在控制台输出即可。

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**预期输出**（假设矩形捕获了收据上的总金额）：

```
ROI text:
$12.34
```

如果 ROI 为空或图像模糊，你会看到空字符串或乱码。此时请调整矩形、提升图像质量，或启用 Aspose 的预处理选项（例如 `setAutoSkewCorrection(true)`）。

## 完整可运行示例

下面是完整的、可直接运行的程序。复制粘贴到名为 `RoiDemo.java` 的文件中，修改图像路径后执行 `javac RoiDemo.java && java RoiDemo`。

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **结果验证：** 运行后，将控制台输出与矩形内部的实际文本进行比对。若一致，即成功使用 Aspose OCR **从图像中提取文本**。

## 常见问题与技巧

### 如果需要在同一图像中处理多个 ROI，怎么办？
为每个区域创建新的 `Rectangle`，再次调用 `setRegionOfInterest`，然后重新执行 `process()`。引擎会复用相同的图像数据，保持高性能。

### Aspose 如何处理不同语言或字体？
可以通过 `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` 切换语言模型。对于非拉丁文字，需要加载相应的语言包（可在 Aspose 下载页面获取）。

### 库是否支持 PDF 输入？
支持——Aspose OCR 可以直接接受 PDF 流。只需将 `ImageStream.fromFile` 替换为 `ImageStream.fromPdfFile("doc.pdf")`，并可选指定页码。

### 如何提升低质量扫描的识别准确度？
启用预处理：

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

这些选项会在识别前清除噪点并对齐文本。

## 结论

我们已经完整演示了一个 **aspose ocr tutorial**，展示了如何使用 Java **提取图像中的文本**、**加载图像用于 OCR**，以及 **从矩形读取文本**。关键步骤包括：初始化引擎、提供图像、定义感兴趣区域、处理并最终打印结果。

接下来，你可以探索：

* **批量处理** – 循环遍历收据文件夹，将每个总额存入数据库。  
* **动态 ROI 检测** – 使用图像处理库（如 OpenCV）自动定位文本块。  
* **后处理** – 使用正则或模糊匹配清理 OCR 产生的异常字符。

尝试这些思路，调整矩形以适配自己的文档，你将拥有一个强大的文本提取流水线。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}