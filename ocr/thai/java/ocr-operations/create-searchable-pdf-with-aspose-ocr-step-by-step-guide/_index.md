---
category: general
date: 2026-01-02
description: สร้าง PDF ที่ค้นหาได้จาก PDF รูปสแกนโดยใช้ Aspose OCR เรียนรู้การตั้งค่าภาษา
  OCR ฝังชั้นข้อความใน PDF และใช้ตัวเลือกการบีบอัดสูงสำหรับ PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: th
og_description: สร้าง PDF ที่ค้นหาได้อย่างรวดเร็ว คู่มือนี้แสดงวิธีแปลง PDF ที่สแกนเป็นภาพ,
  ฝังชั้นข้อความ, ตั้งค่าภาษา OCR และเปิดใช้งานการบีบอัด PDF สูง
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – คู่มือฉบับสมบูรณ์
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด
url: /th/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้องการ **สร้าง PDF ที่ค้นหาได้** จากภาพสแกนแต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในกระบวนการทำงานที่ต้องจัดการเอกสารจำนวนมาก PDF ที่เป็นเพียงภาพอย่างเดียวเป็นทางตันสำหรับการค้นหาและการทำดัชนี  

ข่าวดีคือด้วย Aspose OCR คุณสามารถ **แปลง PDF ภาพสแกน** ให้เป็นเอกสารที่ค้นหาได้เต็มรูปแบบได้ด้วยเพียงไม่กี่บรรทัดของ Java บทเรียนนี้จะพาคุณผ่านทุกขั้นตอน—การเริ่มต้นเครื่องมือ OCR, การกำหนดค่าการบีบอัด PDF ระดับสูง, การฝังชั้นข้อความที่ซ่อนอยู่, และแม้กระทั่งการเลือกภาษาของ OCR ที่เหมาะสม  

เมื่อจบคู่มือนี้ คุณจะมีโปรแกรมที่สามารถรันได้ซึ่งสร้าง PDF ที่ค้นหาได้ ไฟล์นี้คุณสามารถนำไปใส่ในเครื่องมือค้นหาใด ๆ หรือระบบจัดการเอกสารได้โดยไม่มีปัญหา  

---

## สร้าง PDF ที่ค้นหาได้ – ภาพรวม

ก่อนที่เราจะลงลึกในโค้ด มาทำความเข้าใจกันว่า “สร้าง PDF ที่ค้นหาได้” จริง ๆ หมายถึงอะไร PDF ที่ค้นหาได้ประกอบด้วยสองชั้นที่ทำงานพร้อมกัน:

1. **Visual layer** – ภาพสแกนต้นฉบับ (หรือหน้าที่เรนเดอร์)  
2. **Text layer** – ตัวอักษรที่มองไม่เห็นแต่เครื่องสามารถอ่านได้ซึ่งได้มาจาก OCR  

เมื่อคุณเปิด PDF แบบนี้ใน Adobe Reader แล้วเลือกข้อความ คุณกำลังโต้ตอบกับชั้นข้อความที่ซ่อนอยู่ ไม่ใช่ภาพ การใช้สองชั้นนี้ทำให้สามารถทำงาน **embed text layer PDF** ได้  

## แปลง PDF ภาพสแกนโดยใช้ Aspose OCR

สิ่งแรกที่คุณต้องการคือภาพสแกน (PNG, JPEG, TIFF) ที่ต้องการแปลงเป็น PDF Aspose OCR สามารถอ่านภาพนั้น, ทำ OCR, และส่งผลลัพธ์ให้กับตัวเขียน PDF  

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**ทำไมวิธีนี้ถึงได้ผล:**  
- `setCreateSearchablePdf(true)` บอก Aspose ให้สร้างชั้นข้อความที่ซ่อนอยู่ เพื่อตอบสนองความต้องการ **embed text layer pdf**  
- `setCompressionLevel(9)` ทำให้ไฟล์เข้าสู่ช่วง **high compression pdf** ลดขนาดสุดท้ายโดยไม่เสียความแม่นยำของ OCR  
- อาร์กิวเมนต์ `RecognitionLanguage.ENGLISH` แสดงวิธี **set OCR language**; คุณสามารถเปลี่ยนเป็นภาษาฝรั่งเศส, เยอรมัน ฯลฯ ตามวัสดุต้นฉบับของคุณ  

## การตั้งค่า PDF การบีบอัดระดับสูง

PDF สแกนขนาดใหญ่สามารถบวมเป็นหลายร้อยเมกะไบต์ได้อย่างรวดเร็ว Aspose มี API การบีบอัดที่ทำงานระดับ PDF เมธอด `setCompressionLevel` รับค่าตั้งแต่ 0 (ไม่มีการบีบอัด) ถึง 9 (บีบอัดสูงสุด)  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

เคล็ดลับบางประการ:  

