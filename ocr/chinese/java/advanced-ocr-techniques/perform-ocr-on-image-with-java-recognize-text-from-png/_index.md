---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 在 Java 中对图像执行 OCR。了解如何从 PNG 识别文本，并通过内置拼写校正提升 OCR 准确率。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: zh
og_description: 使用 Aspose OCR for Java 对图像执行 OCR。本指南展示了如何从 PNG 识别文本并在几分钟内提升 OCR 准确率。
og_title: 使用 Java 对图像进行 OCR – 完整指南
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 使用 Java 对图像进行 OCR – 识别 PNG 中的文本
url: /zh/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中对图像执行 OCR – 从 PNG 识别文本

是否曾经需要**对图像执行 OCR**但总是得到乱码结果？你并不孤单——噪声扫描、低对比度的 PNG 和奇怪的字体会把原本干净的文档变成字符的乱麻。  

在本指南中，我们将带你一步步完成一个完整、可直接运行的 Java 示例，使用 Aspose OCR **从 PNG 识别文本**，并展示如何通过库的拼写纠正功能**提升 OCR 准确率**。完成后，你将能够可靠地**读取图像文本**，即使源文件并不完美。

## 你将学到

- 如何在 Maven 项目中为 Java 设置 Aspose OCR。  
- 执行 **对图像执行 OCR** 数据的完整步骤，从加载文件到提取干净文本。  
- 为什么启用拼写纠正可以显著提升输出质量。  
- 常见陷阱（文件缺失、不支持的格式）以及如何优雅地处理它们。  
- 一个完整的、可直接复制粘贴的代码示例，今天即可运行。

### 前置条件

- 在机器上已安装 Java 8 或更高版本。  
- 用于依赖管理的 Maven（任何支持 Maven 的 IDE 都可以）。  
- 一张包含可读文本的 PNG 图像——最好是有点噪声的，这样你可以看到拼写纠正的好处。

> **专业提示：**如果手头没有 PNG，随便截取一张文档的截图或标志的照片。噪声越多，你越能体会到准确率的提升。

---

## 第一步：添加 Aspose OCR 依赖

首先——将 Aspose OCR 库添加到你的 `pom.xml` 中。这一行代码会拉取最新版本（截至 2026 年 3 月）并解析所有传递依赖。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **为什么这很重要：**没有此库你无法创建 `OcrEngine`，整个 **对图像执行 OCR** 工作流将在运行时崩溃。

---

## 第二步：初始化 OCR 引擎

创建引擎很简单，但将初始化与识别调用分离有一个微妙的原因：它为你提供了调整语言、DPI，或对我们最重要的拼写纠正等设置的空间。

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

请注意注释——当你的 PNG 包含非英文字符时，设置语言可以救命。  

---

## 第三步：启用拼写纠正以**提升 OCR 准确率**

Aspose OCR 自带内置的拼写纠正模块，像轻量级词典一样工作。打开它只需一行代码，但对最终输出的影响可能非常大，尤其是对噪声图像。

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **如果你不需要它怎么办？**只需将标志设为 `false`。在领域特定文本中禁用它可能有用，因为词典会把合法术语误判为错误。

---

## 第四步：加载并识别 PNG

现在我们真正从文件中**读取图像文本**。`recognizeImage` 方法接受路径字符串，但如果你从数据库或网络获取图像，也可以传入 `java.io.InputStream`。

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

如果文件未找到，Aspose 会抛出描述性异常——你无需手动检查 `File.exists()`。不过，像我们这样将调用包装在 `try/catch` 中，可以为最终用户提供清晰的错误信息。

---

## 第五步：输出纠正后的文本

最后，将结果打印到控制台。在真实应用中，你可能会将其写入数据库或下游服务，但控制台非常适合快速演示。

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**预期输出**（假设 PNG 包含短语 “Aspose OCR library” 且有一些噪声）：

```
Corrected text:
Aspose OCR library
```

如果禁用拼写纠正，你可能会看到类似 “Asp0se OCR libr@ry” 的结果——这正说明了 **提升 OCR 准确率** 的重要性。

---

## 第六步：验证结果 —— 它真的**读取图像文本**吗？

盲目信任控制台输出很诱人，但快速的合理性检查可以为你省下数小时。以下是几种验证提取文本的方法：

1. **长度检查** – 将 `ocrResult.getText().length()` 与预期字符数进行比较。  
2. **关键字搜索** – 使用 `String.contains("Aspose")` 确保关键词出现。  
3. **单元测试** – 如果将其集成到更大的系统中，编写 JUnit 测试，断言输出与已知正确值匹配。

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## 常见边缘情况及处理方法

| 情况 | 为什么会发生 | 快速解决方案 |
|-----------|----------------|-----------|
| **文件未找到** | 路径错误或缺少权限 | 在调用 `recognizeImage` 前验证 `imagePath` 并使用 `Files.isReadable(Paths.get(imagePath))`。 |
| **不支持的格式** | Aspose OCR 支持 PNG、JPEG、BMP、TIFF 等 | 先将图像转换为 PNG（例如使用 ImageIO），或使用 `ocrEngine.recognizeImage(InputStream)`。 |
| **DPI 极低** | OCR 引擎至少需要约 300 DPI 才能获得不错的准确率 | 在送入引擎前使用 `BufferedImage` 和 `Graphics2D` 放大图像。 |
| **领域特定术语** | 拼写纠正可能会把有效术语替换为词典单词 | 禁用拼写纠正 (`setEnableSpellCorrection(false)`) 或通过 `ocrEngine.getRecognitionSettings().setCustomDictionary(...)` 提供自定义词典。 |

---

## 完整可运行示例（复制粘贴即用）

下面是完整的源文件，已准备好编译运行。将 `YOUR_DIRECTORY/noisy-image.png` 替换为你的测试图像的实际路径。

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

使用以下方式运行：

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

你应该会看到打印出的**纠正后文本**，这表明你已成功**对图像执行 OCR**。

---

## 可视化摘要

![Perform OCR on image example](/images/ocr-example.png){alt="执行 OCR 示例 – 拼写纠正前后"}

该截图左侧显示噪声 PNG，右侧显示干净且经过拼写纠正的输出。

---

## 结论

我们刚刚完整演示了如何使用 Aspose OCR for Java **对图像执行 OCR** 的端到端解决方案。通过启用内置的拼写纠正标志，你可以 **提升

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}