---
category: general
date: 2026-02-17
description: Learn how to use OCR in Java to recognize text from image files, extract
  text from PNG receipts and convert receipt to JSON with Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: en
og_description: Step‑by‑step guide on how to use OCR in Java to recognize text from
  image, extract text from PNG receipts and convert receipt to JSON.
og_title: How to Use OCR in Java – Recognize Text from Image
tags:
- OCR
- Java
- Aspose
- Image Processing
title: How to Use OCR in Java – Recognize Text from Image Quickly
url: /java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR in Java – Recognize Text from Image Quickly

Ever wondered **how to use OCR** to pull text out of a photo of a receipt? Maybe you’ve tried a few online tools, only to end up with garbled characters or a format you can’t parse. The good news is that with a few lines of Java code you can **recognize text from image** files, **extract text from PNG** receipts, and even **convert receipt to JSON** for downstream processing.  

In this tutorial we’ll walk through the complete workflow—from licensing the Aspose OCR library to getting a clean JSON payload you can feed into a database or a machine‑learning model. No fluff, just a practical, runnable example you can copy‑paste into your IDE. By the end you’ll have a self‑contained program that takes `receipt.png` and spits out a ready‑to‑use JSON string.

## What You’ll Need

- **Java Development Kit (JDK) 8+** – any recent version works.
- **Aspose OCR for Java** library (the Maven artifact is `com.aspose:aspose-ocr`).
- A **valid Aspose OCR license file** (`Aspose.OCR.lic`). The free trial works for testing, but a proper license removes evaluation limits.
- An image file (PNG, JPEG, etc.) that contains the text you want to read—let’s call it `receipt.png` and place it in a known folder.
- Your favorite IDE (IntelliJ IDEA, Eclipse, VS Code…) – you’re free to choose.

> **Pro tip:** Keep your license file outside the source folder and reference it via an absolute or relative path to avoid committing it to version control.

Now that the prerequisites are clear, let’s dive into the actual code.

## How to Use OCR – Core Steps

Below is a high‑level overview of the actions we’ll perform:

1. **Load the Aspose OCR library** and apply your license.  
2. **Create an `OcrEngine` instance** – this is the engine that does the heavy lifting.  
3. **Prepare an `OcrInput` object** pointing at the image you want to process.  
4. **Call `recognize` with `ResultFormat.JSON`** to get a JSON representation of the extracted text.  
5. **Handle the JSON output** – print it, write it to a file, or parse it further.

Each step is explained in detail in the sections that follow.

## Step 1 – Install Aspose OCR and Apply Your License

First, add the Aspose OCR dependency to your `pom.xml` if you’re using Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Now, in your Java code, load the license. This step is essential; without it the library runs in evaluation mode and may embed watermarks in the output.

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

> **Why this matters:** The `License` object tells the OCR engine that you’re authorized to use the full feature set, which includes high‑accuracy recognition and JSON export. Skipping this step will still let you **recognize text from image**, but the results may be throttled.

## Step 2 – Create the OCR Engine Instance

The `OcrEngine` class is the entry point for all OCR operations. Think of it as the “brain” that reads the pixels and decides what characters they represent.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

You can customize the engine (e.g., set language, enable deskew) later if your receipts contain non‑Latin scripts or are scanned at an angle. For most US‑based receipts, the defaults work just fine.

## Step 3 – Load the Image You Want to Process

Now we’ll point the OCR engine at the file that holds the receipt. The `OcrInput` class can accept multiple images, but for this tutorial we’ll keep it simple with a single PNG.

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

If you ever need to **extract text from PNG** files in bulk, just call `input.add()` repeatedly or pass a list of file paths.

## Step 4 – Recognize Text and Convert Receipt to JSON

Here’s the heart of the tutorial. We ask the engine to recognize the text and ask for the result in JSON format. The `ResultFormat.JSON` flag does all the heavy lifting for us.

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

The JSON payload includes each recognized line, its bounding box, confidence score, and the raw text. This structure makes it trivial to **convert receipt to JSON** and then feed it into any downstream API.

## Step 5 – Put It All Together and Run the Program

Below is the complete, ready‑to‑run Java class that ties everything together. Save it as `JsonExportDemo.java` (or any name you like) and run it from your IDE or command line.

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

### Expected Output

Running the program prints a JSON string similar to the following (the exact content depends on your receipt):

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

You can now feed this JSON into a database, a REST endpoint, or a data‑analysis pipeline. The **convert receipt to JSON** step is already done for you.

## Common Questions and Edge Cases

### What if the image is rotated?

Aspose OCR automatically detects and corrects mild rotations. For severely skewed images, call `engine.getImagePreprocessingOptions().setDeskew(true)` before recognition.

### How do I handle multiple languages?

Use `engine.getLanguage()` to set the desired language, e.g., `engine.setLanguage(Language.FRENCH)`. This is handy when you need to **recognize text from image** that contains multilingual receipts.

### Can I output plain text instead of JSON?

Absolutely. Replace `ResultFormat.JSON` with `ResultFormat.TEXT` and call `result.getText()`.

### Is there a way to limit the OCR to a specific region?

Yes—use `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` to focus on the receipt area, which can improve speed and accuracy.

## Pro Tips for Production‑Ready OCR

- **Cache the license** object if you’re processing many files in a loop; creating it repeatedly adds overhead.
- **Batch process**: load all receipt paths into a single `OcrInput` and call `recognize` once. The JSON will contain an array of pages, each with its own lines.
- **Validate JSON**: after you get the string, parse it with a library like Jackson to ensure it’s well‑formed before storing it.
- **Monitor confidence**: the JSON includes a `confidence` field per line. Filter out lines below a threshold (e.g., 0.85) to avoid garbage data.
- **Secure your license**: store `Aspose.OCR.lic` in a secure vault or environment variable, especially in cloud deployments.

## Conclusion

We’ve covered **how to use OCR** in Java to **recognize text from image**, **extract text from PNG** receipts, and **convert receipt to JSON**—all with a concise, end‑to‑end example. The steps are straightforward, the code is fully runnable, and the JSON output gives you a structured representation ready for any downstream system.

Next, you might explore more advanced scenarios: feeding the JSON into Apache Kafka for real‑time processing, applying regex patterns to pull out line‑item totals, or integrating with a cloud OCR service for scalability. Whatever you choose, the fundamentals you’ve just learned will stay the same.

Got questions, or ran into a hiccup while trying this out? Drop a comment below, and let’s troubleshoot together. Happy coding, and enjoy turning those messy receipt images into clean, searchable data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}