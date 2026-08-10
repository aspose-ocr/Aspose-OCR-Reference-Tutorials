---
category: general
date: 2026-07-21
description: ดึงข้อความจากภาพด้วย Java OCR. เรียนรู้วิธีแปลง PNG เป็นข้อความ, อ่านข้อความจาก
  PNG, โหลดภาพสำหรับ OCR, และทำ OCR บนภาพเพียงไม่กี่ขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: th
lastmod: 2026-07-21
og_description: ดึงข้อความจากภาพด้วย Java คู่มือนี้จะแสดงวิธีแปลง PNG เป็นข้อความ,
  อ่านข้อความจาก PNG, โหลดภาพสำหรับ OCR, และทำ OCR บนภาพอย่างมีประสิทธิภาพ.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: ดึงข้อความจากรูปภาพใน Java – คู่มือ OCR ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: ดึงข้อความจากภาพใน Java – คู่มือ OCR ฉบับสมบูรณ์
url: /th/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพใน Java – คู่มือ OCR ฉบับสมบูรณ์

เคยต้องการ **extract text from image** แต่ไม่แน่ใจว่าจะเลือกไลบรารี Java ตัวไหน? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะทำการดิจิไทซ์ใบเสร็จ, สแกน PDF, หรือสร้างคลังข้อมูลที่ค้นหาได้ การดึงข้อความออกจาก PNG เป็นปัญหาประจำวันของนักพัฒนาหลายคน

ในบทเรียนนี้เราจะพาคุณผ่านโซลูชันแบบทำมือที่ทำให้คุณ **convert PNG to text**, **read text from PNG**, **load image for OCR**, และ **perform OCR on image**—ทั้งหมดด้วยไม่กี่บรรทัดของโค้ด Java ที่สะอาดตา เมื่อเสร็จสิ้นคุณจะมีโปรแกรมที่รันได้และสามารถนำไปใส่ในโปรเจกต์ใดก็ได้

## สิ่งที่คุณจะสร้าง

เราจะสร้างแอปคอนโซล Java เล็ก ๆ ที่:

1. โหลดไฟล์ PNG จากดิสก์  
2. ส่งภาพไปยังเอนจิน OCR (Tess4J, ตัวห่อหุ้ม Java สำหรับ Tesseract)  
3. พิมพ์ข้อความที่ได้รับการจดจำออกทางคอนโซล

ไม่มีบริการภายนอก, ไม่มีเวทมนตร์—เพียงแค่ Java แท้ ๆ และเอนจิน OCR แบบโอเพนซอร์ส

## ข้อกำหนดเบื้องต้น

- **Java 17** หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับเวอร์ชันเก่าได้, แต่ Java 17 ให้ฟีเจอร์ภาษาใหม่ล่าสุด)  
- **Maven** หรือ **Gradle** สำหรับจัดการ dependencies  
- PNG ตัวอย่างชื่อ `sample.png` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้ (เช่น `src/main/resources`)  
- ความคุ้นเคยพื้นฐานกับเมธอด `main` ของ Java และการจัดการข้อยกเว้น

หากมีส่วนใดที่คุณไม่คุ้นเคย, อย่ากังวล—แต่ละขั้นตอนจะมีการสรุปสั้น ๆ ให้คุณตามมา

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่มไลบรารี OCR

เริ่มต้นด้วยการสร้างโปรเจกต์ Maven ใหม่ (หรือ Gradle หากคุณชอบ) แล้วเพิ่ม dependency ของ Tess4J ซึ่งจะดึงไบนารีของ Tesseract มาให้คุณโดยอัตโนมัติ

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **เคล็ดลับ:** หากคุณใช้ Gradle, บรรทัดที่เทียบเท่าคือ `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

การเพิ่มไลบรารีนี้จะทำให้คุณได้คลาส `Tesseract` ที่รับหน้าที่ **performing OCR on image** ให้คุณ

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR

ต่อไปเราต้อง **load image for OCR** Tess4J ทำงานกับ `java.awt.image.BufferedImage` ดังนั้นเราจะอ่าน PNG ด้วย `ImageIO`

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

เมธอดด้านบนแยกส่วน **load image for OCR** อย่างชัดเจน ทำให้โค้ดส่วนอื่นง่ายต่อการทดสอบ สังเกตคอมเมนต์ – มันสะท้อนสแนปเพล็ตเดิมพร้อมขยายความเพื่อความชัดเจน

## ขั้นตอนที่ 3: ทำ OCR บนภาพ

เมื่อภาพอยู่ในหน่วยความจำแล้ว เราสามารถ **perform OCR on image** ได้ทันที อินสแตนซ์ `Tesseract` คือเอนจินของเรา; เราจะตั้งค่าให้ใช้ข้อมูลภาษาอังกฤษเริ่มต้นที่มาพร้อมกับ Tess4J

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

ที่นี่เราได้รวม “Step 1” และ “Step 4” ดั้งเดิมไว้ในเมธอดเดียว เนื่องจากการสร้างอ็อบเจกต์ `Tesseract` มีค่าใช้จ่ายต่ำและเราต้องการให้โค้ดกระชับ คอมเมนต์ยังคงอ้างอิงขั้นตอนเดิมเพื่อความสามารถในการติดตาม

## ขั้นตอนที่ 4: รวมทุกอย่างเข้าด้วยกัน – เมธอด main

สุดท้ายเราจะนำทุกอย่างมารวมกันใน `main` ที่นี่คุณจะ **read text from PNG** และเห็นผลลัพธ์ที่พิมพ์ออกทางคอนโซล

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

เมื่อคุณรัน `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (หรือคำสั่งเทียบเท่าใน Gradle) คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

