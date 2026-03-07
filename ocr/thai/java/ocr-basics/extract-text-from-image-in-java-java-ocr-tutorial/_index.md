---
category: general
date: 2026-03-07
description: ดึงข้อความจากภาพด้วย Java OCR. เรียนรู้วิธีโหลดภาพสำหรับ OCR, ตั้งค่าภาษา,
  และทำการสอน Java OCR อย่างเต็มรูปแบบภายในไม่กี่นาที.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: th
og_description: ดึงข้อความจากภาพด้วย Java OCR. บทเรียนนี้แสดงวิธีโหลดภาพสำหรับ OCR
  ตั้งค่าภาษา และทำตามขั้นตอนการสอน Java OCR ทีละขั้นตอน.
og_title: ดึงข้อความจากภาพใน Java – คู่มือ OCR ครบวงจร
tags:
- OCR
- Java
- Image Processing
title: สกัดข้อความจากภาพใน Java – บทเรียน OCR ของ Java
url: /th/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Java – คู่มือ OCR ฉบับสมบูรณ์

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่รู้จะเริ่มต้นอย่างไรใน Java หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักเจออุปสรรคเมื่อต้องแปลงสัญญาณ, ใบเสร็จ, หรือโน้ตมือเป็นสตริงที่ค้นหาได้  

ข่าวดีคือ? เพียงไม่กี่นาทีคุณก็สามารถสร้าง pipeline OCR ที่อ่านภาษากันนาดา, อังกฤษ, หรือภาษาที่รองรับใด ๆ ได้ ในบทเรียนนี้เราจะ **โหลดรูปภาพสำหรับ OCR**, ตั้งค่าเอนจิน, และเดินผ่าน **Java OCR tutorial** ที่คุณสามารถคัดลอก‑วางและรันได้ทันที

## สิ่งที่คู่มือนี้ครอบคลุม

เราจะเริ่มด้วยการรายการเครื่องมือที่คุณต้องการ, แล้วลงลึกตรงการทำ **ขั้นตอน‑ต่อ‑ขั้นตอน** สุดท้ายคุณจะสามารถ:

* โหลดไฟล์รูปภาพเข้าสู่ `ImageInputStream` ของ Java
* ตั้งค่า OCR engine ให้รับรู้ภาษาที่ต้องการ (ในตัวอย่างใช้กันนาดา)
* รันกระบวนการจดจำและพิมพ์ข้อความที่ดึงออกมา
* ปรับแต่งการตั้งค่าเพื่อความแม่นยำที่ดียิ่งขึ้นและจัดการกับข้อผิดพลาดทั่วไป

ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่  

**ข้อกำหนดเบื้องต้น**: Java 17 หรือใหม่กว่า, เครื่องมือสร้างเช่น Maven หรือ Gradle, และไลบรารี OCR ที่มีคลาส `OcrEngine` (เช่น SDK *SimpleOCR* สมมติ) หากคุณใช้ Maven ให้เพิ่ม dependency ตามที่แสดงต่อไปนี้

---

## ขั้นตอนที่ 1 – ตั้งค่าโปรเจกต์และเพิ่มไลบรารี OCR

ก่อนเขียนโค้ดใด ๆ ให้แน่ใจว่าโปรเจกต์ของคุณสามารถเห็นคลาส OCR ได้ ด้วย Maven ให้วางสแนปช็อตนี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

หากคุณใช้ Gradle ให้ใช้รูปแบบที่เทียบเท่า:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **เคล็ดลับ:** คอยอัปเดตเวอร์ชันของไลบรารีอยู่เสมอ; รุ่นใหม่มักมาพร้อมการปรับปรุงโมเดลภาษา ที่ช่วยเพิ่มความแม่นยำ

เมื่อ dependency ถูกดึงมาแล้ว รีเฟรช IDE ของคุณและคุณก็พร้อมเขียนโค้ด

## ขั้นตอนที่ 2 – นำเข้าคลาสที่จำเป็น

ด้านล่างเป็นรายการ import ทั้งหมดที่คุณต้องใช้สำหรับตัวอย่างนี้ เราเก็บให้เหลือน้อยที่สุดเพื่อให้คุณเห็นว่าคลาสแต่ละตัวทำอะไร

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **ทำไมต้อง import เหล่านี้?** `OcrEngine` และ `OcrResult` เป็นหัวใจของกระบวนการ OCR, ส่วน `ImageInputStream` ช่วยซ่อนรายละเอียดการอ่านไฟล์. การใช้ `java.nio.file.Paths` ทำให้โค้ดทำงานได้บนทุก OS

## ขั้นตอนที่ 3 – โหลดรูปภาพสำหรับ OCR

ตอนนี้มาถึงส่วนที่หลายคนมักพลาด: ส่งรูปแบบภาพที่ถูกต้องให้กับเอนจิน SDK OCR ต้องการ `ImageInputStream` ซึ่งคุณสามารถสร้างจากไฟล์ใดก็ได้บนดิสก์

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **กรณีขอบ:** หากภาพเสียหายหรือเป็นฟอร์แมตที่ไม่รองรับ (เช่น GIF) ตัวสร้างจะโยน `IOException`. ควรห่อการเรียกใน `try‑catch` หรือทำการตรวจสอบไฟล์ล่วงหน้า

## ขั้นตอนที่ 4 – ตั้งค่าเอนจินให้รับรู้ภาษาที่ต้องการ

OCR engine ส่วนใหญ่รองรับหลายภาษา เพื่อความแม่นยำที่ดีกว่า คุณควรบอกเอนจินว่าต้องการภาษาใด ในกรณีของเราจะใช้รหัสภาษา `"kn"` สำหรับกันนาดา

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **ทำไมต้องตั้งค่าภาษา?** การจำกัดชุดอักขระช่วยลด false positives, โดยเฉพาะเมื่อจัดการกับสคริปต์ที่มี glyph คล้ายกันหลายตัว

