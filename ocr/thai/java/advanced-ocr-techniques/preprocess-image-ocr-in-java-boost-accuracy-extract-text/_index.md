---
category: general
date: 2026-02-27
description: ทำการเตรียมภาพ OCR เพื่อดึงข้อความจากภาพโดยใช้ Aspose OCR ใน Java. เรียนรู้วิธีปรับปรุงความแม่นยำของ
  OCR และแปลงข้อความจากภาพสแกนอย่างมีประสิทธิภาพ.
draft: false
keywords:
- preprocess image OCR
- extract text from image
- improve OCR accuracy
- java OCR example
- convert scanned image text
language: th
og_description: ทำการประมวลผลล่วงหน้าภาพ OCR เพื่อดึงข้อความจากภาพด้วย Aspose OCR
  คู่มือนี้แสดงวิธีปรับปรุงความแม่นยำของ OCR และแปลงข้อความจากภาพสแกนใน Java.
og_title: การเตรียมภาพ OCR ใน Java – เพิ่มความแม่นยำและดึงข้อความ
tags:
- OCR
- Java
- Image Processing
title: การเตรียมภาพสำหรับ OCR ใน Java – เพิ่มความแม่นยำและดึงข้อความ
url: /th/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพ OCR – คู่มือ Java ฉบับสมบูรณ์

เคยเจอปัญหาในการ **preprocess image OCR** ทำให้ข้อความที่ดึงออกมาดูไม่สมบูรณ์หรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการ การสแกนดิบมักเต็มไปด้วยการเอียง จุดรบกวน หรือคอนทราสต์ต่ำ ซึ่งความบกพร่องเล็ก ๆ เหล่านี้สามารถทำลายกระบวนการสกัดข้อความทั้งหมดได้

ข่าวดีคือ? ด้วยการทำขั้นตอนการเตรียมล่วงหน้าไม่กี่ขั้นตอน—deskew, denoise, และ binarization—คุณสามารถปรับปรุงผลลัพธ์ของ OCR ได้อย่างมหาศาล ในบทเรียนนี้เราจะเดินผ่าน **java OCR example** ที่แสดงอย่างชัดเจนว่า **extract text from image** อย่างไร เพิ่มความแม่นยำ และสุดท้าย **convert scanned image text** ให้เป็นสตริงที่สะอาดและค้นหาได้

> **สิ่งที่คุณจะได้:** โปรแกรม Java พร้อมรันโดยใช้ Aspose OCR คำอธิบายว่าทำไมแต่ละการตั้งค่าถึงสำคัญ และเคล็ดลับการจัดการกรณีขอบเช่นหน้าที่หมุนมากหรือสแกนความละเอียดต่ำ

---

## สิ่งที่คุณต้องเตรียม

- **Java Development Kit (JDK) 8** หรือใหม่กว่า  
- ไลบรารี **Aspose.OCR for Java** (เวอร์ชันล่าสุด ณ เวลาที่เขียน, 23.10)  
- ไฟล์ตัวอย่าง TIFF/PNG/JPEG ที่คุณต้องการอ่าน—ตั้งชื่อว่า `input.tif`  
- IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, VS Code… ใดก็ได้)

ไม่ต้องมีการพึ่งพา native dependencies หรือเครื่องมือภายนอกเพิ่มเติม; เอนจิน Aspose OCR จะทำงานหนักทั้งหมดให้คุณ

---

## Preprocess Image OCR – ตั้งค่า Engine

ก่อนอื่นเราจะสร้างอินสแตนซ์ `OcrEngine` วัตถุนี้เก็บการกำหนดค่าที่จะขับเคลื่อนการเตรียมล่วงหน้าทั้งหมด

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the configuration follows...
```

**ทำไมจึงสำคัญ:** Engine คือประตูสู่ทุกฟีเจอร์—ถ้าข้ามขั้นตอนนี้ การตั้งค่าต่อ ๆ ไปจะไม่มีผลเลย คิดว่าเป็นการเปิดกล่องเครื่องมือก่อนเริ่มใช้ค้อน

---

## เปิดใช้งาน Deskew เพื่อแก้ไขการหมุน

หน้าที่สแกนมักไม่ตรงแนวอย่างสมบูรณ์ การเอียงเล็กน้อยทำให้ตัวอักษรอ่านผิดได้ การเปิด deskew จะบอก engine ให้ตรวจจับอัตโนมัติและหมุนภาพกลับไปที่ 0°

```java
        // Step 2: Turn on automatic deskew
        ocrEngine.getConfig().setDeskewEnabled(true);