ผลลัพธ์นี้พิสูจน์ว่าคุณได้ **extract text from image**, **convert PNG to text**, และ **read text from PNG** สำเร็จในโปรแกรมเดียวที่เรียบร้อย

## จัดการกับกรณีขอบที่พบบ่อย

### ภาพคุณภาพต่ำ

หาก PNG เบลอหรือคอนทราสต์ต่ำ ความแม่นยำของ OCR จะลดลง วิธีแก้อย่างรวดเร็วคือการทำพรี‑โปรเซสภาพ:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### รองรับหลายภาษา

Tess4J รองรับหลายภาษา เพียงดาวน์โหลดไฟล์ `.traineddata` ที่เหมาะสมและตั้งค่า `tesseract.setLanguage("spa")` สำหรับภาษาสเปนเป็นตัวอย่าง

### PDF ขนาดใหญ่หรือภาพหลายหน้า

หากคุณต้อง **extract text from image** ไฟล์ภายใน PDF, ให้แยกแต่ละหน้าเป็น PNG ก่อน (ใช้ PDFBox) แล้วจึงส่งแต่ละ PNG ไปยังรูทีน OCR เดียวกัน

## ตัวอย่างทำงานเต็มรูปแบบ (โค้ดทั้งหมดในที่เดียว)

ด้านล่างเป็นคลาส Java ที่พร้อมรันเต็มรูปแบบ คัดลอก‑วางลงใน `src/main/java/com/example/ocrdemo/OcrDemo.java` แล้วคุณก็พร้อมใช้งาน

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

การรันคลาสนี้จะแสดงผล OCR, ยืนยันว่าคุณได้ **performed OCR on image** และแปลง PNG เป็นข้อความที่แก้ไขได้สำเร็จ

## สรุป & ขั้นตอนต่อไป

เราเริ่มด้วยการ **extracting text from image** ด้วยการตั้งค่า Java ที่เบา ๆ ตอนนี้คุณรู้วิธี **load image for OCR**, **perform OCR on image**, และ **read text from PNG**—บล็อกพื้นฐานสำคัญสำหรับสายงานดิจิไทซ์เอกสารใด ๆ

อยากไปต่อ? ลองไอเดียต่อไปนี้:

- **ประมวลผลเป็นชุด:** วนลูปผ่านไดเรกทอรีของ PNG และเขียนผลลัพธ์แต่ละไฟล์เป็น `.txt`  
- **เชื่อมต่อกับฐานข้อมูล:** เก็บสตริงที่สกัดได้พร้อมเมตาดาต้าเพื่อสร้างคลังข้อมูลที่ค้นหาได้  
- **ผสานกับ NLP:** ส่งผลลัพธ์ OCR ไปยังโมเดลวิเคราะห์อารมณ์เพื่อรับข้อมูลเชิงลึกอย่างรวดเร็ว  

แต่ละส่วนขยายเหล่านี้สร้างบนแนวคิดหลักที่เราได้ครอบคลุมแล้ว ดังนั้นคุณพร้อมที่จะทดลองแล้ว

---

*Happy coding! If you hit any snags

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [สกัดข้อความจากรูปภาพ Java ด้วย Aspose.OCR โหมดตรวจจับพื้นที่](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: แปลงรูปภาพเป็นข้อความด้วย Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [วิธี OCR ข้อความรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}