---
category: general
date: 2026-03-28
description: ใช้ OCR บนภาพใน Java ด้วย Aspose OCR เพื่อแปลงภาพเป็นข้อความ ดึงข้อความภาษาไทยจาก
  PNG อย่างรวดเร็วและเชื่อถือได้.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: th
og_description: ทำ OCR บนรูปภาพด้วย Java และ Aspose OCR. เรียนรู้วิธีแปลงรูปภาพเป็นข้อความ,
  ดึงข้อความภาษาไทยจากไฟล์ PNG, และจัดการกับข้อผิดพลาดทั่วไป.
og_title: ทำ OCR บนรูปภาพด้วย Java – ดึงข้อความภาษาไทยอย่างรวดเร็ว
tags:
- OCR
- Java
- Aspose
- Image Processing
title: ทำ OCR บนรูปภาพด้วย Java – ดึงข้อความภาษาไทยจากไฟล์ PNG
url: /th/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รัน OCR บนรูปภาพด้วย Java – บทแนะนำเต็มรูปแบบ

เคยสงสัยไหมว่าเราจะ **run OCR on image** ไฟล์โดยตรงจากโค้ด Java ได้อย่างไร? บางทีคุณอาจมีชุดใบเสร็จไทย, เอกสารสแกน, หรือภาพหน้าจอและต้องการข้อความโดยไม่ต้องพิมพ์ด้วยตนเอง นี่เป็นปัญหาที่พบบ่อยโดยเฉพาะเมื่อแหล่งเป็น PNG และภาษาที่ใช้ไม่ใช่ Latin  

ในคู่มือนี้เราจะแสดงให้คุณเห็นอย่างละเอียดว่าเราจะ **run OCR on image** ด้วยไลบรารี Aspose OCR อย่างไร, แปลงรูปภาพเป็นข้อความธรรมดา, และดึงอักขระภาษาไทยออกมาอย่างแม่นยำ. เมื่อจบคุณจะสามารถ **convert image to text**, **extract text from PNG**, และแม้กระทั่ง **recognize Thai text** ด้วยเพียงไม่กี่บรรทัดของโค้ด.

## สิ่งที่บทเรียนนี้ครอบคลุม

* ตั้งค่า dependency ของ Aspose OCR ในโครงการ Maven/Gradle.  
* เริ่มต้น `OcrEngine` และกำหนดค่าภาษาไทย.  
* รัน OCR บนไฟล์ PNG และจัดการข้อผิดพลาดที่อาจเกิดขึ้น.  
* พิมพ์ผลลัพธ์ไปยังคอนโซลและตรวจสอบผลลัพธ์.  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน—แค่ IDE Java เบื้องต้นและไฟล์รูปภาพที่คุณต้องการประมวลผล.

## ข้อกำหนดเบื้องต้น

* ติดตั้ง Java 8 หรือใหม่กว่า (ไลบรารีทำงานกับ Java 11+ ด้วย).  
* เครื่องมือสร้าง – Maven หรือ Gradle (เราจะแสดงตัวอย่าง Maven).  
* ใบอนุญาต Aspose OCR (รุ่นทดลองฟรีใช้สำหรับทดสอบ, แต่ใบอนุญาตจะลบข้อจำกัดการประเมิน).  
* PNG ที่มีข้อความภาษาไทย, เช่น `input.png` ที่วางในโฟลเดอร์ resources ของโครงการของคุณ.

---

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโครงการของคุณ

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** ควรทำให้เวอร์ชันของไลบรารีสอดคล้องกับบันทึกการปล่อยของ Aspose อย่างเป็นทางการ; เวอร์ชันใหม่จะเพิ่ม language packs และการปรับปรุงประสิทธิภาพ.

เมื่อ dependency ถูกแก้ไขแล้ว, IDE ของคุณควรทำการ import คลาสที่จำเป็นโดยอัตโนมัติ.

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine

Engine คือหัวใจของกระบวนการ – คิดว่าเป็น “สมอง” ที่วิเคราะห์รูปแบบพิกเซล. เราจะบอกให้มันรู้ว่าเราสนใจเฉพาะอักขระภาษาไทย.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

ทำไมต้องตั้งค่าภาษาอย่างชัดเจน? เพราะการระบุ `"th"` จะจำกัดชุดอักขระ, ทำให้การจดจำเร็วขึ้นและลดการอ่านผิดของ glyph ที่คล้ายกัน.

## ขั้นตอนที่ 3: รัน OCR บนไฟล์ PNG

ตอนนี้เราจะส่งภาพที่ต้องการถอดรหัสให้กับ engine. เมธอด `recognizeImage` จะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่เก็บสตริงที่สกัดและคะแนนความเชื่อมั่น.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

หากไม่พบไฟล์, Aspose จะโยน `FileNotFoundException`. ควรห่อการเรียกในบล็อก `try‑catch` สำหรับโค้ดการผลิต, แต่ในบทเรียนนี้เราจะทำให้เรียบง่าย.

## ขั้นตอนที่ 4: แสดงข้อความที่จดจำได้

