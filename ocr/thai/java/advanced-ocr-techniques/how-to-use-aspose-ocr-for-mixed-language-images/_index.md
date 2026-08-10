---
category: general
date: 2026-05-06
description: วิธีใช้ Aspose OCR เพื่อจดจำข้อความจากภาพ, เปิดใช้งานการตรวจจับภาษาอัตโนมัติ,
  และเพิ่มความเร็วของ OCR ใน Java.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: th
og_description: วิธีใช้ Aspose OCR เพื่อจดจำข้อความจากภาพอย่างรวดเร็ว เปิดใช้งานการตรวจจับภาษาอัตโนมัติ
  และเพิ่มความเร็วของ OCR ใน Java
og_title: วิธีใช้ Aspose OCR สำหรับภาพหลายภาษา
tags:
- Aspose
- OCR
- Java
- Image Processing
title: วิธีใช้ Aspose OCR สำหรับภาพหลายภาษา
url: /th/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose OCR สำหรับรูปภาพหลายภาษา

เคยสงสัย **วิธีใช้ Aspose** เพื่อดึงข้อความจากภาพที่มีหลายภาษาในครั้งเดียวหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักเจออุปสรรคเมื่อภาพผสมภาษาอังกฤษ, รัสเซีย, ฮินดี หรือสคริปต์อื่นใด ข่าวดีคือ Aspose OCR จัดการเรื่องนี้ได้อย่างราบรื่น และคุณยังสามารถ **recognize text from image** ได้เร็วขึ้นโดยการจำกัดชุดภาษา

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่าง Java ที่สมบูรณ์และพร้อมรัน ซึ่ง **loads image for OCR**, เปิด **automatic language detection**, และแสดงเทคนิคง่าย ๆ เพื่อ **improve OCR speed**. เมื่อจบคุณจะมีโปรแกรมอิสระที่พิมพ์ข้อความที่สกัดออกมาที่คอนโซล และคุณจะเข้าใจว่าการตั้งค่าแต่ละอย่างมีความสำคัญอย่างไร

> **Prerequisites** – ติดตั้ง Java 17+ แล้ว, มี Maven หรือ Gradle สำหรับการจัดการ dependencies, และมีใบอนุญาต Aspose OCR (รุ่นทดลองฟรีใช้สำหรับการประเมิน). ไม่จำเป็นต้องใช้ไลบรารีอื่น

---

## ขั้นตอนที่ 1 – เพิ่ม Aspose OCR ไปยังโปรเจกต์ของคุณ

ก่อนที่คุณจะ **use Aspose**, คุณต้องมีไลบรารีนี้ใน classpath. กับ Maven จะเป็นแบบนี้:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

หากคุณต้องการใช้ Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** ควรใช้เวอร์ชัน stable ล่าสุด; เวอร์ชันใหม่มักมีการปรับปรุงประสิทธิภาพที่ส่งผลโดยตรงต่อ **improve OCR speed**.

---

## ขั้นตอนที่ 2 – สร้างอินสแตนซ์ของ OCR Engine  

หัวใจของทุก workflow ของ Aspose OCR คือ `OcrEngine`. การสร้างอินสแตนซ์นั้นง่ายดาย, แต่ควรทราบว่า engine มีแคชภายใน. การใช้ instance เดียวซ้ำหลายภาพจริง ๆ แล้วสามารถ **improve OCR speed** ได้ เพราะไลบรารีหลีกเลี่ยงการเริ่มต้น native ซ้ำ ๆ

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## ขั้นตอนที่ 3 – **Load Image for OCR**  

Aspose รองรับรูปแบบภาพหลายประเภท (PNG, JPEG, TIFF, BMP). ที่นี่เราจะแสดงการโหลด PNG ที่มีข้อความภาษาอังกฤษ, รัสเซีย, และฮินดี. ตัวช่วย `ImageStream.fromFile` จะทำให้การทำงานกับไฟล์‑I/O ซับซ้อนน้อยลงและรับประกันว่าภาพจะถูกสตรีมเข้าสู่ engine อย่างถูกต้อง.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **What if the image is in memory?** ใช้ `ImageStream.fromByteArray(byte[])` แทน—เหมาะสำหรับเว็บเซอร์วิสที่รับภาพเป็น byte stream.

---

## ขั้นตอนที่ 4 – เปิดใช้งาน Automatic Language Detection  

