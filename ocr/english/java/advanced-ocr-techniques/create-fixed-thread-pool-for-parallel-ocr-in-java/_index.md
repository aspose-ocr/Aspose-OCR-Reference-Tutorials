---
category: general
date: 2026-05-03
description: Create fixed thread pool in Java to extract text from images quickly.
  Learn how to run OCR, convert image to text, and boost performance with parallel
  OCR processing.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: en
og_description: Create fixed thread pool in Java to extract text from images quickly.
  Learn how to run OCR, convert image to text, and boost performance with parallel
  OCR processing.
og_title: Create Fixed Thread Pool for Parallel OCR in Java
tags:
- Java
- OCR
- Multithreading
title: Create Fixed Thread Pool for Parallel OCR in Java
url: /java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Fixed Thread Pool for Parallel OCR in Java

Ever needed to **create fixed thread pool** to speed up OCR jobs, but weren’t sure where to start? You’re not alone. In many image‑heavy projects the bottleneck is the single‑threaded OCR call, and the fix is surprisingly simple: spin up a pool of worker threads and let them chew through the files in parallel.  

In this tutorial you’ll learn how to **extract text from images** using Aspose OCR, how to **run OCR** efficiently, and how to **convert image to text** without blowing up your CPU. By the end you’ll have a ready‑to‑run Java program that demonstrates **parallel OCR processing** on a handful of sample pictures.

## What You’ll Build

We’ll put together a small console app that:

* Reads a list of image paths (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** sized to the number of CPU cores.
* Dispatches an OCR task for each image.
* Collects the recognized text and prints it to the console.
* Shuts the executor down cleanly.

No external build tools, no fancy frameworks—just plain Java and the Aspose OCR library. If you’ve got Java 8+ and a decent IDE, you’re set.

## Prerequisites

* **Java Development Kit (JDK) 8 or newer** – the code uses lambdas, so older versions won’t compile.
* **Aspose OCR for Java** – download the JAR from the Aspose website or pull it via Maven (`com.aspose:aspose-ocr`).
* A folder with a few test images (the code points to `YOUR_DIRECTORY`).  
* Basic familiarity with Java concurrency (we’ll explain the rest).

> *Pro tip:* If you’re using Maven, add the dependency to your `pom.xml` and let the IDE handle the classpath.  

---

## Step 1: Add the Required Imports

First, bring the classes we need into scope. This isn’t just boilerplate; each import tells the JVM where to find the OCR engine, image handling utilities, and the concurrency tools that let us **create fixed thread pool** instances.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – the core OCR API.  
* `java.util.*` – collections for storing image paths and results.  
* `java.util.concurrent.*` – the concurrency package that houses `ExecutorService` and `Future`.

---

## Step 2: Define the Images to Process

Next, we list the files we want to **extract text from images**. Using `Arrays.asList` keeps the code concise and lets us swap in your own directory without touching the rest of the logic.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Feel free to add more entries; the thread pool will scale automatically based on the number of CPU cores you have.

---

## Step 3: **Create Fixed Thread Pool** Matching the CPU Cores

Here’s the heart of the tutorial. We ask the runtime how many cores are available and ask the `Executors` factory to give us a pool of exactly that size. Why fixed? Because a predictable number of threads prevents the dreaded “thread explosion” that can starve the OS of resources.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` returns the logical core count (including hyper‑threads).  
* `newFixedThreadPool(coreCount)` guarantees we never exceed the CPU’s capacity, which is the safest way to **run OCR** in parallel.

---

## Step 4: Submit an OCR Task for Each Image

Now we turn each file path into a callable that **runs OCR**, recognises the text, and returns the result. Notice we instantiate a fresh `OcrEngine` inside the lambda—this avoids thread‑unsafe sharing of engine state.

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

* Each `submit` call hands the lambda to the pool, which schedules it on an idle thread.  
* The `Future<String>` objects let us retrieve the recognized text later, preserving order if you need it.

---

## Step 5: Retrieve and Display the Recognized Text

Once all tasks are queued, we simply iterate over the `Future` list, calling `get()` to block until each OCR job finishes. This is where the **convert image to text** step becomes visible to you: the `engine.getText()` call returns the raw string.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Typical console output looks like:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

If a file fails (perhaps it’s corrupted), you’ll see a line that starts with `Failed:` followed by the path—handy for quick debugging.

---

## Step 6: Clean Up the Executor Service

Never forget to shut down the pool; otherwise the JVM may linger, thinking there’s still work to do. A graceful shutdown lets any running tasks finish before the process exits.

```java
executor.shutdown();
```

You can also call `awaitTermination` if you need to enforce a timeout, but for most command‑line utilities a plain `shutdown()` is sufficient.

---

## Full Working Example

Below is the complete, ready‑to‑run program. Copy‑paste it into a file named `ParallelOcrTutorial.java`, adjust the image paths, and run `javac` + `java` as you normally would.

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

**Expected result:** each image’s textual content printed to the console, in the same order as the `imagePaths` list. If any image can’t be processed, you’ll see a failure notice instead of a blank line.

---

## Common Questions & Edge Cases

### What if I have more images than threads?

The fixed thread pool will automatically queue the excess tasks. As soon as a thread finishes its current OCR job, it picks up the next one. This queuing behavior is the essence of **parallel OCR processing**—you get maximum throughput without overwhelming the CPU.

### Can I change the language?

Absolutely. Replace `engine.getLanguage().setEnglish(true);` with the appropriate language flag, e.g., `setFrench(true)` or enable multiple languages by calling several setters before `recognize()`.

### How do I handle very large images?

Large files can consume a lot of memory per thread. If you notice `OutOfMemoryError`, consider scaling the image down before feeding it to the engine, or increase the heap size with `-Xmx`. Another approach is to use a **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}