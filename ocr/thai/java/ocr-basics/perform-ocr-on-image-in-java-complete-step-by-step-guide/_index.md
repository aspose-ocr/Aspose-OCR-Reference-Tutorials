---
category: general
date: 2026-06-16
description: เรียนรู้วิธีทำ OCR บนไฟล์รูปภาพใน Java การสอนนี้ครอบคลุมการจดจำข้อความจาก
  PNG การดึงข้อความจากรูปภาพ การแปลงรูปภาพเป็นข้อความ และการโหลดรูปภาพสำหรับ OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: th
og_description: ทำ OCR บนภาพด้วย Java คู่มือนี้แสดงวิธีจดจำข้อความจาก PNG, ดึงข้อความจากภาพ,
  และแปลงภาพเป็นข้อความพร้อมตัวอย่างที่พร้อมใช้งาน
og_title: ทำ OCR บนภาพด้วย Java – คู่มือการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: ทำ OCR บนภาพใน Java – คู่มือขั้นตอนเต็มรูปแบบ
url: /th/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพใน Java – คู่มือขั้นตอนเต็ม

เคยต้องการ **perform OCR on image** ไฟล์แต่ไม่แน่ใจว่าจะเลือกไลบรารี Java ใด? คุณไม่ได้อยู่คนเดียว ไม่ว่าคุณจะสร้างสแกนเนอร์ใบเสร็จ, ระบบจัดเก็บเอกสาร, หรือแค่สนใจการแปลงรูปภาพให้เป็นข้อความที่ค้นหาได้ การเรียนรู้วิธี **perform OCR on image** ด้วย Java เป็นทักษะที่มีประโยชน์

ในบทแนะนำนี้เราจะพาคุณผ่านทุกขั้นตอนที่จำเป็นสำหรับการ **perform OCR on image** ไฟล์: การโหลดรูปภาพ, การตั้งค่าเอนจิน, การจดจำข้อความ, และสุดท้ายการพิมพ์ผลลัพธ์ เมื่อจบคุณจะสามารถ **recognize text from PNG** ไฟล์, **extract text from image** แหล่งต่าง ๆ, และ **convert image to text** ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด

## ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับ JDK ล่าสุดใดก็ได้)
- Maven ติดตั้งแล้ว (หรือเครื่องมือ build ที่คุณชื่นชอบ)
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java
- ไฟล์ PNG ที่คุณต้องการทดสอบ (เราจะเรียกว่า `hello.png`)

> **Pro tip:** หากคุณไม่มี PNG อยู่มือ, สร้างไฟล์หนึ่งโดยการถ่ายภาพหน้าจอของข้อความใด ๆ แล้วบันทึกเป็น `hello.png` ในโฟลเดอร์ชื่อ `resources`

## สิ่งที่เราจะสร้าง

แอปพลิเคชันคอนโซลขนาดเล็กชื่อ `OcrDemo` ที่:

1. **Loads image for OCR** – อ่าน PNG จากดิสก์
2. **Performs OCR on image** – ใช้เอนจิน Tesseract ผ่าน Tess4J
3. **Extracts text from image** – คืนค่า `String` ที่มีเนื้อหาที่ถูกจดจำ
4. พิมพ์ผลลัพธ์ไปยังคอนโซล

มาเริ่มกันเลย

## Step 1: Set Up the Project and Add Tess4J

ก่อนอื่นสร้างโปรเจกต์ Maven ใหม่ (หรือ Gradle หากคุณต้องการ) แล้วเพิ่ม dependency ของ Tess4J ซึ่งเป็น wrapper ของเอนจิน Tesseract OCR ที่ได้รับความนิยม

