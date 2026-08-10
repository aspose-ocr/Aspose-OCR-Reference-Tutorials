---
category: general
date: 2026-05-06
description: 使用 Aspose OCR 在 Java 中将图像创建为可搜索的 PDF。学习将图像转换为 PDF，启用拼写纠正，并使用 OCR GPU
  以获得快速结果。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: zh
og_description: 使用 Aspose OCR 在 Java 中将图像创建为可搜索的 PDF。本指南展示了如何将图像转换为 PDF、启用拼写纠正以及使用
  OCR GPU。
og_title: 使用 Java OCR 将图像转换为可搜索的 PDF
tags:
- OCR
- Java
- PDF
title: 使用 Java OCR 将图像转换为可搜索的 PDF
url: /zh/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java OCR 从图像创建可搜索的 PDF

是否曾需要从扫描的图片**创建可搜索的 PDF**但不知从何入手？你并不孤单——大多数开发者在首次处理基于图像的 PDF 时都会遇到这个难题。幸运的是，使用 Aspose OCR for Java，你可以**将图像转换为 PDF**，将文本变为可选择的内容，甚至加入拼写校正以获得更完美的结果。

在本教程中，我们将演示一个完整、可直接运行的示例，展示如何在有 GPU 时**使用 OCR GPU**，如何高效**处理图像 OCR**，以及为何启用拼写校正对后续搜索至关重要。完成后，你将拥有一键生成可搜索 PDF 的方法，可供用户使用或用于合规存档。

> **专业提示：** 如果你的机器没有 GPU，代码会自动回退到 CPU，无需修改任何代码。

---

## 需要的环境

- **Java 8+**（代码在 JDK 8 及以上版本编译通过）
- **Aspose OCR for Java** 库（从 Aspose 官网下载最新 JAR 包）
- 一张 **输入图像**（JPEG、PNG、TIFF 等），用于转换为可搜索的 PDF
- （可选）支持 CUDA 的 **GPU**，以获得最快的识别速度

无需额外框架，无需 Maven/Gradle 魔法——只需在类路径上放置一个 JAR，即可开始。

---

## 第一步：初始化 OCR 引擎 – 过程的核心  

首先创建一个 `OcrEngine` 实例并指向源文件。该对象是工作马，负责读取图像、运行神经网络并返回文本。

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*为什么重要：* 只初始化一次并复用引擎，可避免反复加载本地库的开销——这在批量处理数十个文件时会带来显著的性能提升。

---

## 第二步：选择处理设备 – 有 GPU 时使用 OCR GPU  

如果工作站配备兼容的 GPU，可以告诉 Aspose 将繁重的计算交给它。否则引擎会自动切换到 CPU。

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*有什么好处？* GPU 加速可以为每页节省数秒，尤其是高分辨率扫描时。回退机制确保相同代码在任何环境下都能运行，这也是我们默认推荐**使用 OCR GPU**的原因。

---

## 第三步：加速扫描 – 利用所有 CPU 核心  

即使 GPU 正在忙碌，周边的预处理步骤仍可并行化。将线程数设置为可用处理器的数量，让引擎能够同时处理多个块。

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*注意：* 在四核笔记本上会启动四个线程；在十六核工作站上则可充分发挥性能。只需留意线程数增加会导致更高的内存占用。

---

## 第四步：清理图像 – 预处理过滤器  

模糊或噪声较大的扫描会产生垃圾文本。添加几种内置过滤器可显著提升准确率。

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*为什么使用这些过滤器？* `DeskewFilter` 校正文档在扫描时常出现的倾斜角度。`NoiseRemovalFilter` 去除会被误识别为字符的杂散像素。可以把它想象成给 OCR 引擎提供一张干净的纸张。

---

## 第五步：开启智能特性 – 启用拼写校正与自动语言检测  

如果要处理多语言文档，或仅希望减少错别字，请打开内置拼写检查器并让引擎自动识别语言。

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*何时有用？* 假设你的扫描件同时包含英文和西班牙文段落。自动检测功能会即时切换词典，而拼写校正会纠正如将 “0” 误读为 “O” 等错误。此步骤对于生成**可搜索的 PDF**并返回正确搜索结果至关重要。

---

## 第六步：保存结果 – 将图像转换为 PDF 并使其可搜索  

最后，让引擎生成一个 PDF，原始图像位于不可见的文字层后面。这是经典的**将图像转换为 PDF**工作流，只是生成的 PDF 现在是可搜索的。

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

输出文件 (`output-searchable.pdf`) 可在任何 PDF 查看器中打开；你将能够像操作原生 PDF 那样选择、复制和搜索文本。无需额外工具。

---

## 完整可运行示例 – 复制即用  

下面是完整程序代码，已准备好编译。将 `YOUR_DIRECTORY` 替换为存放 `input.jpg` 的文件夹路径。

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**预期输出：** 运行程序后，控制台会显示 *“Searchable PDF generated successfully.”*。在 Adobe Reader 中打开 `output-searchable.pdf`，在搜索框输入原始图像中的任意单词，即可瞬间定位到对应位置。

---

## 常见问题与边缘情况  

- **如果未检测到 GPU 会怎样？**  
  `setDeviceType(OcrDeviceType.GPU)` 调用不会抛异常，它仅指示引擎优先尝试 GPU。如果失败，引擎会静默回退到 CPU。

- **能在一次运行中处理多张图像吗？**  
  可以。将代码放入循环中，每次迭代更换文件名，并复用同一个 `OcrEngine` 实例，以保持低内存占用。

- **我的 PDF 很大——如何压缩？**  
  OCR 完成后可使用 Aspose 的 PDF 优化 API，或在将图像送入引擎前先降低分辨率（例如 `ImageStream.fromFile(...).setResolution(150)` 设为 150 DPI）。

- **需要保留原始图像分辨率以满足合规要求。**  
  `PDF_SEARCHABLE` 格式会完整保留原始位图，文字层以不可见方式叠加在上方，不会影响视觉质量。

---

## 可视化概览  

![create searchable pdf example](placeholder-image.png "create searchable pdf example")

*Alt text:* *create searchable pdf example – Java OCR 引擎将扫描的 JPG 转换为可搜索的 PDF。*

---

## 结论  

现在，你拥有一个使用 Aspose OCR for Java 将任意图像转换为**可搜索的 PDF**的**完整端到端解决方案**。通过**将图像转换为 PDF**、**启用拼写校正**以及在可能时**使用 OCR GPU**，即可获得快速、准确且可搜索的结果，跨平台通用。

接下来可以尝试：

- **不同的输出格式**（`PDF`、`DOCX`、`HTML`），观察文字层的表现。
- **自定义词典**，如果你处理的是行业专用术语。
- **批量处理**，自动处理成千上万的扫描件。

随意调整线程数、替换过滤器或接入自己的预处理管道。核心模式保持不变：加载 → 预处理 → 配置 → OCR → 保存。

祝编码愉快，愿你的 PDF 永远可搜索！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}