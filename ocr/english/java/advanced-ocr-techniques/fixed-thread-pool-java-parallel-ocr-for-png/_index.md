---
category: general
date: 2026-02-17
description: Learn how to use a fixed thread pool java to extract text from PNG images
  with parallel OCR processing and properly shut down executor service.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: en
og_description: Discover how a fixed thread pool java can extract text from PNG images
  in parallel, convert scanned pages text, and shut down executor service safely.
og_title: fixed thread pool java – parallel OCR for PNG
tags:
- java
- ocr
- multithreading
- aspose
title: fixed thread pool java – parallel OCR for PNG
url: /java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – parallel OCR for PNG

Ever wondered how to speed up OCR on a bunch of PNG files using a **fixed thread pool java**? In this tutorial we'll walk through **extract text from PNG** images in parallel, **convert scanned pages text** into editable strings, and safely **shut down executor service** once the work is done.

If you’ve ever stared at a single‑threaded loop that drags on for minutes, you know the frustration of waiting for each page to finish before the next even starts. The good news? With a few lines of Java and Aspose OCR you can unleash the power of all your CPU cores, turn those scanned pages into searchable text, and keep your application responsive.  

Below you’ll find a complete, ready‑to‑run example, plus explanations of why each piece matters, common pitfalls, and tips you can apply to any OCR library.

---

## What You’ll Need

- **Java 17** (or any recent JDK) – the code uses the modern `var` syntax sparingly, but works on older versions too.  
- **Aspose.OCR for Java** library – you can grab it from Maven Central or download a trial from Aspose.  
- A set of **PNG** files you want to process – think scanned receipts, book pages, or screenshots.  
- Basic familiarity with Java concurrency – not required, but helpful.

That’s it. No external services, no Docker, just plain Java and a little multithreading magic.

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