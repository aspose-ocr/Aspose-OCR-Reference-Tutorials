---
category: general
date: 2026-05-03
description: ตัวอย่าง Aspose OCR Java แสดงวิธีการโหลดภาพเพื่อทำ OCR และสกัดข้อความจากบริเวณหนึ่งโดยใช้เพียงไม่กี่บรรทัดของโค้ด.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: th
og_description: ตัวอย่าง Aspose OCR Java แสดงการโหลดภาพเพื่อทำ OCR และสกัดข้อความจากพื้นที่เฉพาะ
  เหมาะอย่างยิ่งสำหรับการประมวลผลใบแจ้งหนี้
og_title: ตัวอย่าง Aspose OCR Java – การสกัดข้อความจากพื้นที่
tags:
- Aspose OCR
- Java
- Image Processing
title: 'ตัวอย่าง Aspose OCR Java: ดึงข้อความจากพื้นที่'
url: /th/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวอย่าง Aspose OCR Java: ดึงข้อความจากพื้นที่

กำลังมองหาตัวอย่าง **Aspose OCR Java** ที่ให้คุณดึงเฉพาะส่วนที่ต้องการจากภาพหรือไม่? ในคู่มือนี้เราจะอธิบาย **การโหลดภาพสำหรับ OCR** และ **การดึงข้อความจากพื้นที่** ซึ่งเหมาะสำหรับหมายเลขใบแจ้งหนี้, ฟิลด์ฟอร์ม, หรือข้อมูลใด ๆ ที่ซ่อนอยู่ในภาพขนาดใหญ่

คุณอาจสงสัยว่าทำไมต้องจำกัด OCR ไว้ที่สี่เหลี่ยมแทนการสแกนทั้งหน้า คำตอบสั้น ๆ คือ ความเร็วและความแม่นยำ เมื่อเครื่องมือมองแค่ส่วนที่กำหนด มันจะข้ามเสียงรบกวนที่ไม่เกี่ยวข้อง, ทำงานเร็วขึ้น, และมักให้ผลลัพธ์ที่สะอาดกว่า เมื่อจบบทเรียนนี้คุณจะมีโปรแกรม Java ที่ทำงานอิสระได้อย่างครบถ้วน พร้อมเคล็ดลับหลากหลายเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไปที่ผู้เริ่มต้นมักเจอ

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- **Java Development Kit (JDK) 11** หรือใหม่กว่า
- ไลบรารี **Aspose.OCR for Java** (คุณสามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central หรือพอร์ทัลดาวน์โหลดของ Aspose)
- ไฟล์ภาพที่มีข้อความที่คุณต้องการอ่าน – สำหรับสาธิตนี้เราจะใช้ `invoice.png` ซึ่งมีหมายเลขใบแจ้งหนี้อยู่ใกล้มุมบน‑ขวา
- IDE ที่คุณชื่นชอบหรือเพียงแค่ตัวแก้ไขข้อความธรรมดาพร้อมเทอร์มินัล; เครื่องมือสร้างใด ๆ (Maven, Gradle, หรือ `javac` ธรรมดา) ก็ใช้ได้

แค่นั้นเอง ไม่ต้องมีเอนจิน OCR เพิ่มเติม, ไม่ต้องมีไบนารีเนทีฟ, เพียงแค่ Java และ Aspose

![ภาพตัวอย่าง Aspose OCR Java](/images/aspose-ocr-java-example.png "Aspose OCR Java แสดงการดึงข้อความจากพื้นที่")

## ตัวอย่าง Aspose OCR Java – เริ่มต้น Engine OCR

สิ่งแรกที่ทุก workflow ของ OCR ต้องมีคืออินสแตนซ์ของ engine. Aspose มีคลาส `OcrEngine` ที่เบาและจัดการทุกอย่างตั้งแต่การโหลดภาพจนถึงการเลือกภาษา

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**ทำไมจึงสำคัญ:** การสร้าง engine ล่วงหน้าจะให้คุณมีอ็อบเจกต์ที่สะอาดสำหรับการตั้งค่า คุณสามารถใช้ `OcrEngine` เดียวกันสำหรับหลายภาพได้หากต้องประมวลผลเป็นชุด, ช่วยประหยัดหน่วยความจำและเวลาเริ่มต้น

