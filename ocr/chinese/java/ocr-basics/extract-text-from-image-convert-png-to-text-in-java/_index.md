---
category: general
date: 2026-10-30
description: 使用 Aspose OCR Java 从图像中提取文本 – 学习如何将 PNG 转换为文本，加载图像进行 OCR，并遵循 Java OCR
  教程。
draft: false
keywords:
- convert png to text
- ocr image to text
- extract text from png
- aspose ocr java
- extract text image java
lastmod: 2026-10-30
og_description: 使用 Aspose OCR Java 从图像中提取文本。遵循此分步 Java OCR 教程，将 PNG 转换为文本，加载图像进行 OCR，并高效处理多语言内容。
og_image_alt: Screenshot of Java OCR code converting PNG to text using Aspose OCR
og_title: 使用 Java OCR 将 PNG 转换为文本 – Aspose 指南
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: extract text from image using Aspose OCR Java – learn how to convert
    PNG to text, load image for OCR, and follow a java ocr tutorial.
  headline: Extract text from image – convert PNG to text in Java
  type: TechArticle
- questions:
  - answer: Yes, a commercial license is required for production use; a free trial
      is available for evaluation.
    question: Can I use Aspose OCR in a commercial application without extra licensing
      fees?
  - answer: Absolutely. The library includes language packs for Arabic, Hebrew, Persian,
      and other RTL scripts.
    question: Does Aspose OCR support right‑to‑left scripts such as Arabic or Hebrew?
  - answer: Aspose OCR can process images up to 10 000 × 10 000 pixels using streaming
      mode, which keeps memory usage under 200 MB.
    question: How large of an image can the engine handle?
  - answer: Yes, `OcrResult.getWords()` returns a collection where each word has a
      `getConfidence()` method.
    question: Is there a way to get confidence scores for each recognized word?
  - answer: The library supports JDK 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 从图像中提取文本 – 在 Java 中将 PNG 转换为文本
url: /zh/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 将 PNG 转换为文本（Java）

是否曾经需要**从图像中提取文本**，但不确定哪个库可以让你轻松实现？你并非唯一——开发者经常问：“如何在 Java 中将 PNG 转换为文本？”好消息是 Aspose OCR 让整个过程如同散步般轻松。在本指南中，我们将完整演示**java ocr tutorial**，展示如何**load image for OCR**，并得到干净、可搜索的文本。

我们将涵盖从设置引擎到处理多语言内容的所有内容，最终你将能够**convert PNG to text** 任意大小、格式或语言的文件。无需外部服务，无需 API 密钥——只需一个 JAR 和几行代码。

## 快速回答
- **什么库可以在 Java 中将 PNG 转换为文本？** Aspose OCR for Java.  
- **进行基本转换需要多少行代码？** 添加库后大约五行代码。  
- **Aspose OCR 是否支持除英语之外的语言？** 是的——超过 70 种语言包，包括高棉语、中文、阿拉伯语等。  
- **我可以离线运行 OCR 引擎吗？** 当然；引擎完全在本地运行，无需互联网连接。  
- **需要哪个 Java 版本？** JDK 8 或更高；JDK 11+ 完全受支持。  

## 什么是将 PNG 转换为文本？
**Convert PNG to text** 指的是提取 PNG 图像内部出现的文本字符，并将其转换为可编辑、可搜索或可存储的纯文本字符串。此过程通常称为光学字符识别（OCR）。它通过分析像素模式并与特定语言的词典匹配，实现对扫描文档、截图或任何包含可读文本的位图的转换为可编辑数据。

## 为什么使用 Aspose OCR for Java？
Aspose OCR 支持 **50+ 输入格式**（包括 PNG、JPEG、BMP、TIFF），并且能够在不将整个文件加载到内存的情况下处理 **数百页文档**，这得益于其流式架构。该库提供 **70+ 语言包**，在高分辨率扫描上可实现高达 **95 % 的准确率**，并且每月都会更新，添加新脚本和性能改进。

