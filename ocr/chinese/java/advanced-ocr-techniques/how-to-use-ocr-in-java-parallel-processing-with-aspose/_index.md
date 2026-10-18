---
category: general
date: 2026-02-27
description: 学习如何在 Java 中使用 OCR，通过 Aspose OCR 的并行处理从 TIFF 和 PDF 文件中提取图像文本。快速、简明的指南。
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: zh
og_description: 了解如何在 Java 中使用 OCR，通过 Aspose OCR 的并行处理从 TIFF 和 PDF 文件中提取图像文本。
og_title: 如何在 Java 中使用 OCR – 使用 Aspose 进行并行处理
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 OCR —— 使用 Aspose 进行并行处理
url: /zh/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 使用 Aspose 的并行处理

有没有想过 **如何使用 OCR** 从扫描文档中提取文本而不费力？你并不是唯一的。开发者在需要从图像（尤其是 TIFF 和 PDF）中读取文本时经常碰壁，同时还要保持性能。

在本教程中，我们将展示一个完整、可直接运行的解决方案，**使用 Aspose OCR 在 Java 中提取图像文本**，开启并行处理，并且还能限制线程数。完成后，你将拥有一个单一类，能够 **在 PDF 上执行 OCR** 并 **从 TIFF 图像中提取文本**，速度是单线程方式的数倍。

> **你将收获**  
> * 为什么并行 OCR 很重要的清晰解释。  
> * 完整的 Java 程序（无缺失的 import）。  
> * 调整线程使用和处理常见陷阱的技巧。  

## 前置条件

- Java 8 或更高（代码同样可以在 JDK 11 上编译）。  
- Aspose.OCR for Java 库 – 你可以从 Maven Central 获取最新的 JAR (`com.aspose:aspose-ocr`)。  
- 一个图像文件（`.tif`, `.tiff`）或你想处理的 PDF。  
- 适量的内存——并行处理会启动几个线程，但 Aspose 对内存使用效率很高。

如果你已经具备以上条件，下面开始吧。

![Diagram showing the OCR pipeline – how to use OCR in Java with parallel processing](how-to-use-ocr-pipeline.png)

*Image alt text: how to use OCR example diagram*

---

## 第 1 步：设置项目并添加 Aspose OCR

### 为什么重要

在 **对 PDF 执行 OCR** 或对任何图像执行 OCR 之前，必须将库放入 classpath。缺少它编译器会抛出 `ClassNotFoundException`，导致后续步骤无法进行。

### 操作方法

如果使用 Maven，添加依赖：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

对于 Gradle：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **小贴士：** 保持版本号与 Aspose 发布说明同步；新版通常包含并行处理的性能改进。

---

## 第 2 步：创建 OCR 引擎并启用并行处理

### 为什么重要

默认情况下 Aspose OCR 只在单线程上运行。当你给它一个多页 PDF 或一批 TIFF 时，引擎会逐页顺序处理——既慢又低效。启用并行处理可以让 CPU 同时处理多页，大幅缩短运行时间。

### 代码

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**关键行解释**

- `setUseParallelProcessing(true)`: 告诉 Aspose 将工作负载分配到可用的 CPU 核心。  
- `setMaxThreads(...)`: 如果在共享服务器上或想为其他服务留出余量，可以限制线程池大小。  
- `processImage(inputPath)`: 同时适用于图像文件和 PDF 文档，因此同一调用 **在 PDF 上执行 OCR** 以及在 TIFF 上执行 OCR。

---

## 第 3 步：处理不同输入类型 – PDF 与 TIFF

### 为什么重要

虽然 `processImage` 接受路径字符串，但底层处理方式不同。PDF 通常包含多页，每页会成为单独的 OCR 任务。TIFF 可以是单页或多页；Aspose 将每帧视为一页。

### 注意事项

| 输入 | 常见问题 | 推荐解决方案 |
|------|----------|--------------|
| PDF | 大型 PDF 若一次性加载所有页可能耗尽内存。 | 使用 `ocrEngine.getConfig().setMemoryOptimization(true);`（在新版本中可用）。 |
| 多页 TIFF | 某些旧版 TIFF 使用不受支持的压缩方式。 | 先转换为受支持的格式，或使用 Aspose 的 `TiffImage` 辅助类。 |

下面是一个快速代码片段，演示如何检测文件类型并记录友好信息：

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## 第 4 步：验证输出 – 应该看到什么？

程序结束后，控制台会打印原始提取的文本。对于一张简单的扫描发票，输出可能类似于：

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

如果 OCR 在某页上遇到困难，Aspose 会插入占位行 `[Unrecognizable]`。后续可以过滤这些行以获得干净的数据。

**快速检查**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## 第 5 步：调优性能 – 何时调整线程数

### 为什么重要

线程数越多并不一定越快。在一台 4 核笔记本上启动 8 条线程可能导致上下文切换开销。相反，在 32 核服务器上，你可能希望充分利用全部核心。

### 如何找到最佳配置

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

使用不同设置运行程序并计时：

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

记录时间，选出吞吐量最高的配置，并在生产环境中固定使用。

---

## 第 6 步：扩展示例 – 批量处理多个文件

如果需要 **从整个文件夹中提取图像文本 java**，可以将核心逻辑包装在循环中：

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

该模式扩展性良好，因为引擎已经对每个文件的页面并行处理。外层循环是顺序的，但如果需要充分利用大规模 CPU 农场，也可以将每个文件提交给 `ExecutorService`。

---

## 常见陷阱与规避方法

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| `OutOfMemoryError` | 一次加载过多页面（尤其是巨大的 PDF）。 | 启用内存优化 (`setMemoryOptimization(true)`) 或使用 `processPage` 按页处理 PDF。 |
| 字符乱码 | 语言/字符集配置错误。 | 调用 `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` 或相应语言枚举。 |
| 并行标志开启仍慢 | 操作系统限制线程创建或 JVM 堆内存过小。 | 增加 `-Xmx` 堆大小，并检查 OS 线程限制 (`ulimit -u`)。 |
| 输出为空 | 输入图像分辨率 < 300 dpi。 | 在 OCR 前放大图像，或使用更高分辨率的扫描仪。 |

---

## 小结 – 本文覆盖内容

- **如何在 Java 中使用 OCR**，通过 Aspose 的 `OcrEngine`。  
- 启用 **并行处理** 加速 **在 PDF 上执行 OCR** 与 **从 TIFF 中提取文本**。  
- 调整线程数以获得最佳性能。  
- 处理大 PDF、多页 TIFF 以及语言设置等边缘情况。  
- 将单文件示例扩展为批量处理，以适应真实工作负载。

---

## 后续步骤

掌握基础后，你可以进一步探索以下相关主题：

- **从手写笔记中提取图像文本 java**（启用 `setHandwritingRecognition(true)`）。  
- 将 OCR 输出与 Apache Tika 集成以提取元数据。  
- 将结果存入 Elasticsearch，实现可搜索的文档归档。  
- 在其他语言（如 Python 或 .NET）中使用 Aspose OCR——原理相同。

欢迎尝试不同的线程限制、图像格式和语言包。多实验才能更好地理解速度与准确性的权衡。

---

### Happy coding!

如果遇到任何问题或有进一步优化的想法，欢迎在下方留言。我们随时乐于讨论 OCR 小技巧——不费力，只写代码。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}