---
category: general
date: 2026-03-28
description: 学习如何使用 Aspose OCR 在 Java 中识别 PNG 图像中的文本。包括从图像中提取文本以及为混合语言启用自动语言检测。
draft: false
keywords:
- recognize text from png
- extract text from image
- enable auto language detection
language: zh
og_description: 即时识别 PNG 中的文字。本指南展示如何从图像中提取文字，并为混合语言的 PDF 启用自动语言检测。
og_title: 使用 Aspose OCR 从 PNG 识别文本 – 完整 Java 教程
tags:
- Aspose OCR
- Java
- Image Processing
title: 使用 Aspose OCR 识别 PNG 文本 – 完整 Java 指南
url: /zh/java/ocr-operations/recognize-text-from-png-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 识别 PNG 文本 – 完整 Java 教程

是否曾需要 **从 png 中识别文本**，但不确定哪个库能够优雅地处理混合语言？你并不孤单——许多开发者在需要读取收据、护照或多语言标识时都会遇到这个难题。

好消息是 Aspose OCR 让这变得轻而易举：只需几行代码即可 **从图像中提取文本**，将 PNG 转换为可搜索的数据，甚至 **启用自动语言检测**，让引擎能够实时选择正确的文字脚本。

在本教程中，我们将逐步演示你需要的全部内容：前置条件、一步步的代码、每个设置的意义以及如何验证输出。完成后，你将拥有一个可运行的 Java 程序，能够读取包含英文、俄文和中文的 PNG——无需手动切换语言包。

---

## 你需要准备的东西

- **Java Development Kit (JDK) 8+** – 代码可在任何近期的 JDK 上编译。
- **Aspose.OCR for Java** 库（截至 2026 年的最新版本）。可从 Maven Central 或 Aspose 官网获取。
- 一张图像文件（例如 `mixed-lang.png`），其中包含多种语言的文本。
- 一个不错的 IDE（IntelliJ IDEA、Eclipse，甚至 VS Code）——普通文本编辑器也可以。

> **专业提示：** 如果使用 Maven，请在下面添加依赖；否则下载 JAR 并加入到类路径中。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the newest version -->
</dependency>
```

---

## 第一步：初始化 OCR 引擎以识别 png 中的文本

在引擎能够工作之前，需要创建一个 `OcrEngine` 实例。该对象保存所有配置选项并执行繁重的识别工作。

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine – this is the entry point for all operations
        OcrEngine ocrEngine = new OcrEngine();

        // --------------------------------------------------------------
        // Step 2 and 3 are configured here (see next sections)
        // --------------------------------------------------------------

        // Recognize the image and get the result object
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **为什么重要：** `OcrEngine` 抽象了底层 OCR 算法。一次实例化后在多张图片之间复用，比对每个文件重新创建引擎更高效。

---

## 第二步：启用自动语言检测

如果跳过此步骤，引擎会默认使用单一语言（通常是英文），导致西里尔字母或中文字符出现乱码。打开自动检测后，Aspose 会扫描图像并自动选择最佳语言模型。

```java
// Enable automatic language detection – the engine will sniff the script
ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);
```

> **内部原理是什么？** Aspose OCR 会进行轻量级的预分析，检查字符频率和 Unicode 区间。当检测到占主导的语言时，会在正式 OCR 之前切换到对应的语言模型。

---

## 第三步：（可选）限制检测语言以提升速度

如果你已经知道可能出现的语言集合，可以给引擎一个提示。这会缩小搜索空间，降低 CPU 使用率，并通常带来更快的结果。

```java
// Suggest candidate languages – only English, Russian, and Chinese will be considered
ocrEngine.getRecognitionSettings()
         .setCandidateLanguages(new String[] { "en", "ru", "zh" });
```

> **提示：** 若省略此步骤，引擎仍能工作，只是会评估所有受支持的语言，在大批量处理时可能会多耗几秒。

---

## 第四步：识别 PNG 并从图像中提取文本

引擎配置完成后，调用 `recognizeImage`。该方法接受文件路径、`java.io.File`，甚至 `java.io.InputStream`，为网页上传或云存储提供了灵活性。

```java
// Perform OCR on the specified PNG file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