```

*เคล็ดลับ:* Deskew ทำงานดีที่สุดกับภาพที่เส้นข้อความชัดเจน หากคุณกำลังจัดการกับโน้ตมือเขียน คุณอาจต้องทดลองใช้เมธอด `setDeskewAngleTolerance` (ไม่ได้แสดงที่นี่) เพื่อปรับความอ่อนไหวให้เหมาะสม

---

## ใช้ Denoising เพื่อลบสัญญาณรบกวน

สัญญาณรบกวน—จุดสุ่มหรือเม็ดฝุ่นพื้นหลัง—ทำให้ขั้นตอน OCR สับสน การเปิด denoising จะทำให้ภาพเรียบขึ้น เก็บเส้นสเก็ตช์ไว้แต่กำจัดพิกเซลที่ไม่เกี่ยวข้อง

```java
        // Step 3: Enable denoising to clean up speckles
        ocrEngine.getConfig().setDenoiseEnabled(true);
```

**กรณีขอบ:** สำหรับสแกนความละเอียดต่ำมาก (ต่ำกว่า 150 dpi) การ denoise อย่างรุนแรงอาจลบตัวอักษรอ่อน ๆ ไปได้ ในกรณีนี้คุณอาจลดระดับ `setDenoiseLevel` (ค่าเริ่มต้นคือ medium) หรือข้ามขั้นตอนนี้เลย

---

## ปรับค่า Binarization Threshold เพื่อคอนทราสต์ที่ดีกว่า

Binarization แปลงภาพระดับสีเทาเป็นสีขาว‑ดำ ทำให้คอนทราสต์ระหว่างหมึกกับกระดาษคมชัด ค่าธรณี (0‑255) กำหนดจุดตัด ค่า 180 ทำงานได้ดีสำหรับสแกนที่สะอาดส่วนใหญ่ แต่คุณอาจต้องปรับให้เหมาะ

```java
        // Step 4: Set a custom binarization threshold
        ocrEngine.getConfig().setBinarizationThreshold(180);
