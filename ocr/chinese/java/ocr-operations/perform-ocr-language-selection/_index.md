---
date: 2025-12-13
description: 学习如何使用 Aspose.OCR for Java 并选择语言从图像中提取文本。此一步一步的 Aspose OCR Java 教程展示了精确的
  OCR 配置。
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: 使用 Aspose.OCR 进行语言选择的图像文字提取方法
url: /zh/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.OCR 进行语言选择从图像中提取文本

## 介绍

从图像文件中提取文本是一个常见需求，无论是数字化扫描文档、处理收据，还是构建可搜索的档案。Aspose.OCR for Java 使此任务变得简单，并提供对语言选择、倾斜校正和识别区域的细粒度控制。在本教程中，我们将通过一个完整的实战示例，展示 **如何使用特定语言设置从图像中提取文本**，以便您今天就能将可靠的 OCR 集成到 Java 应用程序中。

## 快速答案
- **在 Java 中使用哪个库进行 OCR？** Aspose.OCR for Java  
- **哪个设置用于选择语言？** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **开发时需要许可证吗？** 免费评估许可证可用于测试；生产环境需要商业许可证。  
- **我可以将 OCR 限制在图像的某个区域吗？** 可以，使用 `RecognitionSettings.setRecognitionAreas()` 并传入矩形。  
- **典型的运行时间是多少？** 在标准笔记本电脑上每页几秒，具体取决于图像大小和语言复杂度。

## 什么是“从图像中提取文本”？

从图像中提取文本（OCR）将字符的视觉表示转换为机器可读的字符串。这使得搜索、分析和数据提取工作流成为可能，否则这些工作流需要手动转录。

## 为什么在语言选择下使用 Aspose.OCR？

- **多语言支持** – 选择图像中实际存在的语言以提升准确率。  
- **细粒度控制** – 调整倾斜、定义识别区域，并设置自动倾斜行为。  
- **纯 Java API** – 无本地依赖，易于集成到任何 Java 项目中。  
- **丰富的结果数据** – 一次调用即可获取纯文本、JSON、边界矩形和警告信息。

## 前置条件

- **已安装 Java Development Kit (JDK)**（JDK 8 或更高）。  
- **Aspose.OCR for Java** 库 – 从官方网站 [here](https://reference.aspose.com/ocr/java/) 下载。  
- 包含要提取文本的图像文件，例如 `p3.png`。

## 导入包

在您的 Java 源文件中，包含所需的 Aspose.OCR 类和标准 Java 工具类：

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

将 `"Your Document Directory"` 替换为 `p3.png` 所在的绝对路径。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

### 步骤 2：定义图像路径

确保 `file` 变量指向您要处理的确切图像。

```java
// The image path
String file = dataDir + "p3.png";
```

### 步骤 3：创建 Aspose.OCR API 实例

`AsposeOCR` 对象为您提供所有 OCR 操作的访问权限。

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### 步骤 4：设置识别选项（语言选择）

这里我们：

1. 禁用自动倾斜，因为我们提供了手动倾斜值。  
2. 定义矩形区域（`RecognitionAreas`），将 OCR 限制在实际包含文本的图像部分。  
3. 将 **语言** 设置为英语 (`Language.Eng`)。根据源图像的语言，可更改为 `Language.Fra`、`Language.Spa` 等。

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

### 步骤 5：执行 OCR 并获取结果

`RecognizePage` 调用使用图像和您定义的设置运行 OCR 引擎。结果存储在 `RecognitionResult` 对象中。

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 步骤 6：打印并使用结果

控制台输出显示：

- 完整的提取文本 (`recognitionText`)。  
- 每个定义矩形的文本 (`recognitionAreasText`)。  
- 边界矩形坐标。  
- 便于下游处理的 JSON 表示。  
- 检测到的倾斜角度和任何警告。

您现在可以将 `result.recognitionText` 传入业务逻辑——存储、索引或传递给其他服务。

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

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **乱码字符** | 选择了错误的语言 | 设置正确的 `Language` 枚举（例如，法语使用 `Language.Fra`）。 |
| **未返回文本** | 识别区域未覆盖文本 | 调整 `Rectangle` 坐标，或移除 `RecognitionAreas` 以处理整幅图像。 |
| **性能慢** | 图像过大或分辨率过高 | 在 OCR 前缩小图像，或为 JVM 增加内存分配。 |
| **不支持的格式警告** | 未识别的图像格式 | 在处理前将图像转换为 PNG、JPEG 或 TIFF。 |

## 常见问答

**Q: 我可以在一次 OCR 调用中识别多种语言吗？**  
A: 可以。使用 `settings.setLanguage(Language.Eng | Language.Fra)` 启用多语言识别。

**Q: Aspose.OCR 支持哪些图像格式？**  
A: PNG、JPEG、BMP、TIFF、GIF 等多种格式。只需提供正确的文件路径。

**Q: 图像大小是否有限制？**  
A: 没有硬性限制，但非常大的图像会增加内存使用和处理时间。建议对大文件进行缩放。

**Q: 如何获取生产许可证？**  
A: 从 Aspose 网站购买许可证，并按照 Aspose 文档中示例通过 `License` 类进行应用。

**Q: 我可以直接从 PDF 页面提取文本吗？**  
A: Aspose.OCR 不能直接处理 PDF。请先将 PDF 页面转换为图像（例如使用 Aspose.PDF），然后再进行 OCR。

## 结论

您现在已经了解如何使用 Aspose.OCR for Java 在选择适当语言并将识别限制在特定区域的情况下 **从图像中提取文本**。这种方法提供了准确、高性能的 OCR，能够嵌入任何基于 Java 的工作流——从文档管理系统到数据捕获管道。

---

**最后更新：** 2025-12-13  
**测试环境：** Aspose.OCR 24.11 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}