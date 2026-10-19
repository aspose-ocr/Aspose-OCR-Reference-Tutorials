---
category: general
date: 2026-05-25
description: 如何在 Java 中实现 OCR 并从图像中提取原始文本。学习如何关闭拼写校正、识别手写文本以及如何高效加载图像。
draft: false
keywords:
- how to get ocr
- extract raw text
- turn off spell correction
- recognize handwritten text
- how to load image
language: zh
og_description: 如何在 Java 中实现 OCR 并从图像中提取原始文本。本指南展示了如何关闭拼写纠正、识别手写文本以及正确加载图像。
og_title: 如何在 Java 中获取 OCR——逐步提取原始文本
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  headline: How to Get OCR in Java – Complete Guide to Extract Raw Text
  type: TechArticle
- description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  name: How to Get OCR in Java – Complete Guide to Extract Raw Text
  steps:
  - name: Maven Dependency
    text: If you’re using Maven, paste this into your `pom.xml`. It pulls the latest
      Aspose.OCR library (as of May 2026).
  - name: Gradle Alternative
    text: '```gradle implementation ''com.aspose:aspose-ocr:23.11'' ```'
  - name: Expected Output
    text: 'Assuming `handwritten.png` contains the phrase *“Hello World”* written
      in cursive, you’ll see something like:'
  type: HowTo
tags:
- OCR
- Java
- Aspose.OCR
title: 如何在 Java 中实现 OCR – 提取原始文本的完整指南
url: /zh/java/advanced-ocr-techniques/how-to-get-ocr-in-java-complete-guide-to-extract-raw-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中获取 OCR – 提取原始文本的完整指南

是否曾经想过 **如何获取 OCR** 结果而不使用库的自动清理？也许你正在处理手写笔记，需要引擎看到的精确字符，而不是“美化”后的版本。在本教程中，我们将通过一个动手示例，准确展示 **如何获取 OCR** 输出、如何 **提取原始文本**，以及在识别手写文本时为何可能需要 **关闭拼写校正**。最后，你还将了解 **如何加载图像** 文件到 Aspose OCR 引擎而不出错。

我们将使用 Aspose.OCR for Java，但这些概念同样适用于任何提供拼写校正开关的 OCR SDK。无需深奥理论——只要一个实用的、可直接复制粘贴的解决方案，今天即可运行。

---

## 你将学到的内容

- 如何在 Java 项目中设置 Aspose.OCR  
- 获取 **OCR 原始输出** 的确切步骤  
- 为什么以及 **如何关闭拼写校正** 以获得纯净文本  
- 最佳的 **如何加载图像** 文件方式，以实现最佳识别  
- 如何 **识别手写文本** 并验证结果  

先决条件非常少：已安装 Java 8+，以及兼容 Maven 的 IDE（IntelliJ、Eclipse 或 VS Code），还有一张包含手写字符的示例图片。如果缺少任何一个，只需从 Oracle 下载 JDK，并从手机获取图片——毫无问题。

![展示 OCR 工作流的图示，显示如何从图像获取 OCR 原始文本](/images/ocr-workflow.png){: .center alt="获取 OCR 原始文本工作流"}

---

## 第一步：将 Aspose.OCR 添加到项目中

### Maven 依赖

如果你使用 Maven，请将以下内容粘贴到 `pom.xml` 中。它会拉取最新的 Aspose.OCR 库（截至 2026 年 5 月）。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **专业提示：** 始终检查官方 Aspose Maven 仓库以获取更新的版本。`23.11` 版本增加了对连笔脚本的更好支持，这在 **识别手写文本** 时非常有用。

### Gradle 替代方案

```gradle
implementation 'com.aspose:aspose-ocr:23.11'
```

依赖解析完成后，你就可以编写实际 **获取 OCR** 结果的代码了。

---

## 第二步：创建 OCR 引擎实例

引擎是整个过程的核心。实例化它很简单，但真正的魔法在于配置它时开始显现。

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

为什么需要一个专用的 `OcrEngine` 对象？它存储所有运行时选项，包括我们接下来要使用的拼写校正开关。将引擎隔离还能让你并行运行多个识别任务而不会相互污染。

---

## 第三步：关闭拼写校正（如果需要原始输出）

大多数 OCR 库会自动纠正拼写错误，这对印刷文本很有帮助，但对原始数据提取却是灾难。以下是 **关闭拼写校正** 的方法：

```java
        // Step 3: Turn off the built‑in spell‑corrector to get raw text
        engine.getEngineOptions().setSpellCorrectorEnabled(false);
```

当该标志为 `false` 时，引擎会返回位图上看到的内容，保留换行、标点，甚至偶尔的杂散字符。这在你随后将输出喂入期望原始噪声的机器学习流水线时至关重要。

---

## 第四步：加载图像——正确方式

你可能认为 `engine.getImage().loadFromFile("path")` 已足够，但还有一些细节需要注意：