```

*ทำไมถึงเป็น 180?* ค่าดังกล่าวสูงพอที่จะทำให้ข้อความสีเข้มเป็นสีดำและพื้นหลังอ่อนเป็นสีขาว ช่วยให้ engine โฟกัสที่อักขระจริง หากแหล่งข้อมูลของคุณเป็นเอกสารเก่าที่ซีดเซียว ลองค่าต่ำกว่าเช่น 120

---

## ประมวลผลภาพและสกัดข้อความ

เมื่อ engine พร้อมแล้ว เราจะส่งพาธไฟล์เข้าไป เมธอด `processImage` จะคืนค่าอ็อบเจกต์ `OcrResult` ที่บรรจุข้อความที่รับรู้และคะแนนความเชื่อมั่น

```java
        // Step 5: Process the image file
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/input.tif");
```

**ถ้าไฟล์ไม่พบจะเกิดอะไร?** เมธอดจะโยน `IOException` ในโค้ดจริงคุณควรห่อการเรียกนี้ใน try‑catch และบันทึกข้อความข้อผิดพลาดที่เป็นมิตร

---

## ตรวจสอบผลลัพธ์

สุดท้ายเราจะพิมพ์สตริงที่สกัดออกมาที่คอนโซล นี่คือจุดที่คุณจะเห็นว่าการเตรียมล่วงหน้าช่วยได้จริงหรือไม่

```java
        // Step 6: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult.getText());
    }
}
```

ผลลัพธ์ที่คาดหวัง (ตัดย่อเพื่อความกระชับ):

```
=== OCR Result ===
The quick brown fox jumps over the lazy dog.
```

หากผลยังมีอักขระขยะ ให้กลับไปตรวจสอบค่า threshold หรือพิจารณาใช้ฟิลเตอร์กำหนดเอง (เช่น morphological opening) ก่อนส่งภาพให้ Aspose OCR

---

## วิธีสกัดข้อความจากภาพด้วย Aspose OCR

โค้ดข้างต้นเป็น **java OCR example** ที่สาธิตกระบวนการทั้งหมด—from การโหลดภาพจนถึงการพิมพ์ข้อความที่สะอาด เพราะการเตรียมล่วงหน้าทั้งหมดจัดการผ่านอ็อบเจกต์ `Config` คุณจึงสามารถสลับขั้นตอนใดขั้นตอนหนึ่งได้โดยไม่ต้องเขียนโลจิกหลักใหม่

**เช็คลิสต์สั้นสำหรับการสกัด:**

1. **Load** ภาพด้วย `processImage`  
2. **Enable** `Deskew` และ `Denoise` หากแหล่งเป็นเอกสารสแกน  
3. **Tune** `BinarizationThreshold` ตามการตรวจสอบด้วยตาเปล่า  
4. **Read** `ocrResult.getText()` แล้วเก็บไว้ที่ที่ต้องการ—ฐานข้อมูล, ไฟล์, หรือ UI

---

## เคล็ดลับเพิ่มความแม่นยำของ OCR ใน Java

- **Resolution matters:** ควรสแกนที่ความละเอียดอย่างน้อย 300 dpi ความละเอียดสูงให้ข้อมูลพิกเซลมากขึ้นสำหรับ engine  
- **Color vs. grayscale:** แปลงสแกนสีเป็น grayscale ก่อนประมวลผล; ลดเวลาการประมวลผลโดยไม่กระทบความแม่นยำ  
- **Batch processing:** หากมีหลายสิบไฟล์ ให้ใช้ `OcrEngine` ตัวเดียวซ้ำหลายครั้ง—การสร้างใหม่บ่อย ๆ เพิ่มภาระงาน  
- **Language packs:** Aspose OCR รองรับหลายภาษา; ตั้งค่า `ocrEngine.getConfig().setLanguage(OcrLanguage.English)` (หรือภาษาอื่น) เพื่อเพิ่มการรับรู้สำหรับข้อความที่ไม่ใช่ภาษาอังกฤษ

---

## แปลงข้อความสแกนเป็นสตริงที่แก้ไขได้

เมื่อคุณได้สตริงดิบแล้ว คุณอาจต้องทำความสะอาดต่อ—ลบการขึ้นบรรทัดใหม่, ปรับ whitespace, หรือใช้ spell‑checking Java มีเมธอด `String` และไลบรารีอย่าง Apache Commons Text ที่ทำให้งานนี้ง่ายดาย

```java
String cleaned = ocrResult.getText()
                          .replaceAll("\\s+", " ")
                          .trim();
System.out.println("Cleaned text: " + cleaned);
```

ตอนนี้ข้อความพร้อมบันทึกเป็นไฟล์ `.txt`, แทรกเข้า PDF, หรือส่งต่อไปยัง pipeline NLP ต่อไป

---

![ตัวอย่างการเตรียมภาพ OCR](/images/preprocess-ocr-demo.png "ตัวอย่างการเตรียมภาพ OCR แสดงผลลัพธ์บนคอนโซล")

*ภาพหน้าจอด้านบนแสดงผลลัพธ์บนคอนโซลหลังจากรันโปรแกรม Java ฉบับเต็ม*

---

## สรุป

คุณเพิ่งเรียนรู้วิธี **preprocess image OCR** ด้วย Java โดยเปิดใช้งาน deskew, denoise, และ binarization เพื่อ **extract text from image** อย่างมีความน่าเชื่อถือมากขึ้น ด้วยการปรับค่า configuration เพียงไม่กี่ตัว คุณสามารถ **improve OCR accuracy**, จัดการสแกนที่ยากลำบาก, และสุดท้าย **convert scanned image text** ให้เป็นสตริงที่สะอาดและค้นหาได้—all within a compact, self‑contained **java OCR example**.

พร้อมก้าวต่อไปหรือยัง? ลองนำข้อความที่สกัดไปเก็บในฐานข้อมูล, สร้าง PDF ที่ค้นหาได้ด้วย Aspose PDF, หรือทดลองรองรับหลายภาษาเดียวกัน กระบวนการเตรียมล่วงหน้านี้ทำงานได้กับ PDF, PNG, และ JPEG จึงสามารถขยายใช้ได้กับโครงการดิจิไทเซชันเอกสารใด ๆ

ขอให้เขียนโค้ดสนุกและผลลัพธ์ OCR ของคุณใสสะอาดเหมือนคริสตัล!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}