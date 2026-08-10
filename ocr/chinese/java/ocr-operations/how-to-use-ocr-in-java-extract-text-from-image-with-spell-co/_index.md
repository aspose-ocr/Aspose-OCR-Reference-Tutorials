---
category: general
date: 2026-05-06
description: 如何在 Java 中使用 OCR 从图像中提取文本。学习 OCR 图像转文本转换，纠正 OCR 错误，并使用 Aspose OCR 加载图像进行
  OCR。
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: zh
og_description: 如何在 Java 中使用 OCR 从图像提取文本，纠正 OCR 错误，并使用 Aspose OCR 加载图像进行 OCR。
og_title: 如何在 Java 中使用 OCR – 完整指南
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 OCR —— 从图像提取文本并进行拼写校正
url: /zh/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 从图像提取文本并进行拼写校正

是否曾想过 **如何使用 OCR** 将模糊的收据照片转换为干净、可搜索的文本？你并不孤单。在许多项目中——费用跟踪应用、发票数字化流水线，甚至是快速记事脚本——从图像中获取可靠的文本是第一道障碍。

本教程将手把手教你在 Java 中使用 OCR，涵盖从加载图像进行 OCR 到纠正 OCR 错误，使结果看起来像是人工输入的全部过程。完成后，你将能够 **从图像中提取文本**，执行 **OCR 图像转文本** 转换，并自动修复常见的识别错误。

## 你将构建的内容

我们将创建一个小型 Java 控制台程序，能够：

1. 将 PNG（或任何受支持的格式）加载到 Aspose OCR 引擎。  
2. 启用内置的拼写校正功能以 **纠正 OCR 错误**。  
3. 运行识别过程并打印清理后的文本。  

无需外部服务，也不需要重量级框架——只需一个 JAR 和几行代码。

### 前置条件

- Java Development Kit (JDK) 8 或更高版本。  
- Maven（或任何构建工具）用于拉取 Aspose OCR 库。  
- 一张你想要分析的图像文件（例如 `receipt.png`）。  

如果缺少 Aspose OCR JAR，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **小技巧：** 免费评估版可用于测试，但购买许可证后可去除评估水印。

## 步骤 1 – 初始化 OCR 引擎（关键字在行动）

首先需要创建 `OcrEngine` 的实例。可以把它想象成读取像素并将其转换为字符的大脑。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*为什么重要：* 初始化引擎会设置内部资源（语言模型、词典等）。如果跳过此步骤，后续加载图像时会抛出 `NullPointerException`。

## 步骤 2 – 为 OCR 加载图像

现在我们真正 **为 OCR 加载图像**。Aspose 提供了便利的 `ImageStream.fromFile` 辅助方法，也可以直接传入 `byte[]`。

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*常见陷阱：* 文件路径必须是绝对路径或相对于工作目录的相对路径。如果找不到图像，引擎会抛出 `IOException`。请仔细检查路径，尤其是在 IDE 与打包后的 JAR 中运行时的差异。

## 步骤 3 – 启用拼写校正以 **纠正 OCR 错误**

开箱即用的 OCR 可能会产生噪音——比如把 “love” 识别成 “l0ve”，或把 “O” 识别成 “0”。启用拼写校正会让引擎在后处理阶段修正常见错误。

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*为什么需要：* 如果不使用拼写校正，你可能需要手动清理输出，这违背了自动化的初衷。内置词典对英语及其他几种语言表现良好。

## 步骤 4 – 执行识别（**OCR 图像转文本**）

在图像加载并启用拼写校正后，我们终于可以让引擎进行文字识别。

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*边缘情况：* 如果图像对比度低或倾斜严重，结果仍可能出现乱码。考虑在送入引擎前进行预处理（例如二值化、去倾斜）。

## 步骤 5 – 输出清理后的文本

最后一步只需打印结果。在真实应用中，你可能会把它写入数据库或文件，但演示中 `System.out` 已足够。

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### 预期输出

假设 `receipt.png` 包含清晰的商品列表，输出可能类似于：

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

请注意，即使原始扫描中出现了错误的 “Qy”，输出中的 “Qty” 与 “Price” 仍然拼写正确。

## 完整工作示例

下面是完整程序，可复制粘贴到名为 `SpellCorrectDemo.java` 的文件中。确保 Aspose OCR JAR 已加入类路径。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

使用以下命令运行：

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

现在你应该能在控制台看到清理后的文本。

## 进阶：调优设置以获得更高准确率

默认配置适用于大多数印刷文档，但在特定场景下可能需要调整以下参数：

| 设置 | 功能说明 | 何时更改 |
|------|----------|----------|
| `setLanguage(OcrLanguage.English)` | 强制使用英语词典（降低误报） | 当图像仅包含英文文本时。 |
| `setResolution(300)` | 告知引擎源图像的 DPI | 对于高分辨率扫描。 |
| `setEnableAutoSkewCorrection(true)` | 自动纠正轻微倾斜的页面 | 当图像由手机拍摄时。 |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## 常见问题

**问：这能处理 PDF 吗？**  
答：可以。先将每页 PDF 转为图像（例如使用 Aspose PDF），再将图像喂给 OCR 引擎。

**问：如果我的图像是 BMP 格式怎么办？**  
答：`ImageStream.fromFile` 原生支持 PNG、JPEG、BMP、TIFF 和 GIF。只需更改文件扩展名即可。

**问：我可以关闭拼写校正吗？**  
答：完全可以——如果需要原始 OCR 输出供下游处理，只需调用 `setEnableSpellCorrection(false)`。

## 结论

现在你已经掌握了 **如何在 Java 中使用 OCR** 来 **从图像中提取文本**，并自动 **纠正 OCR 错误**，以及使用 Aspose OCR 正确 **为 OCR 加载图像** 的完整流程。初始化、加载、启用拼写校正、识别、输出这五步几乎涵盖了日常 OCR 任务的全部需求。

接下来，你可以将此逻辑与数据库写入、REST 接口或批处理器结合，实现一次性处理大量收据。尝试上表中的额外设置，争取把准确率推向极致。

祝编码愉快，愿你的 OCR 结果永远比咖啡渍的收据更干净！

![如何使用 OCR 的示意图：图像 → OCR 引擎 → 校正后文本]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}