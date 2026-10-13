---
category: general
date: 2026-02-14
description: 'Batch image OCR made easy: learn how to extract text from PNG files
  using Aspose OCR with parallel processing in Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: en
og_description: Batch image OCR tutorial showing how to extract text from PNG files
  using Aspose OCR's asynchronous API in Java.
og_title: Batch Image OCR in Java – Fast PNG Text Extraction
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Batch Image OCR in Java – Extract Text from PNG Files Fast
url: /java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch Image OCR in Java – Extract Text from PNG Files Fast

Ever needed to run **batch image OCR** on a folder of PNG scans but worried about speed? You’re not alone. In many real‑world projects—invoice digitization, archival of scanned books, or processing receipts—developers must **extract text from PNG** images quickly and reliably.  

The good news? With Aspose OCR’s asynchronous API you can spin up a parallel OCR pipeline in just a few lines of Java. In this guide we’ll walk through the complete, runnable solution, explain why each piece matters, and show you how to verify the results. By the end you’ll have a self‑contained program that processes a whole batch of PNG files in parallel, giving you clean, spell‑checked text output.

## What You’ll Learn

- How to list PNG files for batch processing  
- Configuring the Aspose `OcrEngine` for English language and spell correction  
- Running OCR asynchronously with `processAsync` and handling the `Future` result  
- Reading and displaying the recognized text for each image  
- Tips for scaling, handling errors, and tweaking performance  

### Prerequisites

- Java 8 or newer installed (the code uses the standard `java.util.concurrent` package)  
- An Aspose OCR for Java license or a free trial (download from the Aspose website)  
- A folder containing a few PNG screenshots or scanned pages you want to test with  

Now, let’s dive in.

## Step 1 – Gather Your PNG Files for a Batch

Before the OCR engine can do any work, it needs to know which images to process. The simplest way is to build a `List<String>` of absolute or relative file paths.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Why this matters:**  
Creating the list up front lets the engine schedule each file independently, which is the foundation of true batch processing. If you later need to scan a directory dynamically, just replace the static `Arrays.asList` with a `Files.walk` stream.

## Step 2 – Initialise and Tune the Aspose OCR Engine

Aspose’s `OcrEngine` is highly configurable. Here we set the language to English and turn on spell correction—two options that dramatically improve the quality of extracted text, especially from noisy PNG scans.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Why these settings:**  
- **Language selection** tells the engine which character set and dictionary to use, cutting down false recognitions.  
- **Spell correction** catches common OCR mis‑reads (e.g., “1” vs “l”) without you having to post‑process the output.

> **Pro tip:** If your images contain multiple languages, you can pass a list like `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Step 3 – Fire Off Asynchronous Batch Processing

The heavy lifting happens in `processAsync`. It returns a `Future<List<OcrResult>>`, allowing your main thread to keep doing other work while the OCR runs in the background.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Why async:**  
Running OCR sequentially can be painfully slow—each PNG might take a second or more. By delegating the work to a thread pool, you exploit multiple CPU cores and reduce total runtime dramatically.

## Step 4 – Retrieve the Results When They’re Ready

When you’re ready to consume the output, simply call `get()` on the `Future`. This call blocks only until the OCR finishes, then hands you a list of `OcrResult` objects in the same order as the input list.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Handling time‑outs:**  
If you want to avoid an indefinite block, use `ocrFuture.get(60, TimeUnit.SECONDS)` and catch `TimeoutException` to implement a fallback.

## Step 5 – Display the Recognised Text for Each PNG

Now that you have the results, iterate over them and print the extracted text alongside the original file name. This is where you finally **extract text from PNG** files.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Expected output example**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

If the OCR engine cannot recognise a page, the corresponding `getText()` will return an empty string—always worth checking in production code.

## Full Working Example

Below is the complete, ready‑to‑run program that puts all the pieces together. Copy‑paste it into a file named `ParallelOcrDemo.java`, replace `YOUR_DIRECTORY` with the path to your PNG folder, and run `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Running the Demo

1. **Compile** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Execute** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

You should see each PNG file name followed by the extracted text, separated by dashes.  

> **Note:** If you encounter a `LicenseException`, make sure to load your Aspose license before creating the engine:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Scaling Up – Tips for Real‑World Batch OCR

| Situation | Recommendation |
|-----------|----------------|
| **Hundreds of PNGs** | Increase the thread pool size via `ocrEngine.setThreadPoolSize(8)` (or higher, matching CPU cores). |
| **Memory constraints** | Process files in smaller chunks (e.g., batches of 50) and release the `OcrResult` list after each chunk. |
| **Variable image quality** | Enable `setPreprocessingOptions` to auto‑rotate, deskew, or enhance contrast before recognition. |
| **Multiple languages** | Call `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` and optionally set a custom dictionary. |
| **Error handling** | Wrap `ocrFuture.get()` in a try‑catch block for `ExecutionException` to log failed files without aborting the whole batch. |

These strategies keep your **batch image OCR** pipeline robust, even when the input set grows.

## Frequently Asked Questions

**Q: Does this work with JPEG or TIFF files?**  
A: Absolutely. The `processAsync` method accepts any format supported by Aspose OCR (PNG, JPEG, TIFF, BMP, etc.). Just change the file extensions in your list.

**Q: What if I need to preserve layout (tables, columns)?**  
A: Aspose OCR provides a `getLayoutResult()` method that returns positional data. You can reconstruct tables by analyzing the bounding boxes of each word.

**Q: Can I run this on a serverless platform?**  
A: Yes—just package the JAR with the Aspose library and deploy to AWS Lambda, Azure Functions, or Google Cloud Functions. Remember to keep the function’s memory allocation high enough for the OCR thread pool.

## Conclusion

You now have a complete, self‑contained **batch image OCR** solution that efficiently **extracts text from PNG** files using Aspose OCR’s asynchronous API in Java. The tutorial covered everything from preparing the file list to configuring language and spell‑checking, launching parallel processing, handling results, and scaling the pipeline for production workloads.

Ready for the next step? Try swapping the language to French, experiment with custom dictionaries, or integrate the output into a searchable ElasticSearch index. The sky’s the limit when you combine fast batch OCR with modern Java concurrency.

Happy coding, and may your text extraction be swift and spot‑on! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="Batch image OCR processing diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}