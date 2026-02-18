---
category: general
date: 2026-02-17
description: 'บทเรียน Java แปลงภาพเป็นข้อความ: เรียนรู้วิธีดึงข้อความอูรดูจากภาพโดยใช้
  Aspose OCR ตัวอย่าง Java OCR ครบถ้วนรวมอยู่ด้วย'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: th
og_description: บทเรียน Java แปลงภาพเป็นข้อความแสดงวิธีการสกัดข้อความอูรดูจากภาพโดยใช้
  Aspose OCR. ทำตามตัวอย่าง Java OCR อย่างครบถ้วนขั้นตอนต่อขั้นตอน.
og_title: 'แปลงรูปเป็นข้อความใน Java: ดึงข้อความอูรดูด้วย Aspose OCR'
tags:
- OCR
- Java
- Aspose
title: 'แปลงภาพเป็นข้อความใน Java: ดึงข้อความอูรดูด้วย Aspose OCR'
url: /th/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: แยกข้อความ Urdu ด้วย Aspose OCR

หากคุณต้องการทำการแปลง **image to text java** สำหรับเอกสาร Urdu คุณมาถูกที่แล้ว. เคยสงสัยไหมว่า *วิธีการแยกข้อความ* จากรูปภาพของโน้ตมือหรือหน้าหนังสือพิมพ์ที่สแกน? คู่มือนี้จะพาคุณผ่าน **java ocr example** ที่ดึงอักขระ Urdu ออกมาจากภาพโดยใช้ Aspose OCR.

เราจะครอบคลุมทุกอย่างตั้งแต่การขอใบอนุญาตของไลบรารีจนถึงการพิมพ์ผลลัพธ์บนคอนโซล. เมื่อจบคุณจะสามารถ **load image ocr** ไฟล์, ตั้งค่าภาษาเป็น Urdu, และได้ผลลัพธ์ Unicode ที่สะอาด—ไม่ต้องใช้เครื่องมือเพิ่มเติม.  

## สิ่งที่คุณต้องการ

- **Java Development Kit (JDK) 8+** – โค้ดทำงานบน JDK เวอร์ชันล่าสุดใดก็ได้.
- **Aspose.OCR for Java** JAR (ดาวน์โหลดจากเว็บไซต์ Aspose).  
- ไฟล์ **Aspose OCR license** ที่ถูกต้อง (`Aspose.OCR.lic`).  
- ภาพที่มีข้อความ Urdu, ตัวอย่างเช่น `urdu-sample.png`.  

เมื่อมีพื้นฐานเหล่านี้แล้ว คุณสามารถกระโดดเข้าสู่โค้ดได้โดยตรงโดยไม่ต้องค้นหา dependencies ที่ขาดหาย.

## image to text java – ตั้งค่า Aspose OCR

ก่อนแรก เราต้องบอก Aspose ว่าเรามีใบอนุญาต หากไม่มีไลบรารีจะทำงานในโหมดประเมินผลและจะใส่ลายน้ำในผลลัพธ์.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การขอใบอนุญาตจะลบข้อจำกัดการประมวลผล 5 วินาทีและปลดล็อกแพ็คภาษา Urdu เต็มรูปแบบที่เพิ่มในไตรมาส 3 ปี 2025 หากคุณข้ามขั้นตอนนี้ OCR engine ยังทำงานได้ แต่คุณจะเห็นแท็ก “Evaluation” เล็ก ๆ ในผลลัพธ์.

## วิธีการแยกข้อความ – เริ่มต้น OCR Engine

ตอนนี้เราจะสร้าง engine และบอกอย่างชัดเจนว่าเราต้องการ Urdu ค่าคงที่ `OcrLanguage.URDU` จะเปิดใช้งานชุดอักขระและกฎการแบ่งส่วนที่เหมาะสม.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**เคล็ดลับ:** หากคุณต้องการประมวลผลหลายภาษาในหนึ่งรอบ คุณสามารถส่งรายการคั่นด้วยคอมม่า เช่น `OcrLanguage.ENGLISH, OcrLanguage.URDU`. Engine จะตรวจจับแต่ละพื้นที่โดยอัตโนมัติ.

## โหลด Image OCR – เตรียมข้อมูลเข้า

Aspose ทำงานกับอ็อบเจ็กต์ `OcrInput` ที่สามารถเก็บหนึ่งหรือหลายภาพ ที่นี่เราจะ **load image ocr** ข้อมูลจากไฟล์ในเครื่อง.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **หมายเหตุ:** แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มหรือพาธสัมพัทธ์จากโฟลเดอร์รากของโปรเจกต์ หากไฟล์ไม่พบ Aspose จะโยน `FileNotFoundException` การตรวจสอบอย่างรวดเร็วด้วย `new File(path).exists()` สามารถช่วยประหยัดเวลา debug ได้มาก.

