---
category: general
date: 2026-02-14
description: 学习如何在 Java 中使用 Aspose OCR 对图像进行 OCR 并提取图像中的文本。包括加载图像进行 OCR、自定义词典和拼写纠正。
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: zh
og_description: 在 Java 中使用 Aspose OCR 对图像执行 OCR。本指南展示了如何加载图像进行 OCR、从图像中提取文本以及启用拼写校正。
og_title: 在图像上执行 OCR – 完整的 Java 教程
tags:
- OCR
- Java
- Aspose
title: 使用 Aspose OCR 对图像进行 OCR – Java 步骤指南
url: /zh/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在图像上执行 OCR – 完整 Java 教程

是否曾需要**在图像上执行 OCR**但不知从何入手？你并不孤单；许多开发者在首次尝试从图像数据中提取文本时都会遇到同样的难题。好消息是，使用 Aspose OCR for Java，你只需几行代码就能获得可靠的结果——并且可以通过自定义词典和拼写检查来提升准确率。

在本指南中，我们将逐步介绍你需要了解的所有内容：从加载用于 OCR 的图像、启用拼写校正，到最终打印清理后的文本。完成后，你将能够在自己的 Java 项目中**在图像上执行 OCR**，并且还能看到如何**从图像中提取文本**，即使面对噪声较多的扫描件也能正常工作。

## 你需要的准备

- **Java Development Kit (JDK) 8+** – 代码使用标准的 Java API。
- **Aspose OCR for Java** 库（你可以从 Aspose 官网或 Maven Central 获取最新的 JAR）。
- 你想要处理的图像文件（例如 `invoice.png`）。
- （可选）一个纯文本文件 `custom_dict.txt`，其中包含每行一个的领域特定词汇。

就这些——无需笨重的框架，也不需要外部服务。只需纯 Java 和 Aspose OCR JAR。

## 步骤 1：设置项目并导入依赖

首先，创建一个新的 Maven（或 Gradle）项目并添加 Aspose OCR 依赖。如果使用 Maven，你的 `pom.xml` 应该包含：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

如果你更倾向于手动下载 JAR，只需将其放入 `libs` 文件夹并添加到类路径中。

> **专业提示：** 在撰写时务必核实版本号；新版本可能会引入诸如语言包等附加功能。

## 步骤 2：加载图像进行 OCR

第一步实际的代码是将 OCR 引擎指向你想要分析的图像。Aspose OCR 使用 `ImageStream` 包装器，它可以从文件、字节数组甚至 URL 读取。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

请注意，我们通过一次方法调用就**加载用于 OCR 的图像**——无需繁琐的 `BufferedImage` 操作。如果你的图像位于 resources 中，只需将路径替换为 `getClass().getResourceAsStream(...)` 即可。

## 步骤 3：启用拼写校正（可选但强大）

Aspose OCR 可以自动纠正常见的 OCR 错误（例如 “l” 与 “1” 的混淆）。打开此功能只需切换一个标志即可：

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

为什么要这么做？想象一下扫描一张印刷的发票，字体很小且扫描仪会产生杂散点。拼写校正通常会将 “Inv0ice” 自动恢复为 “Invoice”，而无需你额外操作。

## 步骤 4：提供自定义词典（定制引擎）

如果你处理的是行业特定术语——比如医学代码、法律行话或产品 SKU——自定义词典可以显著提升准确率。词典仅是每行一个单词的文本文件。

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

确保文件使用 UTF‑8 编码；否则非 ASCII 单词可能会出现乱码。

## 步骤 5：运行 OCR 过程

现在我们终于让引擎发挥其魔力。`process()` 调用返回一个 `OcrResult` 对象，其中包含识别的文本、置信度分数，甚至还有布局信息（如果你后续需要的话）。

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

如果你想确认引擎是否抛出了异常，可以将此调用包裹在 try‑catch 块中，并检查 `ocrResult.getErrorMessage()` 以获取详细信息。

## 步骤 6：输出识别（并校正）后的文本

最后一步是显示或存储提取的字符串。为了快速演示，我们只会将其打印到控制台：

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

运行程序后应打印类似如下内容：

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

如果出现杂散字符，请再次检查你的自定义词典，并考虑调整图像质量（例如，在送入引擎前提高对比度）。

### 完整可运行示例

将所有内容整合在一起，下面是完整的、可直接运行的类：

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

将此文件保存为 `SpellCorrectDemo.java`，调整路径后使用 `javac` 编译，并使用 `java SpellCorrectDemo` 运行。现在你应该能够**在图像上执行 OCR**并看到打印出的提取文本。

## 常见问题与边缘情况

### 如果图像是其他格式（PDF、TIFF 等）怎么办？

Aspose OCR 开箱即支持多种光栅格式。对于 PDF，你需要先将每页提取为图像——Aspose PDF for Java 能很好地完成此工作。一旦拥有 `BufferedImage` 或字节流，同样的 `setImage` 调用即可使用。

### 如何处理多页文档？

遍历每页图像，执行 OCR 步骤并将结果拼接。若希望每页拥有独立的拼写检查上下文，请记得在每页重置或创建新的 `OcrEngine` 实例。

### 我能限制语言或字符集吗？

可以。使用 `ocrEngine.getEngineOptions().setLanguage(Language.English);`（或其他受支持的语言）来减少误报并加快处理速度。

### 大批量处理的性能如何？

Aspose OCR 对只读操作是线程安全的。你可以启动线程池并发处理图像——只需避免在多个线程间共享同一个 `OcrEngine` 实例。

## 提升准确率的技巧

- **预处理图像**：提升对比度、去除背景噪声或转换为灰度。
- **使用高分辨率扫描**（300 dpi 或更高）。分辨率过低常导致字符乱码。
- **保持自定义词典精简**：过多不相关的词会干扰拼写检查器。
- **验证输出**：如果你知道预期格式（例如日期、数字），可使用正则表达式进行后处理以捕获异常。

## 下一步

现在你已经可以使用 Aspose OCR **在图像上执行 OCR**并**从图像中提取文本**，接下来可以探索以下内容：

- **将 OCR 输出保存为带可搜索文本层的 PDF**。
- **与数据库集成**，自动存储提取的发票数据。
- **应用机器学习后处理**，在手写笔记上实现更高的准确率。
- **在接受用户上传图片的 Web 服务中使用 `load image for OCR` 标志**。

这些主题都基于我们所讲的核心步骤，你会发现过渡十分顺畅。

---

*祝编码愉快！如果遇到任何问题，欢迎留言——没有什么比真实案例的学习更好。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}