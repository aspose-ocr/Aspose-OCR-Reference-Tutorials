---
category: general
date: 2026-01-02
description: แปลงภาพเป็นข้อความด้วย Java โดยใช้ Aspose OCR. เชี่ยวชาญการประมวลผล OCR
  แบบชุด, อ่านภาพจากโฟลเดอร์, และกรองไฟล์ตามนามสกุล.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: th
og_description: แปลงภาพเป็นข้อความอย่างรวดเร็วด้วย Java บทเรียนนี้ครอบคลุมการประมวลผล
  OCR แบบเป็นชุด การอ่านภาพจากโฟลเดอร์ และการกรองไฟล์ตามนามสกุล
og_title: แปลงรูปภาพเป็นข้อความใน Java – คู่มือ OCR แบบแบตช์ครบวงจร
tags:
- OCR
- Java
- Aspose
title: แปลงรูปภาพเป็นข้อความใน Java – คู่มือการประมวลผล OCR แบบชุด
url: /th/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงรูปภาพเป็นข้อความใน Java – คู่มือการประมวลผล OCR แบบแบตช์

Ever needed to **convert images to text** but weren't sure how to handle dozens of files at once? You're not alone—developers constantly wrestle with pulling data out of PNGs, JPGs, and other scans. The good news? With Aspose OCR you can spin up a batch OCR processing pipeline in minutes, read images from folder structures, and even filter files by extension so you only work on what matters.

เคยต้องการ **แปลงรูปภาพเป็นข้อความ** แต่ไม่แน่ใจว่าจะจัดการกับไฟล์หลายสิบไฟล์พร้อมกันอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาต่าง ๆ มักต้องต่อสู้กับการดึงข้อมูลจาก PNG, JPG และสแกนอื่น ๆ ข่าวดีคืออะไร? ด้วย Aspose OCR คุณสามารถสร้างสายการประมวลผล OCR แบบแบตช์ได้ในไม่กี่นาที, อ่านรูปภาพจากโครงสร้างโฟลเดอร์, และแม้กระทั่งกรองไฟล์ตามนามสกุลเพื่อให้คุณทำงานกับสิ่งที่สำคัญเท่านั้น.

In this tutorial we'll build a self‑contained Java program that walks a directory, picks out every `.png` or `.jpg`, sends each picture to Aspose OCR asynchronously, and prints the extracted text in the original order. By the end you'll have a reusable snippet you can drop into any project that needs to **convert images to text** at scale.

ในบทเรียนนี้ เราจะสร้างโปรแกรม Java ที่ทำงานอิสระซึ่งเดินผ่านไดเรกทอรี, เลือกไฟล์ `.png` หรือ `.jpg` ทุกไฟล์, ส่งรูปแต่ละรูปไปยัง Aspose OCR อย่างอะซิงโครนัส, และพิมพ์ข้อความที่สกัดออกมาในลำดับเดิม. เมื่อเสร็จคุณจะมีโค้ดสั้นที่สามารถนำไปใช้ในโปรเจกต์ใด ๆ ที่ต้องการ **แปลงรูปภาพเป็นข้อความ** ในระดับใหญ่.

---

