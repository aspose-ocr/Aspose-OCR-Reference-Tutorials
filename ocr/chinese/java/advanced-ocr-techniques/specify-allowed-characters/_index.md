---
date: 2026-05-24
description: 了解如何在 Java 中使用 Aspose.OCR 进行 OCR，提取图像中的文本，设置允许的字符，并在几分钟内应用临时许可证。
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: 在 Aspose.OCR 中指定允许的字符
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: 如何使用 OCR – 使用 Aspose.OCR 从图像中提取文本
url: /zh/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR – 使用 Aspose.OCR 从图像中提取文本

在现代 Java 应用程序中，**如何使用 OCR** 是一个常见问题，尤其是当您需要将扫描的发票、收据或打印表单转换为可搜索的文本时。本教程将带您完成一个完整的 **Aspose.OCR for Java** 示例：从图像中提取文本，限制输出为自定义字符集，并应用临时许可证以快速评估。

## 快速答案
- **Aspose.OCR 的作用是什么？** 它能够高精度地从图像中提取文本，并允许您限制识别的字符。  
- **我需要许可证吗？** 在生产环境中需要临时或永久许可证；临时密钥可以去除水印。  
- **支持哪个 JDK 版本？** 该库兼容最新的 JDK 发行版（JDK 17、19、21）。  
- **我可以限制识别的字符吗？** 可以——使用 `setAllowedCharacters` 方法来限制输出。  
- **设置需要多长时间？** 基本的端到端实现大约需要 10‑15 分钟。

## 什么是“从图像中提取文本”？

从图像中提取文本，也称为光学字符识别（OCR），将视觉字符——无论是印刷的、手写的还是打字的——转换为机器可读的字符串。此转换使应用程序能够以编程方式搜索、索引、编辑和分析内容，支持诸如发票处理、文档归档和数据录入自动化等工作流。

## 为什么使用 Aspose.OCR for Java？

Aspose.OCR 支持 **60+ 种语言**，能够在不将整个文件加载到内存的情况下处理高达 **10 MB** 的图像，并在干净的扫描件上实现 **>95 % 的准确率**。该库是自包含的，无需外部 OCR 引擎，从而简化部署并降低许可成本。

## 前提条件

### Java Development Kit (JDK)

确保已安装最新的 Java Development Kit。您可以从 [here](https://www.oracle.com/java/technologies/javase-downloads.html) 下载。

### Aspose.OCR for Java 库

从 [download link](https://releases.aspose.com/ocr/java/) 下载并安装 Aspose.OCR for Java 库。

### Aspose.OCR 许可证

要解锁全部功能，请获取许可证。您可以从 [here](https://purchase.aspose.com/buy) 购买，或请求 [temporary license](https://purchase.aspose.com/temporary-license/) 进行试用。

## 如何在 Java 中使用 Aspose.OCR 进行 OCR？

加载图像，配置 OCR 引擎，并调用识别方法——只需几行简洁代码。本段直接回答告诉您该怎么做：使用许可证字符串创建 `AsposeOCR` 实例，设置允许的字符，然后在目标图像上调用 `RecognizeLine` 以获取提取的文本。API 在内部处理图像预处理，因此无需额外代码即可获得干净的结果。

### 导入包

`AsposeOCR` 类位于 `com.aspose.ocr` 包中。在开始编码之前，请导入所需的类。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## 步骤指南

### 步骤 1：设置文档目录

选择一个文件夹，用于存放 OCR 结果和临时文件。稍后将使用此路径定位要处理的图像。

```java
String dataDir = "Your Document Directory";
```

### 步骤 2：指定图像路径

提供指向您要分析的图像的完整文件系统路径或类路径资源位置。

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 步骤 3：创建 Aspose.OCR 实例

`AsposeOCR` 是执行光学字符识别的核心引擎。使用临时或永久许可证字符串实例化它。

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### 步骤 4：执行 OCR 识别

`RecognizeLine` 从提供的图像中提取单行文本，并将其作为普通的 Java `String` 返回。您可以对多行文档重复调用此方法。

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **技巧提示：** 如果您需要将输出限制为仅数字（例如发票号码），请在调用 `RecognizeLine` 之前对 `AsposeOCR` 实例调用 `setAllowedCharacters("0123456789")`。这会强制引擎忽略所有非数字符号。  
> `setAllowedCharacters` 是 `AsposeOCR` 的一个方法，用于将 OCR 输出限制在指定的字符白名单中。

## 常见问题及解决方案

| Issue | Reason | Fix |
|-------|--------|-----|
| **没有输出或为空字符串** | 图像路径不正确或格式不受支持 | 验证 `imagePath` 并使用受支持的格式（JPEG、PNG、BMP） |
| **识别错误** | 低分辨率图像或噪声背景 | 在 OCR 前对图像进行预处理（提高对比度、二值化） |
| **许可证未应用** | 缺少或无效的许可证密钥 | 确保许可证字符串正确并传递给 `AsposeOCR` 构造函数 |

## 常见问题

**Q: 如何获取 Aspose.OCR 的临时许可证？**  
A: 访问 [temporary license page](https://purchase.aspose.com/temporary-license/) 以请求一个去除评估水印的试用密钥。

**Q: 在哪里可以找到 Aspose.OCR 的支持？**  
A: 加入 [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) 社区获取帮助和讨论。

**Q: 我可以在 Aspose.OCR 中指定允许的字符吗？**  
A: 可以，使用 `setAllowedCharacters` API 定义自定义字符白名单。这对于仅数字字段非常理想。

**Q: Aspose.OCR 与最新的 JDK 版本兼容吗？**  
A: 完全兼容——Aspose.OCR 会定期更新，以保持与最新 Java 发行版的兼容性。

**Q: 除了行识别之外，是否还有其他 OCR 功能？**  
A: 该库还支持块、段落和整页识别、语言包以及高级图像预处理。

## 结论

通过本 **Aspose OCR Java 教程**，您现在了解了 **如何使用 OCR** 从图像中提取文本、限制字符集，并应用临时许可证进行快速测试。深入阅读完整的 [documentation](https://reference.aspose.com/ocr/java/) 以探索多语言支持、批处理和自定义预处理管道。

---

**最后更新：** 2026-05-24  
**测试环境：** Aspose.OCR for Java 24.11  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相关教程

- [如何在 Java 中设置许可证并验证 Aspose.OCR 许可证](/ocr/java/ocr-basics/set-license/)
- [使用 Aspose.OCR BufferedImage 将图像转换为文本（Java）](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java 示例 – 识别图像中的行](/ocr/java/advanced-ocr-techniques/recognize-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}