// The result object holds the raw text, confidence scores, and layout info
String extractedText = ocrResult.getText();
```

> **边缘情况：** 若图像被旋转，Aspose OCR 能自动旋转。若发现输出倾斜，也可以手动设置 `setDetectOrientation(true)`。

---

## 第五步：显示结果 – 验证输出

在控制台打印足以演示，但在实际应用中，你可能会将文本存入数据库、写入搜索索引，或通过 REST API 返回。下面是一个最小化的验证代码片段。

```java
System.out.println("=== Recognized Text ===");
System.out.println(extractedText);
```

### 预期的控制台输出

假设 `mixed-lang.png` 包含以下三行：

```
Hello world!
Привет мир!
你好，世界！
```

你应该看到类似的结果：

```
=== Recognized Text ===
Hello world!
Привет мир!
你好，世界！
```

如果输出出现乱码，请再次确认已启用 `setAutoDetectLanguage(true)`，并且候选语言列表中包含所需的文字脚本。

---

## 完整工作示例（所有步骤合并）

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);

        // Step 3: (Optional) Limit detection to likely languages
        ocrEngine.getRecognitionSettings()
                 .setCandidateLanguages(new String[] { "en", "ru", "zh" });

        // Step 4: Recognize the PNG image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **运行方式：** 使用 `javac MixedLangExample.java` 编译，然后执行 `java MixedLangExample`。确保 Aspose OCR JAR 已加入类路径（例如 Windows 上 `-cp aspose-ocr-23.12.jar;.`，Linux/macOS 上 `-cp aspose-ocr-23.12.jar:.`）。

---

## 常见问题与注意事项

| Question | Answer |
|----------|--------|
| **如果我的图像是 JPEG 而不是 PNG，怎么办？** | 同样的 `recognizeImage` 方法支持 JPEG、BMP、TIFF 等，只需更换文件扩展名即可。 |
| **能否处理来自 HTTP 请求的流？** | 完全可以。使用 `recognizeImage(InputStream)`，直接传入请求的输入流。 |
| **自动语言检测在相似脚本（如塞尔维亚西里尔文 vs 俄文）上的准确度如何？** | 通常非常准确，但你可以通过向 `candidateLanguages` 添加目标语言并移除其他语言来强制指定。 |
| **使用 Aspose OCR 是否需要许可证？** | 免费评估许可证可用于测试，生产环境需购买许可证以去除水印并解锁全部功能。 |
| **大批量处理的性能如何？** | 重复使用同一个 `OcrEngine` 实例，并顺序或使用线程池处理图片。引擎对只读操作是线程安全的。 |

---

## 后续步骤与相关主题

- **从 PDF 文件中的图像提取文本** – 将 Aspose PDF 与 OCR 结合，处理扫描文档。  
- **批量处理** – 使用 Java 的 `ExecutorService` 并行处理成千上万的 PNG。  
- **后处理** – 在提取后进行拼写检查或语言特定的分词。  
- **与云存储集成** – 直接从 AWS S3 或 Azure Blob Storage 读取 PNG，使用流式方式处理。

欢迎自行实验：如果扫描件有旋转，可尝试添加 `setDetectOrientation(true)`；或者在候选语言列表中加入日语 (`"ja"`) 或阿拉伯语 (`"ar"`)。API 足够灵活，能满足大多数以 OCR 为核心的项目需求。

---

## 结论

现在，你已经拥有一个完整的端到端示例，展示了如何使用 Aspose OCR **识别 png 中的文本**、**从图像中提取文本**，以及 **启用自动语言检测** 以处理混合语言内容。代码完整，解释覆盖了“怎么做”和“为什么”，并提供了预期输出，帮助你在本机上验证一切正常。

有其他使用场景吗？欢迎留言、分享你的发现，或探索上文的后续步骤。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}