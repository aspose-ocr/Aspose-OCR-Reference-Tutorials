---
category: general
date: 2026-01-07
description: รับข้อความ OCR จากภาพโดยใช้ Aspose OCR Java เรียนรู้วิธีดึงข้อความจากภาพ
  โหลดภาพสำหรับ OCR และรันตัวอย่าง OCR ด้วย Java ภายในไม่กี่นาที.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: th
og_description: รับข้อความ OCR จากภาพด้วย Aspose OCR Java คู่มือนี้แสดงตัวอย่าง OCR
  ด้วย Java วิธีดึงข้อความจากภาพและวิธีโหลด OCR ของภาพอย่างมีประสิทธิภาพ
og_title: ดึงข้อความ OCR ใน Java – คู่มือ Aspose OCR อย่างสมบูรณ์
tags:
- OCR
- Java
- Aspose
- Image Processing
title: ดึงข้อความ OCR ใน Java – ตัวอย่าง Aspose OCR อย่างสมบูรณ์
url: /th/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับข้อความ OCR ใน Java – ตัวอย่าง Aspose OCR ครบถ้วน

เคยต้องการ **รับข้อความ OCR** จากเอกสารที่สแกนแต่ไม่แน่ใจว่าจะเลือกไลบรารีใด? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่น การอัตโนมัติใบแจ้งหนี้, การประมวลผลใบเสร็จ, หรือการแปลงฟอร์มหลายภาษา—การสกัดข้อความจากภาพเป็นขั้นตอนแรกสู่การอัตโนมัติ  

ในบทแนะนำนี้เราจะพาไปผ่าน **java OCR example** ที่ใช้ไลบรารี Aspose OCR for Java. เมื่อจบคุณจะรู้วิธี **load image OCR**, เรียกใช้เอนจิน, และ **extract text image** ด้วยเพียงไม่กี่บรรทัดของโค้ด ไม่ได้มีเนื้อหาเกินความจำเป็น เพียงวิธีแก้ปัญหาที่คุณสามารถคัดลอก‑วางไปใช้ในโปรเจคของคุณได้

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR for Java (รวมถึง Maven coordinates)  
- ขั้นตอนที่แน่นอนเพื่อ **load image OCR** และระบุภาษา  
- วิธี **get OCR text** เป็นสตริงธรรมดาและพิมพ์ออกที่คอนโซล  
- เคล็ดลับในการจัดการกับภาพหลายภาษาและการตรวจจับภาษาอัตโนมัติ  

*Prerequisites*: Java 8 หรือใหม่กว่า, IDE ที่รองรับ Maven (IntelliJ IDEA, Eclipse, หรือ VS Code), และไลเซนส์ Aspose OCR for Java ที่ถูกต้อง (รุ่นทดลองฟรีใช้สำหรับการประเมิน)

---