## โหลดภาพสำหรับ OCR

ต่อไปเราต้องบอก engine ว่าจะสแกนภาพไหน Aspose มีตัวช่วย `ImageStream.fromFile` ที่ทำให้คุณไม่ต้องจัดการกับโค้ด `FileInputStream` ระดับล่าง

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**เคล็ดลับ:** แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มหรือพาธสัมพันธ์ที่ชี้ไปยังตำแหน่งที่คุณเก็บ `invoice.png` หากไฟล์ไม่พบ Aspose จะโยน `IOException` ดังนั้นคุณอาจต้องใส่โค้ดในบล็อก try‑catch สำหรับโค้ดที่ใช้ใน production

## กำหนดและดึงข้อความจากพื้นที่

ตอนนี้มาถึงส่วนสำคัญ: สี่เหลี่ยมที่บอก engine ว่าจะมองที่ไหน คอนสตรัคเตอร์ `java.awt.Rectangle` รับค่า `(x, y, width, height)` – ทั้งหมดเป็นพิกเซล

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**วิธีทำงาน:** การเรียก `setRegion` จะจำกัดการสแกน OCR ให้เป็นส่วนกว้าง 300 พิกเซลที่เริ่มจาก 120 พิกเซลจากขอบซ้ายและ 250 พิกเซลจากด้านบน ปรับค่าตามเลย์เอาต์ของคุณ; วิธีง่าย ๆ คือเปิดภาพในโปรแกรมกราฟิกใด ๆ ที่แสดงพิกเซลคอร์ดิเนต

## เปิดใช้งานภาษาและรันการจดจำ

Aspose OCR รองรับหลายสิบภาษา, แต่สำหรับหมายเลขใบแจ้งหนี้เราต้องการแค่ภาษาอังกฤษเท่านั้น การเปิดใช้ภาษาเดียวจะลด false positives อย่างมาก

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**ทำไมต้องเปิดใช้เฉพาะอังกฤษ?** Engine OCR จะพยายามจับคู่ตัวอักษรจากทุกภาษาที่เปิดใช้งาน, ซึ่งอาจทำให้สับสนเมื่อข้อความเป็นอักขระอัลฟานูเมอริกง่าย ๆ การจำกัดขอบเขตภาษาเพิ่มความเร็วและความแม่นยำ

### ผลลัพธ์ที่คาดหวัง

เมื่อทุกอย่างทำงานตรงกัน, คุณจะเห็นข้อความประมาณนี้:

```
Extracted region text: INV-12345
```

หากสี่เหลี่ยมเลื่อนตำแหน่งไปไม่ตรงพิกเซลไม่กี่พิกเซล, ผลลัพธ์อาจเป็นข้อความเสียหรือว่างเปล่า นี่คือการตรวจสอบอย่างง่าย: รันโปรแกรม, ดูที่คอนโซล, และยืนยันว่าข้อความตรงกับที่คุณเห็นในภาพ

## รันโค้ดและตรวจสอบผลลัพธ์

สมมติว่าคุณใช้ Maven, เพิ่ม dependency ของ Aspose OCR ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

คอมไพล์และรัน:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

หรือ, หากคุณชอบใช้ `javac` ธรรมดา:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

คุณควรเห็นบรรทัด **Extracted region text** ปรากฏบนคอนโซล หากเจอ “OCR recognition failed,” ตรวจสอบพาธไฟล์และให้แน่ใจว่าพื้นที่ที่กำหนดมีอักขระที่อ่านได้จริง

