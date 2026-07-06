---
category: general
date: 2026-02-19
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพและกำจัดสัญญาณรบกวนสำหรับ OCR บทแนะนำนี้แสดงวิธีการจดจำข้อความในภาพ,
  แก้ไขการหมุนของภาพ, และทำการเตรียมภาพสำหรับ OCR ด้วย Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: th
og_description: วิธีแก้ไขการเอียงของภาพและทำความสะอาดสัญญาณรบกวนเพื่อให้คุณสามารถจดจำข้อความในภาพได้อย่างรวดเร็ว
  ปฏิบัติตามคำแนะนำนี้เพื่อแก้ไขการหมุนของภาพและเตรียมการประมวลผล OCR ของภาพด้วย Aspose.
og_title: วิธีแก้ไขการเอียงของภาพ – คู่มือการเตรียม OCR อย่างครบถ้วน
tags:
- OCR
- Java
- Image Processing
title: วิธีแก้ไขการเอียงของภาพ — คู่มือการเตรียม OCR ขั้นตอนโดยละเอียด
url: /th/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

< blocks/products/products-backtop-button >}}

All good.

Now produce final content with translations.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ — การสอนการเตรียมการ OCR อย่างสมบูรณ์

เคยสงสัยไหมว่า **how to deskew image** ไฟล์ก่อนนำเข้าเครื่อง OCR? บางทีคุณอาจสแกนชุดใบเสร็จและหน้ากระดาษดูเหมือนจะเอียงเล็กน้อย หรือสแกนมีจุดสีสุ่ม นั่นเป็นปัญหาที่พบบ่อย—ภาพที่เอียงและมีเสียงรบกวนทำให้การจดจำข้อความล้มเหลว.  

ข่าวดีคืออะไร? คุณสามารถทำให้ภาพตรง (correct image rotation) และลดสัญญาณรบกวน (how to remove noise) ได้ด้วยเพียงไม่กี่บรรทัดของ Java โดยใช้ Aspose.OCR. ในคู่มือนี้เราจะอธิบายขั้นตอนทั้งหมด: ตั้งแต่การโหลด PNG ที่มีเสียงรบกวนและเอียง, การใช้ deskew + median denoise, จนถึง **recognize text image** และพิมพ์ผลลัพธ์. เมื่อจบคุณจะมีโค้ดสั้นที่สามารถนำไปใช้ในโปรเจค Java ใดก็ได้.

## สิ่งที่คุณต้องการ

- **Java 17** หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับเวอร์ชันเก่าได้ แต่ 17 เป็นจุดที่เหมาะที่สุด).  
- **Aspose.OCR for Java** – คุณสามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central (`com.aspose:aspose-ocr`).  
- ไฟล์รูปภาพที่ทั้งเอียงและมีสัญญาณรบกวน (เช่น `noisy-rotated.png`).  
- IDE ที่ไม่ซับซ้อน (IntelliJ, Eclipse หรือแม้แต่ VS Code).  

ไม่จำเป็นต้องใช้เครื่องมือสร้างที่ซับซ้อน; การรัน `javac` + `java` อย่างง่ายก็ทำงานได้ดี.

---

## ขั้นตอนที่ 1 – สร้างอินสแตนซ์ของ OCR Engine  

สิ่งแรกที่คุณทำคือสร้าง `OcrEngine`. คิดว่าเป็นสมองที่จะอ่านอักขระให้คุณในภายหลัง.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **เคล็ดลับ:** เก็บ engine เป็น singleton หากคุณประมวลผลหลายภาพ; มันจะใช้บัฟเฟอร์ภายในซ้ำและทำให้เร็วขึ้น.

## ขั้นตอนที่ 2 – เปิดใช้งาน Deskew และ Median Denoise (How to Remove Noise)

ตอนนี้เราบอก engine ให้ **correct image rotation** และ **how to remove noise**. ทั้งสองฟิลเตอร์เป็นทางเลือก, แต่เมื่อใช้ร่วมกันจะเพิ่มความแม่นยำอย่างมาก.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

ทำไมต้องใช้ median denoise? มันรักษาขอบ (เส้นที่กำหนดอักขระ) ในขณะที่ลบพิกเซลที่โดดเดี่ยว—ตรงกับสิ่งที่คุณต้องการสำหรับ OCR ที่สะอาด.

## ขั้นตอนที่ 3 – โหลดภาพที่คุณต้องการประมวลผล  

ที่นี่เราชี้ engine ไปที่ไฟล์ที่ต้องทำความสะอาด. `ImageStream.fromFile` อ่าน PNG เข้าไปในหน่วยความจำ.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

หากภาพของคุณอยู่บนเซิร์ฟเวอร์ระยะไกล, เพียงส่ง `InputStream` แทน—Aspose จะจัดการอย่างราบรื่น.

## ขั้นตอนที่ 4 – รัน OCR และจับข้อความที่จดจำได้  

เมื่อเปิดใช้งานการเตรียมข้อมูลล่วงหน้า, engine จะอ่านภาพที่แก้ไขแล้ว. การเรียก `recognize()` จะคืนค่า `RecognitionResult` ที่มีสตริงที่สกัดออกมา.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