สุดท้าย, เราจะพิมพ์ผลลัพธ์. เมธอด `getText()` จะคืนค่า `String` ของ Java ธรรมดาที่คุณสามารถเก็บ, ส่งผ่านเครือข่าย, หรือเขียนลงไฟล์.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

เมื่อคุณรันโปรแกรม, คุณควรเห็นอย่างเช่น:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบอีกครั้งว่า PNG ต้นฉบับมีความละเอียดสูง (อย่างน้อย 300 dpi) และรหัสภาษา `"th"` ตรงกับภาษาที่คุณต้องการ.

### รายการโค้ดเต็ม

ด้านล่างเป็นไฟล์ Java ที่สมบูรณ์พร้อมรัน. คัดลอกและวางลงใน IDE ของคุณ, แทนที่เส้นทางรูปภาพหากจำเป็น, แล้วกด **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![ตัวอย่างการรัน OCR บนรูปภาพ](image.png "ตัวอย่างการรัน OCR บนรูปภาพ – โค้ด Java ดึงข้อความภาษาไทยจาก PNG")

## ขั้นตอนที่ 5: การเปลี่ยนแปลงทั่วไปและกรณีขอบ

### การแปลงรูปภาพเป็นข้อความในรูปแบบอื่น

หากคุณต้องการ **convert image to text** สำหรับ JPEG หรือ BMP, เพียงเปลี่ยนส่วนขยายไฟล์ใน `imagePath`. Aspose OCR รองรับ PNG, JPEG, BMP, TIFF, และแม้กระทั่งหน้า PDF.

### การสกัดข้อความจาก PNG ด้วยหลายภาษา

คุณสามารถให้ engine ตรวจจับหลายภาษาได้พร้อมกัน:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

ผลลัพธ์จะมีอักขระภาษาไทยและอังกฤษผสมกัน, ซึ่งสะดวกสำหรับใบเสร็จสองภาษา.

### การจัดการภาพคุณภาพต่ำ

สำหรับสแกนที่เบลอ, พิจารณาเปิดการทำ preprocessing:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

นี่จะเรียกใช้อัลกอริธึมการลดสัญญาณรบกวนและเพิ่มคอนทราสต์ในตัว, ปรับปรุงขั้นตอน **extract text from PNG**.

### การเปิดใช้งานใบอนุญาต

หากไม่มีใบอนุญาต, Aspose จะใส่บรรทัดลายน้ำในผลลัพธ์หลังจาก 100 หน้า. เปิดใช้งานใบอนุญาตของคุณตั้งแต่ต้น:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

วางไฟล์ `.lic` ข้างไฟล์ JAR ของคุณหรืออ้างอิงผ่านเส้นทางแบบ absolute.

## คำถามที่พบบ่อย

**Q: ทำงานบน Linux ได้หรือไม่?**  
**A:** แน่นอน. Aspose OCR เป็น Java แท้, ดังนั้น OS ที่รองรับ JVM ใดก็ใช้ได้.

**Q: PNG มีข้อความไทยเป็นลายมือหรือไม่?**  
**A:** การจดจำลายมือมีข้อจำกัด; คุณอาจต้องใช้โมเดล neural‑network เฉพาะ. Aspose OCR ทำได้ดีกับข้อความพิมพ์.

**Q: สามารถประมวลผลหลายภาพในโฟลเดอร์พร้อมกันได้หรือไม่?**  
**A:** ห่อการเรียก `recognizeImage` ในลูปที่วน `Files.list(Paths.get("folder"))`. จำไว้ว่าให้ใช้ instance ของ `OcrEngine` เดียวกันเพื่อประสิทธิภาพ.

## สรุป

เราได้อธิบายตัวอย่างครบวงจรของการ **run OCR on image** ไฟล์ใน Java, โดยเฉพาะการ **extract Thai text** จาก PNG. ด้วยการเริ่มต้น `OcrEngine`, ตั้งค่าภาษา, เรียก `recognizeImage`, และพิมพ์ผลลัพธ์, ตอนนี้คุณมีวิธีที่เชื่อถือได้ในการ **convert image to text** โดยไม่ต้องใช้บริการของบุคคลที่สาม.

จากนี้คุณอาจ:

* **extract text from PNG** ไฟล์เป็นจำนวนมากสำหรับโครงการทำเหมืองข้อมูล.  
* ผสานผลลัพธ์ OCR กับ API แปลภาษาเพื่อรับข้อความภาษาอังกฤษ.  
* สำรวจภาษอื่นที่ Aspose รองรับ, เช่น จีนหรืออาหรับ, โดยเปลี่ยนรหัสภาษา.

ลองใช้กับรูปภาพของคุณเอง—ปรับการตั้งค่า preprocessing, ทดลองกับรูปแบบไฟล์ต่าง ๆ, และดูว่าการแก้ปัญหานี้มีความทนทานแค่ไหนในกระบวนการทำงานจริงของคุณ.

ขอให้สนุกกับการเขียนโค้ด, และขอให้ pipeline OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}