## 您需要的准备
- 已安装 JDK 8 或更高版本（代码在 JDK 11+ 上也可运行）。  
- 使用 Maven 或 Gradle 拉取 Aspose OCR 库，或可从 Aspose 网站手动下载 JAR。  
- 一张包含可读文本的 PNG 图像（示例中使用 `khmer-sign.png`）。  
- 您熟悉的 IDE 或文本编辑器——IntelliJ IDEA、Eclipse、VS Code，任意均可。

就这么简单。无需重量级框架，无需云凭证。准备好了吗？让我们开始从图像文件中提取文本。

## 如何将 Aspose OCR 添加到项目中？
将 OCR 引擎添加到构建配置中，使类在编译时可用。此步骤确保 Aspose OCR JAR 及其依赖项被正确引用，允许在 Java 源文件中导入所需的包。声明依赖后，Maven 或 Gradle 将从中央仓库下载库并放置在类路径上，以供编译和运行时使用。

**Maven** – add this dependency to `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

**Gradle** – add the following line to your `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

如果你更喜欢手动方式，可从 Aspose 下载页面获取 JAR 并放入项目的 `libs` 文件夹，然后将其添加到构建路径中。

> **专业提示：** 始终选择最新的稳定版本；旧版可能缺少语言包或错误修复。

## 如何创建 OCR 引擎实例？
OcrEngine 是执行 OCR 识别的核心类。它封装了将图像像素转换为文本所需的所有内部缓冲区、语言数据和处理设置。为每次操作创建全新的实例可保证结果确定，尤其是在不同运行之间切换语言或处理模式时。

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

为什么每次都创建新的引擎？因为引擎会缓存语言词典；重置它可防止不同语言扫描之间的交叉污染。

## 如何启用所需语言（可选但推荐）？
OcrLanguage 表示引擎在识别期间使用的特定语言词典。选择合适的语言可缩小搜索空间，加快处理速度，并通过聚焦图像中预期的字符集提升准确率。

`OcrLanguage` 表示特定语言词典。在我们的示例中我们将启用高棉语（`khm`），但你可以将其替换为 `ENG`（英语）、`CHN`（中文）等。

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **为何重要：** 当你**load image for OCR** 时，引擎只会搜索已启用的语言词典。保持所有语言开启会降低速度并增加误报。

## 如何加载图像进行 OCR – 将 PNG 转换为文本
ImageStream 是一个包装器，用于将图像文件读取为与 OCR 引擎兼容的流，并自动处理格式检测。它抽象了底层 I/O，使你能够向引擎传递一个简单对象，而无需担心文件处理细节。

`ImageStream` 是一个包装器，用于将图像文件读取为与 OCR 引擎兼容的流，并自动处理格式检测。

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

如果你的图像是其他格式（JPEG、BMP、TIFF），同样的方法也适用——Aspose 会自动检测格式。只需确保文件路径正确，否则会抛出 `FileNotFoundException`。

## 如何运行 OCR 过程并将 PNG 转换为文本？
OcrResult 保存识别操作的结果，包括提取的文本以及每个字符或单词的置信度指标。调用引擎的 `recognize()` 方法后，你会得到一个 OcrResult 对象，可查询原始字符串及其他细节。

`ocrEngine.recognize()` 返回一个 `OcrResult`，其中包含 `getText()` 用于获取提取的字符串，以及 `getConfidence()` 用于获取每个字符的置信度指标。

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

就这样——你已经**convert PNG to text**。返回的字符串可能包含与引擎看到的完全相同的换行和空白。你可以使用 `trim()`、`replaceAll("\\s+", " ")` 或其他任何清理方法进行后处理。

## 如何输出结果（或存储）？
Result 是 OcrResult 的实例，通过 `getText()` 提供识别的文本。将结果打印到控制台是快速验证 OCR 成功的方式，而在生产环境中，你可能会将文本写入文件、数据库或其他服务。

`System.out.println(result.getText());` 打印提取的文本。

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**预期输出**（针对提供的高棉标志）可能如下：

```
សួស្តី
Welcome
```

如果输出乱码，请再次确认在步骤 3 中启用了正确的语言，并且图像不太模糊。提高图像分辨率（例如使用 300 dpi 扫描）通常有帮助。