โดยค่าเริ่มต้น Aspose OCR จะสมมติว่ามีภาษาเดียว, ซึ่งอาจทำให้ผลลัพธ์เป็นข้อความเสียหายในภาพหลายภาษา. การเปิดการตรวจจับอัตโนมัติจะบอก engine ให้ตรวจสอบสคริปต์ของแต่ละบล็อกข้อความก่อนการรู้จำ.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## ขั้นตอนที่ 5 – **Improve OCR Speed** โดยการจำกัด Language Pool  

การตรวจจับอัตโนมัติเต็มรูปแบบจะสแกนทุกภาษาที่ Aspose รองรับ (มากกว่า 70). หากคุณทราบภาษาที่อาจเกิดขึ้นล่วงหน้า, คุณสามารถให้คำแนะนำกับ engine. การให้ array ที่เล็กลงจะลดพื้นที่ค้นหาและดังนั้น **improves OCR speed**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Why does this help?** engine จะข้ามโมเดลภาษาที่ไม่จำเป็น, ประหยัด CPU cycles และหน่วยความจำ. หากคุณเพิ่มภาษาในภายหลัง, เพียงอัปเดต array—ไม่ต้องเขียนโค้ดใหม่.

---

## ขั้นตอนที่ 6 – ทำการ Recognize และ **Recognize Text from Image**

ตอนนี้การทำงานหนักเริ่มขึ้น. `recognize()` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่มีข้อความธรรมดา, คะแนนความมั่นใจ, และแม้แต่ข้อมูล layout หากคุณต้องการใช้ต่อในภายหลัง.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

หากภาพมีสัญญาณรบกวนหรือข้อความเอียง, คุณอาจเห็นคะแนนความมั่นใจต่ำสำหรับบรรทัดเหล่านั้น. ในกรณีนั้น, พิจารณา pre‑processing ภาพ (deskew, binarisation) ก่อนส่งให้ Aspose.

---

## คำถามทั่วไปและกรณีขอบ

### ถ้าภาพมีขนาดใหญ่มาก (เช่น >10 MP)?

ภาพขนาดใหญ่ใช้หน่วยความจำมากและอาจทำให้การประมวลผลช้าลง. วิธีเร็ว ๆ เพื่อ **improve OCR speed** คือการลดขนาดภาพโดยยังคงความอ่านได้:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### จะจัดการกับสคริปต์ขวา‑ไป‑ซ้าย เช่น Arabic อย่างไร?

Aspose OCR จะเคารพทิศทางสคริปต์โดยอัตโนมัติ, แต่คุณอาจต้องตั้งค่า `RightToLeft` flag สำหรับการ post‑processing:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### สามารถสกัดข้อความจาก PDF แทนภาพได้หรือไม่?

ได้—แปลงแต่ละหน้า PDF เป็นภาพ (โดยใช้ Aspose PDF หรือ rasterizer ใด ๆ) แล้วส่งผลลัพธ์ไปยัง pipeline OCR เดียวกัน. ตรรกะ **recognize text from image** จะใช้ได้เช่นเดียวกัน.

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

บันทึกไฟล์เป็น `MixedLanguageDemo.java`, คอมไพล์ด้วย `javac`, และรันด้วย `java MixedLanguageDemo`. หากทุกอย่างตั้งค่าอย่างถูกต้อง, คุณจะเห็นข้อความหลายภาษาถูกพิมพ์ที่คอนโซล.

---

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to use Aspose** เพื่อ **recognize text from image** ไฟล์ที่มีหลายภาษา, วิธี **enable automatic language detection**, และเคล็ดลับปฏิบัติเพื่อ **improve OCR speed** โดยการจำกัด language pool. โค้ดเต็มที่อยู่ด้านบนพร้อมคัดลอก‑วาง, และคำอธิบายจะช่วยให้คุณมั่นใจในการปรับใช้—ไม่ว่าคุณจะต้อง **load image for OCR** จากสตรีม, byte array, หรือแม้แต่ภาพจากเว็บแคม

ขั้นตอนต่อไป? ลองทดลองกับ:

* การเพิ่ม image pre‑processing (denoise, binarise) สำหรับสแกนคุณภาพต่ำ  
* การส่งออก `OcrResult` เป็น JSON สำหรับบริการ downstream  
* การรวม engine เข้าไปใน Spring Boot REST endpoint เพื่อให้ลูกค้าสามารถอัปโหลดภาพและรับข้อความที่สกัดได้ทันที

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้ pipeline OCR ของคุณเร็ว, แม่นยำ, และหลายภาษา!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}