![แผนผังแสดงวิธีรับข้อความ OCR จากภาพโดยใช้ Aspose OCR Java](https://example.com/ocr-flowchart.png "แผนผังการไหลของการรับข้อความ OCR")

## ขั้นตอนที่ 1 – เพิ่ม Aspose OCR Dependency (Load Image OCR)

แรกสุด ให้บอก Maven ให้ดึงไลบรารี Aspose OCR. เปิดไฟล์ `pom.xml` ของคุณและแทรกบล็อก `<dependency>` ต่อไปนี้ภายใน `<dependencies>`:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip**: หากคุณใช้ Gradle, คำสั่งที่เทียบเท่าคือ `implementation 'com.aspose:aspose-ocr:23.9'`. การเพิ่ม dependency นี้เป็นวิธีที่ประหยัดที่สุดเพื่อให้ความสามารถ **load image OCR** ในโปรเจคของคุณ.

## ขั้นตอนที่ 2 – สร้าง OCR Engine และโหลดภาพของคุณ

ต่อไปเราจะเขียนคลาส Java เล็ก ๆ ที่สร้างอินสแตนซ์ `OcrEngine`, ชี้ไปที่ไฟล์ภาพ, และบอกเอนจินว่าต้องจดจำภาษาใด. ภาษานั้นระบุด้วยรหัส ISO‑639‑2 (เช่น `"tam"` สำหรับ Tamil).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### ทำไมต้องตั้งค่าภาษาอย่างชัดเจน?

การระบุภาษาช่วยลดผลลัพธ์เท็จและเร่งความเร็วการจดจำ. สำหรับ PDF หลายภาษา คุณสามารถวนลูปผ่านอาเรย์ของรหัสภาษา, หรือเปิดใช้งาน auto‑detect เพื่อความสะดวก.

## ขั้นตอนที่ 3 – รันกระบวนการ OCR และ **Get OCR Text**

เมื่อเอนจินถูกตั้งค่าแล้ว บรรทัดต่อไปนี้จะทำการจดจำจริง ๆ. วัตถุผลลัพธ์จะมีสตริงที่สกัดและเมตาดาต้าเพิ่มเติม.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

เมื่อคุณรัน `LanguageExample`, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

หากคุณใช้ `setAutoDetectLanguage(true)`, เอนจินจะพยายามทายภาษาสำหรับคุณ, ซึ่งเป็นประโยชน์เมื่อจัดการกับเอกสารที่ไม่ทราบภาษา.

## ขั้นตอนที่ 4 – การจัดการกับกรณีขอบที่พบบ่อย (Extract Text Image Variations)

### การจัดการกับภาพความละเอียดต่ำ

ความแม่นยำของ OCR ลดลงอย่างมากเมื่อความละเอียดต่ำกว่า 300 dpi. หากภาพต้นทางของคุณมีความละเอียดต่ำ, ควรอัปสแคลภาพก่อน:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### การกำจัดสัญญาณรบกวนพื้นหลัง

บางครั้งฟอร์มที่สแกนมีจุดสกปรกที่ทำให้เอนจินสับสน. คุณสามารถเปิดใช้งานการเตรียมข้อมูลล่วงหน้า:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### การสกัดข้อความจากพื้นที่เฉพาะ

หากคุณต้องการข้อความจากสี่เหลี่ยมเฉพาะ (เช่น เซลล์ตาราง), ตั้งค่า `Rectangle` ก่อนเรียก `recognize()`:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

การปรับแต่งเหล่านี้ทำให้ **java OCR example** ของคุณแข็งแรงพอสำหรับงานในระดับผลิต

## ขั้นตอนที่ 5 – ตรวจสอบผลลัพธ์ (คุณควรคาดหวังอะไร?)

การรันสำเร็จจะพิมพ์ข้อความธรรมดาของภาพออก. สำหรับภาพหลายภาษา คุณอาจเห็นสคริปต์ผสมกัน:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

หากผลลัพธ์ว่างหรือเป็นอักขระผิดพลาด, ตรวจสอบสองครั้ง:

1. เส้นทางไฟล์ใน `setImage` (ถูกต้องหรือไม่?)  
2. รหัสภาษาตรงกับสคริปต์ในภาพหรือไม่.  
3. คุณภาพของภาพ (คอนทราสต์, DPI) เพียงพอหรือไม่.

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นไฟล์ทั้งหมด, พร้อมคอมไพล์และรัน. แทนที่ `YOUR_DIRECTORY/multilingual.png` ด้วยเส้นทางจริงของภาพทดสอบของคุณ.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

คอมไพล์และรัน:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

ตอนนี้คุณควรเห็นเนื้อหาที่สกัดพิมพ์ออกที่คอนโซลของคุณ

---

## สรุป

เราได้แสดงให้คุณเห็น **วิธีรับข้อความ OCR** จากภาพโดยใช้ Aspose OCR for Java. ด้วยการทำตาม **java OCR example** นี้, คุณสามารถ **extract text image** ข้อมูล, **load image OCR**, และแม้แต่ปรับเอนจินสำหรับอินพุตหลายภาษา หรือมีสัญญาณรบกวน  

จากนี้คุณอาจ:

- ผสานขั้นตอน OCR เข้ากับเวิร์กโฟลว์ที่ใหญ่ขึ้น (เช่น เก็บข้อความในฐานข้อมูล)  
- รวมกับ API แปลภาษาเพื่อแปลงการสแกนหลายภาษาเป็นภาษาเดียว  
- ทดลองใช้ฟีเจอร์ Aspose OCR อื่น ๆ เช่น การแปลง PDF หรือการตรวจจับบาร์โค้ด  

ลองใช้งาน, ทดลองทำให้บางอย่างล้มเหลว, แล้วปรับตั้งค่าให้ผลลัพธ์แม่นยำที่สุด. ขอให้สนุกกับการเขียนโค้ด, และขอให้ OCR ของคุณชัดเจนเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}