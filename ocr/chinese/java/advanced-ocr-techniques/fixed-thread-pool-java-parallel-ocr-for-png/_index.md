---
category: general
date: 2026-02-17
description: 学习如何使用固定线程池 Java 从 PNG 图像中提取文本，进行并行 OCR 处理，并正确关闭 ExecutorService。
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: zh
og_description: 了解如何使用固定线程池的 Java 并行从 PNG 图像中提取文本，转换扫描页的文本，并安全地关闭 ExecutorService。
og_title: 固定线程池 Java – PNG 的并行 OCR
tags:
- java
- ocr
- multithreading
- aspose
title: 固定线程池 Java – 对 PNG 的并行 OCR
url: /zh/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – PNG 并行 OCR

Ever wondered how to speed up OCR on a bunch of PNG files using a **fixed thread pool java**? In this tutorial we'll walk through **extract text from PNG** images in parallel, **convert scanned pages text** into editable strings, and safely **shut down executor service** once the work is done.

如果你曾经盯着一个单线程循环看了好几分钟，你一定体会过那种每页处理完才开始下一页的沮丧。好消息是，只需几行 Java 代码和 Aspose OCR，就能释放所有 CPU 核心的威力，将扫描页转换为可搜索的文本，并保持应用响应。

下面你会看到一个完整、可直接运行的示例，以及每个部分为何重要、常见陷阱和可用于任何 OCR 库的技巧。

---

## What You’ll Need

- **Java 17**（或任何近期的 JDK）– 代码偶尔使用 `var` 语法，但在旧版本上也能运行。  
- **Aspose.OCR for Java** 库 – 可从 Maven Central 获取，或从 Aspose 下载试用版。  
- 一组你想处理的 **PNG** 文件 – 如扫描收据、书页或截图。  
- 对 Java 并发的基本了解 – 不是必须，但有帮助。

就这些。无需外部服务、无需 Docker，只有纯 Java 和一点多线程魔法。

---

## Step 1: Add Aspose OCR Dependency & License (Optional)

First, make sure the Aspose OCR JAR is on your classpath. If you use Maven, add:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

If you don’t have a license, the library will run in evaluation mode; the code works the same way. To load a license (recommended for production), place `Aspose.OCR.lic` in your resources folder and use:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Keep the license file outside version control to avoid accidental exposure.

---

## Step 2: Create a Thread‑Safe `OcrEngine` Instance

Aspose OCR’s `OcrEngine` is thread‑safe as long as you reuse the same instance across tasks. Creating it once saves memory and avoids the overhead of re‑initializing the engine for every image.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Why reuse? Think of the engine as a heavy‑weight worker that loads language models into memory. Spawning a new engine per image would be like hiring a new specialist for every tiny job – costly and unnecessary.

---

## Step 3: Set Up a Fixed Thread Pool Java

Now comes the star of the show: a **fixed thread pool java**. We’ll size it to the number of logical processors so every core gets work without oversubscribing.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Using a *fixed* pool (instead of a cached one) gives you predictable resource usage and prevents the dreaded “out‑of‑memory” spikes when hundreds of images arrive at once.

---

## Step 4: List the PNG Files You Want to Process (Extract Text from PNG)

Collect the paths to the images you wish to OCR. In a real project you might scan a directory or read from a database; here we’ll hard‑code a few examples.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note:** The file extension **png** is important because Aspose OCR automatically detects the format, but you could feed JPEG or TIFF as well.

---

## Step 5: Submit OCR Tasks – Parallel OCR Processing

Each image becomes a callable that returns the recognized text. Because the `OcrEngine` is shared, we only need to pass the file path into the task.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Why wrap it in a `Future`? It lets us fire off all jobs instantly, then later collect results in the order they were submitted – perfect for preserving page order when **convert scanned pages text** back into a document.

---

## Step 6: Retrieve Results and Display (Convert Scanned Pages Text)

Now we wait for each `Future` to finish and print the output. The `get()` call blocks only until the specific task completes, not the whole pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Typical console output looks like:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

If you prefer to write the results to files, replace the `System.out.println` with a `Files.writeString` call.

---

## Step 7: Cleanly Shut Down the Executor Service

When every task is done, it’s crucial to **shut down executor service**; otherwise your JVM may keep non‑daemon threads alive, preventing a graceful exit.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

The `awaitTermination` pattern gives the pool a chance to finish ongoing work before we force it. Ignoring this step is a common source of memory leaks in long‑running applications.

---

## Full Working Example

Putting it all together, here’s the complete program you can copy‑paste into `ParallelBatchDemo.java` and run:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}