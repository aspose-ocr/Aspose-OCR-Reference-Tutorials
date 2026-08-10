---
category: general
date: 2026-02-19
description: 使用 Aspose OCR Java 从图像中提取文本——学习如何将 PNG 转换为文本，加载图像进行 OCR，并遵循 Java OCR
  教程。
draft: false
keywords:
- extract text from image
- convert png to text
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- OCR language support
language: zh
og_description: 使用 Aspose OCR Java 从图像中提取文本。按照此分步 Java OCR 教程将 PNG 转换为文本并加载图像进行 OCR。
og_title: 从图像提取文本 – Java OCR指南
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 从图像中提取文本——在 Java 中将 PNG 转换为文本
url: /zh/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – Java OCR 教程

是否曾经需要 **extract text from image**，但不确定哪个库可以让你轻松实现，而不必费力？你并不是唯一的——开发者们经常问：“如何在 Java 中将 PNG 转换为文本？”好消息是，Aspose OCR 让整个过程轻而易举。在本指南中，我们将完整演示一个 **java ocr tutorial**，展示如何 **load image for OCR**，并最终得到干净、可搜索的文本。

我们将覆盖从设置引擎到处理多语言内容的所有步骤，结束时你将能够从任何尺寸、格式或语言的 **extract text from image** 文件中提取文本。无需外部服务，无需 API 密钥——只需一个 JAR 和几行代码。

## 您需要的条件

在开始之前，请确保您拥有：

- 已安装 JDK 8 或更高版本（代码在 JDK 11+ 上也可运行）。
- Maven 或 Gradle 用于获取 Aspose OCR 库，或者也可以手动从 Aspose 网站下载 JAR。
- 一张包含可读文字的 PNG 图像（本例中使用 `khmer-sign.png`）。
- 您熟悉的 IDE 或文本编辑器——IntelliJ IDEA、Eclipse、VS Code，任意一种均可。

就这些。没有重量级框架，没有云凭证。准备好了吗？让我们开始从图像文件中提取文本吧。

## 步骤 1：将 Aspose OCR 添加到项目中

首先——你需要在类路径上加入 OCR 引擎。如果使用 Maven，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

或者使用 Gradle：

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

如果你更喜欢手动方式，可从 Aspose 下载页面获取 JAR 并放入项目的 `libs` 文件夹，然后将其加入构建路径。

> **Pro tip:** 始终选择最新的稳定版本；旧版本可能缺少语言包或 bug 修复。

## 步骤 2：创建 OCR 引擎实例

现在库已经可用，我们可以实例化一个 `OcrEngine`。可以把引擎想象成读取像素并将其转换为字符的大脑。

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

为什么每次都要创建一个全新的引擎？引擎内部会持有缓冲区和语言数据；每次从干净状态开始可以保证结果确定，尤其是在后期切换语言时。

## 步骤 3：启用所需语言（可选但推荐）

Aspose OCR 附带数十种语言包。如果你知道源图像的语言，显式启用它可以加快识别速度并提升准确率。示例中我们启用高棉语 (`khm`)，你也可以改为 `ENG`（英语）、`CHN`（中文）等。

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **Why this matters:** 当你 **load image for OCR** 时，引擎只会搜索已启用的语言词典。保持所有语言都开启会降低速度并增加误报。

## 步骤 4：加载图像进行 OCR – 将 PNG 转换为文本

这里就是执行 **load image for OCR** 步骤的地方。Aspose 提供了便利的 `ImageStream.fromFile` 辅助方法，屏蔽了底层 I/O 细节。

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

如果你的图像是其他格式（JPEG、BMP、TIFF），同样的方法也适用——Aspose 会自动检测格式。只需确保文件路径正确，否则会抛出 `FileNotFoundException`。

## 步骤 5：运行 OCR 过程并将 PNG 转换为文本

引擎准备好且图像已加载后，实际识别只需一次方法调用。返回的结果对象提供原始字符串以及置信度分数。

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

就这样——你已经 **convert PNG to text**。返回的字符串可能包含换行和空白，完全按照引擎看到的方式。你可以使用 `trim()`、`replaceAll("\\s+", " ")` 或其他清理方式进行后处理。

## 步骤 6：输出结果（或存储）

为了快速验证，可将结果打印到控制台。在真实应用中，你可能会将其写入文件、数据库，或传递给其他服务。

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**Expected output**（针对提供的高棉语标志）可能如下所示：

```
សួស្តី
Welcome
```

如果输出乱码，请再次确认在步骤 3 中启用了正确的语言，并确保图像足够清晰。提升图像分辨率（例如使用 300 dpi 扫描）通常能改善效果。

## 完整工作示例

将所有代码片段组合起来，下面是一个可直接复制粘贴到 `ExtractTextExample.java` 并运行的自包含程序：

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

使用以下命令运行程序：

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

或者，如果你使用 Gradle：

```bash
./gradlew run --args='ExtractTextExample'
```

运行后，你应该会在控制台看到提取的文本，证明你已经成功使用 Aspose OCR **extract text from image**。

## 常见问题及解决方案

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| 返回空字符串 | 未启用语言或语言代码错误 | 添加相应的 `OcrLanguage`（例如 `ENG` 表示英语）。 |
| 字符乱码 | 图像分辨率太低或背景噪声 | 使用更高分辨率的源图像，或使用锐化滤波器进行预处理。 |
| `OutOfMemoryError` | 加载了全尺寸的超大图像 | 在送入引擎前缩小图像（`ImageStream.fromFile(...).scale(0.5)`）。 |
| `FileNotFoundException` | 路径不正确 | 检查绝对或相对路径；使用 `Paths.get(...).toAbsolutePath()`。 |

> **Remember:** OCR 是一种概率过程。即使设置完美，你仍可能需要手动纠正少量字符，尤其是手写或草体文字。

## 扩展教程 – 后续步骤

- **批量处理：**遍历 PNG 文件目录，对每个图像调用相同的逻辑。  
- **PDF 输出：**使用 Aspose PDF 将提取的文本嵌入可搜索的 PDF 中。  
- **语言检测：**在设置语言前调用 `ocrEngine.detectLanguage()`，让引擎自动判断。  
- **云集成：**如果需要扩展，可将代码封装为 REST 接口，让微服务调用。

所有这些主题都自然地建立在我们刚完成的 **java ocr tutorial** 基础上，展示了 Aspose OCR API 的多才多艺。

## 结论

我们已经完整演示了一个 **java ocr tutorial**，让你能够使用 Aspose OCR **extract text from image** 文件、**convert PNG to text**，并正确 **load image for OCR**。步骤非常直接：添加库、创建引擎、启用正确语言、加载 PNG、调用 `recognize()`，然后处理输出。基于此，你可以实现数据录入自动化、构建可搜索档案，或为任何需要从图片中获取机器可读文本的应用提供支持。

尝试使用你自己的图像吧——比如收据的截图或扫描的合同。调节语言设置，实验不同分辨率，你会快速体会到该方案的灵活性。如果遇到问题，回顾上表或查阅 Aspose 官方文档；文档完整且保持最新。

祝编码愉快，愿你的下一个项目充满干净、可搜索的文本！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}