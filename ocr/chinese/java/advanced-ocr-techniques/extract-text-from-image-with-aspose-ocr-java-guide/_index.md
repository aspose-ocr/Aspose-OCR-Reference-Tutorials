---
category: general
date: 2026-02-14
description: 使用 Aspose OCR 在 Java 中从图像提取文本。了解如何在感兴趣区域内从表单字段提取文本，以获得精确的结果。
draft: false
keywords:
- extract text from image
- extract text from form
language: zh
og_description: 使用 Aspose OCR 在 Java 中从图像提取文本。本教程展示了如何通过感兴趣区域从表单字段中提取文本。
og_title: 使用 Aspose OCR 从图像提取文本 – Java 指南
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 使用 Aspose OCR 从图像提取文本 – Java 指南
url: /zh/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像提取文本 – Java 指南

是否曾经需要**从图像中提取文本**，却不得不解析整张图片，浪费 CPU 资源并得到嘈杂的结果？你并非唯一遇到这种情况的人。在许多真实场景的应用中——比如发票扫描仪、护照阅读器或数据录入表单——你只关心少数几个字段，而不是整个画布。  

好消息是，Aspose OCR 允许你**从图像中提取文本** *以及*通过定义多边形从特定表单区域提取文本。在本教程中，你将看到如何使用 Java **从表单中提取文本**，了解这种方法为何重要，以及当出现问题时该如何调整。  

下面我们将覆盖从设置库到处理棘手边缘情况的所有内容，最终你将拥有一个可直接运行的代码片段，只提取你需要的数据。

## 你需要的条件

- Java 17（或任何较新的 JDK）——更新的版本对 Unicode 支持更好。  
- Aspose.OCR for Java 23.10（或阅读时的最新版本）。  
- 一张名为 `form.png`、包含清晰定义字段的示例图像。  
- 一个 IDE 或简单的文本编辑器——IntelliJ IDEA、VS Code，甚至 Notepad 都可以。  

核心演示不需要 Maven/Gradle 的魔法，只需将 Aspose OCR JAR 添加到类路径中即可。

---

## 步骤 1 – 初始化 OCR 引擎并加载图像

引擎首先需要一个位图来工作。我们将指向 `form.png`，它位于与源文件相同的文件夹中。

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*为什么这很重要:*  
创建一个全新的 `OcrEngine` 能让你拥有干净的起点，确保没有残留设置影响运行。提前加载图像还能验证文件是否存在，这样在后续步骤浪费时间之前就能抛出有用的异常。

> **专业提示：** 如果你的图像很大（超过 5 MB），考虑先对其进行缩放。Aspose OCR 在任一维度低于 2000 px 的图像上运行更快。

---

## 步骤 2 – 为要读取的字段定义多边形

*感兴趣区域*（ROI）只是一段多边形，用来告诉引擎在哪里查找。下面我们创建两个矩形——一个用于“First Name”，另一个用于“Date of Birth”。根据你的表单调整坐标即可。

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*为什么使用多边形而不是矩形？*  
多边形提供了处理倾斜或非矩形框的灵活性——这在扫描未完全对齐的印刷表单时很常见。

---

## 步骤 3 – 告诉 Aspose OCR 只关注这些区域

现在我们将多边形绑定到引擎。`setRegionsOfInterest` 方法接受一个列表，你可以添加任意数量的字段。

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*内部发生了什么？*  
Aspose OCR 会将每个多边形裁剪为单独的位图，运行识别算法，然后将结果拼接在一起。这大幅降低了来自周围图形的误报。

---

## 步骤 4 – 运行 OCR 过程

所有配置完成后，我们启动 OCR。`process()` 调用返回一个包含提取文本和置信度分数的 `OcrResult` 对象。

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

如果需要每个字段的置信度，可以检查 `ocrResult.getRegions()`——每个区域都有自己的分数。对于大多数简单表单，整体文本已经足够。

---

## 步骤 5 – 显示（或存储）提取的文本

最后，我们将结果打印到控制台。在实际应用中，你可能会写入数据库、JSON 文件或通过 API 发送。

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**预期输出（示例）：**

```
=== Extracted Text ===
John Doe
12/04/1990
```

这两行对应我们定义的两个多边形。如果看到多余的空白，请使用 `String.trim()` 进行修剪。

---

## 当表单拥有众多字段时如何提取文本

当表单包含数十个输入时，手动输入坐标会变得繁琐。这里提供一个快速的模式供你采用：

1. **创建 CSV**，每行包含 `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`。  
2. **在运行时加载 CSV**，遍历每行，构建 `Polygon` 并将其添加到 ROI 列表中。  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*为什么要这么做？*  
自动化 ROI 生成让你可以在多个表单布局之间复用相同的 Java 代码，使项目保持 DRY（不要重复自己）。

---

## 边缘情况及你可能未想到的技巧

- **旋转的扫描图像：** 如果整张图像被旋转，调用 `ocrEngine.getEngineOptions().setRotateAngle(degrees)`。  
- **低对比度：** 设置 `ocrEngine.getEngineOptions().setContrast(1.5f)` 提高可读性。  
- **非拉丁脚本：** 使用 `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)`（或任何受支持的语言）切换语言。  
- **部分 OCR 失败：** 始终检查 `ocrResult.getConfidence()`；如果低于 80 %，考虑提示用户进行手动验证。  

---

## 完整可运行示例（复制粘贴即可）

下面是完整的程序，已准备好编译运行。将 `YOUR_DIRECTORY` 替换为存放 `form.png` 的文件夹路径。

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

编译方式：

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

你应该会看到属于已定义 ROI 的两行文本。

---

## 常见问题

**Q: 这能用于 PDF 吗？**  
A: 不能直接使用。先将每页 PDF 转换为图像（例如使用 Aspose PDF），再将图像输入 OCR 引擎。

**Q: 如果我的表单有复选框怎么办？**  
A: OCR 不能读取布尔状态，但你可以将复选框区域视为 ROI，检查像素密度以推断是否被勾选。

**Q: 能一次性从多页表单中提取文本吗？**  
A: 对每页图像循环，复用相同的 ROI 列表，并将结果拼接起来。

---

## 结论

我们已经完整演示了使用 Aspose OCR **从图像中提取文本** 的端到端解决方案，并展示了相同技术如何让你 **从表单中提取文本** 字段，达到精准定位。通过定义多边形、限制引擎的关注范围并处理常见陷阱，你可以快速获得干净的数据，而无需处理整张图片的开销。  

准备好下一步了吗？尝试将 OCR 输出链入 JSON 负载，或喂给机器学习模型进行校验。天地无限，而现在你

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}