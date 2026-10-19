---
category: general
date: 2026-05-25
description: Extract text from image in Java using OCR. Learn how to load image for
  OCR, recognize text from photo, and get text from OCR with a simple code example.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: en
og_description: Extract text from image in Java with a step‑by‑step guide. Learn to
  load image for OCR, recognize text from photo, and get text from OCR efficiently.
og_title: Extract Text from Image in Java – Get Text from OCR
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
title: Extract Text from Image in Java – Get Text from OCR
url: /java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in Java – Get Text from OCR

Ever needed to **extract text from image** but weren’t sure which Java library to pick? You’re not alone. Whether you’re digitizing receipts, pulling serial numbers from product photos, or just playing with a fun side project, turning a picture into editable text is a common hurdle.

In this tutorial we’ll walk through a complete, ready‑to‑run example that shows you how to **load image for OCR**, configure the engine, and finally **recognize text from photo** so you can **get text from OCR** with just a few lines of code. No vague references—everything you need is right here.

## What You’ll Learn

* How to set up a lightweight OCR engine in Java.  
* The exact steps to **load image for OCR** and handle different file paths.  
* Why configuring the language matters when you want to **extract text from image** that isn’t English.  
* How to safely output the result and what to do when the engine returns nothing.  
* A handful of pro tips to avoid the most common pitfalls.

By the end of this guide you’ll have a self‑contained program that reads a JPEG (or PNG) containing Ukrainian characters and prints the recognized string to the console. Feel free to swap the language or image—everything is modular.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: Flow diagram of extract text from image process in Java.*

## Prerequisites

* **Java Development Kit (JDK) 11+** – the code uses the modern module system, but older versions work with minor tweaks.  
* **Maven or Gradle** – to pull the OCR library (we’ll use **Asprise OCR** as a lightweight, free‑for‑development option).  
* A sample image file (e.g., `ukrainian_sign.jpg`) placed somewhere your program can read.  
* Basic familiarity with Java’s `main` method and exception handling.

If you’ve got these, you’re good to go. Otherwise, grab the JDK from Oracle or AdoptOpenJDK and set up a simple Maven project—nothing too fancy.

---

## Step 1: Add the OCR Dependency

First, tell your build tool to fetch the OCR engine. For Maven, drop this into `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

If you prefer Gradle, the equivalent is:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

These coordinates pull a compact JAR that includes `OcrEngine`, `OcrLanguage`, and the helper classes we’ll use. No extra native binaries are required for basic Latin and Cyrillic scripts.

---

## Step 2: Create a Java Class to **Extract Text from Image**

Now we’ll write the actual program. Save the following as `ExtractTextDemo.java` inside `src/main/java/com/example/ocr/`.

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

### Why This Structure Works

* **Separate numbered blocks** make the flow easy to follow, especially when you’re scanning for where to **load image for OCR** or **recognize text from photo**.  
* The `try/catch` around image loading and recognition ensures the program fails gracefully—useful when the file path is wrong or the OCR engine can’t find language data.  
* Setting the language early (step 2) dramatically improves accuracy for non‑English scripts. If you later need **java image to text** for other languages, just swap `OcrLanguage.UKRAINIAN` for `OcrLanguage.ENGLISH`, `FRENCH`, etc.

---

## Step 3: Build and Run the Program

From the project root, execute:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Or, if you’re using Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Assuming `ukrainian_sign.jpg` contains the text *«Ласкаво просимо»* (Ukrainian for “Welcome”), you should see something like:

```
=== OCR Result ===
Ласкаво просимо
```

That output confirms you successfully **extract text from image** and **get text from OCR** in a single run.

---

## Step 4: Tweak the Workflow – From **Java Image to Text** in Real Projects

While the demo is minimal, real‑world applications often need a bit more:

| Scenario | What to Adjust | Reason |
|----------|----------------|--------|
| **Batch processing** | Loop over a `List<Path>` and store each result in a database. | Reduces manual work when you have hundreds of photos. |
| **Different image formats** | Use `ImageIO.read(new File(path))` to pre‑process, then pass the `BufferedImage` to `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Handles PNG, BMP, or even PDFs after conversion. |
| **Performance tuning** | Call `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` if you’re okay with slightly lower accuracy. | Speeds up recognition on low‑end hardware. |
| **Post‑processing** | Trim whitespace, replace common OCR mis‑reads (`0` → `O`, `1` → `I`). | Improves downstream data quality. |

These variations keep the core idea—**recognize text from photo**—intact while giving you flexibility for production workloads.

---

## Common Pitfalls & Pro Tips

1. **Wrong language setting** – If you forget step 2, the engine defaults to English, turning Cyrillic characters into gibberish. Always double‑check the language code.  
2. **Image quality matters** – Low‑resolution or blurry photos will degrade accuracy. Pre‑process with contrast enhancement or binarization if needed.  
3. **File path quirks** – On Windows, backslashes need escaping (`C:\\images\\file.jpg`). Using `Path.of(...)` from `java.nio.file` sidesteps this.  
4. **Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()` when you’re done, especially in long‑running services.  
5. **Thread safety** – The engine isn’t thread‑safe out of the box. Create a separate instance per thread or synchronize access.

---

## Full Working Example (All‑In‑One)

Below is a single file you can copy‑paste into any IDE. It includes the `dispose()` call and a tiny helper method to make the code a bit cleaner.

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

Running this program yields the same console output shown earlier. Feel free to replace `OcrLanguage.UKRAINIAN` with `OcrLanguage.ENGLISH` or any other supported language to see how the engine adapts.

---

## Conclusion

We’ve walked through everything you need to **extract text from image** using Java: from adding the OCR dependency, to **load image for OCR**,


## Related Tutorials

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}