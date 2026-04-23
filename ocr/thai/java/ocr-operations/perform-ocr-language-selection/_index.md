---
date: 2026-02-12
description: เรียนรู้วิธีทำ OCR ข้อความในรูปภาพพร้อมการเลือกภาษาโดยใช้ Aspose.OCR
  สำหรับ Java คู่มือแบบขั้นตอนนี้ครอบคลุมการดึงข้อความใน Java, การแก้ไขการเอียงของ
  OCR, และอื่น ๆ อีกมากมาย.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: วิธีทำ OCR ข้อความในภาพด้วยภาษาโดยใช้ Aspose.OCR
url: /th/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ข้อความในรูปภาพด้วยภาษาโดยใช้ Aspose.OCR

## บทนำ

การสกัดข้อความจากไฟล์รูปภาพเป็นความต้องการทั่วไป ไม่ว่าจะเป็นการแปลงเอกสารสแกนเป็นดิจิทัล การประมวลผลใบเสร็จ หรือการสร้างคลังข้อมูลที่สามารถค้นหาได้ ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างเต็มรูปแบบแบบทำ‑มือที่แสดง **วิธีทำ OCR ข้อความในรูปภาพ** พร้อมการตั้งค่าภาษาเฉพาะ เพื่อให้คุณสามารถรวม OCR ที่เชื่อถือได้เข้าไปในแอปพลิเคชัน Java ของคุณได้ทันที คุณยังจะได้เห็นวิธีจัดการการแก้ไขการเอียงของ OCR และการจดจำตามพื้นที่เพื่อความแม่นยำสูงสุด

## คำตอบสั้น
- **ไลบรารีใดที่ทำ OCR ใน Java?** Aspose.OCR for Java  
- **การตั้งค่าใดที่เลือกภาษา?** `settings.setLanguage(Language.Eng)` (หรือภาษาอื่นที่รองรับ)  
- **ต้องใช้ไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ทดลองฟรีใช้ได้สำหรับการทดสอบ; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **สามารถจำกัด OCR ให้ทำงานเฉพาะส่วนของรูปภาพได้หรือไม่?** ได้, ใช้ `RecognitionSettings.setRecognitionAreas()` พร้อมสี่เหลี่ยมผืนผ้า  
- **ระยะเวลาการทำงานโดยทั่วไปเป็นเท่าไหร่?** ไม่กี่วินาทีต่อหน้าในแล็ปท็อปมาตรฐาน, ขึ้นอยู่กับขนาดรูปภาพและความซับซ้อนของภาษา

## วิธีทำ OCR ข้อความในรูปภาพพร้อมการเลือกภาษา
ในส่วนนี้เราจะตอบคำถามหลัก **วิธีทำ OCR** รูปภาพเมื่อคุณทราบภาษาของข้อความ การเลือกภาษาอย่างถูกต้องจะเพิ่มความแม่นยำของการจดจำอย่างมาก เพราะเครื่องมือ OCR สามารถใช้พจนานุกรมและโมเดลอักขระที่เฉพาะเจาะจงต่อภาษา

### ทำไมจึงสำคัญ
- **ความแม่นยำสูงขึ้น** – โมเดลเฉพาะภาษา ลดการจดจำผิดพลาด  
- **เพิ่มประสิทธิภาพ** – เครื่องมือข้ามการตรวจสอบภาษาที่ไม่จำเป็น  
- **จัดการอักขระพิเศษได้ดี** – ภาษาฝรั่งเศส, สเปน, เยอรมัน ฯลฯ จะถูกจดจำอย่างถูกต้องเมื่อใช้ `Language` enum ที่ตรงกัน

## “สกัดข้อความจากรูปภาพ” คืออะไร?
การสกัดข้อความจากรูปภาพ (OCR) แปลงการแสดงผลภาพของอักขระให้เป็นสตริงที่เครื่องคอมพิวเตอร์อ่านได้ ซึ่งทำให้สามารถค้นหา, วิเคราะห์, และทำกระบวนการสกัดข้อมูลได้โดยไม่ต้องพิมพ์ข้อความด้วยมือ

