---
category: general
date: 2026-04-26
description: วิธีปรับปรุงความแม่นยำของ OCR ด้วยการกำจัดสัญญาณรบกวน การแก้ไขการเอียงของภาพ
  และการแปลงภาพเป็นข้อความ เรียนรู้ขั้นตอนโดยละเอียดกับ Aspose OCR.
draft: false
keywords:
- how to improve ocr
- how to remove noise
- how to extract text
- how to deskew image
- convert image to text
language: th
og_description: วิธีเพิ่มความแม่นยำของ OCR ใน Java—ลบสัญญาณรบกวน, แก้ไขการเอียงของภาพ,
  และแปลงภาพเป็นข้อความโดยใช้ Aspose OCR.
og_title: วิธีปรับปรุง OCR ด้วยการประมวลผลล่วงหน้าขั้นสูงใน Java
tags:
- OCR
- Java
- Image Processing
title: วิธีปรับปรุง OCR ด้วยการประมวลผลล่วงหน้าขั้นสูงใน Java
url: /th/java/advanced-ocr-techniques/how-to-improve-ocr-with-advanced-preprocessing-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีปรับปรุง OCR ด้วยการประมวลผลล่วงหน้าขั้นสูงใน Java

เคยสงสัยไหมว่า **วิธีปรับปรุง OCR** อย่างไรเมื่อสแกนของคุณดูเป็นกองกาก? บางทีเอกสารอาจถูกหมุน, มีจุดรบกวนแบบเม็ดเม็ด, หรือความคมชัดต่ำเกินกว่าจะอ่านได้ ข่าวดีคือขั้นตอนการประมวลผลล่วงหน้าจำนวนไม่มากสามารถเปลี่ยนภาพที่ไม่คมชัดให้กลายเป็นข้อความที่เครื่องอ่านได้อย่างสะอาด—ไม่ต้องใช้เวทมนตร์ใดๆ

ในบทแนะนำนี้เราจะพาคุณผ่าน **วิธีการลบสัญญาณรบกวน**, **วิธีการแก้ไขการเอียงของภาพ** และสุดท้าย **วิธีการดึงข้อความ** (หรือ *แปลงภาพเป็นข้อความ*) ด้วย Aspose OCR สำหรับ Java. เมื่อเสร็จคุณจะมีโปรแกรมที่พร้อมรันซึ่งให้ความแม่นยำของ OCR ที่ดีกว่าอย่างเห็นได้ชัด

## สิ่งที่คุณต้องเตรียม

- **Java Development Kit (JDK) 11+** – เวอร์ชันล่าสุดใดก็ได้ทำงานได้
- **Aspose.OCR for Java** library (รุ่นทดลองฟรีใช้สำหรับการทดสอบได้)
- ภาพตัวอย่างที่เอียง, มีสัญญาณรบกวน, หรือความคมชัดต่ำ (เช่น `skewed_noisy.jpg`)
- IDE หรือโปรแกรมแก้ไขข้อความง่ายๆ; เราจะใช้โค้ดแบบพื้นฐาน

> **เคล็ดลับพิเศษ:** หากคุณใช้ Maven ให้เพิ่ม dependency ของ Aspose OCR ลงใน `pom.xml` ของคุณ หากคุณชอบ Gradle ให้ใช้พารามิเตอร์เดียวกัน

## ขั้นตอนที่ 1: ตั้งค่า Aspose OCR Engine – *พื้นฐานของการปรับปรุง OCR*

ขั้นแรก ให้สร้างอินสแตนซ์ของ `OcrEngine`. วัตถุนี้เป็นจุดเริ่มต้นสำหรับการทำ OCR ทุกครั้ง

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*ทำไมเรื่องนี้ถึงสำคัญ:* Engine จะเก็บการตั้งค่าทั้งหมดที่กำหนดว่า Aspose จะตีความภาพอย่างไร หากไม่มีมัน คุณจะไม่สามารถเปิดใช้เทคนิคการประมวลผลล่วงหน้าที่จริงๆ แล้ว **วิธีปรับปรุง OCR** ได้

## ขั้นตอนที่ 2: เปิดใช้งานการประมวลผลภาพขั้นสูง – แกนหลักของ *การปรับปรุง OCR*

ตอนนี้เราจะเปิดสวิตช์การประมวลผลล่วงหน้าสี่ตัวที่ตอบคำถาม **วิธีปรับปรุง OCR** โดยตรง: deskew, denoise, contrast stretch, และ binarize.

```java
        // Step 2: Turn on preprocessing features
        ImagePreprocessingSettings preprocessing = ocrEngine.getPreprocessingSettings();
        preprocessing.setDeskew(true);           // how to deskew image
        preprocessing.setDenoise(true);         // how to remove noise
        preprocessing.setContrastStretch(true); // boost contrast automatically
        preprocessing.setBinarize(true);        // Otsu binarization for clean black‑white
```

