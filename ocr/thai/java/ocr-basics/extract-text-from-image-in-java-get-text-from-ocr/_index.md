---
category: general
date: 2026-05-25
description: ดึงข้อความจากภาพใน Java ด้วย OCR. เรียนรู้วิธีโหลดภาพสำหรับ OCR, จดจำข้อความจากรูปถ่าย,
  และรับข้อความจาก OCR ด้วยตัวอย่างโค้ดง่าย ๆ.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: th
og_description: ดึงข้อความจากภาพใน Java ด้วยคู่มือขั้นตอนอย่างละเอียด เรียนรู้วิธีโหลดภาพสำหรับ
  OCR จดจำข้อความจากรูปถ่าย และรับข้อความจาก OCR อย่างมีประสิทธิภาพ
og_title: ดึงข้อความจากรูปภาพใน Java – รับข้อความจาก OCR
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
title: สกัดข้อความจากภาพใน Java – รับข้อความจาก OCR
url: /th/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Java – รับข้อความจาก OCR

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารี Java ตัวไหนไหม? คุณไม่ได้อยู่คนเดียว ไม่ว่าคุณจะกำลังทำการแปลงใบเสร็จเป็นดิจิทัล, ดึงหมายเลขซีเรียลจากรูปสินค้, หรือแค่ทำโปรเจกต์สนุก ๆ การเปลี่ยนรูปภาพให้เป็นข้อความที่แก้ไขได้เป็นอุปสรรคที่พบบ่อย

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบซึ่งจะแสดงให้คุณเห็นว่า **โหลดรูปภาพสำหรับ OCR** อย่างไร, ตั้งค่าเอนจิน, และสุดท้าย **จดจำข้อความจากรูปถ่าย** เพื่อให้คุณ **รับข้อความจาก OCR** ได้ด้วยไม่กี่บรรทัดของโค้ด ไม่มีการอ้างอิงที่คลุมเครือ—ทุกอย่างที่คุณต้องการอยู่ที่นี่

## สิ่งที่คุณจะได้เรียน

* วิธีตั้งค่าเอนจิน OCR ที่เบาใน Java  
* ขั้นตอนที่แม่นยำในการ **โหลดรูปภาพสำหรับ OCR** และจัดการกับเส้นทางไฟล์ต่าง ๆ  
* ทำไมการกำหนดภาษาถึงสำคัญเมื่อคุณต้อง **ดึงข้อความจากรูปภาพ** ที่ไม่ใช่ภาษาอังกฤษ  
* วิธีแสดงผลลัพธ์อย่างปลอดภัยและวิธีจัดการเมื่อเอนจินไม่คืนค่าอะไรเลย  
* เคล็ดลับระดับมืออาชีพเพื่อหลีกเลี่ยงปัญหาที่พบบ่อยที่สุด

เมื่ออ่านจบบทนี้คุณจะมีโปรแกรมที่ทำงานได้เองซึ่งอ่านไฟล์ JPEG (หรือ PNG) ที่มีอักขระยูเครนและพิมพ์สตริงที่จดจำได้ลงคอนโซล คุณสามารถสลับภาษา หรือรูปภาพได้ตามต้องการ—ทุกอย่างเป็นโมดูลาร์

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*ข้อความแทน: แผนภาพการไหลของกระบวนการดึงข้อความจากรูปภาพใน Java.*

## ข้อกำหนดเบื้องต้น

* **Java Development Kit (JDK) 11+** – โค้ดใช้ระบบโมดูลสมัยใหม่ แต่เวอร์ชันเก่าก็ทำงานได้ด้วยการปรับเล็กน้อย  
* **Maven หรือ Gradle** – เพื่อดึงไลบรารี OCR (เราจะใช้ **Asprise OCR** ซึ่งเป็นตัวเลือกฟรี‑for‑development ที่เบา)  
* ไฟล์รูปตัวอย่าง (เช่น `ukrainian_sign.jpg`) ที่วางไว้ในตำแหน่งที่โปรแกรมของคุณสามารถอ่านได้  
* ความคุ้นเคยพื้นฐานกับเมธอด `main` ของ Java และการจัดการข้อยกเว้น

