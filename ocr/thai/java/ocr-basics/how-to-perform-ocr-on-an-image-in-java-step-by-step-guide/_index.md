---
category: general
date: 2026-11-17
description: เรียนรู้วิธีทำ OCR บนรูปภาพด้วย Java และดึงข้อความจากภาพโดยใช้ตัวอย่างโค้ดง่าย
  ๆ รวมเคล็ดลับการอ่านรูปภาพใน Java
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: th
lastmod: 2026-11-17
og_description: วิธีทำ OCR บนรูปภาพใน Java และดึงข้อความออกอย่างรวดเร็ว ทำตามคำแนะนำนี้เพื่ออ่านรูปภาพใน
  Java และแปลงรูปภาพเป็นข้อความพร้อมตัวอย่างที่พร้อมใช้งาน
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: วิธีทำ OCR บนภาพใน Java – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: วิธีทำ OCR บนภาพใน Java – คู่มือแบบขั้นตอนโดยละเอียด
url: /th/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนรูปภาพใน Java – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **วิธีทำ OCR** บนรูปภาพ คู่มือนี้จะแสดงวิธีแก้ปัญหาที่สมบูรณ์และสามารถรันได้ใน Java คุณจะได้เห็นวิธีอ่านไฟล์รูปภาพ, ตั้งค่าเครื่องมือ OCR, และดึงข้อความที่เครื่องมือจดจำได้

การทำงานกับเอกสารสแกน, ใบเสร็จ, หรือภาพหน้าจอมักต้องแปลงเนื้อหาภาพเป็นข้อความที่ค้นหาได้ คู่มือนี้จะพาคุณผ่านทุกขั้นตอน ตั้งแต่การโหลดรูปภาพจนถึงการพิมพ์ข้อความที่ดึงออกมา และยังครอบคลุมข้อผิดพลาดทั่วไป เช่น รูปแบบไฟล์ที่ไม่รองรับและผลลัพธ์เป็น null

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

* Java Development Kit (JDK) 8 หรือใหม่กว่า
* เครื่องมือสร้าง (Maven หรือ Gradle) เพื่อดึงไลบรารี OCR
* ไฟล์รูปภาพ (JPEG, PNG, BMP) ที่ต้องการประมวลผล

โค้ดนี้ใช้ **ไลบรารี OCR จากแพ็กเกจ `com.asprise.ocr`** เนื่องจากต้องการเพียง JAR เดียวและทำงานบนแพลตฟอร์มหลักทั้งหมด คุณสามารถเปลี่ยนเป็นผู้ให้บริการอื่น (Tesseract, Google Vision ฯลฯ) ได้โดยเปลี่ยนคำสั่ง import และโค้ดการเริ่มต้นเครื่องมือ

## ขั้นตอนที่ 1: เพิ่ม dependency ของ OCR

หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