## 完整工作示例是什么样的？
下面是一个独立的 Java 程序，演示了从添加依赖到打印 OCR 结果的每一步。类 `ExtractTextExample` 包含一个 `main` 方法，创建引擎、设置语言、加载图像、运行识别并输出文本。你可以将此代码复制粘贴到名为 `ExtractTextExample.java` 的文件中直接运行。

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

使用以下方式运行程序：

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

或者，如果你使用 Gradle：

```bash
./gradlew run --args='ExtractTextExample'
```

你应该在控制台看到提取的文本，确认已成功使用 Aspose OCR **extract text from image**。

## 常见陷阱及解决方法
| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 返回空字符串 | 未启用语言或语言代码错误 | 添加适当的 `OcrLanguage`（例如 `ENG` 表示英语）。 |
| 字符乱码 | 图像分辨率太低或背景噪声 | 使用更高分辨率的源，或使用锐化滤波器进行预处理。 |
| `OutOfMemoryError` | 加载了全尺寸的超大图像 | 在将图像提供给引擎之前进行降尺度处理（`ImageStream.fromFile(...).scale(0.5)`）。 |
| `FileNotFoundException` | 路径不正确 | 验证绝对或相对路径；使用 `Paths.get(...).toAbsolutePath()`。 |

> **记住：** OCR 是一种概率过程。即使设置完美，也可能需要手动纠正少量字符，尤其是手写体脚本。

## 完成本教程后可以进行的后续步骤
- **批量处理：** 遍历 PNG 文件目录，对每个图像调用相同逻辑。  
- **PDF 输出：** 使用 Aspose PDF 将提取的文本嵌入可搜索的 PDF 中。  
- **语言检测：** 在设置语言之前调用 `ocrEngine.detectLanguage()`，让引擎自动猜测。  
- **云集成：** 将代码包装为 REST 接口，让微服务调用以实现可扩展的 OCR 服务。  

所有这些主题都自然地基于我们刚完成的 **java ocr tutorial**，展示了 Aspose OCR API 的多功能性。

## 常见问题

**Q: 我可以在商业应用中使用 Aspose OCR 而无需额外的授权费用吗？**  
A: 可以，生产使用需要商业许可证；提供免费试用供评估。

**Q: Aspose OCR 是否支持从右到左的脚本，如阿拉伯语或希伯来语？**  
A: 当然。该库包含阿拉伯语、希伯来语、波斯语以及其他 RTL 脚本的语言包。

**Q: 引擎能处理多大的图像？**  
A: Aspose OCR 在流式模式下可处理最高 10 000 × 10 000 像素的图像，内存使用保持在 200 MB 以下。

**Q: 是否有办法获取每个识别单词的置信度分数？**  
A: 有，`OcrResult.getWords()` 返回一个集合，每个单词都有 `getConfidence()` 方法。

**Q: 官方支持哪些 Java 版本？**  
A: 该库支持 JDK 8、11、17 以及后续的 LTS 版本。

## 结论
我们已经完整演示了一个 **java ocr tutorial**，让你能够使用 Aspose OCR **extract text from image** 文件、**convert PNG to text**，并正确 **load image for OCR**。步骤简明：添加库、创建引擎、启用正确语言、加载 PNG、运行 `recognize()`，并处理输出。凭借此基础，你可以实现数据录入自动化、构建可搜索档案，或为任何需要从图片获取机器可读文本的应用提供支持。

尝试使用自己的图像——比如收据截图或扫描的合同。调整语言设置，尝试不同分辨率，你会快速体会到该方案的灵活性。如果遇到问题，重新查看陷阱表或查阅 Aspose 官方文档；文档详尽且保持最新。

祝编码愉快，愿你的下一个项目充满干净、可搜索的文本！

---

**最后更新：** 2026-10-30  
**测试版本：** Aspose OCR for Java 24.10  
**作者：** Aspose

## 相关教程

- [从图像中提取文本 Java 加载图像进行 OCR](/ocr/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/)
- [Aspose OCR Java 示例 快速将图像转换为文本](/ocr/java/ocr-operations/aspose-ocr-java-example-convert-image-to-text-fast/)
- [Java 批量图像 OCR 快速从 PNG 文件提取文本](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}