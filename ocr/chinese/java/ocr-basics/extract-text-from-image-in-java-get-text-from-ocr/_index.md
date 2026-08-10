---
category: general
date: 2026-05-25
description: 在 Java 中使用 OCR 提取图像文本。了解如何加载 OCR 图像、从照片中识别文字，并通过简洁的代码示例获取 OCR 文本。
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: zh
og_description: 使用分步指南在 Java 中从图像提取文本。学习如何加载图像进行 OCR，识别照片中的文字，并高效获取 OCR 文本。
og_title: 在 Java 中从图像提取文本 – 从 OCR 获取文本
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中从图像提取文本 – 获取 OCR 文本
url: /zh/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中从图像提取文本 – 从 OCR 获取文本

是否曾经需要**从图像中提取文本**但不确定该选择哪个 Java 库？你并不孤单。无论是数字化收据、从产品照片中提取序列号，还是仅仅玩个有趣的副项目，将图片转换为可编辑文本都是一个常见的难题。

在本教程中，我们将演示一个完整、可直接运行的示例，向您展示如何**加载图像进行 OCR**、配置引擎，最终**从照片中识别文本**，让您只需几行代码即可**从 OCR 获取文本**。没有模糊的引用——所有内容都在这里。

## 您将学到

* 如何在 Java 中设置轻量级 OCR 引擎。  
* **加载图像进行 OCR** 并处理不同文件路径的确切步骤。  
* 当您想要**从图像中提取文本**且不是英文时，配置语言为何重要。  
* 如何安全地输出结果以及引擎返回空时该怎么办。  
* 一些专业技巧，帮助避免最常见的陷阱。  

阅读完本指南后，您将拥有一个独立的程序，能够读取包含乌克兰字符的 JPEG（或 PNG）并将识别出的字符串打印到控制台。随意更换语言或图像——所有内容都是模块化的。

---

![使用 Java OCR 引擎从图像提取文本的流程图](/images/extract-text-from-image-java.png)

*Alt text: Java 中从图像提取文本过程的流程图*

## 前置条件

* **Java Development Kit (JDK) 11+** – 代码使用现代模块系统，但旧版本通过少量调整也能工作。  
* **Maven or Gradle** – 用于获取 OCR 库（我们将使用 **Asprise OCR** 作为轻量级、免费用于开发的选项）。  
* 一个示例图像文件（例如 `ukrainian_sign.jpg`），放置在程序可读取的位置。  
* 对 Java 的 `main` 方法和异常处理有基本了解。  

如果您已经具备这些条件，就可以开始了。否则，请从 Oracle 或 AdoptOpenJDK 获取 JDK 并设置一个简单的 Maven 项目——无需复杂操作。

---

## 步骤 1：添加 OCR 依赖

首先，告诉您的构建工具获取 OCR 引擎。对于 Maven，请将以下内容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

如果您更喜欢 Gradle，等价的写法是：

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

这些坐标会拉取一个紧凑的 JAR，其中包含 `OcrEngine`、`OcrLanguage` 以及我们将使用的辅助类。对于基本的拉丁和西里尔字母脚本，不需要额外的本地二进制文件。

---

## 步骤 2：创建一个用于**从图像提取文本**的 Java 类

现在我们来编写实际的程序。将以下代码保存为 `ExtractTextDemo.java`，放在 `src/main/java/com/example/ocr/` 目录下。

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### 为什么这种结构有效

- **分离的编号块** 使流程易于跟踪，尤其是在查找**加载图像进行 OCR**或**从照片中识别文本**的位置时。  
- 围绕图像加载和识别的 `try/catch` 确保程序能够优雅地失败——当文件路径错误或 OCR 引擎找不到语言数据时非常有用。  
- 在步骤 2 早期设置语言可显著提升非英文脚本的准确性。如果以后需要 **java image to text** 的其他语言，只需将 `OcrLanguage.UKRAINIAN` 替换为 `OcrLanguage.ENGLISH`、`FRENCH` 等。

---

## 步骤 3：构建并运行程序

在项目根目录下执行：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

或者，如果您使用 Gradle：

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

假设 `ukrainian_sign.jpg` 包含文本 *«Ласкаво просимо»*（乌克兰语的 “Welcome”），您应该会看到类似如下的输出：

```
=== OCR Result ===
Ласкаво просимо
```

该输出确认您已成功**从图像提取文本**并在一次运行中**从 OCR 获取文本**。

---

## 步骤 4：微调工作流 – 在实际项目中实现**Java Image to Text**

虽然演示代码很简洁，实际项目通常需要更多功能：

| 场景 | 需要调整的内容 | 原因 |
|----------|----------------|--------|
| **批量处理** | 遍历 `List<Path>`，并将每个结果存入数据库。 | 当有数百张照片时，可减少手动工作。 |
| **不同的图像格式** | 使用 `ImageIO.read(new File(path))` 进行预处理，然后将 `BufferedImage` 传递给 `ocrEngine.getImage().loadFromBufferedImage(bufImg)`。 | 支持 PNG、BMP，甚至转换后的 PDF。 |
| **性能调优** | 如果可以接受稍低的准确率，调用 `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)`。 | 在低端硬件上加快识别速度。 |
| **后处理** | 去除空白，替换常见的 OCR 误读（`0` → `O`，`1` → `I`）。 | 提升下游数据质量。 |

这些变体保持核心思路——**从照片中识别文本**——不变，同时为生产工作负载提供灵活性。

---

## 常见陷阱与专业提示

1. **错误的语言设置** – 如果忘记步骤 2，引擎默认使用英语，会把西里尔字符变成乱码。务必再次确认语言代码。  
2. **图像质量很重要** – 低分辨率或模糊的照片会降低准确率。如有需要，可使用对比度增强或二值化进行预处理。  
3. **文件路径细节** – 在 Windows 上，反斜杠需要转义（`C:\\images\\file.jpg`）。使用 `java.nio.file` 的 `Path.of(...)` 可以规避此问题。  
4. **内存泄漏** – `OcrEngine` 持有本地资源。完成后调用 `ocrEngine.dispose()`，尤其是在长时间运行的服务中。  
5. **线程安全** – 引擎默认不是线程安全的。为每个线程创建单独实例或对访问进行同步。

---

## 完整工作示例（全合一）

下面是一个单文件示例，您可以复制粘贴到任何 IDE 中。它包含 `dispose()` 调用以及一个小的辅助方法，使代码更简洁。

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

运行此程序会得到前面展示的相同控制台输出。随意将 `OcrLanguage.UKRAINIAN` 替换为 `OcrLanguage.ENGLISH` 或其他受支持的语言，以观察引擎的适配情况。

---

## 结论

我们已经完整演示了使用 Java **从图像提取文本** 所需的全部内容：从添加 OCR 依赖，到 **加载图像进行 OCR**，

## 相关教程

- [使用 Aspose OCR 识别图像文本 – 完整 Java OCR 教程](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [使用 Aspose.OCR 进行语言选择的图像文字 OCR 方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [使用 Aspose.OCR BufferedImage 将图像转换为文本（Java）](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}