สำหรับ Gradle ให้ใส่บรรทัดนี้ใน `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

บรรทัดเหล่านี้ทำให้โค้ด **read image Java** สามารถคอมไพล์และทำให้เครื่องมือ OCR พร้อมใช้งานในเวลารัน

## ขั้นตอนที่ 2: อ่านรูปภาพด้วย Java

การอ่านไฟล์รูปภาพเป็นขั้นตอนแรกที่ชัดเจนในทุก workflow **extract text image** Java `ImageIO` ของ Java จัดการรูปแบบที่พบบ่อยส่วนใหญ่

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**เหตุผลที่สำคัญ:** `ImageIO.read` จะคืนค่า `null` หากรูปแบบไม่รองรับหรือไฟล์เสียหาย วิธีการข้างต้นจะบันทึกปัญหาและคืนค่า `null` เพื่อให้ขั้นตอนถัดไปสามารถจัดการได้อย่างเหมาะสม

## ขั้นตอนที่ 3: สร้างและตั้งค่าเครื่องมือ OCR

เครื่องมือ OCR ต้องรู้ว่าจะจดจำภาษาอะไร การตั้งค่าภาษาเพิ่มความแม่นยำอย่างมาก โดยเฉพาะกับเอกสารที่ไม่ใช่ภาษาอังกฤษ

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**เหตุผลที่สำคัญ:** การเริ่มเครื่องมือเป็นการดำเนินการที่ค่อนข้างหนัก ดังนั้นควรสร้างครั้งเดียวและนำกลับมาใช้ใหม่สำหรับหลายรูปภาพหากแอปของคุณประมวลผลเป็นชุด

## ขั้นตอนที่ 4: ทำ OCR และแปลงรูปภาพเป็นข้อความ

เมื่อรูปภาพโหลดแล้วและเครื่องมือพร้อม คุณสามารถรันขั้นตอนการจดจำได้ นี่คือหัวใจของ **วิธีทำ OCR**

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**การจัดการกรณีขอบ:** หากรูปภาพเป็น `null` วิธีการจะคืนสตริงว่างแทนการโยน `NullPointerException` ทำให้โค้ดโดยรอบแข็งแรงขึ้นเมื่อรับไฟล์จากผู้ใช้

## ขั้นตอนที่ 5: แสดงข้อความที่ดึงออกมา

สุดท้าย พิมพ์ผลลัพธ์ลงคอนโซลหรือส่งต่อไปยังส่วนประกอบอื่น (เช่น ฐานข้อมูลหรือวิดเจ็ต UI)

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

เมื่อคุณรันโปรแกรมด้วย `java OcrDemo sample.jpg` คอนโซลจะแสดงอักขระที่จดจำได้ นี่คือวงจร **convert image to text** ที่สมบูรณ์

### ผลลัพธ์ที่คาดหวัง

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

หากรูปภาพไม่มีอักขระที่อ่านได้ โปรแกรมจะพิมพ์ `(no text detected)`

## ความแตกต่างทั่วไปและวิธีปรับใช้

| Variation | What changes | When to use |
|-----------|--------------|-------------|
| **Different language** | Replace `"eng"` with `"spa"` for Spanish, `"fra"` for French, etc. | Documents written in a language other than English |
| **Batch processing** | Loop over a list of file paths, reuse the same `Ocr` instance. | Large sets of scanned pages |
| **Higher accuracy** | Use `Ocr.SPEED_SLOW` or enable `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` for numeric-only scans. | When OCR quality is critical (e.g., invoice numbers) |
| **Tesseract alternative** | Swap the import to `net.sourceforge.tess4j.Tesseract` and adjust the initialization code. | Projects that already depend on Tesseract |

## เคล็ดลับระดับมืออาชีพ

* **Resize large images** ก่อนส่งให้เครื่องมือ; ความเร็ว OCR ขึ้นกับจำนวนพิกเซล
* **Pre‑process** รูปภาพ (grayscale, contrast boost) ด้วยไลบรารีเช่น OpenCV หากแหล่งที่มามีสัญญาณรบกวน
* **Cache the OCR engine** หากเรียกใช้บ่อยในช่วงเวลาสั้น ๆ — การเริ่มและหยุดเครื่องมือมีค่าใช้จ่าย
* **Validate the result** ด้วย regular expressions เมื่อคุณคาดหวังรูปแบบเฉพาะ (เช่น วันที่, เบอร์โทร)

## สรุป

ตอนนี้คุณรู้ **วิธีทำ OCR** บนรูปภาพใน Java ตั้งแต่การอ่านไฟล์จนถึงการแสดงข้อความที่ดึงออกมาแล้ว คู่มือได้ครอบคลุมเทคนิค **read image Java**, **extract text image**, **convert image to text**, และ **image to text java** พร้อมให้คำแนะนำเชิงปฏิบัติสำหรับสถานการณ์จริง  

จากนี้คุณสามารถ:

* ผสานขั้นตอน OCR เข้าไปในเว็บเซอร์วิสที่รับไฟล์อัปโหลด
* รวมผลลัพธ์กับดัชนีการค้นหาเพื่อทำ full‑text search บนเอกสารสแกน
* สำรวจตัวเลือก OCR ขั้นสูง เช่น การสนับสนุนหลายภาษา หรือชุดอักขระกำหนดเอง

ขอให้สนุกกับการเขียนโค้ดและแปลงรูปภาพให้เป็นข้อความที่ค้นหาได้!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}