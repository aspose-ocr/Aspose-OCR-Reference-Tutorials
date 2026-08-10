---
category: general
date: 2026-05-25
description: How to get OCR in Java and extract raw text from images. Learn to turn
  off spell correction, recognize handwritten text, and how to load image efficiently.
draft: false
keywords:
- how to get ocr
- extract raw text
- turn off spell correction
- recognize handwritten text
- how to load image
language: en
og_description: How to get OCR in Java and extract raw text from an image. This guide
  shows how to turn off spell correction, recognize handwritten text, and how to load
  image correctly.
og_title: How to Get OCR in Java – Extract Raw Text Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  headline: How to Get OCR in Java – Complete Guide to Extract Raw Text
  type: TechArticle
- description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  name: How to Get OCR in Java – Complete Guide to Extract Raw Text
  steps:
  - name: Maven Dependency
    text: If you’re using Maven, paste this into your `pom.xml`. It pulls the latest
      Aspose.OCR library (as of May 2026).
  - name: Gradle Alternative
    text: '```gradle implementation ''com.aspose:aspose-ocr:23.11'' ```'
  - name: Expected Output
    text: 'Assuming `handwritten.png` contains the phrase *“Hello World”* written
      in cursive, you’ll see something like:'
  type: HowTo
tags:
- OCR
- Java
- Aspose.OCR
title: How to Get OCR in Java – Complete Guide to Extract Raw Text
url: /java/advanced-ocr-techniques/how-to-get-ocr-in-java-complete-guide-to-extract-raw-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Get OCR in Java – Complete Guide to Extract Raw Text

Ever wondered **how to get OCR** results without the library’s automatic clean‑up? Maybe you’re dealing with a handwritten note and you need the exact characters the engine saw, not a “pretty‑printed” version. In this tutorial we’ll walk through a hands‑on example that shows exactly **how to get OCR** output, how to **extract raw text**, and why you might want to **turn off spell correction** when recognizing handwritten text. By the end you’ll also know **how to load image** files into the Aspose OCR engine without a hitch.

We’ll use Aspose.OCR for Java, but the concepts translate to any OCR SDK that offers a spell‑corrector toggle. No heavy theory—just a practical, copy‑and‑paste solution you can run today.

---

## What You’ll Learn

- How to set up Aspose.OCR in a Java project  
- The exact steps **how to get OCR** raw output  
- Why and **how to turn off spell correction** for pristine text  
- The best way **how to load image** files for optimal recognition  
- How to **recognize handwritten text** and verify the result  

Prerequisites are minimal: Java 8+ installed, a Maven‑compatible IDE (IntelliJ, Eclipse, or VS Code), and a sample image containing handwritten characters. If you’re missing any of those, just grab the JDK from Oracle and the image from your phone—no problem.

---

![Diagram illustrating the OCR workflow, showing how to get OCR raw text from an image](/images/ocr-workflow.png){: .center alt="how to get OCR raw text workflow"}

---

## Step 1: Add Aspose.OCR to Your Project

### Maven Dependency

If you’re using Maven, paste this into your `pom.xml`. It pulls the latest Aspose.OCR library (as of May 2026).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **Pro tip:** Always check the official Aspose Maven repository for newer versions. The `23.11` release adds better support for cursive scripts, which is handy when you **recognize handwritten text**.

### Gradle Alternative

```gradle
implementation 'com.aspose:aspose-ocr:23.11'
```

Once the dependency resolves, you’re ready to write code that actually **gets OCR** results.

---

## Step 2: Create the OCR Engine Instance

The engine is the heart of the process. Instantiating it is straightforward, but the real magic begins when you configure it.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

Why do we need a dedicated `OcrEngine` object? It stores all runtime options, including the spell‑corrector toggle we’ll touch next. Keeping the engine isolated also lets you run multiple recognitions in parallel without cross‑contamination.

---

## Step 3: Turn Off Spell Correction (If You Need Raw Output)

Most OCR libraries try to be helpful by correcting misspelled words automatically. That’s great for printed text but disastrous for raw data extraction. Here’s how to **turn off spell correction**:

```java
        // Step 3: Turn off the built‑in spell‑corrector to get raw text
        engine.getEngineOptions().setSpellCorrectorEnabled(false);
```

When the flag is `false`, the engine returns exactly what it saw on the bitmap, preserving line breaks, punctuation, and even the occasional stray glyph. This is essential when you later feed the output into a machine‑learning pipeline that expects the original noise.

---

