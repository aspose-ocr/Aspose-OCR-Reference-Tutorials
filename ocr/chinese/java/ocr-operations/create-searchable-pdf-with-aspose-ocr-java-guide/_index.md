---
category: general
date: 2026-03-26
description: 使用 Aspose.OCR Java 创建可搜索的 PDF —— 学习加载图像进行 OCR、设置主要语言、提取图像文本并保存为 OCR PDF。
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: zh
og_description: 使用 Aspose.OCR Java 创建可搜索的 PDF。一步步指南，加载图像进行 OCR，设置主要语言，从图像提取文本，并保存
  OCR PDF。
og_title: 使用 Aspose.OCR 创建可搜索 PDF – Java 指南
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: 使用 Aspose.OCR 创建可搜索 PDF – Java 指南
url: /zh/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 创建可搜索 PDF – Java 指南

是否曾需要从扫描文档**创建可搜索的 PDF**但不知从何入手？你并不孤单——许多开发者在首次使用 Java 进行 OCR 时都会遇到这个难题。好消息是 Aspose.OCR 让整个流程——从加载图像、设置主要语言到最终保存带 OCR 功能的 PDF——变得相当轻松。在本教程中，我们将演示一个完整、可运行的示例，**从图像中提取文本**、**设置主要语言**，并以**保存 OCR PDF**结束，你可以在任何阅读器中打开它。

我们还会介绍一些实用技巧，例如启用 GPU 加速以提升处理速度，以及处理混合语言文档（本例中为泰米尔语 + 英语）。完成后，你将拥有一段稳健、可直接投入生产的代码片段，可直接嵌入你的项目。

## 你需要的环境

- **Java 17**（或任何近期的 JDK；Aspose.OCR 支持 Java 8+）
- **Aspose.OCR for Java** 库（从官方网站下载或通过 Maven 添加）
- **license file**（许可证文件，或 30 天试用）
- 包含文本的图像文件（演示使用 `sample-mixed-tamil-eng.jpg`）

无需额外框架，也不需要本地依赖——仅使用纯 Java 和 Aspose.JAR 包。

---

## 步骤 1：创建可搜索 PDF – 项目设置

在深入代码之前，让我们确保项目已准备好**创建可搜索的 PDF**文件。

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **专业提示：** 保持版本号为最新；新版本通常包含针对 GPU 使用的性能修复。

现在创建一个名为 `RecentFeaturesDemo` 的简单 Java 类。该类将包含我们需要的所有逻辑，以**加载图像 OCR**、配置语言设置，最终**保存 OCR PDF**。

## 步骤 2：加载图像 OCR 并初始化引擎

管道中的第一步是真正的**加载图像 OCR**。这告诉 Aspose.OCR 要分析哪个文件。

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **为什么重要：** 启用 GPU (`setUseGpu(true)`) 可以在现代硬件上将处理时间缩短最多 70 %，而并行处理确保在 GPU 工作时 CPU 不会闲置。

## 步骤 3：设置主要语言（以及次要语言）

如果跳过此步骤，Aspose.OCR 将尝试猜测语言，这会更慢且准确度更低。下面演示如何将**主要语言**设置为 Tamil，并添加 English 作为回退。

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **解释：** 主要语言会影响识别时使用的字符集和词典。为混合脚本文档添加次要语言至关重要（比如收据中同时包含 Tamil 和 English 文本）。  
> **边缘情况：** 如果文档包含超过两种语言，可以对每一种额外语言调用 `addAdditionalLanguage(...)`。

## 步骤 4：预处理图像 – 去倾斜与去噪

扫描图像常常出现旋转或背景噪声。预处理有助于 OCR 引擎更可靠地**从图像中提取文本**。

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **提示：** 如果你知道图像已经很干净，可以跳过 `setDenoise(true)`，省去几毫秒的时间。

## 步骤 5：加载图像文件

引擎准备就绪后，我们将其指向要分析的文件。

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **如果路径错误怎么办？** Aspose.OCR 会抛出明确的 `FileNotFoundException`。如果需要优雅的错误处理，请将调用包装在 try‑catch 中。

## 步骤 6：运行 OCR 并从图像中提取文本

在完成所有配置后，是时候实际运行识别了。此步骤既**从图像中提取文本**，又为 PDF 创建准备所需的数据。

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

演示图像的典型控制台输出如下：

```
வணக்கம் World
This is a mixed language sample.
```

你会注意到 Tamil 行被正确渲染，随后是 English。这正是正确**设置主要语言**的回报。

## 步骤 7：保存 OCR PDF – 最终步骤

拼图的最后一块是**保存 OCR PDF**。Aspose.OCR 可以在原始图像上嵌入不可见的文本层，使 PDF 可搜索。

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

在 Adobe Reader 中打开 `searchable.pdf`，按 **Ctrl + F**，即可搜索 Tamil 和 English 单词——这正是**创建可搜索 PDF**工作流所承诺的效果。

## 完整可运行示例（复制粘贴）

下面是完整的程序，你可以直接编译运行。请将占位路径替换为你自己的目录。

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

使用以下方式运行：

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

你应该会在控制台看到提取的文本，随后确认 **searchable pdf** 已写入磁盘。

## 常见问题与边缘情况

### 如果我需要从字节数组**加载图像 OCR**怎么办？

你可以将 `ImageStream.fromFile(imagePath)` 替换为 `ImageStream.fromBytes(byteArray)`。当图像来自数据库或 Web 服务时，这非常方便。

### 如何处理已经包含图像的 PDF？

Aspose.OCR 可以直接对 PDF 页面工作：`ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`。引擎会在识别前内部对每页进行光栅化。

### 我的 GPU 未被检测到——我还应该保留 `setUseGpu(true)` 吗？

如果 `setUseGpu(true)` 失败，Aspose.OCR 会自动回退到 CPU。你可以在启用之前检查 `ocrEngine.getEngineSettings().isGpuAvailable()`。

### 我可以使用自定义元数据**保存 OCR PDF**吗？

可以。识别后，在调用 `save` 之前使用 `ocrEngine.getPdfSaveOptions().setTitle("My Document")` 或 `setAuthor("John Doe")` 设置自定义元数据。

## 大批量处理的性能技巧

- **批处理：** 在多个图像之间复用同一个 `OcrEngine` 实例。每次运行之间仅调用 `ocrEngine.clear()`。
- **线程池：** 将每个图像任务包装为 `Callable` 并提交给 `ExecutorService`。由于我们启用了并行处理，每个线程都能受益于多核使用。
- **内存管理：** 对于千兆像素的图像，考虑使用 `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` 降采样，以保持 RAM 使用在合理范围。

## 结论

我们刚刚使用 Aspose.OCR for Java 完整演示了一个**创建可搜索 PDF**的工作流。从**加载图像 OCR**开始，我们

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}