คุณควรเห็นข้อความที่สะอาดและอ่านง่ายในคอนโซล, แม้ว่าภาพต้นฉบับจะเอียงและมีเม็ดสี.

## ขั้นตอนที่ 5 – ตรวจสอบผลลัพธ์ (What to Expect)

เมื่อทุกอย่างทำงาน, คอนโซลจะแสดงผลบางอย่างเช่น:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

หากผลลัพธ์ยังมีอักขระผิดรูป, ให้ตรวจสอบสองครั้ง:

- ความละเอียดของภาพ (≥ 300 dpi เป็นที่เหมาะสม).  
- ว่าเส้นทางไฟล์ถูกต้องหรือไม่.  
- ว่าฟิลเตอร์เพิ่มเติม (เช่น `setContrastStretch`) อาจช่วยได้หรือไม่.

---

## ตัวเลือก: การยืนยันด้วยภาพตัวอย่าง  

ด้านล่างเป็นตัวอย่างขนาดเล็กของใบเสร็จที่เอียงและมีสัญญาณรบกวน. สังเกตการเอียง—โค้ดของเราจะทำให้ตรงสำหรับคุณ.

![ตัวอย่างการแก้ไขการเอียงของภาพ](deskew-demo.png "การแก้ไขการเอียงของภาพ")

*ข้อความแทนภาพ: การแก้ไขการเอียงของภาพ – ก่อนและหลังการประมวลผล.*

## คำถามที่พบบ่อย

### ทำงานกับ PDF หรือเฉพาะ PNG/JPEG เท่านั้น?  

Aspose.OCR สามารถอ่าน PDF ได้โดยตรง; เพียงเปลี่ยน `ImageStream.fromFile` เป็น `ImageStream.fromPdf`. ธงการเตรียมข้อมูลล่วงเดิมยังคงใช้ได้, ดังนั้นคุณยังคงได้ **how to deskew image** และ **how to remove noise**.

### ถ้าฉันต้องการเก็บการวางแนวเดิมไว้สำหรับขั้นตอนต่อไป?  

คุณสามารถคลอนภาพก่อนการเตรียมข้อมูลล่วงหน้า:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### ฉันสามารถเปลี่ยนมุม deskew ด้วยตนเองได้หรือไม่?  

ใช่—`setDeskewAngle(double degrees)` ให้คุณแทนที่อัลกอริทึมการตรวจจับอัตโนมัติ. มีประโยชน์เมื่อการตรวจจับอัตโนมัติล้มเหลวกับการเอียงที่รุนแรง.

### median denoise แตกต่างจาก Gaussian blur อย่างไร?  

ฟิลเตอร์ median แทนที่พิกเซลแต่ละตัวด้วยค่ามัธยฐานของเพื่อนบ้าน, ซึ่งรักษาขอบ. Gaussian blur ทำให้ทุกอย่างเรียบ, อาจทำให้เส้นอักขระเบลอ—ดังนั้น median จึงเป็นตัวเลือกที่ปลอดภัยกว่าสำหรับ OCR.

## สรุป  

ในบทเรียนนี้เราได้ครอบคลุมไฟล์ **how to deskew image**, แสดง **how to remove noise**, และสาธิตวิธี **recognize text image** ด้วยการเตรียมข้อมูลล่วงหน้าที่มาพร้อมกับ Aspose OCR. โดยการเปิด `setDeskew(true)` และ `setMedianDenoise(true)`, คุณจะทำให้ **correct image rotation** และทำความสะอาดจุดรบกวนโดยอัตโนมัติ, เปลี่ยนการสแกนที่ยุ่งเหยิงให้เป็นสตริงข้อความที่สะอาด.  

ลองทดลองได้ตามสบาย: ลองใช้กลยุทธ์การลดสัญญาณรบกวนต่าง ๆ, ป้อน PDF, หรือเชื่อมต่อหลายภาพในลูป. รูปแบบเดียวกัน—engine → preprocess → recognize—ใช้ได้กับทุกสถานการณ์, ทำให้เป็นพื้นฐานที่มั่นคงสำหรับ pipeline OCR ใด ๆ.  

**ขั้นตอนต่อไป** ที่คุณอาจสำรวจ:

- **การประมวลผลเป็นชุด** – วนลูปผ่านโฟลเดอร์ของภาพและเขียนผลลัพธ์แต่ละไฟล์เป็นไฟล์ `.txt`.  
- **แพ็คเกจภาษา** – โหลดพจนานุกรมภาษาที่เฉพาะเจาะจงเพื่อเพิ่มความแม่นยำสำหรับข้อความที่ไม่ใช่ภาษาอังกฤษ.  
- **ฟิลเตอร์ขั้นสูง** – เช่น `setContrastStretch` หรือ `setBinarization` สำหรับการสแกนที่มีคอนทราสต์ต่ำ.  

มีคำถามเพิ่มเติม? แสดงความคิดเห็นได้, และขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}