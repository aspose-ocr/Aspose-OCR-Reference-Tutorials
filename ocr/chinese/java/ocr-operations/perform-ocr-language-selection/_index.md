---
date: 2026-02-12
description: 学习如何使用 Aspose.OCR for Java 对图像文字进行 OCR 并选择语言。本分步指南涵盖 Java 文本提取、OCR 倾斜校正等内容。
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: 如何使用 Aspose.OCR 对图像文本进行语言识别
url: /zh/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 进行语言选择的图像文字 OCR

## 介绍

从图像文件中提取文字是一个常见需求，无论是数字化扫描文档、处理收据，还是构建可搜索的档案库。在本教程中，我们将通过一个完整的实战示例，展示 **如何使用特定语言设置进行图像文字 OCR**，帮助您将可靠的 OCR 集成到 Java 应用程序中。您还将了解如何处理 OCR 斜倾校正和基于区域的识别，以获得最佳准确性。

## 快速答案
- **什么库在 Java 中处理 OCR？** Aspose.OCR for Java  
- **哪个设置用于选择语言？** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **开发是否需要许可证？** 免费评估许可证可用于测试；生产环境需要商业许可证。  
- **我可以将 OCR 限制在图像的某个区域吗？** 是的，使用 `RecognitionSettings.setRecognitionAreas()` 并配合矩形。  
- **典型运行时间是多少？** 在标准笔记本电脑上每页几秒，具体取决于图像大小和语言复杂度。

## 如何在语言选择下进行图像文字 OCR
在本节中，我们回答核心问题 **如何 OCR** 图像（已知文本语言）的方式。选择正确的语言可显著提升识别准确率，因为 OCR 引擎能够使用语言特定的词典和字符模型。

### 为什么这很重要
- **更高的准确性** – 语言特定模型减少误识别。  
- **性能提升** – 引擎跳过不必要的语言检查。  
- **更好地处理变音符号** – 当使用匹配的 `Language` 枚举时，法语、西班牙语、德语等能够被正确识别。

## 什么是“从图像提取文字”？
从图像提取文字（OCR）将字符的视觉表现转换为机器可读的字符串。这使得搜索、分析和数据提取工作流成为可能，否则需要手动转录。

## 为什么在语言选择下使用 Aspose.OCR？
- **多语言支持** – 选择图像中实际存在的语言以提升准确性。  
- **精细控制** – 调整斜倾、定义识别区域，并设置自动斜倾行为。  
- **纯 Java API** – 无本地依赖，易于集成到任何 Java 项目。  
- **丰富的结果数据** – 一次调用即可获取纯文本、JSON、边界矩形和警告信息。

## 前提条件

在开始之前，请确保您已拥有：

- **Java Development Kit (JDK)** 已安装（JDK 8 或更高）。  
- **Aspose.OCR for Java** 库 – 从官方站点[此处](https://reference.aspose.com/ocr/java/)下载。  
- 包含您想要提取的文字的图像文件，例如 `p3.png`。

## 导入包

在 Java 源文件中，包含所需的 Aspose.OCR 类和标准 Java 实用工具：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 步骤指南

### 步骤 1：设置文档目录

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

将 `"Your Document Directory"` 替换为 `p3.png` 所在的绝对路径。

### 步骤 2：定义图像路径

```java
// The image path
String file = dataDir + "p3.png";
```

确保 `file` 变量指向您要处理的确切图像。

### 步骤 3：创建 Aspose.OCR API 实例

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 对象为您提供所有 OCR 操作的访问权限。

### 步骤 4：设置识别选项（语言选择）

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

这里我们：

1. 禁用自动斜倾，因为我们提供了手动斜倾值。  
2. 定义矩形区域（`RecognitionAreas`），将 OCR 限制在实际包含文本的图像部分。  
3. 将 **语言** 设置为英语 (`Language.Eng`)。根据源图像，可更改为 `Language.Fra`、`Language.Spa` 等。

### 步骤 5：执行 OCR 并获取结果

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 调用使用图像和您定义的设置运行 OCR 引擎。结果存储在 `RecognitionResult` 对象中。

### 步骤 6：打印并利用结果

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

控制台输出显示：

- 完整提取的文本 (`recognitionText`).  
- 每个定义矩形的文本 (`recognitionAreasText`).  
- 边界矩形坐标。  
- 用于下游处理的 JSON 表示。  
- 检测到的斜倾角度及任何警告。

现在您可以将 `result.recognitionText` 输入到业务逻辑中——存储、索引或传递给其他服务。

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|-------|-------|-----|
| **乱码字符** | 选择了错误的语言 | 设置正确的 `Language` 枚举（例如，法语使用 `Language.Fra`）。 |
| **未返回文本** | 识别区域未覆盖文本 | 调整 `Rectangle` 坐标或移除 `RecognitionAreas` 以处理整张图像。 |
| **性能慢** | 图像过大或分辨率过高 | 在 OCR 前缩小图像或为 JVM 增加内存分配。 |
| **不支持的格式警告** | 图像格式未被识别 | 在处理前将图像转换为 PNG、JPEG 或 TIFF。 |

## 常见问答

**Q: 我可以在一次 OCR 调用中识别多种语言吗？**  
A: 可以。使用 `settings.setLanguage(Language.Eng | Language.Fra)` 启用多语言识别。

**Q: Aspose.OCR 支持哪些图像格式？**  
A: PNG、JPEG、BMP、TIFF、GIF 等多种格式。只需提供正确的文件路径。

**Q: 图像大小有上限吗？**  
A: 没有硬性限制，但非常大的图像会增加内存使用和处理时间。建议对大文件进行缩放。

**Q: 如何获取生产许可证？**  
A: 从 Aspose 网站购买许可证，并按照 Aspose 文档中示例通过 `License` 类进行应用。

**Q: 我可以直接从 PDF 页面提取文字吗？**  
A: Aspose.OCR 不能直接处理 PDF。请先将 PDF 页面转换为图像（例如使用 Aspose.PDF），再进行 OCR。

## 结论

您已经了解了如何使用 Aspose.OCR for Java **从图像提取文字**，并选择合适的语言以及将识别限制在特定区域。此方法提供了准确、高性能的 OCR，可嵌入任何基于 Java 的工作流——从文档管理系统到数据采集管道。准备好继续了吗？尝试更换语言枚举，实验不同的识别区域，并将结果集成到您自己的应用逻辑中。

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}