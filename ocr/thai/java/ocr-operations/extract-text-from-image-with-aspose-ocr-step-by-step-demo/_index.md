---
category: general
date: 2026-02-14
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR. เรียนรู้วิธีโหลดภาพสำหรับ OCR, อ่านข้อความจากสี่เหลี่ยม,
  และทำตามบทเรียน Aspose OCR นี้ภายในไม่กี่นาที.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: th
og_description: ดึงข้อความจากภาพได้ทันที คู่มือนี้แสดงวิธีโหลดภาพสำหรับ OCR, อ่านข้อความจากสี่เหลี่ยม,
  และทำบทเรียน Aspose OCR ให้เสร็จสมบูรณ์.
og_title: สกัดข้อความจากภาพด้วย Aspose OCR – คู่มือด่วน
tags:
- Aspose
- OCR
- Java
title: สกัดข้อความจากภาพด้วย Aspose OCR – สาธิตแบบขั้นตอนต่อขั้นตอน
url: /th/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Aspose OCR – สาธิตขั้นตอนโดยละเอียด

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องทำการสแกนใบเสร็จหรือยืนยันตัวตนด้วยบัตรประชาชน ข่าวดีคืออะไร? ด้วย Aspose OCR คุณสามารถโหลดรูปภาพ กำหนดพื้นที่ที่ข้อความอยู่ แล้วดึงอักขระออกมาได้ในไม่กี่บรรทัดโค้ด

ใน **aspose ocr tutorial** นี้ เราจะพาคุณผ่านทุกขั้นตอนที่ต้องทำ: โหลดรูปภาพสำหรับ OCR, ตั้งสี่เหลี่ยมที่บอกเครื่องว่าให้มองหาในส่วนไหน, และสุดท้ายอ่านข้อความที่ดึงออกมา เมื่อเสร็จคุณจะได้โปรแกรม Java ที่รันได้และพิมพ์ข้อความ ROI ไปที่คอนโซล—ไม่มีความลับ แค่โซลูชันที่ชัดเจนและทำงานได้

## สิ่งที่คุณต้องเตรียม

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมีพื้นฐานดังต่อไปนี้:

| ข้อกำหนดเบื้องต้น | เหตุผลที่สำคัญ |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR มีรูปแบบเป็นไลบรารี Java; JDK สมัยใหม่ใดก็ใช้ได้. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | ให้บริการคลาส `OcrEngine`, `ImageStream`, และคลาสที่เกี่ยวข้อง. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | เราจะชี้เครื่องไปที่สี่เหลี่ยมภายในไฟล์นี้. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | ช่วยให้คุณคอมไพล์และรันตัวอย่างได้อย่างรวดเร็ว. |

หากคุณใช้ Maven ให้เพิ่ม dependency นี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **เคล็ดลับมืออาชีพ:** หมายเลขเวอร์ชันด้านบนเป็นเวอร์ชันล่าสุด ณ เดือนกุมภาพันธ์ 2026 การอัปเดตเป็นเวอร์ชันใหม่ล่าสุดจะช่วยให้คุณได้รับการแก้ไขบั๊กและปรับปรุงประสิทธิภาพ

