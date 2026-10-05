---
category: general
date: 2026-01-12
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน Java. เรียนรู้วิธีดึงข้อความจากภาพใบแจ้งหนี้ด้วยตัวอย่าง
  OCR ใน Java และรับผลลัพธ์เป็นข้อความ OCR.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน Java คู่มือนี้แสดงวิธีดึงข้อความจากภาพใบแจ้งหนี้
  รวมตัวอย่าง Java OCR และแสดงผลข้อความ OCR
og_title: ดึงข้อความจากภาพใน Java – ตัวอย่าง OCR ครบถ้วน
tags:
- OCR
- Java
- Aspose
title: สกัดข้อความจากภาพใน Java – ตัวอย่าง OCR อย่างสมบูรณ์
url: /th/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Java – ตัวอย่าง OCR ครบวงจร

เคยสงสัยไหมว่า **การดึงข้อความจากไฟล์รูปภาพ** ทำอย่างไรโดยไม่ต้องเสียศีรษะ? บางครั้งคุณอาจมีใบแจ้งหนี้สแกนหลายใบและต้องการตัวเลขอย่างรวดเร็ว จากประสบการณ์ของผม วิธีที่ง่ายที่สุดคือให้ไลบรารี OCR เฉพาะทำงานหนักให้เรา บทแนะนำนี้จะแสดง *วิธีดึงข้อความ* จากรูปใบแจ้งหนี้ทั่วไปโดยใช้ Aspose OCR for Java และยังมี **java ocr example** ที่แสดงการแสดงผลข้อความ OCR ที่คุณสามารถส่งต่อไปยังระบบต่อท้ายได้

เราจะเดินผ่านทุกขั้นตอนที่คุณต้องรู้: ตั้งค่าโปรเจกต์, กำหนดพื้นที่สนใจ (ROI) ที่โฟกัสที่หัวเรื่องและยอดรวม, จนถึงการพิมพ์ข้อความที่ดึงออกมา เมื่อเสร็จสิ้นคุณจะสามารถ **process invoice image** ไฟล์ได้โดยอัตโนมัติและได้ข้อความที่สะอาดและค้นหาได้

> **สิ่งที่คุณจะได้:** โปรแกรม Java ที่พร้อมรัน, คำอธิบายแต่ละขั้นตอนอย่างชัดเจน, และเคล็ดลับการจัดการใบแจ้งหนี้ในโลกจริง

---

## Prerequisites

ก่อนที่เราจะลงลึก, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- Java Development Kit (JDK) 8 หรือใหม่กว่า
- Maven หรือ Gradle สำหรับจัดการ dependency (ตัวอย่างใช้ Maven)
- ใบอนุญาต Aspose OCR for Java (เวอร์ชันทดลองฟรีใช้สำหรับทดสอบ)
- รูปใบแจ้งหนี้ (`invoice.png`) ที่วางไว้ในไดเรกทอรีที่ทราบ

หากสิ่งใดดูแปลกใจ, ไม่ต้องกังวล—ส่วนใหญ่สามารถดาวน์โหลดได้ทันทีและโค้ดยังคงคอมไพล์ได้ด้วยรุ่น community edition

---

## Step 1: Set Up Your Maven Project

เริ่มแรก, สร้างโปรเจกต์ Maven ใหม่ (หรือเพิ่มในโปรเจกต์ที่มีอยู่) ในไฟล์ `pom.xml` ของคุณ ให้เพิ่ม dependency ของ Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** คอยอัปเดตหมายเลขเวอร์ชันอยู่เสมอ; เวอร์ชันใหม่มักปรับปรุงความแม่นยำสำหรับฟอนต์ที่ซับซ้อนบนใบแจ้งหนี้

หลังจากบันทึกไฟล์, รัน `mvn clean install` เพื่อดึงไลบรารีเข้าสู่ repository ภายในเครื่องของคุณ

---

## Step 2: Load the Invoice Image

เมื่อไลบรารีพร้อม, เรามาเขียนคลาส Java เล็ก ๆ ตัวแรกที่เราจะทำคือสร้างอินสแตนซ์ `OcrEngine` แล้วชี้ไปที่รูปที่ต้องการอ่าน

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

ทำไมเราต้องสร้าง engine **ก่อน** โหลดรูป? Engine จะเก็บการตั้งค่าเช่นภาษา, DPI, และ ROI การตั้งค่ารูปล่วงหน้าช่วยให้การตั้งค่าเหล่านั้นใช้กับไฟล์ที่กำลังจะประมวลผลได้อย่างแม่นยำ

---

## Step 3: Define Regions of Interest (ROI)

ใบแจ้งหนี้มักมีสัญญาณรบกวนมาก—ตาราง, โลโก้, ตัวอักษรเล็ก ๆ การจำกัด OCR ให้ทำงานเฉพาะส่วนหัวและยอดรวมจะเพิ่มความเร็วและความแม่นยำอย่างมาก Aspose ให้คุณกำหนดโซนเหล่านี้ด้วยสี่เหลี่ยม

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

