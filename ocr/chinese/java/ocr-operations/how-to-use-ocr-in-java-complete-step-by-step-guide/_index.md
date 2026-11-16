---
category: general
date: 2026-02-22
description: 如何在 Java 中使用 OCR 从图像提取文本、提升 OCR 准确率，并通过实用代码示例加载图像进行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: zh
og_description: 如何在 Java 中使用 OCR 从图像中提取文本并提升 OCR 准确率。请按照本指南获取可直接运行的示例。
og_title: 如何在 Java 中使用 OCR – 完整的逐步指南
tags:
- OCR
- Java
- Image Processing
title: 如何在 Java 中使用 OCR——完整的逐步指南
url: /zh/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 完整分步指南

是否曾经需要在一张倾斜的截图上 **how to use OCR**，却惊讶于输出像乱码一样？你并非唯一。在许多真实场景的应用中——扫描收据、数字化表单或从表情包中提取文字——获得可靠结果取决于几个简单的设置。

在本教程中，我们将逐步演示如何使用 **how to use OCR** 来 *extract text from image* 文件，向您展示如何 **improve OCR accuracy**，并演示使用流行的 Java OCR 库正确的 **load image for OCR** 方法。完成后，您将拥有一个可直接嵌入任何项目的独立程序。

## 您将学习的内容

- 您需要的确切代码以 **load image for OCR**（无隐藏依赖）。
- 哪些预处理标志可以提升 **improve OCR accuracy**，以及它们为何重要。
- 如何读取 OCR 结果并将其打印到控制台。
- 常见陷阱——例如忘记设置感兴趣区域或忽略噪声消除——以及如何避免。

### 前置条件

- Java 17 或更高（代码可在任何近期 JDK 上编译）。
- 提供 `OcrEngine`、`ImagePreprocessingOptions`、`OcrInput` 和 `OcrResult` 类的 OCR 库（例如本文片段中使用的虚构 `com.example.ocr` 包）。请替换为您实际使用的库。
- 放置在可引用文件夹中的示例图像（`skewed_noisy.png`）。

> **Pro tip:** 如果您使用的是商业 SDK，请确保许可证文件在您的 classpath 中；否则引擎会抛出初始化错误。

---

## 第一步：创建 OCR 引擎实例 – 有效的 **how to use OCR**

您首先需要的是一个 `OcrEngine` 对象。可以把它想象成解释像素的大脑。

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Why this matters:* 没有引擎，您将缺乏语言模型、字符集或图像启发式的上下文。提前实例化还能让您随后附加预处理选项。

---

## 第二步：配置图像预处理 – **improve OCR accuracy**

预处理是将嘈杂扫描转化为干净、机器可读文本的秘密调味料。下面我们启用去倾斜、高级噪声消除、自动对比度以及感兴趣区域（ROI），以聚焦图片的相关部分。

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Why this matters:*  
- **Deskew** 对齐旋转的文字，这在扫描不完全平整的收据时至关重要。  
- **Noise reduction** 去除会被误识别为字符的杂散像素。  
- **Auto‑contrast** 扩展色调范围，使微弱的字母更加突出。  
- **ROI** 告诉引擎忽略无关的边框，节省时间和内存。

如果跳过其中任何一步，您可能会看到 **improve OCR accuracy** 结果下降。

---

## 第三步：加载图像进行 OCR – 正确的 **load image for OCR**

现在我们真正将引擎指向要读取的文件。`OcrInput` 类可以接受多张图像，但在本示例中我们保持简洁。

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Why this matters:* 路径必须是绝对路径或相对于工作目录的相对路径；否则引擎会抛出 `FileNotFoundException`。另外，请注意方法名 `add` 暗示您可以排队多个图像——这对批处理非常方便。

---

## 第四步：执行 OCR 并输出识别文本 – **how to use OCR** 全流程

最后，我们让引擎识别文本并打印。`OcrResult` 对象包含原始字符串、置信度分数以及逐行元数据（如果您以后需要）。

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output**（假设示例图像包含 “Hello, OCR World!”）：

```
=== OCR Output ===
Hello, OCR World!
```

如果结果出现乱码，请返回第 2 步并调整预处理选项——可能需要降低噪声消除级别或修改 ROI 矩形。

---

## 完整、可运行的示例

下面是一个完整的 Java 程序，您可以复制粘贴到名为 `OcrDemo.java` 的文件中。它将我们讨论的每一步串联起来。

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

保存文件后，使用 `javac OcrDemo.java` 编译，并运行 `java OcrDemo`。如果一切配置正确，您将看到提取的文本打印在控制台上。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| **如果我的图像是 JPEG 格式怎么办？** | `OcrInput.add()` 方法接受任何受支持的光栅格式——PNG、JPEG、BMP、TIFF。只需在路径中更改文件扩展名即可。 |
| **我可以一次处理多页吗？** | 当然可以。对每个文件调用 `ocrInput.add()`，然后将同一个 `ocrInput` 传递给 `recognize()`。引擎会返回一个合并后的 `OcrResult`。 |
| **如果 OCR 结果为空怎么办？** | 再次确认 ROI 实际上包含文字。同时确保已启用 `setDeskewEnabled(true)`；90° 旋转会导致引擎认为图像为空白。 |
| **如何更改语言模型？** | 大多数库在 `OcrEngine` 上提供 `setLanguage(String)` 方法。请在 `recognize()` 之前调用，例如 `ocrEngine.setLanguage("eng")`。 |
| **有没有办法获取置信度分数？** | 可以，`OcrResult` 通常提供每行或每字符的 `getConfidence()`。可利用它过滤低置信度的结果。 |

---

## 结论

我们已经从头到尾介绍了在 Java 中 **how to use OCR** 的全过程：创建引擎、配置预处理以 **improve OCR accuracy**、正确 **load image for OCR**，以及最终打印提取的文本。完整的代码片段已可直接运行，解释也阐明了每行代码背后的“为什么”。

准备好下一步了吗？尝试更换 ROI 矩形以聚焦图像的不同部分，实验 `NoiseReduction.MEDIUM`，或将输出集成到可搜索的 PDF 中。您还可以探索诸如使用云服务 **extract text from image** 或使用多线程队列批量处理数千个文件等相关主题。

对 OCR、图像预处理或 Java 集成还有其他疑问？留下评论吧，祝编码愉快！

![如何使用 OCR 示例](/images/ocr-demo.png "how to use OCR – 展示预处理和结果的 Java 示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}