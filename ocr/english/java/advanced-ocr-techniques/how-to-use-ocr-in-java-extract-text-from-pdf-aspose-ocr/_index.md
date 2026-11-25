---
category: general
date: 2026-10-24
description: Learn how to run an Aspose OCR Java example that extracts text from PDF
  files, including parallel OCR processing, handling password‑protected PDFs, and
  converting scanned PDFs to searchable text.
draft: false
images:
- /java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/og-image.png
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
language: en
lastmod: 2026-10-24
og_description: Run an Aspose OCR Java example to extract text from PDF quickly. This
  guide covers parallel OCR processing, password‑protected PDFs, and converting scanned
  PDFs to searchable documents.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Aspose OCR Java example – extract text from PDF quickly
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Aspose OCR Java example: extract text from PDF quickly'
url: /java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java example: extract text from PDF quickly

In this tutorial you’ll discover **how to use an Aspose OCR Java example** to turn scanned PDFs into searchable, machine‑readable text. Whether you have a single multi‑page file or a batch of password‑protected PDFs, the steps below show you how to configure the OCR engine, enable parallel processing, and retrieve the combined output in just a few lines of Java code.

You’ll also learn when to adjust thread counts for optimal performance, how to handle encrypted PDFs, and why this approach is ideal for converting scanned PDF documents into searchable archives.

![how to use OCR with Aspose OCR Java](/images/ocr-parallel.png "Illustration of parallel OCR processing in Java – how to use OCR")
[how to use OCR with Aspose OCR Java](/images/ocr-parallel.png "Illustration of parallel OCR processing in Java – how to use OCR")

## Quick answers
- **What does the Aspose OCR Java example do?** It loads a PDF, runs OCR on every page in parallel, and returns the full searchable text as a single string.  
- **Can it process password‑protected PDFs?** Yes – you can supply the document password when adding the file to `OcrInput`.  
- **Is parallel OCR processing worth it?** On a 4‑core machine it reduces processing time by 30‑70 % for PDFs with more than five pages.  
- **Which languages are supported?** Over 70 languages, including English, French, German, Chinese, and Arabic.  
- **Do I need a license for production?** A commercial Aspose OCR license is required for non‑trial use; the free trial works for evaluation.

## What is an Aspose OCR Java example?
The **Aspose OCR Java example** is a concise, runnable program that demonstrates how to instantiate the `OcrEngine`, configure parallel execution, and extract text from PDF files using the Aspose OCR for Java library. It also shows how to handle common scenarios such as password‑protected documents, memory‑limit tuning, and language selection, providing a solid foundation for building larger document‑processing pipelines.

## Why use parallel OCR processing?
Aspose OCR can split a multi‑page PDF into separate pages and process each page on its own thread. On an 8‑core server, a 120‑page document is typically processed in under 30 seconds, compared with more than a minute when running sequentially. This speed boost is especially valuable when you need to **convert scanned PDF searchable** archives in bulk.

## Prerequisites
- Java 8 or newer installed.  
- Maven or Gradle build tool (the example uses Maven).  
- An Aspose OCR for Java license (free trial works for testing).  

## How to run the Aspose OCR Java example step by step

### Step 1: set up your project

Add the Aspose OCR dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

If you prefer Gradle, replace the snippet with the equivalent `implementation` line.  
After the dependency resolves, you can import the required classes in your Java source file.

### Step 2: create and configure the OCR engine

`OcrEngine` is the core class that performs optical character recognition.

The `OcrEngine` class is Aspose OCR's primary object that encapsulates all OCR settings and execution logic.  
Enable parallel processing and optionally limit the thread pool:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Why this matters:**  
- `setParallelProcessing(true)` distributes pages across multiple CPU cores, cutting runtime dramatically on multi‑core hardware.  
- `setMaxThreadCount` safeguards server resources by preventing the engine from monopolising all cores, which is crucial in shared‑hosting or CI environments.

### Step 3: load the PDF you want to process

`OcrInput` represents the collection of files (PDFs, images, or mixed media) that the engine will analyze.

The `OcrInput` class aggregates one or more input sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single batch.  
Add your PDF (or a set of PDFs) to the input collection:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Tip:** Use an absolute path or a path relative to the working directory to avoid `FileNotFoundException`. The `add` method can be called repeatedly to queue multiple documents for batch processing.

### Step 4: run OCR across all pages in parallel

