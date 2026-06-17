---
category: general
date: 2026-02-17
description: 如何在 Java 中使用 OCR 从 PDF 提取文本，将 PDF 转换为图像，并使用 Aspose.OCR 对扫描的 PDF 文件执行
  OCR。
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: zh
og_description: 如何在 Java 中使用 OCR 从 PDF 文件中提取文本。学习将 PDF 转换为图像，并使用 Aspose.OCR 识别扫描的
  PDF。
og_title: 如何在 Java 中使用 OCR – 完整指南
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 OCR – 使用 Aspose.OCR 从 PDF 中提取文本
url: /zh/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 使用 Aspose.OCR 从 PDF 中提取文本

有没有想过 **如何使用 OCR** 将扫描的 PDF 转换为可搜索的文本？你并不是唯一有此困惑的人。大多数开发者在面对以图像形式存在的 PDF 时都会卡住，常规的文本提取器往往返回空。好消息是，只需几行 Java 代码和 Aspose.OCR，你就可以 **从 PDF 中提取文本**、**将 PDF 转换为图像**，以及 **识别扫描的 PDF**，整个工作流轻松完成。

在本教程中，我们将一步步讲解从授权库到打印最终结果的全部过程。完成后，你将拥有一个可直接运行的程序，能够从任何扫描的报告、发票或电子书中提取纯文本。无需外部服务，无需魔法——只有你掌控的纯 Java 代码。

## 你需要准备的环境

- **Java Development Kit (JDK) 8+** – 任意近期版本均可。  
- **Aspose.OCR for Java** JAR（从 Aspose 官网下载）。  
- 一个 **有效的 Aspose.OCR 授权文件** (`Aspose.OCR.lic`)。免费试用版可以使用，但正式授权可解锁完整精度。  
- 一个 **示例扫描 PDF**（例如 `scanned-report.pdf`）。  
- 一个 IDE 或简单的文本编辑器加上终端。

就这些。无需 Maven、Gradle 或其他额外依赖——只需把 Aspose.OCR JAR 放入类路径即可。

![how to use OCR example](image-placeholder.png "how to use OCR example")

## 第一步 – 加载 Aspose.OCR 授权（为何重要）

在引擎能够全速运行之前，你必须告诉它授权文件所在位置。跳过此步骤会使库进入评估模式，输出会带有水印并可能限制精度。

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**工作原理：** `License` 类读取 `.lic` 文件并在全局注册。一旦设置，后续创建的每个 `OcrEngine` 都会自动使用授权功能。

## 第二步 – 创建 OCR 引擎（魔法背后的核心）

`OcrEngine` 实例是负责扫描图像并输出文本的工作马。可以把它看作解释像素模式的大脑。

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**小贴士：** 你可以通过引擎的属性调整语言、置信度阈值，甚至启用 GPU 加速。对于大多数英文 PDF，默认设置已经足够。

## 第三步 – 准备输入：添加 PDF（内部实现为 PDF 转图像）

Aspose.OCR 将 PDF 的每一页视为图像。当调用 `addPdf` 时，库会悄悄地对每页进行光栅化，这正是 **将 PDF 转换为图像** 以便后续识别所必需的。

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**发生了什么：**  
- 打开 PDF。  
- 每页以 300 dpi（默认）渲染，以保留字符细节。  
- 渲染得到的位图对象被存入 `OcrInput` 集合。

如果你需要原始图像（用于调试或自定义预处理），可以在此步骤后调用 `ocrInput.getPages()`。

## 第四步 – 执行 OCR 过程（对 PDF 进行 OCR）

现在开始真正的重活。`recognize` 方法会遍历每张图像，运行识别算法，并将结果聚合到 `OcrResult` 中。

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**为何在意：** `OcrResult` 不仅包含纯文本，还包括置信度分数、边界框以及原始图像引用。大多数场景只需要调用 `getText()` 即可。

## 第五步 – 获取并显示提取的文本

最后，从结果中取出纯文本字符串并打印。你也可以将其写入文件、送入搜索索引，或传递给下游的 NLP 流程。

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### 预期输出

如果 `scanned-report.pdf` 包含一个简单段落，你会看到类似下面的输出：

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

格式基本保持原始布局，尽可能保留换行。

## 常见边缘情况处理

### 1. 多语言 PDF

如果文档中包含法语或西班牙语等文字，请在调用 `recognize` 前设置语言：

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

可以提供语言数组，让引擎自动检测。

### 2. 低分辨率扫描

面对 150 dpi 的扫描件时，提升内部渲染 DPI：

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

更高的 DPI 能提升字符清晰度，但会占用更多内存。

### 3. 大型 PDF（内存管理）

对于页数众多的 PDF，建议分批处理：

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

此方式可防止 JVM 堆内存膨胀。

## 完整可运行示例

下面是完整程序代码——包括 import 和授权处理——你可以直接复制粘贴后立即运行。

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

使用以下命令运行：

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

你应该会在控制台看到提取的文本。

## 小结 – 本文涵盖内容

- **如何在 Java 中使用 OCR**，配合 Aspose.OCR。  
- **从 PDF 中提取文本** 的完整工作流。  
- 库内部 **先将 PDF 转换为图像**，再进行字符识别。  
- 在多语言、低分辨率扫描和大文档场景下执行 OCR 的技巧。  
- 一个完整、可直接运行的代码示例，适用于任何 Java 项目。

## 后续步骤与相关主题

既然已经能够 **识别扫描 PDF**，可以进一步尝试以下方向：

- **可搜索 PDF 生成** – 将 OCR 文本覆盖回原始 PDF，生成可搜索文档。  
- **批量处理服务** – 将代码封装为 Spring Boot 微服务，通过 REST 接收 PDF。  
- **与 Elasticsearch 集成** – 将提取的文本索引到 Elasticsearch，实现快速全文检索。  
- **图像预处理** – 使用 OpenCV 对页面进行去倾斜或去噪，进一步提升识别准确率。

这些主题都基于本教程的核心概念，欢迎自行实验，让 OCR 引擎为你承担繁重工作。

---

*祝编码愉快！如果在使用过程中遇到授权错误或意外的空结果等问题，欢迎在下方留言，我随时乐意帮助调试。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}