---
date: 2025-12-10
description: Learn how to recognize text from image and extract paragraphs from image
  using Aspose.OCR for Java. Step‑by‑step guide with code examples.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 识别图像中的文字并获取文字区域矩形
url: /zh/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像识别文本并获取文本区域矩形

## 介绍

如果您需要在 Java 应用程序中 **recognize text from image** 文件，Aspose.OCR for Java 提供了一种快速、准确的解决方案。在本教程中，我们将逐步演示如何从图像中提取段落，获取每个文本区域的边界矩形，并将这些坐标打印到控制台。结束时，您将了解此方法的原理、如何集成库以及可以在哪里扩展以满足自己的使用场景。

## 快速答案
- **“recognize text from image” 是什么意思？** 它指将图片中的可视字符转换为可编辑的字符串数据。  
- **哪个库在 Java 中处理此功能？** Aspose.OCR for Java。  
- **开发阶段需要许可证吗？** 提供临时许可证用于测试；生产环境需要正式许可证。  
- **我可以提取段落而不是单词吗？** 可以 – 使用 `AreasType.PARAGRAPHS` 获取段落级别的矩形。  
- **代码是否兼容 Java 11+？** 完全兼容，API 在 Java 11 及更高版本上均可运行。

## Aspose.OCR 中的 “recognize text from image” 是什么？
Aspose.OCR 的 `RecognizePage` 方法会分析位图，应用 OCR 算法，并返回识别后的字符串。当您请求文本区域时，库还会为每个文本块计算精确的 `Rectangle` 坐标，方便后续高亮或处理特定区域。

## 为什么选择 Aspose.OCR for Java？
- **高精度** – 支持多种语言和复杂字体。  
- **易于集成** – 单个 JAR 即可提供完整的 OCR 功能。  
- **灵活的输出** – 可获取原始文本、格式化的 HTML 或精确的文本区域矩形。  
- **线程安全** – 适用于高吞吐量的服务器环境。

## 前置条件

- 已在机器上安装 **Java Development Kit**（JDK 11 或更高）。  
- 已下载 **Aspose.OCR for Java** 库，可从官方站点 [here](https://releases.aspose.com/ocr/java/) 获取。  
- 需要一个 IDE 或构建工具（Maven/Gradle）来管理 JAR 依赖。

## 导入包

在您的 Java 项目中，导入必要的类：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 步骤指南

### 步骤 1：设置项目
创建一个新的 Java 项目（或在现有项目中添加），并将 Aspose.OCR JAR 放入类路径。如果使用 Maven，请按照下载包中的说明添加依赖。

### 步骤 2：定义文档目录和图像路径
指定示例图像所在的位置：

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 步骤 3：创建 Aspose.OCR 实例
实例化 OCR 引擎：

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### 步骤 4：识别图像中的文本
调用 `RecognizePage` 将图片转换为纯文本。此步骤演示了核心的 **recognize text from image** 能力：

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 步骤 5：获取带有文本区域的矩形
现在检索每个段落（或其他区域类型）的边界矩形。这正是 **extract paragraphs from image** 并获取其坐标的地方：

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## 常见问题与故障排除

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| `IOException` 在 `RecognizePage` 上 | 文件路径不正确或缺少读取权限 | 验证 `imagePath` 指向已有的 PNG/JPG 文件，并确保应用拥有文件系统访问权限。 |
| 结果字符串为空 | 图像质量低或语言不受支持 | 对图像进行预处理（提升对比度、二值化），或使用 `api.setLanguage("eng")` 指定正确的语言。 |
| 未返回矩形 | 使用了错误的 `AreasType`（例如期望段落却用了 `WORDS`） | 根据需求切换为 `AreasType.PARAGRAPHS` 或 `AreasType.LINES`。 |

## 常见问答

**Q: Aspose.OCR 是否兼容 Java 11？**  
A: 是的，Aspose.OCR 在 Java 11 及更高版本上均可正常工作。

**Q: 我可以在个人项目和商业项目中都使用 Aspose.OCR 吗？**  
A: 可以，您可以在任何类型的项目中使用。有关授权详情，请访问 [here](https://purchase.aspose.com/buy)。

**Q: 如何获取用于评估的临时许可证？**  
A: 您可以在此处获取临时许可证 [here](https://purchase.aspose.com/temporary-license/)。

**Q: 哪里可以找到社区支持或官方帮助？**  
A: 请访问 [Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16) 进行支持和讨论。

**Q: Aspose.OCR 支持多线程吗？**  
A: 支持，库是线程安全的，可在并发环境中使用以提升性能。

## 结论

在本教程中，您学习了如何使用 Aspose.OCR for Java **recognize text from image** 文件，提取段落，并获取围绕每个文本块的精确矩形。这些功能可帮助您构建可搜索的 PDF、在 UI 覆盖层中高亮文本，或将结构化数据输送到下游流程。进一步探索 API，可自定义语言设置、处理不同图像格式，或与云存储集成。

---

**最后更新：** 2025-12-10  
**测试环境：** Aspose.OCR 23.10 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}