```xml
<!-- pom.xml -->
<project>
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

> **Why Tess4J?** มันได้รับการดูแลอย่างต่อเนื่อง, ทำงานข้ามแพลตฟอร์ม, และให้ Java API ที่สะอาดสำหรับงาน **perform OCR on image**

## Step 2: Prepare the Image‑Loading Logic

ต่อไปเราจะเขียนเมธอดช่วยเหลือที่ **load image for OCR** เมธอดนี้ใช้ `ImageIO` ของ Java เพื่ออ่าน PNG เข้าไปใน `BufferedImage`

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

สังเกตว่าชื่อเมธอดสื่อความหมายอย่างชัดเจนถึงความตั้งใจของ **load image for OCR**, ทำให้โค้ดเป็น self‑documenting

## Step 3: Configure the OCR Engine to **Perform OCR on Image**

เมื่อมีรูปภาพในมือ เราจะสร้างอินสแตนซ์ `Tesseract`, เปิดการตรวจจับภาษาอัตโนมัติ, และเรียก `doOCR` นี่คือแกนหลักของการ **perform OCR on image** ข้อมูล

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Why enable auto‑detect?** มันทำให้เอนจินเลือกโมเดลภาษาที่ดีที่สุดสำหรับรูปภาพ, ซึ่งมีประโยชน์อย่างยิ่งเมื่อคุณ **convert image to text** จากแหล่งที่ผสมภาษาอังกฤษกับสคริปต์อื่น ๆ

## Step 4: Put It All Together – The Main Application

นี่คือตัวเข้าจุดเริ่มต้นที่ **recognize text from PNG**, **extract text from image**, และสุดท้ายพิมพ์ผลลัพธ์ ตัวอย่างนี้เป็นโค้ดที่สมบูรณ์และสามารถรันได้

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Expected Output

หาก `hello.png` มีข้อความ “Hello, OCR world!” คอนโซลจะแสดงประมาณนี้:

```
=== Recognized Text ===
Hello, OCR world!
```

ผลลัพธ์อาจแตกต่างกันเล็กน้อยขึ้นอยู่กับคุณภาพของรูปภาพ, แต่คุณควรเห็นข้อความที่คุณใส่ใน PNG

## Step 5: Handling Common Edge Cases

### 5.1 Dealing with Low‑Resolution Images

หาก PNG ต้นฉบับเบลอ, ความแม่นยำของ OCR จะลดลง วิธีแก้อย่างรวดเร็วคือการขยายรูปภาพก่อนส่งให้เอนจิน:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

เรียก `upscale(image, 2)` ก่อน `engine.recognize(image)` เพื่อปรับปรุงผลลัพธ์

### 5.2 Multi‑Language Documents

หากคุณคาดว่าจะเจอข้อความภาษาฝรั่งเศสหรือเยอรมัน, เพียงเพิ่มรหัสภาษาใน `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

เอนจินจะพยายาม **extract text from image** ด้วยโมเดลภาษาที่รวมกัน

### 5.3 Skipping Empty Pages

บางครั้งหน้าสแกน PDF จะปรากฏเป็น PNG ว่าง การตรวจจับรูปภาพที่ว่างเปล่าจะช่วยประหยัดเวลาในการประมวลผล:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Step 6: Packaging and Running the Application

1. **Compile:** `mvn clean compile`
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

ตรวจสอบให้แน่ใจว่าโฟลเดอร์ `tessdata` (ที่มีไฟล์ภาษา) อยู่ข้าง ๆ JAR ที่คอมไพล์แล้วหรือระบุพาธเต็มใน `OcrEngine`

## Conclusion

ตอนนี้คุณมีแพทเทิร์นที่มั่นคงและพร้อมใช้งานในระดับ production เพื่อ **perform OCR on image** ไฟล์ด้วย Java ตั้งแต่ **loading image for OCR** ถึง **recognize text from PNG**, เราได้ครอบคลุมวิธี **extract text from image**, **convert image to text**, และจัดการกับสถานการณ์ที่ท้าทายเช่นการสแกนความละเอียดต่ำหรือเนื้อหาหลายภาษา

ต่อไปคุณอาจสำรวจ:

- **Batch processing** – วนลูปผ่านไดเรกทอรีของ PNGs และเขียนผลลัพธ์แต่ละไฟล์เป็นไฟล์ `.txt`
- **PDF generation** – ฝังข้อความที่ดึงออกมากลับเข้าไปใน PDF ที่สามารถค้นหาได้
- **Cloud OCR services** – เปรียบเทียบประสิทธิภาพของ Tesseract ภายในเครื่องกับ API เช่น Google Vision หรือ Azure Cognitive Services

ทดลองปรับพารามิเตอร์ต่าง ๆ ได้ตามต้องการและแบ่งปันผลการค้นพบของคุณ ขอให้เขียนโค้ดอย่างสนุกและภาพของคุณแปลงเป็นข้อความที่สะอาดและค้นหาได้เสมอ!

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบทางเลือกในโปรเจกต์ของคุณ

- [จดจำข้อความจากภาพด้วย Aspose OCR – คู่มือ OCR Java เต็มรูปแบบ](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [แปลงภาพเป็นข้อความใน Java ด้วย Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [ดึงข้อความจากภาพ Java ด้วย Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}