---
category: general
date: 2026-01-12
description: 使用 Aspose OCR 在 Java 中提取图像文本。学习如何使用 Java OCR 示例从发票图像中提取文本并获取 OCR 输出文本。
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: zh
og_description: 使用 Aspose OCR 在 Java 中从图像提取文本。本指南展示如何从发票图像中提取文本，包含 Java OCR 示例，并输出
  OCR 文本。
og_title: 在 Java 中从图像提取文本 – 完整 OCR 示例
tags:
- OCR
- Java
- Aspose
title: 在 Java 中从图像提取文本 – 完整 OCR 示例
url: /zh/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中从图像提取文本 – 完整 OCR 示例

有没有想过如何在不抓狂的情况下**从图像中提取文本**？也许你手头有一堆扫描的发票，需要快速获取数字。根据我的经验，最简单的方法是让专用的 OCR 库来完成繁重的工作。本教程展示了如何使用 Aspose OCR for Java 从典型的发票图像中*提取文本*，并且演示了一个**java ocr example**，输出的 OCR 文本可以直接传入下游系统。

我们将逐步讲解你需要了解的所有内容：从项目设置、定义关注标题和总金额的感兴趣区域（ROI），到最终打印提取的文本。完成后，你将能够自动**处理发票图像**文件，并获取干净、可搜索的文本。

> **你将获得：** 一个可直接运行的 Java 程序、每一步的清晰解释，以及处理真实发票的实用技巧。

---

## 前置条件

- 已安装 Java Development Kit (JDK) 8 或更高版本。
- 用于依赖管理的 Maven 或 Gradle（示例使用 Maven）。
- Aspose OCR for Java 许可证（免费试用可用于测试）。
- 将发票图像（`invoice.png`）放置在已知目录下。

如果这些听起来陌生，也别担心——大多数只需下载即可，代码在社区版下仍可编译。

---

## 步骤 1：设置 Maven 项目

首先，创建一个新的 Maven 项目（或在现有项目中添加）。在 `pom.xml` 中加入 Aspose OCR 依赖：

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **专业提示：** 保持版本号为最新；新版本通常会提升对发票中复杂字体的识别准确度。

保存文件后，运行 `mvn clean install` 将库拉取到本地仓库。

---

## 步骤 2：加载发票图像

库准备好后，我们编写一个小的 Java 类。首先创建一个 `OcrEngine` 实例，并指向要读取的图像。

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

为什么要在加载图像**之前**创建引擎？引擎保存了语言、DPI 和 ROI 等配置。提前设置图像可确保这些设置应用于即将处理的文件。

---

## 步骤 3：定义感兴趣区域（ROI）

发票通常包含大量噪声——表格、标志和细小文字。将 OCR 限定在标题和总金额上，可显著提升速度和准确性。Aspose 允许使用矩形来描述这些区域。

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

坐标单位为像素（`x`、`y`、`width`、`height`）。如果发票尺寸不一，可以动态计算这些值——例如先检查图像尺寸。这是实现批量**处理发票图像**解决方案的好扩展。

---

## 步骤 4：在指定区域运行 OCR

设置好 ROI 后，OCR 引擎即可专注于关键区域。`recognize()` 方法返回包含提取文本的 `OcrResult`。

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

在幕后，Aspose 会执行二值化、去噪和字符分割等预处理步骤。无需手动调用——只需让 `recognize()` 完成即可。

---

## 步骤 5：输出提取的文本

最后，我们将文本打印到控制台。在实际应用中，你可能会将其存入数据库、传入下游分析管道，甚至生成可搜索的 PDF。

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

运行程序后，你应看到类似如下的输出：

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

如果输出乱码，请再次检查矩形坐标或提升图像分辨率。OCR 引擎对清晰的高 DPI 扫描尤为友好。

---

## 完整工作示例

下面是完整的、独立的 Java 文件，可直接复制粘贴到 `src/main/java/RoiExample.java`。无需外部代码片段——所需全部内容均在此。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **注意：** 将 `YOUR_DIRECTORY` 替换为发票图像的绝对路径。如果使用相对路径，请确保工作目录与运行 `java` 命令的目录一致。

---

## 常见问题与边缘情况

### 如果发票尺寸变化怎么办？

可以动态计算 ROI：

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### 如何处理多语言？

Aspose OCR 支持语言包。只需在调用 `recognize()` 前设置语言：

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### 如果 OCR 返回空字符串怎么办？

常见原因包括：

- 图像分辨率低（< 300 DPI）。放大或请求更高质量的扫描。
- 背景过暗或过亮。OCR 前使用简单的对比度增强滤镜。
- ROI 坐标错误，导致完全错过文本。

---

## 生产级 OCR 的技巧

1. **批量处理：** 将逻辑包装在循环中，遍历发票文件目录。记录每个结果以便审计。
2. **错误处理：** 捕获 `OcrException`，在不终止整个任务的情况下优雅地跳过损坏的图像。
3. **性能优化：** 在多个图像之间复用同一个 `OcrEngine` 实例；为每个文件创建新引擎会产生不必要的开销。
4. **验证：** 提取后，对总金额使用正则检查（`\$\d{1,3}(,\d{3})*(\.\d{2})?`），确保数字合理。

实现这些建议后，简单的**java ocr example**将转变为面向每晚需要**处理发票图像**文件的企业的稳健、可扩展的解决方案。

---

## 结论

我们刚刚介绍了如何使用 Aspose OCR 在 Java 中**从图像中提取文本**，并聚焦于实际的发票处理场景。通过定义感兴趣区域、运行 OCR 引擎并打印**输出 OCR 文本**，你现在拥有了构建自动化数据采集流水线的坚实基础。

下一步？尝试将 ROI 扩展到包含明细表格，尝试不同的语言设置，或将提取的字符串输入 PDF 生成库以创建可搜索的文档。将 OCR 与现代 Java 工具相结合，可能性无限。

对其他文档类型的**如何提取文本**还有疑问，或需要帮助调整异常布局的 ROI？在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}