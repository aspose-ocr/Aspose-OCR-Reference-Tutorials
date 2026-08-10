---
category: general
date: 2026-02-19
description: 使用 Java OCR 从图像中提取文本。学习一个 Java OCR 示例，该示例加载图像进行 OCR，并在几个步骤内从发票文件中提取文本。
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: zh
og_description: 使用 Java OCR 从图像中提取文本。本指南展示了如何加载图像进行 OCR，并通过一个简单的 Java OCR 示例从发票中提取文本。
og_title: 使用 Java 从图像提取文本 – 完整 OCR 示例
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 在 Java 中从图像提取文本 – 完整 OCR 示例
url: /zh/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中从图像提取文本 – 完整 OCR 示例

是否曾经需要**从图像中提取文本**但不确定该选哪种库？你并不孤单——许多开发者在自动化发票处理或构建可搜索档案时都会遇到这个难题。好消息是，只需几行 Java 代码，你就可以加载用于 OCR 的图像，定义感兴趣区域（ROI），并提取所需的精确文本。  

在本教程中，我们将演示一个**java ocr example**，展示如何**load image for OCR**，设置 ROI，并使用 Aspose.OCR **extract text from invoice** 文件。完成后，你将拥有一个可直接放入任何 Java 项目的可运行程序。

## 你将学到

- 如何创建 `OcrEngine` 实例以及它为何重要。
- 使用 Aspose 的 `ImageStream` 正确的**load image for OCR** 方法。
- 设置**region of interest (ROI)**，只处理图像中包含发票金额的部分。
- 提取识别的文本并将其打印到控制台。
- 常见陷阱（例如，矩形坐标错误）以及快速解决方案。

**先决条件**

- 已安装 Java 8 或更高版本。
- 使用 Maven 或 Gradle 拉取 Aspose.OCR 库（`com.aspose:aspose-ocr`）。
- 将示例发票图像（`invoice.png`）放置在已知目录中。

准备好了吗？太好了——让我们开始吧。

![使用 Java OCR 从图像提取文本](/images/extract-text-from-image-java.png "提取文本示例")

## 从图像提取文本 – 步骤式 Java OCR 示例

下面是完整的源代码。请随意将其复制粘贴到 `RoiOcrExample.java` 中并直接运行。

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### 为什么每一步都很重要

1. **Creating the OCR engine** – 没有引擎就没有图像处理的上下文。如果需要多语言支持，该对象还可以让你稍后调整语言包。  
2. **Loading the image** – `ImageStream.fromFile` 抽象化了文件格式，确保引擎正确读取字节。如果跳过此步骤，你会收到 `NullPointerException`。  
3. **Setting the ROI** – 处理整页可能会浪费资源。通过将矩形缩小到发票总额区域，你可以加快识别速度并减少噪声。  
4. **Calling `recognize()`** – 这就是魔法发生的地方。该方法在 ROI 上运行 OCR 算法并生成结果对象。  
5. **Printing the output** – 在实际项目中，你可能会将文本存入数据库，但 `System.out.println` 对于快速演示来说非常合适。  

## 加载用于 OCR 的图像

如果你在想路径是需要绝对路径还是相对路径，答案是两者都可以——只要确保 Java 进程能够读取该文件即可。在 Windows 上，反斜杠必须转义（`C:\\images\\invoice.png`），或者也可以使用正斜杠（`C:/images/invoice.png`）。  

**Pro tip:** 如果在循环中处理大量发票，请复用同一个 `OcrEngine` 实例；它会缓存内部资源并提升吞吐量。

## 定义感兴趣区域（ROI）

选择合适的矩形可能需要反复尝试。一个方便的方法是使用任意图形编辑器（如 GIMP 或 Paint.NET）打开图像并将鼠标悬停在目标区域——你会在状态栏看到 X/Y 坐标值。  

边缘情况：某些发票布局多变。在这种情况下，你可以先对整张图像进行快速预扫描，使用正则表达式定位诸如 “Total:” 的关键字，然后动态调整 ROI。

## 执行 OCR 并获取文本

`recognize()` 调用是同步的——你的线程会阻塞直至引擎完成。对于大批量处理，你可能想启动线程池并并行处理图像。只需记住每个线程都需要自己的 `OcrEngine` 实例；它们不是线程安全的。

## 运行并验证输出

编译并运行：

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

你应该会看到类似如下的输出：

```
ROI text: $1,254.00
```

如果输出乱码，请再次检查 ROI 坐标并确保图像质量足够高（300 dpi 或更高效果最佳）。  

### 常见陷阱及解决方法

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| 空字符串 | ROI 超出图像边界 | 验证矩形值是否在图像尺寸范围内 |
| 单词拼写错误 | 分辨率低 | 使用更高分辨率的源图像或进行图像预处理（例如二值化） |
| `java.lang.NoClassDefFoundError` | 类路径缺少 Aspose JAR | 将 `aspose-ocr.jar` 添加到 `-cp`，或使用 Maven/Gradle 进行依赖管理 |

## 结论

现在你已经了解如何在 Java 中使用简洁的 **java ocr example** **extract text from image**。通过正确加载图像、定义聚焦的 ROI 并调用 `recognize()`，你可以可靠地 **extract text from invoice** 文件，并将这些数据输送到下游系统。  

接下来做什么？尝试将 ROI 替换为不同的字段（日期、供应商名称），尝试使用语言包处理多语言发票，或将 OCR 步骤集成到 Spring Boot 微服务中。同样的模式也适用于收据、护照或任何需要精确文本提取的文档。  

如果你对该方案的扩展或处理噪声扫描有疑问，欢迎在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}