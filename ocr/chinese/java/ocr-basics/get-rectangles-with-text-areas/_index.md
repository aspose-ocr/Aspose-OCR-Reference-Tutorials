---
date: 2026-02-09
description: 了解如何使用 Aspose OCR Java 库将图像转换为文本并提取文本区域矩形。分步指南并附代码示例。
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 将图像转换为文本——从图像中识别文本并获取文本区域矩形
url: /zh/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将图像转换为文本 – 从图像识别文本并获取文本区域矩形

## 介绍

如果您需要在 Java 应用程序中 **将图像转换为文本** 并 **从图像识别文本**，Aspose.OCR for Java 提供了一种快速、精准的实现方式。在本教程中，我们将逐步演示如何从图像中提取段落、获取每个文本区域的边界矩形，并将这些坐标打印到控制台。完成后，您将了解该方法的原理、如何集成该库，以及在何处可以扩展以满足自己的使用场景。

## 快速答疑
- **“从图像识别文本”是什么意思？** 指将图片中的可视字符转换为可编辑的字符串数据。  
- **Java 中使用哪个库实现？** Aspose.OCR for Java。  
- **开发阶段需要许可证吗？** 提供用于测试的临时许可证；生产环境需要正式许可证。  
- **可以提取段落而不是单词吗？** 可以——使用 `AreasType.PARAGRAPHS` 获取段落级别的矩形。  
- **代码是否兼容 Java 11+？** 完全兼容，API 支持 Java 11 及更高版本。

## Aspose.OCR 中的 “将图像转换为文本” 是什么？
Aspose.OCR 的 `RecognizePage` 方法会分析位图，应用 OCR 算法，并返回识别后的字符串。当您请求文本区域时，库还会计算每个文本块的精确 `Rectangle` 坐标，便于后续高亮或处理特定区域。

## 为什么选择这款 **java ocr library**？
- **高准确率** – 支持多语言和复杂字体。  
- **易于集成** – 单个 JAR 即可提供完整的 OCR 功能。  
- **灵活的输出** – 可获取原始文本、格式化的 HTML，或精确的文本区域矩形。  
- **线程安全** – 适用于高吞吐量的服务器环境。

## 前置条件

- 已在机器上安装 **Java Development Kit**（JDK 11 或更高）。  
- 已下载 **Aspose.OCR for Java** 库，可从官方站点 [here](https://releases.aspose.com/ocr/java/) 获取。  
- 具备 IDE 或构建工具（Maven/Gradle）以管理 JAR 依赖。

## 导入包

在 Java 项目中导入所需的类：

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
创建一个新的 Java 项目（或在已有项目中添加），并将 Aspose.OCR JAR 放入类路径。如果使用 Maven，请按下载包中的说明添加依赖。

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
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 步骤 4：识别图像中的文本
调用 `RecognizePage` 将图片转换为纯文本。此步骤演示了核心的 **recognize text image java** 能力：

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 步骤 5：获取文本区域的矩形
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

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| `IOException` 在 `RecognizePage` 上抛出 | 文件路径不正确或缺少读取权限 | 确认 `imagePath` 指向存在的 PNG/JPG 文件，并确保应用拥有文件系统访问权限。 |
| 返回的字符串为空 | 图像质量低或语言不受支持 | 对图像进行预处理（提升对比度、二值化），或使用 `api.setLanguage("eng")` 指定正确的语言。 |
| 未返回矩形 | 使用了错误的 `AreasType`（例如期望段落却使用 `WORDS`） | 根据需求切换为 `AreasType.PARAGRAPHS` 或 `AreasType.LINES`。 |

## 常见问答

**问：Aspose.OCR 是否兼容 Java 11？**  
答：是的，Aspose.OCR 可在 Java 11 及更高版本上运行。

**问：我可以在个人项目和商业项目中使用 Aspose.OCR 吗？**  
答：可以，任何类型的项目均可使用。许可证详情请访问 [here](https://purchase.aspose.com/buy)。

**问：如何获取用于评估的临时许可证？**  
答：可在此处获取临时许可证 [here](https://purchase.aspose.com/temporary-license/)。

**问：在哪里可以找到社区支持或官方帮助？**  
答：请访问 [Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16) 进行支持和讨论。

**问：Aspose.OCR 支持多线程吗？**  
答：支持，库是线程安全的，可在并发环境中使用以提升性能。

## 结论

在本 **aspose ocr java tutorial** 中，您学习了如何使用 Aspose.OCR for Java **将图像转换为文本**、提取段落并获取围绕每个文本块的精确矩形。这些功能可帮助您构建可搜索的 PDF、在 UI 覆盖层中高亮文本，或将结构化数据输送到下游流程。进一步探索 API，可自定义语言设置、处理不同图像格式，或与云存储集成。

---

**最后更新：** 2026-02-09  
**测试环境：** Aspose.OCR 23.10 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}