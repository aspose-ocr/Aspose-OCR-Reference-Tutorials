---
category: general
date: 2026-04-29
description: 使用 Aspose OCR 在 Java 中提取图像文本——学习如何加载图像进行 OCR 并以 JSON 格式识别收据文本。
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: zh
og_description: 使用 Aspose OCR 在 Java 中提取图像文字。本教程展示如何加载图像进行 OCR，识别收据中的文字并输出为 JSON。
og_title: Java 从图像中提取文本 – 完整指南
tags:
- Java
- OCR
- Aspose
title: 使用 Java 从图像提取文本 – 加载图像进行 OCR
url: /zh/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extract text from image java – 完整指南

是否曾经需要 **extract text from image java** 但不确定该选哪个库？你并不孤单。许多开发者在尝试 load image for OCR 时会遇到瓶颈，随后得到的原始文本格式难以使用。  

在本教程中，我们将演示一个简洁的端到端解决方案，它不仅能够 **load image for OCR**，还可以 **recognize text from receipt** 并输出整洁的 JSON 字符串。完成后，你将拥有一个可直接运行的 Java 类，能够直接放入任何项目——无需额外的调试。

## 你将学到

- 如何为 Java 设置 Aspose OCR（这个库让繁重的工作变得轻松）。
- 从磁盘 **load image for OCR** 的完整步骤。
- 如何配置引擎以 JSON 格式返回结果，这对下游处理非常理想。
- 如何 **recognize text from receipt** 图像并验证输出。

无需事先了解 Aspose；只需一套可用的 JDK 和你熟悉的 IDE 即可。

## 前提条件

| Requirement | 为什么重要 |
|-------------|------------|
| **Java 17+** (or any recent JDK) | Aspose OCR 随附针对现代 Java 运行时的编译二进制文件。 |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | 让依赖管理变得轻而易举。 |
| **A sample receipt image** (e.g., `receipt.png`) | 我们将使用此文件演示 **recognize text from receipt**。 |
| **Internet connection** (once) | 首次需要下载 Aspose JAR 时使用。 |

如果你已经具备这些，太好了——让我们开始吧。

## 步骤 1：将 Aspose OCR 添加到项目中

首先需要的是 Aspose OCR 库。如果你使用 Maven，请在 `pom.xml` 中添加以下代码段：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

对于 Gradle，则如下所示：

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **小技巧：** 锁定版本号。后续升级可能会引入细微的 API 变化，导致代码出错。

依赖解析完成后，你就可以编写实际执行 **extract text from image java** 的 Java 代码了。

## 步骤 2：加载图像进行 OCR

现在我们展示实现 **load image for OCR** 的确切代码行。Aspose 提供了便利的 `ImageStream.fromFile` 辅助方法。

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

将 `YOUR_DIRECTORY` 替换为收据文件的绝对或相对路径。如果路径错误，引擎会抛出 `FileNotFoundException`，请务必检查拼写。

> **原因说明：** 正确加载图像是基础。如果图像未被读取，OCR 引擎将无可识别的内容，最终只能得到空的 JSON 结果。

## 步骤 3：指示引擎返回 JSON

Aspose OCR 可以输出 XML、纯文本或 JSON。对于现代 API，JSON 最为灵活，因此我们将显式设置输出格式。

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

如果下游系统更偏好 XML，只需将 `OcrResultFormat.XML` 替换即可。该 API 设计为可互换。

## 步骤 4：运行识别过程

在图像已加载且格式已设置后，下一步是实际执行 **recognize text from receipt**。这就是繁重工作所在。

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

`recognize()` 调用会阻塞，直至引擎完成图像分析。对于大图像，你可能希望在后台线程中运行，但对于普通收据来说，几乎在瞬间即可完成。

## 步骤 5：获取 JSON 结果

最后，我们提取原始 JSON 字符串并打印输出。该字符串包含所有识别的文本、其边界框、置信度分数等信息。

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### 预期输出

对清晰的收据运行完整程序后，会得到类似如下的输出：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

请注意，收据的每一行都是带有置信度分数的独立块。现在你可以将该 JSON 输入到任何下游系统——存入数据库、通过 HTTP 发送，或喂给机器学习模型。

## 完整工作示例

下面是完整的、独立的 Java 类，将所有步骤整合在一起。复制粘贴后，调整图像路径，然后运行 `mvn compile exec:java`（或等效的 Gradle 命令）。

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **注意事项：**  
> • **文件路径错误**——在 Windows 与 macOS/Linux 上检查斜杠。  
> • **内存不足**——大图像可能需要 `ocrEngine.setMemoryOptimization(true)`。  
> • **语言设置**——如果收据包含非拉丁字符，请在 `recognize()` 前调用 `ocrEngine.setLanguage(OcrLanguage.SPANISH)`（或任何受支持的语言）。

## 测试解决方案

1. **运行程序** – 你应该在控制台看到 JSON 数据块。  
2. **验证 JSON** – 将输出复制到 <https://jsonlint.com/>，确保其格式正确。  
3. **解析它** – 在实际项目中，你可以使用 Jackson 或 Gson 等库将 JSON 映射为 POJO，以便更易处理。

如果出现空的 `pages` 数组，最常见的原因是：图像文件未找到，或图像对引擎默认设置来说过于模糊。后者情况下，可尝试提升 DPI 或在送入 Aspose 前进行预处理（例如二值化）。

## 变体与边缘情况

| 场景 | 需要更改的内容 |
|------|----------------|
| **Multiple pages** (e.g., multi‑page PDF converted to images) | 在循环中遍历每张图像，在循环内部调用 `ocrEngine.setImage(...)`，并聚合 JSON 结果。 |
| **Different output format** | 将 `OcrResultFormat.JSON` 替换为 `OcrResultFormat.XML` 或 `OcrResultFormat.PLAIN_TEXT`。 |
| **Performance tuning** | 使用 `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` 以提升速度，或使用 `OcrRecognitionMode.ACCURATE` 以获得更高质量。 |
| **Non‑receipt documents** | 如果需要表格提取，请将 `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` 调整为相应设置。 |

这些调整使你能够将核心 **extract text from image java** 流程适配到各种实际场景。

## 结论

我们刚刚介绍了一种简洁、可用于生产环境的方式，使用 Aspose OCR **extract text from image java**。通过遵循这五个步骤——创建引擎、**load image for OCR**、设置 JSON 输出、**recognize text from receipt**，以及最终读取 JSON，你即可轻松将 OCR 集成到任何 Java 后端。

从这里你可能想要：

- 将 JSON 存入 NoSQL 数据库以便后续分析。  
- 将结果输送到聊天机器人，以回答关于收据的问题。  
- 结合 Apache Tika 处理 PDF、DOCX 等其他格式。

试一试，调整设置以匹配你的特定文档，让机器完成繁重工作，而你专注于创造价值。

---

![extract text from image java](placeholder-image.png "extract text from image java")

*图示：OCR 流程的可视化表示——从图像文件到 JSON 输出。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}