## จดจำข้อความ – รันกระบวนการ OCR

เมื่อ engine ถูกตั้งค่าและภาพถูกโหลดแล้ว เราจะเรียก `recognize` สุดท้าย เมธอดนี้จะคืนค่า `OcrResult` ที่บรรจุสตริงที่แยกออกมา.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**อะไรที่เกิดขึ้นภายใน:** OCR engine จะแบ่งภาพเป็นบรรทัดแล้วเป็นอักขระ โดยใช้กฎการจัดรูปแบบเฉพาะ Urdu (เช่น การเชื่อมต่อรูปแบบ) นี่คือเหตุผลที่การตั้งค่าภาษาแต่แรกสำคัญ; หากไม่จะได้ตัวอักษร Latin ที่ผิดรูป.

## พิมพ์ข้อความ Urdu ที่จดจำได้

ขั้นตอนสุดท้ายคือการพิมพ์ผลลัพธ์ออกมา เนื่องจาก Urdu ใช้สคริปต์จากขวาไปซ้าย ตรวจสอบให้แน่ใจว่าคอนโซลของคุณรองรับ Unicode (เทอร์มินัลสมัยใหม่ส่วนใหญ่รองรับ).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

หากคุณเห็นเครื่องหมายคำถามหรือสตริงว่าง ให้ตรวจสอบอีกครั้งว่าการเข้ารหัสคอนโซลของคุณตั้งเป็น UTF‑8 (`chcp 65001` บน Windows, หรือรัน Java ด้วย `-Dfile.encoding=UTF-8`).

## ตัวอย่างทำงานเต็มรูปแบบ – ทุกขั้นตอนในที่เดียว

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางครบถ้วน ไม่ต้องอ้างอิงภายนอก มีเพียงไฟล์ Java เดียว.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

รันด้วย:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

แทนที่เวอร์ชัน JAR (`23.10`) ด้วยเวอร์ชันที่คุณดาวน์โหลด คอนโซลควรแสดงประโยค Urdu ที่แยกจาก PNG ของคุณ.

## ปัญหาที่พบบ่อย & กรณีขอบ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **ผลลัพธ์ว่าง** | ภาพมืดเกินไปหรือความละเอียดต่ำ. | ทำการประมวลผลล่วงหน้าภาพ (เพิ่มคอนทราสต์, ทำไบนารี) ด้วย `BufferedImage` ก่อนส่งให้ Aspose. |
| **อักขระเสีย** | ตั้งค่าภาษาไม่ถูกต้อง (ค่าเริ่มต้นคือ English). | ตรวจสอบว่าได้เรียก `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` ก่อน `recognize`. |
| **ไม่พบใบอนุญาต** | พาธพิมพ์ผิดหรือไฟล์หาย. | ใช้พาธเต็มหรือวางไฟล์ `.lic` ใน classpath แล้วเรียก `license.setLicense("Aspose.OCR.lic");`. |
| **หน่วยความจำเต็มเมื่อใช้ภาพขนาดใหญ่** | PNG ขนาดใหญ่ใช้หน่วยความจำ heap มาก. | เรียก `ocrEngine.setMaxImageSize(2000);` เพื่อลดขนาดภายใน, หรือปรับขนาดภาพด้วยตนเอง. |

## ขยายการสาธิต

- **การประมวลผลเป็นชุด:** วนลูปโฟลเดอร์, เพิ่มไฟล์แต่ละไฟล์ลงใน `OcrInput` เดียวกัน, แล้วเก็บผลลัพธ์ใน CSV.  
- **หลายภาษา:** แทนที่ `OcrLanguage.URDU` ด้วย `OcrLanguage.ARABIC` หรือรวมหลายภาษา.  
- **บันทึกลงไฟล์:** ใช้ `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));`.  

แนวคิดทั้งหมดนี้สร้างบน **java ocr example** ที่เราสร้างขึ้น ช่วยให้คุณปรับโซลูชันให้เหมาะกับโครงการจริง.

## สรุป

ตอนนี้คุณมีเวิร์กโฟลว์ **image to text java** ที่มั่นคงสำหรับแยกอักขระ Urdu จากภาพด้วย Aspose OCR คำแนะนำได้ครอบคลุมทุกขั้นตอน—from การขอใบอนุญาตและการเลือกภาษาไปจนถึงการโหลดภาพและการพิมพ์ผลลัพธ์—เพื่อให้คุณสามารถคัดลอกโค้ดไปใส่ในโปรเจกต์ Java ใดก็ได้และเห็นการทำงาน.  

ต่อไป ลองทดลองกับ PDF ที่ใหญ่ขึ้น, สคริปต์ต่าง ๆ, หรือแม้กระทั่งผสานขั้นตอน OCR เข้าไปใน Spring Boot REST endpoint. หลักการเดียวกัน—**how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}