ถ้าคุณมีสิ่งเหล่านี้แล้วก็พร้อมเริ่มได้เลย หากยังไม่มี ให้ดาวน์โหลด JDK จาก Oracle หรือ AdoptOpenJDK แล้วตั้งค่าโปรเจกต์ Maven อย่างง่าย—ไม่มีอะไรซับซ้อน

---

## ขั้นตอนที่ 1: เพิ่ม Dependency ของ OCR

แรกสุดบอกเครื่องมือสร้างของคุณให้ดึงเอนจิน OCR สำหรับ Maven ให้ใส่ส่วนนี้ลงใน `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

ถ้าคุณใช้ Gradle ให้ใช้รูปแบบที่เทียบเท่า:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

พิกัดเหล่านี้จะดึง JAR ขนาดกะทัดรัดที่รวม `OcrEngine`, `OcrLanguage` และคลาสช่วยเหลือต่าง ๆ ที่เราจะใช้ ไม่ต้องมีไบนารีเนทีฟเพิ่มเติมสำหรับสคริปต์ละตินและซีริลลิกพื้นฐาน

---

## ขั้นตอนที่ 2: สร้างคลาส Java เพื่อ **ดึงข้อความจากรูปภาพ**

ต่อไปเราจะเขียนโปรแกรมจริง บันทึกโค้ดต่อไปนี้เป็นไฟล์ `ExtractTextDemo.java` ภายใน `src/main/java/com/example/ocr/`.

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

### ทำไมโครงสร้างนี้ถึงทำงานได้

* **บล็อกที่มีหมายเลขแยกกัน** ทำให้การไหลของขั้นตอนง่ายต่อการตามหา โดยเฉพาะเมื่อคุณกำลังมองหาที่ **โหลดรูปภาพสำหรับ OCR** หรือ **จดจำข้อความจากรูปถ่าย**  
* `try/catch` รอบการโหลดรูปและการจดจำทำให้โปรแกรมล้มเหลวอย่างสุภาพ—มีประโยชน์เมื่อเส้นทางไฟล์ผิดหรือเอนจิน OCR ไม่พบข้อมูลภาษาที่ต้องการ  
* การตั้งค่าภาษาแต่เนิ่น ๆ (ขั้นตอน 2) ช่วยเพิ่มความแม่นยำอย่างมากสำหรับสคริปต์ที่ไม่ใช่ภาษาอังกฤษ หากคุณต้องการ **java image to text** สำหรับภาษาอื่นในภายหลัง เพียงสลับ `OcrLanguage.UKRAINIAN` เป็น `OcrLanguage.ENGLISH`, `FRENCH` เป็นต้น

---

## ขั้นตอนที่ 3: สร้างและรันโปรแกรม

จากโฟลเดอร์รากของโปรเจกต์ ให้รันคำสั่ง:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

หรือถ้าคุณใช้ Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

สมมติว่า `ukrainian_sign.jpg` มีข้อความ *«Ласкаво просимо»* (ยูเครนแปลว่า “Welcome”) คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== OCR Result ===
Ласкаво просимо
```

ผลลัพธ์นี้ยืนยันว่าคุณได้ **ดึงข้อความจากรูปภาพ** และ **รับข้อความจาก OCR** สำเร็จในหนึ่งรอบการทำงาน

---

## ขั้นตอนที่ 4: ปรับแต่งเวิร์กโฟลว์ – จาก **Java Image to Text** ในโครงการจริง

แม้ตัวอย่างจะเรียบง่าย แต่แอปพลิเคชันจริงมักต้องการสิ่งเพิ่มเติม:

