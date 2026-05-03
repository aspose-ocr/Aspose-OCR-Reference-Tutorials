---
category: general
date: 2026-05-03
description: 使用 Aspose OCR Java 从图像中提取表格。学习如何加载图像进行 OCR，从 PNG 中提取表格，转换图像表格文本，并快速识别收据图像。
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: zh
og_description: 使用 Aspose OCR Java 从图像中提取表格。本指南展示了如何加载图像进行 OCR、从 PNG 中提取表格、转换图像表格文本以及识别收据图像。
og_title: 从图像中提取表格 – Aspose OCR Java 教程
tags:
- Aspose OCR
- Java
- Image Processing
title: 从图像中提取表格 – 完整的 Aspose OCR Java 指南
url: /zh/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取表格 – 完整的 Aspose OCR Java 指南

是否曾经需要**从图像中提取表格**但总是碰壁？也许你手上有一张扫描的收据或拍摄的发票，表格数据埋在 PNG 中。本文将完整演示如何*加载图像进行 OCR*、将图片转化为结构化行，并**将图像表格文本**转换为 Java 中可用的形式。

我们会一步步走过，从授权 Aspose OCR 引擎到打印检测到的每个单元格。结束后，你将能够**识别收据图像**文件并轻松提取其中的表格。

## 你将学到

- 如何初始化 Aspose OCR 引擎并应用许可证。
- 为什么开启表格检测是**从图像中提取表格**的关键。
- 完整的代码示例，演示**加载图像进行 OCR**并在 PNG 上运行识别。
- 处理多表格、低分辨率扫描以及常见坑点的方法。
- 如何**将图像表格文本**转换为可打印（或可写入数据库）的格式。

无需查阅外部文档——所有内容都在这里。

## 前置条件

- Java 17 或更高（代码使用了现代模块系统）。
- Aspose OCR for Java 许可证文件 (`Aspose.OCR.Java.lic`)。如果只是试验，临时评估密钥也可使用。
- 包含清晰表格的 PNG 图像（例如 `receipt_with_table.png`）。  
- Maven 或 Gradle 用于拉取 Aspose OCR 依赖：

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **专业提示：** 将许可证文件放在 `src/main/resources` 文件夹旁边，这样路径在不同环境下保持稳定。

---

## 步骤 1 – 初始化 OCR 引擎以**从图像中提取表格**

在引擎能够工作之前，需要先确认你的合法身份。

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*原因说明：* 没有有效许可证时，OCR 引擎会以试用模式运行，可能截断结果或添加水印——这会导致表格提取不可靠。

---

## 步骤 2 – 启用表格检测（**从 png 中提取表格**）

表格检测默认是关闭的，需要手动打开开关。

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

开启此标志后，Aspose OCR 会把对齐的文本块视为行和列，这正是你在**从图像中提取表格**时所需要的。

---

## 步骤 3 – **加载图像进行 OCR** 并 **识别收据图像**

现在我们把图片真正送入引擎。

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

如果你面对的是**识别收据图像**的场景，可能需要先对图像进行预处理（去倾斜、提升对比度）。这超出本快速指南的范围，但对噪声较多的扫描件非常有帮助。

---

## 步骤 4 – 处理 OCR 结果并 **将图像表格文本** 转换

`OcrResult` 对象可能包含一个或多个表格。我们遍历它们并打印每个单元格。

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**此代码的作用：**  

- 检查是否检测到表格；若没有，提示进行质量调优。  
- 对每个表格，使用制表符分隔的方式打印行，便于 CSV 导入。  
- `Cell::getText` 调用是**将图像表格文本**的核心——它从每个单元格中提取原始 OCR 字符串。

### 预期输出

假设 `receipt_with_table.png` 包含一个简单的 3 × 2 表格，输出大致如下：

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

如果图像中有多个表格，它们之间会用空行分隔。

---

## 步骤 5 – 验证提取的表格并处理边缘情况

### 常见坑点

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **未检测到表格** | 图像过于模糊或对比度低 | 在 OCR 前使用二值化 (`ImageProcessing.applyThreshold`) |
| **单元格合并** | 表格线条太淡，OCR 将其视为一个块 | 在 `ocrEngine.getConfig()` 中提升 `TableDetectionSensitivity` |
| **列顺序错误** | 图像倾斜导致对齐错误 | 使用 `ImageProcessing.deskew` 或将图像旋转 90° |

### 接下来可以做什么

- **导出为 CSV** – 将 `System.out.println(line);` 替换为 `FileWriter`，将数据持久化。  
- **写入数据库** – 将每行映射为 POJO，使用 JPA 完成持久化。  
- **结合其他 API** – 对于收据处理，你还可以使用正则表达式在 OCR 文本中提取总额等信息。

---

## 完整可运行示例（复制粘贴即用）

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

运行此程序，指向包含清晰表格的 PNG，即可在控制台看到整齐的行输出。

---

## 结论

现在你已经掌握了使用 Aspose OCR for Java **从图像中提取表格**的完整端到端方案。从授权到**加载图像进行 OCR**、开启**从 png 中提取表格**，再到**将图像表格文本**转换，每一步都有说明和实用技巧。

接下来，可以尝试将输出写入 CSV 文件、推送到关系型数据库，或与收据总额提取流程结合。相同的模式同样适用于发票、价目表以及任何隐藏在网格后的扫描文档。

对低分辨率收据的处理或批量处理有疑问？欢迎在下方留言，祝编码愉快！  

![Extract tables from image example](https://example.com/assets/extract-tables-from-image.png "Extract tables from image – sample output")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}