## กรณีขอบและความแปรผันทั่วไป

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน |
|-----------|----------------|
| **หลายภาษา** (เช่น อังกฤษ + สเปน) | เรียก `ocrEngine.getLanguage().setSpanish(true);` ควบคู่กับอังกฤษ |
| **พื้นที่อยู่นอกขอบภาพ** | Aspose จะตัดสี่เหลี่ยมโดยอัตโนมัติ, แต่คุณจะสูญเสียข้อมูล ใช้ `ImageInfo` (`ocrEngine.getImage().getWidth()`) เพื่อตรวจสอบขนาดก่อนตั้งค่า region |
| **ใบแจ้งหนี้แบบไดนามิก** (เลย์เอาต์ต่างกัน) | พิจารณาให้ทำการสแกนเบื้องต้นทั่วทั้งภาพเพื่อหาคำสำคัญเช่น “Invoice #” แล้วคำนวณสี่เหลี่ยมแบบโปรแกรม |
| **ภาพ DPI สูง** | เพิ่ม `ocrEngine.getImage().setResolution(300);` เพื่อความแม่นยำที่ดีขึ้นในเอกสารสแกน |
| **การปรับจูนประสิทธิภาพ** | ปิดภาษาที่ไม่จำเป็น, ทำให้ region เล็กที่สุดเท่าที่ทำได้, และใช้ `OcrEngine` ตัวเดียวกันหลายไฟล์ |

## เคล็ดลับระดับมืออาชีพจากสนามรบ

- **Pro tip:** หากคุณต้องการเฉพาะตัวเลข (เช่นหมายเลขใบแจ้งหนี้), เปิดโหมดตัวเลขด้วย `ocrEngine.getLanguage().setDigits(true);` จะช่วยกำจัดเสียงรบกวนจากอักษร
- **ระวัง:** PNG ที่มีความโปร่งใส Aspose บางครั้งอาจตีความช่อง alpha ผิด; การแปลงภาพเป็น JPEG พื้นหลังทึบก่อนจะช่วยแก้ปัญหาเอาต์พุตว่างแปลก ๆ
- **จำไว้:** สี่เหลี่ยมใช้ระบบพิกัดดิบของภาพ, ไม่ใช่การสเกล UI ที่คุณอาจเห็นบนหน้าจอ ควรทดสอบกับไฟล์จริงที่ใช้ใน production เสมอ

## ขั้นตอนต่อไปคืออะไร?

ตอนนี้คุณมี **ตัวอย่าง Aspose OCR Java** สำหรับการดึงข้อความจากพื้นที่แล้ว, คุณสามารถต่อยอดได้หลายทาง:

- **ประมวลผลเป็นชุด:** วนลูปโฟลเดอร์ใบแจ้งหนี้, ใช้ `OcrEngine` ตัวเดียวเพื่อเพิ่มอัตราการทำงาน
- **ตรวจสอบข้อมูล:** ส่งข้อความที่ดึงมาให้ regex เช่น `INV-\\d{5}` เพื่อตรวจสอบว่าคุณได้หมายเลขใบแจ้งหนี้ที่ถูกต้องหรือไม่
- **ผสานกับ PDF:** ใช้ Aspose.PDF เพื่อวางข้อความที่ดึงกลับไปบนเอกสารต้นฉบับเพื่อเป็นร่องรอยการตรวจสอบ
- **ปรับใช้บนคลาวด์:** ห่อโค้ดเป็นบริการ REST ขนาดเบา (Spring Boot) เพื่อให้ระบบอื่นเรียกใช้ตามต้องการ

ขั้นตอนเหล่านี้ทั้งหมดใช้แนวคิดหลักเดียวกัน—**โหลดภาพสำหรับ OCR**, **ดึงข้อความจากพื้นที่**, และจัดการผลลัพธ์—ดังนั้นการเปลี่ยนแปลงจะเป็นเรื่องง่าย

---

*ขอให้เขียนโค้ดอย่างสนุก! หากเจออุปสรรคใด ๆ, แสดงความคิดเห็นด้านล่างหรือเยี่ยมชมฟอรั่มของ Aspose ที่ชุมชนแชร์เทคนิคจริงสำหรับเลย์เอาต์ที่ซับซ้อน*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}