หากต้องการสลับภาษา เพียงเปลี่ยนสตริงรหัสภาษา—ไม่ต้องแก้ไขส่วนอื่นใด

## ขั้นตอนที่ 5 – รันกระบวนการ OCR และดึงข้อความออกมา

เมื่อโหลดภาพและตั้งค่าเอนจินแล้ว การจดจำจริง ๆ คือการเรียกเมธอดเดียว ผลลัพธ์จะให้ข้อความธรรมดาและอาจรวมคะแนนความเชื่อมั่นด้วย

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **คำถามทั่วไป:** *ทำไม OCR คืนสตริงว่าง?*  
> ปกติหมายถึงคุณภาพภาพต่ำ (เบลอ, คอนทราสต์ต่ำ) หรือไม่ได้ตั้งค่าภาษาอย่างถูกต้อง. ลองทำการพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, ทำไบนารี) หรือตรวจสอบรหัสภาษาอีกครั้ง

## ขั้นตอนที่ 6 – แสดงผลลัพธ์

สุดท้ายพิมพ์ผลลัพธ์ออกคอนโซล ในแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูลหรือส่งต่อไปยังดัชนีการค้นหา

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### ผลลัพธ์ที่คาดหวัง

หากภาพต้นฉบับมีวลีกันนาดา “ಕರ್ನಾಟಕ” (Karnataka) คอนโซลจะปรากฏ:

```
Extracted text:
ಕರ್ನಾಟಕ
```

เท่านี้—workflow **ใช้ OCR ใน Java** ครบชุดที่คุณสามารถปรับใช้กับภาษา หรือแหล่งภาพใดก็ได้

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงของไฟล์ภาพของคุณ

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **เคล็ดลับ:** สำหรับโค้ดระดับ production ควรใช้ `OcrEngine` ตัวเดียวกันหลาย ๆ ครั้ง; การสร้างซ้ำอาจทำให้เสียทรัพยากร

---

## คำถามที่พบบ่อย & กรณีขอบ

### จะเพิ่มความแม่นยำบนภาพที่มีเสียงรบกวนอย่างไร?
- **พรี‑โปรเซส** ภาพ: แปลงเป็น grayscale, ใช้ median filter, หรือเพิ่มคอนทราสต์
- **ปรับขนาด** ภาพให้มีความละเอียดอย่างน้อย 300 DPI; OCR engine ส่วนใหญ่คาดหวังความละเอียดนี้
- **ตั้งค่า whitelist** ของอักขระหากคุณรู้ว่าผลลัพธ์ที่คาดหวัง (เช่น ตัวเลขเท่านั้น)

### สามารถใช้วิธีนี้กับ PDF ได้หรือไม่?
ได้. แยกแต่ละหน้าเป็นภาพ (ใช้ PDFBox หรือ iText) แล้วส่งภาพเหล่านั้นเข้าสู่ pipeline เดียวกัน โค้ดไม่เปลี่ยนแปลง ยกเว้นแหล่งภาพเท่านั้น

### หากต้องการจดจำหลายภาษาในภาพเดียวต้องทำอย่างไร?
SDK ส่วนใหญ่รับรายการคอมม่า‑แยก, เช่น `"en,kn"`. เอนจินจะพยายามจับคู่สคริปต์ใดก็ได้จากรายการที่ให้

### มีวิธีรับคะแนนความเชื่อมั่นหรือไม่?
`OcrResult` มักมีเมธอด `getConfidence()` ที่คืนค่า float ระหว่าง 0‑1 สำหรับแต่ละบรรทัด ใช้เพื่อกรองผลลัพธ์ที่ความเชื่อมั่นต่ำ

---

## ขั้นตอนต่อไป

เมื่อคุณสามารถ **ดึงข้อความจากรูปภาพ** ด้วย Java แล้ว คุณอาจสำรวจต่อ:

* **ประมวลผลเป็นชุด** – วนลูปโฟลเดอร์ของภาพและเขียนผลลัพธ์ลง CSV
* **ผสานกับ Apache Tika** – รวม OCR กับการแยกเอกสารเพื่อสร้างดัชนีการค้นหาแบบรวม
* **API ฝั่งเซิร์ฟเวอร์** – เปิดให้บริการโลจิก OCR ผ่าน endpoint REST (Spring Boot ทำได้ง่าย)
* **ไลบรารีทางเลือก** – ลอง Tesseract ผ่าน `tess4j` หากต้องการโซลูชันโอเพนซอร์ส

หัวข้อเหล่านี้ต่อยอดจากแนวคิดหลักใน **java ocr tutorial** นี้ ดังนั้นอย่ากลัวทดลองและขยายโค้ด

---

## สรุป

เราได้เดินผ่านตัวอย่าง Java ครบชุดที่ **ดึงข้อความจากรูปภาพ**, แสดงวิธี **โหลดรูปภาพสำหรับ OCR**, ตั้งค่าภาษา, และ **ใช้ OCR ใน Java** เพื่อรับสตริงที่อ่านได้ โค้ดสั้นกระชับ, จัดการข้อผิดพลาดอย่างเหมาะสม, และสามารถนำไปวางในโปรเจกต์ Java ใดก็ได้โดยไม่ยุ่งยาก  

ลองรัน, ปรับรหัสภาษา, แล้วคุณจะเปลี่ยนเอกสารสแกนเป็นข้อมูลที่ค้นหาได้โดยไม่ต้องเสียแรง. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}