1. **绝对路径与相对路径** – 使用 `Paths.get(...)` 以实现平台无关性。  
2. **支持的格式** – Aspose.OCR 支持 PNG、JPEG、BMP、TIFF 和 GIF。  
3. **分辨率重要** – 更高的 DPI 能带来更好的识别效果，尤其是对连笔书写。

下面是一个稳健的代码片段，演示了 **如何安全加载图像**：

```java
        // Step 4: Load the image that contains handwritten text
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        // Validate the file exists
        java.nio.file.Path path = java.nio.file.Paths.get(imagePath);
        if (!java.nio.file.Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }

        // Load the image into the OCR engine
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());
```

如果你处理的是流（例如，从网页表单上传），请将 `loadFromFile` 替换为 `loadFromStream`。关键要点：在将文件交给引擎之前务必先验证文件是否存在，因为缺失的文件会抛出模糊的 `NullPointerException`，难以调试。

---

## 第五步：执行识别

现在真相时刻到来——**如何获取 OCR** 结果。`recognize()` 方法会运行内部流水线，应用语言模型、分割以及（如果启用）拼写校正。由于我们已关闭它，你将得到未处理的字符。

```java
        // Step 5: Perform OCR recognition
        OcrResult result = engine.recognize();
```

`OcrResult` 对象不仅包含文本，还可以获取置信度分数、边界框，甚至每个字符的概率。本文教程将重点关注纯文本。

---

## 第六步：输出原始 OCR 结果

最后，将结果打印到控制台。这是 **提取原始文本** 用于调试或下游处理的最简方式。

```java
        // Step 6: Output the raw OCR result
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

### 预期输出

假设 `handwritten.png` 包含以连笔书写的短语 *“Hello World”*，你将看到类似如下的输出：

```
Raw OCR output:
H e l l o   W o r l d
```

注意额外的空格——这是有意为之，因为引擎保留了检测到的精确间距。如果之后需要合并空白，请在自己的后处理步骤中完成。

---

## 常见陷阱及避免方法

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **空字符串** | 图像 DPI 太低或图像完全是白色。 | 确保源图像至少为 300 DPI；使用 `engine.getImage().setResolution(300, 300)`。 |
| **乱码字符** | 文件格式错误或字节损坏。 | 使用图像查看器检查文件；重新导出为 PNG。 |
| **拼写校正仍然启用** | 代码其他位置意外重新启用了拼写校正。 | 在创建引擎后立即保持调用 `setSpellCorrectorEnabled(false)`。 |
| **手写文本未被识别** | 引擎默认语言设置为英文印刷文本。 | 调用 `engine.getEngineOptions().setLanguage(Language.English);`，并可选调用 `engine.getEngineOptions().setUseDictionary(false);`。 |

---

## 扩展示例：识别手写文本

如果你的使用场景专门针对 **识别手写文本**，可以调整几个选项以提升准确率：

```java
        // Enable handwritten mode (available in 23.11+)
        engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);
```

这会指示内部神经网络更倾向于连笔模式而非印刷字形。实际使用中，你会看到签名、笔记或快速草图的置信度分数显著提升。

---

## 完整工作示例（可直接复制粘贴）

下面是完整的、独立的 Java 类，包含我们讨论的所有步骤。只需将 `YOUR_DIRECTORY/handwritten.png` 替换为你自己的图像路径，然后运行即可。

```java
import com.aspose.ocr.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Turn off spell correction to get raw output
        engine.getEngineOptions().setSpellCorrectorEnabled(false);

        // Optional: set handwritten mode if needed
        // engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);

        // 3️⃣ Load the image (how to load image safely)
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        Path path = Paths.get(imagePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());

        // 4️⃣ Perform OCR (how to get OCR raw text)
        OcrResult result = engine.recognize();

        // 5️⃣ Print raw result (extract raw text)
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

使用以下方式运行：

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectDemo
```

你应该会看到原始字符，完全按照引擎读取的顺序打印出来。

---

## 结论

我们已经介绍了在 Java 中 **获取 OCR** 原始结果的方法，演示了正确的 **关闭拼写校正** 方式，展示了最佳实践 **如何加载图像**，并解释了 **识别手写文本** 的细微差别。遵循这些步骤，你就能可靠地 **提取原始文本**，无论是构建文档数字化流水线、取证分析工具，还是简单的记事应用。

接下来，你可能想探索：

- **后处理**：去除空白、规范化 Unicode，或将输出喂入语言模型。  
- **批处理**：遍历图像目录并将结果存入数据库。  
- **高级选项**：调整 `EngineOptions` 以支持多语言或自定义词典。

尝试这些吧，并随时在评论中留下你的问题。祝编码愉快，愿你的 OCR 永远精准！

## 相关教程

- [使用 Aspose.OCR 按语言 OCR 图像文本](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [使用 Aspose.OCR 检测区域模式从图像提取文本（Java）](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose OCR 识别文本图像 – 完整 Java OCR 教程](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}