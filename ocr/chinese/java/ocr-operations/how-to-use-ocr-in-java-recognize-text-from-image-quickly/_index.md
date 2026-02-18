---
category: general
date: 2026-02-17
description: 学习如何在 Java 中使用 OCR 识别图像文件中的文本，从 PNG 收据中提取文字，并使用 Aspose OCR 将收据转换为 JSON。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: zh
og_description: 逐步指南，教您如何在 Java 中使用 OCR 识别图像文本、从 PNG 收据中提取文字并将收据转换为 JSON。
og_title: 如何在 Java 中使用 OCR – 从图像识别文本
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 如何在 Java 中使用 OCR —— 快速从图像识别文本
url: /zh/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

trying this out? Drop a comment below, and let’s troubleshoot together. Happy coding, and enjoy turning those messy receipt images into clean, searchable data!"

Translate: "有疑问或在实践中遇到问题？在下方留言，我们一起排查。祝编码愉快，享受将凌乱的收据图像转换为干净、可搜索数据的过程！"

Finally the closing shortcodes.

Now produce final content with same markdown.

Make sure to preserve code block placeholders exactly as they are.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 快速识别图像中的文本

有没有想过 **如何使用 OCR** 从收据的照片中提取文字？也许你尝试过一些在线工具，却只得到乱码或无法解析的格式。好消息是，只需几行 Java 代码，你就可以 **recognize text from image** 文件、**extract text from PNG** 收据，甚至 **convert receipt to JSON** 进行下游处理。  

在本教程中，我们将完整演示工作流——从获取 Aspose OCR 库的授权到获取可直接写入数据库或机器学习模型的干净 JSON 负载。没有冗余内容，只有可直接复制粘贴到 IDE 的实用可运行示例。完成后，你将拥有一个独立程序，读取 `receipt.png` 并输出可直接使用的 JSON 字符串。

## 你需要的环境

- **Java Development Kit (JDK) 8+** – 任意近期版本均可。  
- **Aspose OCR for Java** 库（Maven 坐标为 `com.aspose:aspose-ocr`）。  
- 一个 **有效的 Aspose OCR 许可证文件** (`Aspose.OCR.lic`)。免费试用可用于测试，但正式许可证可去除评估限制。  
- 一张包含待读取文本的图像文件（PNG、JPEG 等）——我们称之为 `receipt.png` 并放置在已知文件夹中。  
- 你喜欢的 IDE（IntelliJ IDEA、Eclipse、VS Code 等）——随意选择。  

> **技巧提示：** 将许可证文件放在源码文件夹之外，并通过绝对或相对路径引用，以避免将其提交到版本控制。  

既然前置条件已经明确，让我们深入实际代码。

## 使用 OCR 的核心步骤

下面是我们将执行的操作的高级概览：

1. **加载 Aspose OCR 库** 并应用你的许可证。  
2. **创建 `OcrEngine` 实例** —— 这是执行繁重任务的引擎。  
3. **准备 `OcrInput` 对象**，指向你要处理的图像。  
4. **调用 `recognize` 并使用 `ResultFormat.JSON`**，获取提取文本的 JSON 表示。  
5. **处理 JSON 输出** —— 打印、写入文件或进一步解析。  

每一步将在后续章节中详细说明。

## 步骤 1 – 安装 Aspose OCR 并应用许可证

如果使用 Maven，首先在 `pom.xml` 中添加 Aspose OCR 依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

接下来，在 Java 代码中加载许可证。此步骤至关重要；如果不加载，库将以评估模式运行，并可能在输出中嵌入水印。

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **为什么重要：** `License` 对象告诉 OCR 引擎你已获得使用全部功能的授权，包括高精度识别和 JSON 导出。跳过此步骤仍然可以 **recognize text from image**，但结果可能受到限制。

## 步骤 2 – 创建 OCR 引擎实例

`OcrEngine` 类是所有 OCR 操作的入口。可以把它看作读取像素并决定字符的“脑”。

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

如果收据包含非拉丁文字或扫描角度倾斜，你可以稍后自定义引擎（例如设置语言、启用去倾斜）。对于大多数美国收据，默认设置已足够。

## 步骤 3 – 加载要处理的图像

现在我们将让 OCR 引擎指向保存收据的文件。`OcrInput` 类可以接受多张图像，但本教程仅使用单个 PNG，保持简单。

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

如果需要批量 **extract text from PNG** 文件，只需重复调用 `input.add()` 或传入文件路径列表即可。

## 步骤 4 – 识别文本并将收据转换为 JSON

下面是本教程的核心。我们让引擎识别文本并请求以 JSON 格式返回结果。`ResultFormat.JSON` 标志帮我们完成所有繁重工作。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON 负载包含每一行识别结果、其边界框、置信度以及原始文本。这种结构使得 **convert receipt to JSON** 变得极其简单，随后即可传递给任何下游 API。

## 步骤 5 – 将所有代码整合并运行程序

下面是完整的、可直接运行的 Java 类，将所有内容串联起来。将其保存为 `JsonExportDemo.java`（或任意名称），然后在 IDE 或命令行中运行。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### 预期输出

运行程序后会打印类似以下的 JSON 字符串（具体内容取决于你的收据）：

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

现在你可以将该 JSON 输入到数据库、REST 接口或数据分析管道中。**convert receipt to JSON** 步骤已经为你完成。

## 常见问题与边缘情况

### 如果图像被旋转了怎么办？

Aspose OCR 会自动检测并纠正轻微旋转。对于严重倾斜的图像，请在识别前调用 `engine.getImagePreprocessingOptions().setDeskew(true)`。

### 如何处理多语言？

使用 `engine.getLanguage()` 设置所需语言，例如 `engine.setLanguage(Language.FRENCH)`。当需要 **recognize text from image** 包含多语言收据时，这非常有用。

### 能否输出纯文本而不是 JSON？

当然可以。将 `ResultFormat.JSON` 替换为 `ResultFormat.TEXT` 并调用 `result.getText()`。

### 有没有办法将 OCR 限制在特定区域？

可以——使用 `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` 将焦点限定在收据区域，这可以提升速度和准确度。

## 生产级 OCR 的实用技巧

- **缓存许可证** 对象，如果在循环中处理大量文件；反复创建会增加开销。  
- **批量处理**：将所有收据路径加载到同一个 `OcrInput`，一次性调用 `recognize`。JSON 将包含页面数组，每页都有其行信息。  
- **验证 JSON**：获取字符串后，使用 Jackson 等库解析，以确保其结构完整后再存储。  
- **监控置信度**：JSON 为每行提供 `confidence` 字段。过滤掉低于阈值（如 0.85）的行，以避免垃圾数据。  
- **保护许可证**：将 `Aspose.OCR.lic` 存放在安全金库或环境变量中，尤其是在云部署时。  

## 结论

我们已经介绍了在 Java 中 **how to use OCR**，实现 **recognize text from image**、**extract text from PNG** 收据以及 **convert receipt to JSON**——全部通过一个简洁的端到端示例。步骤直观，代码可直接运行，JSON 输出提供了结构化的表示，可供任何下游系统使用。  

接下来，你可以探索更高级的场景：将 JSON 输入到 Apache Kafka 进行实时处理、使用正则表达式提取项目总计，或集成云 OCR 服务以实现可扩展性。无论选择何种方式，你刚学到的基础仍然适用。  

有疑问或在实践中遇到问题？在下方留言，我们一起排查。祝编码愉快，享受将凌乱的收据图像转换为干净、可搜索数据的过程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}