*คำอธิบาย:*  
- **Deskew** จะหมุนภาพอัตโนมัติกลับไปที่ 0° เพื่อให้ตัวอักษรเรียงแนวนอน  
- **Denoise** ใช้ฟิลเตอร์ที่ทำให้จุดเม็ดเล็กๆ นุ่มลง—ตรงกับสิ่งที่คุณต้องการเมื่อถาม *วิธีการลบสัญญาณรบกวน*  
- **Contrast stretch** ขยายช่วงโทนสี ทำให้ตัวอักษรที่จางขึ้นเด่นชัดขึ้น  
- **Binarize** บังคับให้พิกเซลทั้งหมดเป็นสีดำหรือสีขาว เป็นเงื่อนไขพื้นฐานของ OCR

## ขั้นตอนที่ 3: โหลดภาพที่มีปัญหา – เตรียมพร้อมสำหรับ *การดึงข้อความ*

```java
        // Step 3: Point the engine at your source image
        ocrEngine.setImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางจริงบนเครื่องของคุณ. ภาพสามารถอยู่ในรูปแบบ JPEG, PNG, BMP หรือ TIFF—Aspose OCR รองรับทั้งหมด

## ขั้นตอนที่ 4: รัน OCR และ *แปลงภาพเป็นข้อความ*

```java
        // Step 4: Perform OCR and capture the result
        String recognizedText = ocrEngine.recognize().getText();
```

ในขั้นตอนนี้ engine ได้ทำการประมวลผลล่วงหน้าตามขั้นตอนแล้วจึงทำการจดจำอักขระ. การเรียก `recognize()` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult`; การเรียก `getText()` จะดึงสตริงข้อความธรรมดา—*วิธีแปลงภาพเป็นข้อความ* ใน Java อย่างตรงไปตรงมา

## ขั้นตอนที่ 5: แสดงผลลัพธ์ที่ทำความสะอาดแล้ว – ตรวจสอบ *การดึงข้อความ*

```java
        // Step 5: Show the OCR output
        System.out.println("Result after advanced preprocessing:\n" + recognizedText);
    }
}
```

เมื่อคุณรันโปรแกรม คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Result after advanced preprocessing:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

หากภาพต้นฉบับเป็นสแกนที่เบลอและหมุน, ให้สังเกตว่าข้อความที่ได้ตอนนี้อ่านได้และเรียงลำดับถูกต้อง นั่นคือประโยชน์ที่จับต้องได้จากการทำตามรายการตรวจสอบ **วิธีปรับปรุง OCR**

---

## วิธีการลบสัญญาณรบกวน – การเจาะลึก

สัญญาณรบกวนมักปรากฏเป็นจุดเม็ดสุ่มหรือเม็ดเม็ดโดยเฉพาะในสแกนความละเอียดต่ำ. ธง `setDenoise(true)` จะเปิดใช้ฟิลเตอร์มัธยฐานที่แทนที่พิกเซลแต่ละตัวด้วยค่ามัธยฐานของพิกเซลใกล้เคียง. ในการใช้งานจริง สิ่งนี้ทำให้จุดสีดำแยกเดี่ยวนุ่มลงในขณะที่คงขอบไว้

**เมื่อควรปรับ:** หากภาพต้นทางของคุณสะอาดอยู่แล้ว คุณสามารถปิด denoise เพื่อเร่งการประมวลผลได้. ในทางกลับกัน หากภาพมีเม็ดเม็ดมาก คุณอาจผสาน denoise ของ Aspose กับฟิลเตอร์ก่อนหน้าแบบ OpenCV ที่กำหนดเองเพื่อเพิ่มประสิทธิภาพ

## วิธีการแก้ไขการเอียงของภาพ – การหมุนกลับสู่ความเป็นจริง

อัลกอริทึม deskew วิเคราะห์เส้นฐานของข้อความและคำนวณมุมการหมุนที่เหมาะที่สุด. มันทำงานดีที่สุดเมื่อมีอย่างน้อยหนึ่งบรรทัดของข้อความที่มองเห็นชัดเจน. หากภาพมีเพียงกราฟิกเท่านั้น ให้พิจารณาหมุนภาพด้วยตนเองก่อนส่งให้ Aspose

**กรณีขอบ:** บางภาษา (เช่น Arabic) มีการจัดเรียงจากขวาไปซ้าย. Deskew ยังทำงานได้, แต่คุณอาจต้องตั้งค่าคำแนะนำภาษา (`ocrEngine.setLanguage(OcrLanguage.Arabic)`) เพื่อหลีกเลี่ยงการหมุนผิด

## วิธีการดึงข้อความ – นอกเหนือจากสตริงธรรมดา

หากคุณต้องการข้อมูลมากกว่าข้อความดิบ—เช่น กล่องขอบเขต, คะแนนความเชื่อมั่น, หรือการตำแหน่งระดับคำ—ให้ใช้ API `OcrResult` ที่เต็มรูปแบบ:

```java
OcrResult result = ocrEngine.recognize();
for (OcrWord word : result.getWords()) {
    System.out.printf("Word: %s, Confidence: %.2f%%, Box: %s%n",
        word.getText(), word.getConfidence() * 100, word.getRectangle());
}
```

โค้ดส่วนนี้แสดง **วิธีการดึงข้อความ** พร้อมเมตาดาต้า, มีประโยชน์สำหรับการสร้าง PDF ที่ค้นหาได้หรือการใส่คำอธิบายลงในเอกสาร

## แปลงภาพเป็นข้อความใน Java – รวมทุกอย่างเข้าด้วยกัน

ตัวอย่างเต็มที่สามารถรันได้รวมทุกสิ่งที่เราได้พูดถึงไว้:

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable preprocessing (how to improve OCR)
        ImagePreprocessingSettings preprocessing = ocrEngine.getPreprocessingSettings();
        preprocessing.setDeskew(true);           // how to deskew image
        preprocessing.setDenoise(true);         // how to remove noise
        preprocessing.setContrastStretch(true);
        preprocessing.setBinarize(true);

        // Load the image you want to convert image to text from
        ocrEngine.setImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Perform OCR
        String recognizedText = ocrEngine.recognize().getText();

        // Output the result
        System.out.println("Result after advanced preprocessing:\n" + recognizedText);
    }
}
```

บันทึกไฟล์นี้เป็น `PreprocessDemo.java`, คอมไพล์ด้วย `javac`, และรันด้วย `java`. คุณจะเห็นข้อความที่ทำความสะอาดแล้วแสดงบนคอนโซล

---

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| ผลลัพธ์เป็นค่าว่าง | เส้นทางภาพผิดหรือรูปแบบไม่รองรับ | ตรวจสอบเส้นทาง, ใช้เส้นทางเต็ม, ตรวจสอบว่าไฟล์เป็น JPEG/PNG/TIFF |
| อักขระแปลกประหลาด | การประมวลผลล่วงหน้าถูกปิดหรือไม่ได้ตั้งค่าภาษา | เปิดใช้งาน `setDeskew`, `setDenoise`, และตั้งค่า `ocrEngine.setLanguage(OcrLanguage.English)` |
| ประสิทธิภาพช้าเมื่อประมวลผลเป็นชุดใหญ่ | ใช้ขั้นตอนการประมวลผลล่วงหน้าทั้งสี่บนทุกภาพ | ปิด `setContrastStretch` หรือ `setBinarize` หากไม่จำเป็น, หรือประมวลผลภาพในเธรดแบบขนาน |

## ขั้นตอนต่อไป – ขยาย Pipeline OCR ของคุณ

เมื่อคุณรู้ **วิธีปรับปรุง OCR** แล้ว, พิจารณาแนวคิดต่อไปนี้:

- **การประมวลผลเป็นชุด:** วนลูปโฟลเดอร์ของภาพ, ใช้การตั้งค่าเดียวกันกับแต่ละไฟล์
- **การประมวลผลหลัง:** ใช้ regular expressions เพื่อล้างข้อผิดพลาด OCR ที่พบบ่อย (เช่น “0” กับ “O”)
- **การรวมกับ PDF:** ผสาน Aspose OCR กับ Aspose PDF เพื่อฝังข้อความที่ดึงออกมาโดยตรงลงใน PDF ที่ค้นหาได้
- **การสนับสนุนภาษา:** เปลี่ยนเป็น `ocrEngine.setLanguage(OcrLanguage.Spanish)` (หรือภาษาใดก็ได้ที่รองรับ) เพื่อจัดการเอกสารหลายภาษา

## สรุป

เราได้อธิบายคำตอบครบถ้วนสำหรับ **วิธีปรับปรุง OCR** ใน Java ด้วยการเปิดใช้ deskew, denoise, contrast stretch, และ binarization—ทั้งหมดใน `OcrEngine` ของ Aspose. ตอนนี้คุณรู้ **วิธีลบสัญญาณรบกวน**, **วิธีแก้ไขการเอียงของภาพ**, **วิธีดึงข้อความ**, และแม้กระทั่ง **แปลงภาพเป็นข้อความ** ในโปรแกรมเดียวที่กระชับ. ทดลองปรับการตั้งค่า, ทดสอบกับสแกนของคุณเอง, แล้วคุณจะเห็นการเพิ่มความแม่นยำของการจดจำอย่างชัดเจน

มีคำถามเพิ่มเติมเกี่ยวกับเทคนิค OCR หรืออยากได้ความช่วยเหลือในการผสานเข้ากับแอปพลิเคชันขนาดใหญ่? แสดงความคิดเห็นด้านล่าง, และขอให้สนุกกับการเขียนโค้ด!

![วิธีปรับปรุงการประมวลผลล่วงหน้า OCR](/images/ocr-preprocess-example.png "วิธีปรับปรุง OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}