## Step 4: Load the Image – The Proper Way

You might think `engine.getImage().loadFromFile("path")` is enough, but there are a few nuances:

1. **Absolute vs. relative paths** – Use `Paths.get(...)` for platform independence.  
2. **Supported formats** – Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF.  
3. **Resolution matters** – Higher DPI yields better recognition, especially for cursive writing.

Here’s a robust snippet that demonstrates **how to load image** safely:

```java
        // Step 4: Load the image that contains handwritten text
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        // Validate the file exists
        java.nio.file.Path path = java.nio.file.Paths.get(imagePath);
        if (!java.nio.file.Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }

        // Load the image into the OCR engine
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());
```

If you’re dealing with a stream (e.g., uploading from a web form), replace `loadFromFile` with `loadFromStream`. The key takeaway: always verify the file before feeding it to the engine, because a missing file throws a vague `NullPointerException` that can be hard to debug.

---

## Step 5: Perform the Recognition

Now the moment of truth arrives—**how to get OCR** results. The `recognize()` method runs the internal pipeline, applying language models, segmentation, and (if enabled) spell correction. Since we disabled it, you’ll receive the untouched characters.

```java
        // Step 5: Perform OCR recognition
        OcrResult result = engine.recognize();
```

The `OcrResult` object holds more than just text; you can also retrieve confidence scores, bounding boxes, and even per‑character probabilities. For this tutorial we’ll focus on the plain text.

---

## Step 6: Output the Raw OCR Result

Finally, print the result to the console. This is the simplest way to **extract raw text** for debugging or downstream processing.

```java
        // Step 6: Output the raw OCR result
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

### Expected Output

Assuming `handwritten.png` contains the phrase *“Hello World”* written in cursive, you’ll see something like:

```
Raw OCR output:
H e l l o   W o r l d
```

Notice the extra spaces—those are intentional because the engine preserves the exact spacing it detected. If you later need to collapse whitespace, do it in your own post‑processing step.

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Empty string** | Image DPI too low or image is completely white. | Ensure the source image is at least 300 DPI; use `engine.getImage().setResolution(300, 300)`. |
| **Garbage characters** | Wrong file format or corrupted bytes. | Verify the file with an image viewer; re‑export as PNG. |
| **Spell‑corrector still active** | Accidentally re‑enabled elsewhere in code. | Keep the `setSpellCorrectorEnabled(false)` call right after engine creation. |
| **Handwritten text not recognized** | Engine default language set to English printed text. | Call `engine.getEngineOptions().setLanguage(Language.English);` and optionally `engine.getEngineOptions().setUseDictionary(false);`. |

---

## Extending the Example: Recognizing Handwritten Text

If your use‑case specifically targets **recognize handwritten text**, you can tweak a couple of options for better accuracy:

```java
        // Enable handwritten mode (available in 23.11+)
        engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);
```

This tells the internal neural network to favor cursive patterns over printed glyphs. In practice, you’ll see a noticeable jump in confidence scores for signatures, notes, or quick sketches.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete, self‑contained Java class that incorporates all the steps we discussed. Just replace `YOUR_DIRECTORY/handwritten.png` with the path to your own image and run it.

```java
import com.aspose.ocr.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Turn off spell correction to get raw output
        engine.getEngineOptions().setSpellCorrectorEnabled(false);

        // Optional: set handwritten mode if needed
        // engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);

        // 3️⃣ Load the image (how to load image safely)
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        Path path = Paths.get(imagePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());

        // 4️⃣ Perform OCR (how to get OCR raw text)
        OcrResult result = engine.recognize();

        // 5️⃣ Print raw result (extract raw text)
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

Run it with:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectDemo
```

You should see the raw characters printed exactly as the engine read them.

---

## Conclusion

We’ve covered **how to get OCR** raw results in Java, demonstrated the proper way to **turn off spell correction**, showed the best practice **how to load image**, and explained the nuances of **recognize handwritten text**. By following these steps you’ll be able to **extract raw text** reliably, whether you’re building a document‑digitization pipeline, a forensic analysis tool, or a simple note‑taking app.

Next up, you might want to explore:

- **Post‑processing**: trimming whitespace, normalizing Unicode, or feeding the output into a language model.  
- **Batch processing**: looping over a directory of images and storing results in a database.  
- **Advanced options**: tweaking `EngineOptions` for multi‑language support or custom dictionaries.

Give those a try, and feel free to drop your questions in the comments. Happy coding, and may your OCR be ever accurate!


## Related Tutorials

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}