| สถานการณ์ | สิ่งที่ต้องปรับ | เหตุผล |
|----------|----------------|--------|
| **การประมวลผลเป็นชุด** | วนลูปผ่าน `List<Path>` แล้วเก็บผลแต่ละรายการลงฐานข้อมูล | ลดงานมือเมื่อมีรูปภาพหลายร้อยรูป |
| **รูปแบบไฟล์รูปภาพต่าง ๆ** | ใช้ `ImageIO.read(new File(path))` เพื่อทำการพรี‑โปรเซส แล้วส่ง `BufferedImage` ให้ `ocrEngine.getImage().loadFromBufferedImage(bufImg)` | รองรับ PNG, BMP หรือแม้แต่ PDF หลังแปลง |
| **การปรับแต่งประสิทธิภาพ** | เรียก `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` หากคุณยอมรับความแม่นยำที่ลดลงเล็กน้อย | เร่งการจดจำบนฮาร์ดแวร์ระดับล่าง |
| **การประมวลผลหลังจดจำ** | ตัด whitespace, แทนที่การอ่านผิดทั่วไป (`0` → `O`, `1` → `I`) | ปรับปรุงคุณภาพข้อมูลต่อไป |

การปรับเปลี่ยนเหล่านี้ยังคงแนวคิดหลัก—**จดจำข้อความจากรูปถ่าย**—โดยให้คุณมีความยืดหยุ่นสำหรับงานผลิตจริง

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

1. **ตั้งค่าภาษาไม่ถูกต้อง** – หากลืมขั้นตอน 2 เอนจินจะใช้ค่าเริ่มต้นเป็นอังกฤษ ทำให้ตัวอักษรซีริลลิกกลายเป็นอักขระไร้ความหมาย ตรวจสอบรหัสภาษาทุกครั้ง  
2. **คุณภาพของรูปภาพสำคัญ** – รูปความละเอียดต่ำหรือเบลอจะลดความแม่นยำ พรี‑โปรเซสด้วยการเพิ่มคอนทราสต์หรือทำไบนารีไลเซชันหากจำเป็น  
3. **ปัญหาเส้นทางไฟล์** – บน Windows ต้องหนีอักขระ backslash (`C:\\images\\file.jpg`) การใช้ `Path.of(...)` จาก `java.nio.file` จะหลีกเลี่ยงปัญหานี้ได้  
4. **การรั่วของหน่วยความจำ** – `OcrEngine` ถือทรัพยากรเนทีฟ ต้องเรียก `ocrEngine.dispose()` เมื่อเสร็จสิ้น โดยเฉพาะในบริการที่ทำงานต่อเนื่องเป็นเวลานาน  
5. **ความปลอดภัยของเธรด** – เอนจินไม่ได้เป็น thread‑safe โดยอัตโนมัติ สร้างอินสแตนซ์แยกสำหรับแต่ละเธรดหรือทำการซิงโครไนซ์การเข้าถึง

---

## ตัวอย่างทำงานเต็มรูปแบบ (All‑In‑One)

ด้านล่างเป็นไฟล์เดียวที่คุณสามารถคัดลอก‑วางไปยัง IDE ใดก็ได้ รวมการเรียก `dispose()` และเมธอดช่วยเหลือขนาดเล็กเพื่อทำให้โค้ดอ่านง่ายขึ้น

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

การรันโปรแกรมนี้จะให้ผลลัพธ์เดียวกับที่แสดงไว้ก่อนหน้า คุณสามารถเปลี่ยน `OcrLanguage.UKRAINIAN` เป็น `OcrLanguage.ENGLISH` หรือภาษาอื่นที่รองรับเพื่อดูการปรับตัวของเอนจิน

---

## สรุป

เราผ่านทุกขั้นตอนที่คุณต้องการเพื่อ **ดึงข้อความจากรูปภาพ** ด้วย Java: ตั้งค่า dependency OCR, **โหลดรูปภาพสำหรับ OCR**,  

## บทเรียนที่เกี่ยวข้อง

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}