## ทำไมต้องใช้ Aspose.OCR พร้อมการเลือกภาษา?
- **รองรับหลายภาษา** – เลือกภาษา(หรือหลายภาษา) ที่ปรากฏในรูปภาพเพื่อเพิ่มความแม่นยำ  
- **ควบคุมได้ละเอียด** – ปรับการแก้ไขการเอียง, กำหนดพื้นที่จดจำ, และตั้งค่าการแก้ไขการเอียงอัตโนมัติ  
- **Pure Java API** – ไม่มีการพึ่งพาไลบรารีเนทีฟ, ผสานรวมง่ายกับโปรเจกต์ Java ใดก็ได้  
- **ข้อมูลผลลัพธ์ที่ครบถ้วน** – รับข้อความธรรมดา, JSON, สี่เหลี่ยมขอบเขต, และคำเตือนในคำเรียกเดียว

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

- **Java Development Kit (JDK)** ติดตั้งแล้ว (JDK 8 หรือใหม่กว่า)  
- **Aspose.OCR for Java** ไลบรารี – ดาวน์โหลดได้จากเว็บไซต์อย่างเป็นทางการ [ที่นี่](https://reference.aspose.com/ocr/java/)  
- ไฟล์รูปภาพที่มีข้อความที่คุณต้องการสกัด เช่น `p3.png`

## นำเข้าแพ็กเกจ

ในไฟล์ซอร์ส Java ของคุณ ให้เพิ่มคลาส Aspose.OCR ที่จำเป็นและยูทิลิตี้ของ Java มาตรฐาน:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## คู่มือขั้นตอน‑โดย‑ขั้นตอน

### ขั้นตอนที่ 1: ตั้งค่าโฟลเดอร์เอกสารของคุณ

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

แทนที่ `"Your Document Directory"` ด้วยเส้นทางเต็มที่ไฟล์ `p3.png` อยู่

### ขั้นตอนที่ 2: กำหนดเส้นทางรูปภาพ

```java
// The image path
String file = dataDir + "p3.png";
```

ตรวจสอบให้แน่ใจว่า ตัวแปร `file` ชี้ไปยังรูปภาพที่คุณต้องการประมวลผลอย่างถูกต้อง

### ขั้นตอนที่ 3: สร้างอินสแตนซ์ Aspose.OCR API

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

อ็อบเจกต์ `AsposeOCR` จะให้คุณเข้าถึงการทำงาน OCR ทั้งหมด

### ขั้นตอนที่ 4: ตั้งค่าตัวเลือกการจดจำ (การเลือกภาษา)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

ในขั้นตอนนี้เราจะทำการ:

1. ปิดการแก้ไขการเอียงอัตโนมัติ เพราะเราจะให้ค่าเอียงด้วยตนเอง  
2. กำหนดพื้นที่สี่เหลี่ยม (`RecognitionAreas`) เพื่อจำกัด OCR ให้ทำงานเฉพาะส่วนของรูปภาพที่มีข้อความจริง  
3. ตั้งค่า **ภาษา** เป็นอังกฤษ (`Language.Eng`) คุณสามารถเปลี่ยนเป็น `Language.Fra`, `Language.Spa` ฯลฯ ตามภาพต้นฉบับของคุณ

### ขั้นตอนที่ 5: ทำ OCR และดึงผลลัพธ์

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

คำเรียก `RecognizePage` จะรันเครื่องมือ OCR ด้วยรูปภาพและการตั้งค่าที่คุณกำหนด ผลลัพธ์จะถูกเก็บไว้ในอ็อบเจกต์ `RecognitionResult`

### ขั้นตอนที่ 6: พิมพ์และใช้งานผลลัพธ์

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

ผลลัพธ์ที่แสดงบนคอนโซลจะประกอบด้วย:

- ข้อความที่สกัดทั้งหมด (`recognitionText`)  
- ข้อความสำหรับแต่ละสี่เหลี่ยมที่กำหนด (`recognitionAreasText`)  
- พิกัดสี่เหลี่ยมขอบเขต  
- การแสดงผลเป็น JSON เพื่อการประมวลผลต่อไปได้ง่าย  
- มุมเอียงที่ตรวจพบและคำเตือนใด ๆ  

คุณสามารถนำ `result.recognitionText` ไปใช้ในโลจิกธุรกิจของคุณได้ — เก็บไว้, ทำดัชนี, หรือส่งต่อให้บริการอื่น

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **อักขระแปลก** | เลือกภาษาผิด | ตั้งค่า `Language` enum ให้ถูกต้อง (เช่น `Language.Fra` สำหรับภาษาฝรั่งเศส) |
| **ไม่มีข้อความคืนค่า** | พื้นที่จดจำไม่ครอบคลุมข้อความ | ปรับค่าพิกัด `Rectangle` หรือเอา `RecognitionAreas` ออกเพื่อให้ OCR ทำงานกับรูปภาพทั้งหมด |
| **ประสิทธิภาพช้า** | รูปภาพขนาดใหญ่มากหรือความละเอียดสูง | ลดขนาดรูปภาพก่อนทำ OCR หรือเพิ่มหน่วยความจำให้ JVM |
| **คำเตือนรูปแบบไม่รองรับ** | รูปแบบไฟล์ไม่ถูกต้อง | แปลงรูปภาพเป็น PNG, JPEG หรือ TIFF ก่อนประมวลผล |

## คำถามที่พบบ่อย

**ถาม: สามารถจดจำหลายภาษาในคำเรียก OCR ครั้งเดียวได้หรือไม่?**  
ตอบ: ได้ ใช้ `settings.setLanguage(Language.Eng | Language.Fra)` เพื่อเปิดใช้งานการจดจำหลายภาษา

**ถาม: Aspose.OCR รองรับรูปแบบไฟล์ภาพใดบ้าง?**  
ตอบ: PNG, JPEG, BMP, TIFF, GIF และอื่น ๆ เพียงให้เส้นทางไฟล์ที่ถูกต้อง

**ถาม: มีขนาดจำกัดของรูปภาพหรือไม่?**  
ตอบ: ไม่มีขีดจำกัดที่แน่นอน แต่รูปภาพขนาดใหญ่มากจะใช้หน่วยความจำและเวลาประมวลผลเพิ่มขึ้น ควรปรับขนาดไฟล์ใหญ่ก่อน

**ถาม: จะได้ไลเซนส์สำหรับการใช้งานจริงอย่างไร?**  
ตอบ: ซื้อไลเซนส์จากเว็บไซต์ Aspose แล้วนำไปใช้ผ่านคลาส `License` ตามที่แสดงในเอกสาร Aspose

**ถาม: สามารถสกัดข้อความจากหน้า PDF ได้โดยตรงหรือไม่?**  
ตอบ: ไม่ได้โดยตรงกับ Aspose.OCR ต้องแปลงหน้า PDF เป็นรูปภาพก่อน (เช่น ใช้ Aspose.PDF) แล้วจึงทำ OCR

## สรุป

คุณได้เรียนรู้วิธี **สกัดข้อความจากรูปภาพ** ด้วย Aspose.OCR for Java พร้อมการเลือกภาษาที่เหมาะสมและการจำกัดการจดจำในพื้นที่เฉพาะ วิธีนี้ให้ผลลัพธ์ OCR ที่แม่นยำและประสิทธิภาพสูง สามารถฝังเข้าไปในเวิร์กโฟลว์ Java ใดก็ได้ — ตั้งแต่ระบบจัดการเอกสารจนถึงสายการจับข้อมูล พร้อมใช้งานแล้วหรือยัง? ลองเปลี่ยนค่า enum ของภาษา, ทดลองกับพื้นที่จดจำต่าง ๆ, แล้วผสานผลลัพธ์เข้ากับแอปพลิเคชันของคุณเอง

---

**อัปเดตล่าสุด:** 2026-02-12  
**ทดสอบกับ:** Aspose.OCR 24.11 for Java  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}