## ขั้นตอน 1 – เริ่มต้นใช้งาน OCR Engine

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine` คิดว่าเป็นสมองที่ทำการวิเคราะห์พิกเซล

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

ทำไมต้องสร้างแบบนี้? Aspose แยกส่วน engine (ซึ่งเก็บการตั้งค่า) ออกจากข้อมูลรูปภาพ ทำให้คุณสามารถใช้ engine เดียวกันกับหลายรูปภาพได้หากต้องการ

## ขั้นตอน 2 – โหลดรูปภาพสำหรับ OCR

ต่อไปเราจะ **โหลดรูปภาพสำหรับ OCR** ตัวช่วย `ImageStream.fromFile` จะอ่านไฟล์เข้าเป็นสตรีมที่ Aspose เข้าใจได้

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

หากไฟล์ไม่พบ engine จะโยน exception ดังนั้นในโค้ดจริงคุณอาจต้องใส่ try‑catch แต่ในสาธิตนี้เราปล่อยให้ exception ลอยขึ้นมา—ทำให้ตัวอย่างดูเรียบง่าย

## ขั้นตอน 3 – กำหนดสี่เหลี่ยม (Read Text from Rectangle)

นี่คือส่วนที่ **read text from rectangle** ทำงานได้ดี คุณบอก engine ว่าจะมองหาในตำแหน่งใด ซึ่งช่วยเร่งการประมวลผลและลดผลบวกเท็จ

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **ทำไมต้องเป็นสี่เหลี่ยม?**  
> เอกสารส่วนใหญ่มีเลย์เอาต์ที่คาดเดาได้—เช่นใบเสร็จที่จำนวนเงินมักอยู่ที่ด้านล่าง เมื่อโฟกัสที่ส่วนนั้น OCR engine จะละเว้นกราฟิกที่ไม่เกี่ยวข้องและเพิ่มความแม่นยำ

**กรณีขอบ:** หากสี่เหลี่ยมเกินขอบของรูปภาพ Aspose จะทำการคลัมป์โดยอัตโนมัติ แต่คุณจะสูญเสียข้อมูล การตรวจสอบความสมเหตุสมผลอย่างง่ายสามารถป้องกันได้:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## ขั้นตอน 4 – ประมวลผลรูปภาพ

เมื่อทุกอย่างพร้อม เราขอให้ engine ทำงานของมัน

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

เมธอด `process()` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความที่ดึงออกมา, คะแนนความเชื่อมั่น, และแม้แต่กรอบล้อมรอบแต่ละคำหากคุณต้องการใช้ต่อไป

## ขั้นตอน 5 – แสดงข้อความที่ดึงออกมา

สุดท้าย พิมพ์ผลลัพธ์ออกมา ในแอปจริงคุณอาจเก็บลงฐานข้อมูลหรือส่งต่อให้บริการอื่น แต่สำหรับสาธิตนี้การแสดงผลบนคอนโซลก็เพียงพอ

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าตรงสี่เหลี่ยมจับจำนวนเงินทั้งหมดบนใบเสร็จ):

```
ROI text:
$12.34
```

หาก ROI ว่างเปล่าหรือรูปภาพเบลอ คุณจะเห็นสตริงว่างหรืออักขระแปลกๆ ปรับสี่เหลี่ยม, ปรับคุณภาพรูป, หรือเปิดใช้งานตัวเลือกการเตรียมข้อมูลของ Aspose (เช่น `setAutoSkewCorrection(true)`)

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมรัน คัดลอกและวางลงในไฟล์ชื่อ `RoiDemo.java` ปรับเส้นทางรูปภาพ แล้วรัน `javac RoiDemo.java && java RoiDemo`

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **การตรวจสอบผลลัพธ์:** หลังจากรันแล้ว ให้เปรียบเทียบข้อความบนคอนโซลกับข้อความจริงในสี่เหลี่ยม หากตรงกัน คุณได้ **extract text from image** ด้วย Aspose OCR อย่างสำเร็จ

## คำถามที่พบบ่อย & เคล็ดลับ

### ถ้าต้องประมวลผลหลาย ROI ในรูปเดียวต้องทำอย่างไร?
สร้าง `Rectangle` ใหม่สำหรับแต่ละพื้นที่, เรียก `setRegionOfInterest` อีกครั้ง, แล้วรัน `process()` ใหม่ Engine จะใช้ข้อมูลรูปภาพเดิม ทำให้ประสิทธิภาพยังคงเร็ว

### Aspose จัดการกับหลายภาษา หรือฟอนต์ต่างๆ อย่างไร?
คุณสามารถสลับโมเดลภาษาได้ด้วย `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` สำหรับสคริปต์ที่ไม่ใช่ละติน ให้โหลด language pack ที่เหมาะสม (ดาวน์โหลดจากหน้า Aspose)

### ไลบรารีรองรับการรับไฟล์ PDF หรือไม่?
ใช่—Aspose OCR สามารถรับสตรีม PDF ได้โดยตรง เพียงเปลี่ยน `ImageStream.fromFile` เป็น `ImageStream.fromPdfFile("doc.pdf")` และระบุหมายเลขหน้าได้ตามต้องการ

### จะเพิ่มความแม่นยำบนสแกนคุณภาพต่ำได้อย่างไร?
เปิดการเตรียมข้อมูลล่วงหน้า:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

ตัวเลือกเหล่านี้จะทำความสะอาดสัญญาณรบกวนและจัดแนวข้อความก่อนการจดจำ

## สรุป

เราได้เดินผ่าน **aspose ocr tutorial** ครบขั้นตอนที่แสดงวิธี **extract text from image**, **load image for OCR**, และ **read text from rectangle** ด้วย Java ขั้นตอนสำคัญคือการเริ่มต้น engine, ป้อนรูปภาพ, กำหนดพื้นที่สนใจ, ประมวลผล, และสุดท้ายพิมพ์ผลลัพธ์

ต่อจากนี้คุณอาจสำรวจ:

* **การประมวลผลเป็นชุด** – วนลูปโฟลเดอร์ใบเสร็จและเก็บจำนวนเงินแต่ละใบลงฐานข้อมูล  
* **การตรวจจับ ROI แบบไดนามิก** – ใช้ไลบรารีประมวลผลภาพ (OpenCV) เพื่อหาบล็อกข้อความโดยอัตโนมัติ  
* **การหลังประมวลผล** – ใช้ regex หรือ fuzzy matching เพื่อลบข้อผิดพลาดของ OCR

ลองนำไอเดียเหล่านี้ไปใช้ ปรับสี่เหลี่ยมให้เหมาะกับเอกสารของคุณ แล้วคุณจะมีระบบดึงข้อความที่แข็งแรงในเวลาอันรวดเร็ว ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}