![ตัวอย่างการแปลงรูปภาพเป็นข้อความ](https://example.com/convert-images-to-text.png "ภาพหน้าจอของผลลัพธ์คอนโซล Java แสดงข้อความที่แปลงจากไฟล์ PNG")

## สิ่งที่คุณจะสร้าง

- A single `AsposeOCR` engine shared across threads (efficient and thread‑safe).  
- A `ParallelRecognizer` that runs OCR jobs in parallel, perfect for **batch OCR processing**.  
- Logic that **reads images from folder** using `java.nio.file.Files`.  
- Simple filters to **extract text from PNG** files while still handling JPGs.  
- Clean shutdown of the internal thread pool to avoid resource leaks.

### ข้อกำหนดเบื้องต้น

- Java 17 (หรือเวอร์ชัน LTS ล่าสุดใด ๆ).  
- Maven หรือ Gradle เพื่อดึงไลบรารี Aspose OCR.  
- โฟลเดอร์ที่เต็มไปด้วยรูปภาพ PNG/JPG ที่คุณต้องการประมวลผล.  
- ความคุ้นเคยพื้นฐานกับ Java streams—ไม่จำเป็นต้องมีความซับซ้อนใด ๆ.

> **เคล็ดลับ:** หากคุณยังไม่มีลิขสิทธิ์, Aspose มีคีย์ชั่วคราวฟรีที่คุณสามารถใช้สำหรับการทดสอบ.

## ขั้นตอนที่ 1 – ตั้งค่าโปรเจกต์และเพิ่ม Aspose OCR

First, create a new Maven project (or Gradle, your call). Add the Aspose OCR dependency to `pom.xml`:

ขั้นแรก, สร้างโปรเจกต์ Maven ใหม่ (หรือ Gradle, ตามที่คุณต้องการ). เพิ่มการพึ่งพา Aspose OCR ลงใน `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **ทำไมเรื่องนี้สำคัญ:** การประกาศการพึ่งพาล่วงหน้าช่วยให้คอมไพเลอร์เห็น `AsposeOCR`, `ParallelRecognizer` และคลาสที่เกี่ยวข้อง. นอกจากนี้ยังรับประกันว่าเวอร์ชันเดียวกันจะถูกใช้บนเครื่องทั้งหมด, ซึ่งเป็นสิ่งสำคัญสำหรับการประมวลผล OCR แบบ **แบตช์** ที่ทำซ้ำได้.

Once the build finishes, refresh your IDE and you should see the Aspose packages under `External Libraries`.

เมื่อการสร้างเสร็จสิ้น, รีเฟรช IDE ของคุณและคุณควรเห็นแพ็กเกจ Aspose ภายใต้ `External Libraries`.

## ขั้นตอนที่ 2 – แปลงรูปภาพเป็นข้อความ – เริ่มต้นเครื่องมือ OCR

We only need **one** OCR engine instance for the whole run. Sharing it across threads saves memory and speeds things up because the engine loads language packs just once.

เราต้องการเพียง **หนึ่ง** อินสแตนซ์ของเครื่องมือ OCR สำหรับการทำงานทั้งหมด. การแชร์มันระหว่างเธรดช่วยประหยัดหน่วยความจำและเร่งความเร็วเนื่องจากเครื่องมือโหลดแพ็คเกจภาษาเพียงครั้งเดียว.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

> **คำอธิบาย:** `ParallelRecognizer` ห่อหุ้มเครื่องมือใน thread‑pool. เมื่อคุณส่งไฟล์หลายไฟล์, แต่ละไฟล์จะได้รับเธรดทำงานของตนเอง, ทำให้เกิดการทำงานขนานจริงบน CPU หลายคอร์.

## ขั้นตอนที่ 3 – อ่านรูปภาพจากโฟลเดอร์ – เดินผ่านโครงสร้างไดเรกทอรี

Now we need to **read images from folder** and collect every PNG or JPG. The `Files.walk` API makes this a one‑liner, but we’ll add a filter to **extract text from PNG** only when needed.

ตอนนี้เราต้อง **อ่านรูปภาพจากโฟลเดอร์** และรวบรวมทุกไฟล์ PNG หรือ JPG. API `Files.walk` ทำให้เรื่องนี้เป็นบรรทัดเดียว, แต่เราจะเพิ่มตัวกรองเพื่อ **สกัดข้อความจาก PNG** เฉพาะเมื่อจำเป็น.

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

> **ทำไมต้องกรองที่นี่:** การใช้ `filter` ทำให้เราสามารถ **กรองไฟล์ตามนามสกุล** ได้ตั้งแต่ต้น, ลดการทำ I/O ที่ไม่จำเป็นในภายหลัง. มันยังทำให้โค้ดอ่านง่าย—ไม่ต้องใช้ regex ซับซ้อน.

## ขั้นตอนที่ 4 – การประมวลผล OCR แบบแบตช์ – ส่งงานแบบอะซิงโครนัส

With the list of files ready, we push each path to the `ParallelRecognizer`. The `recognizeAsync` method returns a `Future<OcrResult>` that we store for later retrieval.

เมื่อรายการไฟล์พร้อม, เราจะผลักดันแต่ละพาธไปยัง `ParallelRecognizer`. เมธอด `recognizeAsync` จะคืนค่า `Future<OcrResult>` ที่เราจะเก็บไว้เพื่อดึงข้อมูลในภายหลัง.

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

> **อะไรกำลังเกิดขึ้นเบื้องหลัง?** แต่ละการเรียกจะใส่งานลงในคิวของบริการ executor ภายในของ recognizer. งานเหล่านี้ทำงานแบบขนาน, ดังนั้นโฟลเดอร์ที่มี 100 รูปภาพสามารถประมวลผลได้ในส่วนหนึ่งของเวลาที่ลูปแบบเธรดเดียวจะใช้.

## ขั้นตอนที่ 5 – ดึงผลลัพธ์ตามลำดับเดิม – รักษาลำดับไฟล์

Because we stored the futures in the same order as `imagePaths`, we can simply iterate over the list and call `get()`. The call blocks only until that particular image is done, preserving order without extra bookkeeping.

เนื่องจากเราเก็บ futures ไว้ในลำดับเดียวกับ `imagePaths`, เราสามารถวนลูปผ่านรายการและเรียก `get()` ได้โดยตรง. การเรียกนี้จะบล็อกเฉพาะจนกว่ารูปภาพนั้นจะเสร็จ, ทำให้รักษาลำดับโดยไม่ต้องบันทึกเพิ่มเติม.

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**ตัวอย่างผลลัพธ์คอนโซล** (ตัดทอนเพื่อความกระชับ):

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

> **การจัดการกรณีขอบ:** หากรูปภาพใด ๆ ทำให้เกิดข้อยกเว้น (ไฟล์เสีย, รูปแบบไม่รองรับ), เราจะจับข้อยกเว้นและดำเนินการต่อกับไฟล์ที่เหลือ—เป็นนิสัยสำคัญสำหรับการทำงานของ **pipeline การประมวลผล OCR แบบแบตช์** ที่เชื่อถือได้.

## ขั้นตอนที่ 6 – ทำความสะอาด – ปิดการทำงานของ Recognizer

Never forget to shut down the internal thread pool; otherwise your JVM may hang on exit.

อย่าลืมปิด thread pool ภายใน; มิฉะนั้น JVM ของคุณอาจค้างเมื่อออก.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

That’s it! The program will now walk any directory, filter for PNG/JPG files, run OCR in parallel, and print the results.

เท่านี้! โปรแกรมจะเดินผ่านไดเรกทอรีใด ๆ, กรองไฟล์ PNG/JPG, รัน OCR แบบขนาน, และพิมพ์ผลลัพธ์.

## ตัวอย่างการทำงานเต็มรูปแบบ

Below is the complete, copy‑and‑paste‑ready Java class. Replace `"YOUR_DIRECTORY"` with the path to your images folder and run it from your IDE or command line.

ด้านล่างเป็นคลาส Java ที่พร้อมคัดลอก‑วางเต็มรูปแบบ. แทนที่ `"YOUR_DIRECTORY"` ด้วยพาธไปยังโฟลเดอร์รูปภาพของคุณและรันจาก IDE หรือบรรทัดคำสั่ง.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

Run the class, watch the console fill with extracted strings, and celebrate the fact that you just **converted images to text** without writing a single loop that blocks on I/O.

รันคลาส, ดูคอนโซลเต็มไปด้วยสตริงที่สกัด, และเฉลิมฉลองว่าคุณเพิ่ง **แปลงรูปภาพเป็นข้อความ** โดยไม่ต้องเขียนลูปเดียวที่บล็อก I/O.

## คำถามที่พบบ่อย (FAQs)

**Q: ฉันสามารถประมวลผล PDF หรือ TIFF ได้เช่นกันหรือไม่?**  
A: แน่นอน. Aspose OCR รองรับหลายรูปแบบ—เพียงเพิ่มนามสกุลไฟล์ที่เหมาะสมในตัวกรองที่ขั้นตอน 2.

**Q: ถ้าฉันต้องการภาษาต่าง ๆ เช่น สเปน?**  
A: เปลี่ยน `RecognitionLanguage.ENGLISH` เป็น `RecognitionLanguage.SPANISH`. ตรวจสอบให้แน่ใจว่าแพ็คเกจภาษาถูกติดตั้ง (Aspose มีภาษาหลักส่วนใหญ่ให้ใช้โดยอัตโนมัติ).

**Q: โฟลเดอร์ของฉันมีโฟลเดอร์ย่อย—จะถูกสแกนหรือไม่?**  
A: ใช่. `Files.walk` จะเดินผ่านต้นไม้ทั้งหมดแบบเรียกซ้ำ, ดังนั้นทุก PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}