- **ใช้รูปแบบภาพที่ไม่มีการสูญเสีย** (PNG) สำหรับสแกนที่มีข้อความหนาแน่น; JPEG เหมาะกับภาพถ่าย  
- **เปิดใช้งานการ subset ฟอนต์** หากคุณฝังฟอนต์แบบกำหนดเอง—Aspose ทำโดยอัตโนมัติเมื่อคุณสร้าง PDF ที่ค้นหาได้  
- **ทดสอบขนาดผลลัพธ์** หลังการเปลี่ยนแปลงแต่ละครั้ง; บางครั้งการบีบอัดระดับ 8 ให้การลดขนาด 10 % โดยคุณภาพสูญเสียเพียงเล็กน้อยเมื่อเทียบกับระดับ 9  

## ฝังชั้นข้อความ PDF เพื่อให้ค้นหาได้

หากคุณข้ามการเรียก `setCreateSearchablePdf(true)` ไฟล์ที่ได้จะดูดีแต่คุณจะไม่สามารถค้นหาข้อมูลภายในได้ ชั้นข้อความที่ซ่อนอยู่ถูกสร้างโดยการแมปแต่ละอักขระที่จดจำได้ไปยังตำแหน่งบนหน้า  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**สิ่งที่ควรระวัง:**  

- **เอกสารหลายภาษา** – คุณอาจต้องรัน OCR สองครั้ง, ครั้งละหนึ่งภาษา, แล้วรวมชั้นข้อความเข้าด้วยกัน  
- **เลย์เอาต์ซับซ้อน** (ตาราง, หลายคอลัมน์) – Aspose ทำได้ค่อนข้างดี, แต่ควรตรวจสอบผลลัพธ์ด้วยโปรแกรมดู PDF ที่แสดงข้อความซ่อนอยู่ (เช่นโหมด “Edit PDF” ของ Adobe Acrobat)  

## ตั้งค่าภาษา OCR เพื่อการจดจำที่แม่นยำ

ความแม่นยำของเครื่องมือ OCR พึ่งพาภาษาที่คุณระบุให้คาดหวัง Aspose มาพร้อมกับชุดภาษาที่ฝังมาในตัว, และคุณยังสามารถเพิ่มแพ็คภาษาที่กำหนดเองได้  

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**เมื่อใดที่ควรเปลี่ยนภาษา:**  

- เอกสารมี **สคริปต์ที่ไม่ใช่ละติน** (เช่น Cyrillic, Arabic) – สลับไปใช้ `RecognitionLanguage` ที่เหมาะสม  
- หน้าเอกสารหลายภาษา – คุณสามารถเรียก `recognizeImageAndSave` สองครั้ง, แต่ละครั้งใช้ภาษาต่างกัน, แล้วรวม PDF เหล่านั้นเข้าด้วยกัน  

## การรันตัวอย่างเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมรัน แทนที่เส้นทาง placeholder ด้วยตำแหน่งไฟล์จริง, ตรวจสอบให้แน่ใจว่า Aspose OCR JAR อยู่ใน classpath ของคุณ, แล้วดำเนินการ  

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เมื่อคุณรันโปรแกรม, คอนโซลจะแสดงผล:  

```
Searchable PDF created.
```

เปิด `searchable.pdf` ในโปรแกรมดู PDF ใด ๆ, ลองเลือกข้อความและคุณจะเห็นชั้นที่ซ่อนอยู่ทำงาน คุณได้ **สร้าง PDF ที่ค้นหาได้** จากภาพสแกนสำเร็จแล้ว  

![ตัวอย่างการสร้าง PDF ที่ค้นหาได้](image-placeholder.png "ตัวอย่างการสร้าง PDF ที่ค้นหาได้")

*ภาพหน้าจอด้านบน (placeholder) จะมักแสดงโปรแกรมดู PDF ที่สามารถเลือกข้อความเหนือหน้าสแกน*  

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **สร้าง PDF ที่ค้นหาได้** ด้วย Aspose OCR:  

- เริ่มต้นเครื่องมือ OCR  
- **แปลง PDF ภาพสแกน** โดยส่ง PNG/JPEG เข้า `recognizeImageAndSave`  
- ใช้ `setCreateSearchablePdf(true)` เพื่อ **embed text layer PDF**  
- ใช้ `setCompressionLevel(9)` สำหรับ **high compression PDF** ที่ยังคงเบา  
- เลือก `RecognitionLanguage` ที่เหมาะสมเพื่อ **set OCR language** ให้แม่นยำสูงสุด  

จากนี้คุณสามารถทดลองประมวลผลเป็นชุด, ใช้ภาษาต่าง ๆ, หรือแม้กระทั่งรวมหลายหน้าสแกนเป็น PDF ที่ค้นหาได้ไฟล์เดียว รูปแบบเดียวกันนี้ทำงานได้กับภาษาต่าง ๆ เช่น สเปนหรือญี่ปุ่น—เพียงสลับค่า enum `RecognitionLanguage`  

หากมีข้อสงสัยหรือเจอปัญหาใด ๆ อย่าลังเลที่จะคอมเมนต์ และขอให้สนุกกับการเขียนโค้ด!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}