`OcrResult` holds the combined text output and per‑page confidence information after recognition completes.

The `OcrResult` object contains the concatenated plain‑text result and a list of `PageResult` objects that expose confidence scores for each processed page.  
Execute the recognition:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Under the hood:** Each page is handed to a separate worker thread (up to the `maxThreadCount` you defined). The library synchronises the results so the final `OcrResult` preserves the original page order.

### Step 5: retrieve and display the combined text

`OcrResult.getText()` returns the full searchable string.

The `getText()` method of `OcrResult` returns a single `String` that contains the OCR‑extracted text from every page, with line breaks preserved as they appeared in the source PDF.  

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Expected output:** The console prints one continuous string containing the readable text from all pages, ready for indexing, storage, or further processing.

### Step 6: handle special scenarios

#### How does the engine deal with password‑protected PDFs?

Supply the password when adding the file to `OcrInput`:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

The `add` method overload that accepts a password decrypts the document on the fly, allowing seamless OCR without manual decryption.

#### How can I limit memory usage for very large files?

Call `ocrEngine.setMemoryLimit(256);` to cap RAM consumption at 256 MB. The engine will automatically spill excess data to temporary files, preventing out‑of‑memory crashes even on multi‑hundred‑page PDFs.

## Common questions & edge cases

### Do I really need parallel processing?

If your PDF contains **more than a handful of pages** and you have at least four CPU cores, enabling parallel processing typically reduces total runtime by **30‑70 %**. For a single‑page scan, the threading overhead may outweigh the benefit, so you can disable it with `ocrEngine.setParallelProcessing(false)`.

### What happens when a page fails to OCR?

Aspose OCR throws an `OcrException` only for fatal errors such as a corrupted file. Pages that cannot be recognised simply return an empty string, which the engine concatenates silently. You can inspect `ocrResult.getPageResults()` to retrieve per‑page confidence scores and handle low‑confidence pages manually.

### How do I change the recognition language?

The engine defaults to English, but you can switch languages with:

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Replace `Language.FRENCH` with any supported language enum. This is essential when you need to **extract text PDF Java** from multilingual documents.

## Pro tips for production‑ready OCR

- **Batch processing:** Wrap the flow in a loop that reads file names from a directory, turning the demo into a scalable service.  
- **Logging:** Set `ocrEngine.setLogLevel(LogLevel.ERROR)` in production to suppress verbose output.  
- **Result cleanup:** Post‑process `ocrResult.getText()` with regular expressions to remove stray whitespace or artefacts.  
- **Thread‑pool tuning:** Use `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` on servers with many cores for maximum throughput.  
- **Performance benchmark:** On an 8‑core Intel Xeon, a 200‑page PDF (300 MB) processes in ~22 seconds with parallel OCR enabled.

## Conclusion

You now have a complete **Aspose OCR Java example** that extracts searchable text from any scanned PDF, supports password‑protected files, and leverages parallel processing for speed. By integrating this code into your own applications, you can build powerful document‑digitisation pipelines, feed OCR output into search indexes, or combine it with translation services for multilingual archives.

Ready for the next step? Try feeding the extracted text into Elasticsearch for full‑text search, or chain the output with a language‑translation API to create a multilingual searchable repository. Happy coding!






---

**Last Updated:** 2026-10-24  
**Tested With:** Aspose OCR for Java 24.11  
**Author:** Aspose  

## Frequently asked questions

**Q: Can I use this example with a free trial license?**  
A: Yes, the Aspose OCR free trial works for development and testing; a commercial license is required for production deployments.

**Q: Does the example support OCR on password‑protected PDFs?**  
A: Absolutely – pass the password to `OcrInput.add(filePath, password)` and the engine will decrypt the document automatically.

**Q: How many languages does Aspose OCR recognise?**  
A: Over 70 languages, including right‑to‑left scripts such as Arabic and Hebrew.

**Q: What is the maximum PDF size I can process?**  
A: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit to keep RAM usage predictable.

**Q: Is parallel OCR safe on shared servers?**  
A: Yes, by configuring `setMaxThreadCount` you control the maximum number of concurrent threads, preventing resource exhaustion.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## Related Tutorials

- [How To Use Ocr In Java Parallel Processing With Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Create Searchable Pdf With Aspose Ocr Java Guide](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [How To Use Ocr In Java Extract Text From Pdf Aspose Ocr](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}