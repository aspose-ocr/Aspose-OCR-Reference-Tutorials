---
category: general
date: 2026-01-12
description: 学习如何使用 Aspose OCR 在 Java 中识别图像中的文本并提取 PNG 文件中的文本。并行处理使其快速。
draft: false
keywords:
- recognize text from images
- extract text from png
language: zh
og_description: 发现使用 Aspose OCR 并行处理在 Java 中识别图像文本并从 PNG 文件提取文本的最简方法。
og_title: 使用 Java 识别图像中的文本 – 并行 OCR 指南
tags:
- OCR
- Java
- Aspose
title: 使用 Java 识别图像中的文本 – 并行 OCR 教程
url: /zh/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 进行图像文字识别 – 并行 OCR 教程

是否曾需要 **recognize text from images**，但在 “how‑do‑I‑do‑that?” 上卡住了？你并不是唯一遇到这种情况的人。无论是数字化发票、从截图中提取数据，还是构建可搜索的档案，能够 *recognize text from images* 都是一个改变游戏规则的能力。  

在本指南中，我们将演示一个完整、可直接运行的 Java 示例，它不仅 **recognize text from images**，还展示了如何使用 Aspose OCR 内置的并行引擎 **extract text from png** 文件。无需外部脚本，无需缺失的代码片段——只有直接的代码和清晰的解释。

## 您将学习

- 在 Java 项目中设置 Aspose OCR  
- 启用并行处理以加速批量作业  
- 加载一组 PNG 文件并高效 **extract text from png**  
- 处理常见陷阱（大文件、空结果、线程限制）  
- 在文章末尾查看完整、可运行的源代码  

## 前提条件

在深入之前，请确保您具备以下条件：

| 需求 | 原因 |
|-------------|----------------|
| Java 8 或更高版本 | Aspose OCR 的 Java API 目标为 Java 8+ |
| Maven 或 Gradle（用于依赖管理） | 简化了 Aspose OCR 库的添加 |
| 一些您想要处理的 PNG 图像 | 本教程使用 `doc1.png`‑`doc4.png` 作为示例 |
| 基本的 Java 语法知识 | 代码很直接，但您需要编译并运行它 |

如果缺少上述任意项，请从 Oracle 或 AdoptOpenJDK 获取最新的 JDK，并建立一个简单的 Maven 项目——无需花哨的配置。

![图像文字识别示意图](image.png){alt="图像文字识别示意图"}

## 第 1 步 – 将 Aspose OCR 添加到项目中

首先，告诉 Maven（或 Gradle）拉取 Aspose OCR 库。在 `pom.xml` 文件中添加：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

如果您更喜欢 Gradle，则等价写法为：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** 检查 [Aspose OCR Maven repository](https://repo.aspose.com/repo) 以获取最新版本。保持库的最新可确保您获得最新的 OCR 改进和 bug 修复。

## 第 2 步 – 启用并行处理（秘密武器）

Aspose OCR 可以将工作负载分布到多个 CPU 核心上。这就是我们在处理数十个 PNG 文件时仍能保持 **recognize text from images** 操作快速的原因。

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

为什么要设置限制？过度分配线程会导致其他进程被饿死，尤其在共享服务器上。四个核心对大多数桌面电脑来说是安全的默认值；如果您知道硬件能够承受更多，可自行提升。

## 第 3 步 – 准备 PNG 文件列表

本教程侧重于 **extract text from png** 文件，但相同代码同样适用于 JPEG、BMP 等格式。将图像放入文件夹并按如下方式引用：

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Note:** 将 `YOUR_DIRECTORY` 替换为 PNG 文件所在的绝对或相对路径。如果需要处理动态文件夹，可使用 `Files.list(Paths.get("YOUR_DIRECTORY"))` 自动构建数组。

## 第 4 步 – 对每张图像运行 OCR（引擎负责繁重工作）

即使我们已经启用并行，也仍然需要遍历文件数组。Aspose OCR 会在内部根据我们配置的线程分配识别工作。

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### 为什么使用循环而不是并行流？

Aspose OCR 已经基于 `ParallelOptions` 在内部拆分图像处理。将调用再包装在外部并行流中会导致双重包装，实际上可能降低性能。请信任库自行管理线程。

## 第 5 步 – 边缘情况与实用技巧

| 情况 | 处理方法 |
|-----------|------------|
| **Huge PNG ( > 10 MB )** | 将 JVM 堆大小提升（`-Xmx2g`）或在送入引擎前调整图像大小。 |
| **Mixed image formats** | 使用 `ocrEngine.setImage(new File(imagePath))` —— 引擎会自动检测格式。 |
| **Need the full text, not just a preview** | 将 `result.getText()` 存入 `StringBuilder`，或写入文件以便后续分析。 |
| **Running on a CI server without a GUI** | 无需额外步骤——Aspose OCR 完全无头。 |
| **License expiration** | 使用 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 注册临时许可证，以避免评估水印。 |

## 完整可运行示例

下面是完整的 Java 类，您可以复制、粘贴并运行。它包含了我们讨论的所有部分，并附带了一些注释以便于理解。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### 预期输出

如果 `doc1.png` 包含短语 “Invoice #12345 – Total $250.00”，您将看到类似如下的输出：

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

预览会在 50 个字符处截断，但完整字符串仍保存在 `result.getText()` 中，可用于后续的任何处理。

## 结论

您现在拥有一套稳固、可投入生产的模式，使用 Aspose OCR 在 Java 中 **recognize text from images**，并且已经看到如何通过并行加速 **extract text from png** 文件。核心步骤——引擎设置、并行配置、图像列表准备以及结果处理——全部覆盖，并提供了一系列实用技巧，帮助您避免常见的头疼问题。

接下来可以做什么？尝试将 PNG 列表换成动态目录扫描，将 OCR 输出导入 Elasticsearch 等搜索索引，或尝试语言特定的 OCR 设置（`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`）。一旦掌握了核心工作流，您就可以随心所欲地扩展功能。

如果在实践中遇到任何奇怪的问题或有扩展本教程的想法，欢迎在下方留言。祝编码愉快，享受将顽固图像转换为可搜索文本的过程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}