พิกัดอยู่ในหน่วยพิกเซล (`x`, `y`, `width`, `height`) หากใบแจ้งหนี้ของคุณมีขนาดต่างกัน, คุณสามารถคำนวณค่าต่าง ๆ แบบไดนามิก—เช่นตรวจสอบขนาดภาพก่อน นี่เป็นการขยายที่ดีหากคุณต้องการโซลูชัน **process invoice image** ที่ทำงานกับหลายไฟล์

---

## Step 4: Run OCR on the Specified Regions

เมื่อกำหนด ROI แล้ว, engine OCR จะโฟกัสที่ส่วนที่สำคัญที่สุด เมธอด `recognize()` จะคืนค่า `OcrResult` ที่บรรจุข้อความที่ดึงออกมา

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

เบื้องหลัง, Aspose ทำขั้นตอนการเตรียมภาพหลายขั้นตอน: การทำไบนารี, การกำจัดสัญญาณรบกวน, และการแยกอักขระ คุณไม่ต้องเรียกใช้ขั้นตอนเหล่านี้เอง—แค่ให้ `recognize()` ทำหน้าที่

---

## Step 5: Output the Extracted Text

สุดท้าย, เราพิมพ์ข้อความลงคอนโซล ในแอปพลิเคชันจริงคุณอาจเก็บไว้ในฐานข้อมูล, ส่งต่อไปยัง pipeline analytics, หรือแม้แต่สร้าง PDF ที่ค้นหาได้

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

เมื่อรันโปรแกรม, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบพิกัดสี่เหลี่ยมอีกครั้งหรือเพิ่มความละเอียดของภาพ OCR ทำงานได้ดีที่สุดกับสแกนที่คมชัดและ DPI สูง

---

## Full Working Example

ด้านล่างเป็นไฟล์ Java ฉบับเต็มที่คุณสามารถคัดลอก‑วางลงใน `src/main/java/RoiExample.java` ไม่ต้องใช้สคริปต์ภายนอก—ทุกอย่างที่ต้องการอยู่ที่นี่แล้ว

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มไปยังรูปใบแจ้งหนี้ของคุณ หากใช้พาธสัมพัทธ์, ตรวจสอบให้แน่ใจว่าไดเรกทอรีทำงานตรงกับที่คุณรันคำสั่ง `java`

---

## Common Questions & Edge Cases

### What if the invoice size changes?

คุณสามารถคำนวณ ROI แบบไดนามิกได้ดังนี้:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### How do I handle multiple languages?

Aspose OCR รองรับ language pack เพียงตั้งค่าภาษาให้ถูกต้องก่อนเรียก `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### What if the OCR returns empty strings?

สาเหตุที่พบบ่อยคือ:

- ความละเอียดภาพต่ำ (< 300 DPI) ให้เพิ่มขนาดหรือขอสแกนคุณภาพสูงขึ้น
- พื้นหลังมืดหรือสว่างเกินไป ให้ใช้ฟิลเตอร์เพิ่มคอนทราสต์ก่อน OCR
- พิกัด ROI ไม่ตรงกับข้อความจริง ทำให้พลาดข้อความทั้งหมด

---

## Tips for Production‑Ready OCR

1. **Batch Processing:** ห่อหุ้มโลจิกในลูปที่วนผ่านไดเรกทอรีของไฟล์ใบแจ้งหนี้หลายไฟล์ บันทึกผลลัพธ์แต่ละไฟล์เพื่อการ audit
2. **Error Handling:** ดักจับ `OcrException` เพื่อข้ามภาพที่เสียหายโดยไม่ทำให้งานทั้งหมดหยุด
3. **Performance:** ใช้ `OcrEngine` ตัวเดียวหลายภาพ; การสร้าง engine ใหม่ต่อไฟล์เพิ่ม overhead ที่ไม่จำเป็น
4. **Validation:** หลังดึงข้อความ, ใช้ regex ตรวจสอบยอดรวม (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) เพื่อให้แน่ใจว่าตัวเลขดูสมเหตุสมผล

การนำข้อแนะนำเหล่านี้ไปใช้จะทำให้ **java ocr example** ของคุณกลายเป็นโซลูชันที่แข็งแรงและขยายได้สำหรับธุรกิจที่ต้อง **process invoice image** ทุกคืน

---

## Conclusion

เราได้อธิบายวิธี **extract text from image** ใน Java ด้วย Aspose OCR โดยเน้นการประมวลผลใบแจ้งหนี้จริง การกำหนด ROI, รัน engine OCR, และพิมพ์ **output OCR text** ตอนนี้คุณมีพื้นฐานที่มั่นคงสำหรับสร้าง pipeline การจับข้อมูลอัตโนมัติ

ขั้นตอนต่อไป? ลองขยาย ROI ให้ครอบคลุมตารางรายการ, ทดลองตั้งค่าภาษาอื่น, หรือส่งข้อความที่ดึงมาให้ไลบรารีสร้าง PDF ที่ค้นหาได้ ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อผสาน OCR กับเครื่องมือ Java สมัยใหม่

มีคำถามเพิ่มเติมเกี่ยวกับ **how to extract text** จากประเภทเอกสารอื่น ๆ หรืออยากปรับ ROI สำหรับเลย์เอาต์แปลก ๆ? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}