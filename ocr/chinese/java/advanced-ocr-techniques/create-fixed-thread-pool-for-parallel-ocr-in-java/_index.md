---
category: general
date: 2026-05-03
description: 在 Java 中创建固定线程池，以快速从图像中提取文本。了解如何运行 OCR，将图像转换为文本，并通过并行 OCR 处理提升性能。
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: zh
og_description: 在 Java 中创建固定线程池，以快速从图像中提取文本。了解如何运行 OCR，将图像转换为文本，并通过并行 OCR 处理提升性能。
og_title: 在 Java 中创建固定线程池用于并行 OCR
tags:
- Java
- OCR
- Multithreading
title: 在 Java 中创建固定线程池用于并行 OCR
url: /zh/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 Java 创建固定线程池以实现并行 OCR

是否曾需要 **创建固定线程池** 来加速 OCR 任务，却不知从何入手？你并不孤单。在许多以图像为主的项目中，瓶颈往往是单线程的 OCR 调用，而解决方案出奇地简单：启动一个工作线程池，让它们并行处理文件。

在本教程中，你将学习如何使用 Aspose OCR **从图像中提取文本**、如何 **高效运行 OCR**，以及如何 **将图像转换为文本** 而不让 CPU 爆炸。完成后，你将拥有一个可直接运行的 Java 程序，演示 **并行 OCR 处理** 在若干示例图片上的效果。

## 你将构建的内容

我们将组合一个小型控制台应用程序，功能包括：

* 读取一组图像路径（PNG、JPG、TIFF、BMP）。
* **创建一个固定线程池**，大小与 CPU 核心数相同。
* 为每张图像分配一个 OCR 任务。
* 收集识别出的文本并打印到控制台。
* 干净地关闭执行器。

不需要外部构建工具，也不需要花哨的框架——只需纯 Java 与 Aspose OCR 库。如果你有 Java 8+ 和一个不错的 IDE，就可以开始了。

## 前置条件

* **Java Development Kit (JDK) 8 或更高** —— 代码使用了 lambda 表达式，旧版本无法编译。
* **Aspose OCR for Java** —— 从 Aspose 官网下载 JAR，或通过 Maven 引入 (`com.aspose:aspose-ocr`)。
* 包含若干测试图片的文件夹（代码中指向 `YOUR_DIRECTORY`）。
* 对 Java 并发有基本了解（其余内容我们会解释）。

> *小技巧：* 如果使用 Maven，将依赖添加到 `pom.xml`，让 IDE 自动处理类路径。

---

## 第一步：添加所需的导入

首先，将需要的类导入到作用域中。这不仅是样板代码；每个导入都告诉 JVM 在哪里找到 OCR 引擎、图像处理工具以及能够 **创建固定线程池** 实例的并发工具。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – 核心 OCR API。  
* `java.util.*` – 用于存储图像路径和结果的集合。  
* `java.util.concurrent.*` – 包含 `ExecutorService` 和 `Future` 的并发包。

---

## 第二步：定义要处理的图像

接下来，列出我们想要 **从图像中提取文本** 的文件。使用 `Arrays.asList` 能让代码保持简洁，并且可以在不修改其余逻辑的情况下替换为自己的目录。

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

随意添加更多条目；线程池会根据 CPU 核心数自动扩展。

---

## 第三步：**创建固定线程池** 与 CPU 核心数匹配

这一步是本教程的核心。我们查询运行时可用的核心数，并让 `Executors` 工厂创建恰好这么大的线程池。为什么要固定？因为可预测的线程数量可以防止“线程爆炸”，避免耗尽操作系统资源。

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` 返回逻辑核心数（包括超线程）。  
* `newFixedThreadPool(coreCount)` 确保我们永远不会超出 CPU 的承载能力，这是 **并行运行 OCR** 最安全的方式。

---

## 第四步：为每张图像提交 OCR 任务

现在把每个文件路径转换为一个 callable，**运行 OCR**、识别文本并返回结果。注意我们在 lambda 中实例化全新的 `OcrEngine`——这避免了引擎状态的线程不安全共享。

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* 每次 `submit` 调用都会把 lambda 交给线程池，由空闲线程调度执行。  
* `Future<String>` 对象让我们稍后检索识别出的文本，并在需要时保持顺序。

---

## 第五步：获取并显示识别的文本

所有任务排队后，只需遍历 `Future` 列表，调用 `get()` 阻塞等待每个 OCR 作业完成。这就是 **将图像转换为文本** 的实际表现：`engine.getText()` 调用返回原始字符串。

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

典型的控制台输出如下：

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

如果文件处理失败（例如文件损坏），你会看到以 `Failed:` 开头的行，后面跟着文件路径——这对快速调试非常有帮助。

---

## 第六步：清理 Executor Service

切记要关闭线程池，否则 JVM 可能会因为仍有工作未完成而挂起。优雅的关闭会让正在运行的任务完成后再退出进程。

```java
executor.shutdown();
```

如果需要强制超时，你也可以调用 `awaitTermination`，但对大多数命令行工具来说，直接 `shutdown()` 已足够。

---

## 完整可运行示例

下面是完整的、可直接运行的程序。将其复制粘贴到名为 `ParallelOcrTutorial.java` 的文件中，调整图像路径后，像往常一样使用 `javac` + `java` 编译运行。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**预期结果：** 每张图片的文本内容会按 `imagePaths` 列表的顺序打印到控制台。如果某张图片无法处理，则会显示失败提示，而不是空行。

---

## 常见问题与边缘情况

### 如果图片数量多于线程数怎么办？

固定线程池会自动将多余的任务排队。线程完成当前 OCR 作业后，会立即取出下一个任务。这种排队行为正是 **并行 OCR 处理** 的精髓——在不压垮 CPU 的前提下实现最大吞吐量。

### 能否更改识别语言？

完全可以。将 `engine.getLanguage().setEnglish(true);` 替换为相应的语言标识，例如 `setFrench(true)`，或在 `recognize()` 前调用多个 setter 以启用多语言识别。

### 如何处理非常大的图像？

大文件会在每个线程中占用大量内存。如果出现 `OutOfMemoryError`，可以在送入引擎前先将图像缩小，或使用 `-Xmx` 增大堆内存。另一种做法是改用 **cached 线程池**（`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}