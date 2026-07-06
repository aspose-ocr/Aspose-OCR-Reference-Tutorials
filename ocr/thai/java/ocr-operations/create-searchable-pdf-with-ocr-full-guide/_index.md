---
category: general
date: 2026-06-22
description: สร้าง PDF ที่ค้นหาได้โดยใช้ OCR ใน Java เรียนรู้วิธีปิดการบีบอัดและแปลง
  PDF รูปภาพสแกนให้เป็น PDF ที่ค้นหาได้อย่างรวดเร็ว.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: th
og_description: สร้าง PDF ที่ค้นหาได้ด้วย OCR ใน Java คู่มือนี้แสดงวิธีปิดการบีบอัด,
  แปลง PDF ที่เป็นภาพสแกน, และสร้าง PDF โดยไม่มีการบีบอัด.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย OCR – คู่มือ Java ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: สร้าง PDF ที่ค้นหาได้ด้วย OCR – คู่มือเต็ม
url: /th/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ด้วย OCR – คู่มือเต็ม

เคยต้องการ **สร้าง PDF ที่ค้นหาได้** จากชุดของภาพสแกนแต่ไม่แน่ใจว่าจะต้องปรับตั้งค่าอย่างไร? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่ก็เจอปัญหาเดียวกันเมื่อผลลัพธ์ออกมาเป็นไฟล์ขนาดใหญ่ที่อ่านไม่ได้  

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่สะอาดและครบวงจรซึ่งจะแสดงให้คุณเห็นอย่างชัดเจนว่า **สร้าง PDF ที่ค้นหาได้** อย่างไรโดยใช้ Java OCR engine, **แปลง PDF ภาพสแกน**, และที่สำคัญ **วิธีปิดการบีบอัด** เพื่อให้ไฟล์ที่ได้คงความเท่าเดิมกับมิติเดิมของต้นฉบับ เมื่อเสร็จคุณจะมีโค้ดสั้นที่พร้อมรันและเข้าใจอย่างลึกซึ้งว่าการตั้งค่าแต่ละอย่างมีความสำคัญอย่างไร

## สิ่งที่คุณจะได้เรียนรู้

* วิธีกำหนดค่า OCR engine ให้ **ocr to searchable pdf**.  
* เหตุผลที่ต้องปิดการบีบอัด PDF และวิธีให้ได้ **pdf without compression**.  
* โปรแกรม Java ฉบับเต็มที่รับภาพสแกน, รัน OCR, และบันทึกเป็น **searchable PDF**.  
* เคล็ดลับการจัดการกรณีขอบเช่นการสแกนหลายหน้า หรือแหล่งที่มาความละเอียดต่ำ.  

**Prerequisites** – ติดตั้ง Java 8+ แล้ว, มี OCR SDK ที่เข้ากันได้ (โค้ดใช้ ABBYY FineReader Engine API, แต่แนวคิดสามารถใช้กับไลบรารีใดก็ได้ที่มี `setOutputFormat` และ `setPdfCompression`). IDE อย่าง IntelliJ IDEA หรือ Eclipse จะทำให้ทำงานง่ายขึ้น, แต่ก็สามารถใช้โปรแกรมแก้ไขข้อความธรรมดาได้เช่นกัน.

---

![ขั้นตอนการสร้าง PDF ที่ค้นหาได้](image-placeholder.png "แผนภาพแสดงกระบวนการสร้าง PDF ที่ค้นหาได้จากภาพสแกนจนถึง PDF สุดท้าย")

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine ให้ **Create Searchable PDF**

สิ่งแรกที่คุณต้องบอก OCR engine คือรูปแบบผลลัพธ์ที่คุณต้องการ โดยค่าเริ่มต้นหลาย SDK จะส่งออกเป็นข้อความธรรมดาหรือ raster PDF ซึ่งไม่สามารถค้นหาได้ การเปลี่ยนรูปแบบจะทำงานหนักให้คุณ

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*ทำไมเรื่องนี้สำคัญ*: ธง `PDF_SEARCHABLE` บอก engine ให้ฝังชั้นข้อความที่มองไม่เห็นใต้ภาพสแกน เครื่องมือค้นหาจึงสามารถทำดัชนีเอกสารได้ ทำให้ทำงานเหมือน PDF ธรรมดาที่คุณเปิดใน Adobe Reader.

## ขั้นตอนที่ 2: ปิดการบีบอัด – **How to Disable Compression** อย่างถูกต้อง

หากคุณข้ามขั้นตอนนี้ engine จะบีบอัดแต่ละหน้าเพื่อประหยัดพื้นที่, แต่การบีบอัดอาจทำให้รายละเอียดละเอียดเบลอ—โดยเฉพาะอย่างยิ่งเมื่อคุณต้องการดึงภาพความละเอียดสูงในภายหลัง.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**เคล็ดลับ**: การปิดการบีบอัดเป็นสิ่งจำเป็นเมื่อคุณต้องการเก็บเอกสารทางกฎหมายหรือสแกนทางการแพทย์ที่ต้องการความละเอียดของพิกเซลทุกพิกเซล ไฟล์ที่ได้อาจใหญ่ขึ้น, แต่คุณจะคงมิติและความคมชัดของต้นฉบับไว้

## ขั้นตอนที่ 3: ทำ OCR และรับเอกสารผลลัพธ์

เมื่อ engine รู้ว่าจะส่งออกอะไรและจะจัดการกับภาพอย่างไร, คุณสามารถเรียกทำการจดจำได้ การเรียกนี้จะคืนค่าอ็อบเจ็กต์ `PdfDocument` ที่พร้อมบันทึกหรือทำการปรับแต่งต่อไป

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*เกิดอะไรขึ้นเบื้องหลัง?* engine ประมวลผลแต่ละหน้าที่รับเข้า, ทำการจดจำอักขระ, และผสานชั้นข้อความที่ซ่อนอยู่กับภาพ หากคุณมีหลายหน้า, จะถูกต่อเข้าด้วยกันโดยอัตโนมัติ

## ขั้นตอนที่ 4: บันทึก **Searchable PDF** ลงดิสก์

สุดท้าย, เขียน PDF ที่อยู่ในหน่วยความจำลงไฟล์ เลือกตำแหน่งที่คุณมีสิทธิ์เขียนและตั้งชื่อไฟล์ให้มีความหมาย

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

เมื่อคุณเปิด `searchable.pdf` ในโปรแกรมดูไฟล์, คุณจะสังเกตว่าสามารถเลือกและค้นหาข้อความได้—แม้ว่าภาพที่มองเห็นยังคงเป็นภาพสแกนต้นฉบับ

### ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นคลาส Java ที่ทำงานอิสระซึ่งรวมสี่ขั้นตอนเข้าด้วยกัน คุณสามารถคัดลอก‑วาง, ปรับเส้นทางอินพุต, และรันได้เลย

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** – หลังจากรันโปรแกรมคุณจะเห็นข้อความในคอนโซลด้านบน, และไฟล์ `searchable.pdf` จะปรากฏใน `YOUR_DIRECTORY`. การเปิดไฟล์ในโปรแกรมอ่าน PDF ใดก็จะทำให้คุณสามารถ:

* ไฮไลท์ข้อความ.
* ใช้การค้นหาในตัว (Ctrl + F) เพื่อหาคำ.
* ส่งออกชั้นข้อความที่ซ่อนอยู่หากต้องการ.

---

## ทำไมต้องปิดการบีบอัด? ทำความเข้าใจ **PDF Without Compression**

คุณอาจสงสัยว่า “การบีบอัดไม่ใช่เรื่องดีเสมอไปหรือ?” คำตอบมีความซับซ้อน:

| สถานการณ์ | คงการบีบอัด (`NORMAL`) | ปิดการบีบอัด (`NONE`) |
|-----------|-----------------------------|------------------------------|
| การเก็บรักษาสัญญากฎหมาย | ❌ อาจทำให้ความละเอียดพิกเซลเปลี่ยน | ✅ รับประกันลักษณะเดิมของต้นฉบับ |
| ชุดสแกนจำนวนมากที่ความละเอียดต่ำ | ✅ ประหยัดพื้นที่จัดเก็บ | ❌ เพิ่มขนาดโดยไม่มีประโยชน์ |
| ต้องการความแม่นยำของ OCR บนฟอนต์ขนาดเล็ก | ❌ ทำให้รายละเอียดละเอียดเบลอ | ✅ คงทุกเส้นของอักขระ |

โดยสรุป, **วิธีปิดการบีบอัด** คือการแลกเปลี่ยนระหว่างการจัดเก็บและความแม่นยำ สำหรับกระบวนการทำ PDF ที่ค้นหาได้ส่วนใหญ่ที่คุณต้องการค้นหาข้อความแทนการพิมพ์ภาพใหม่, การปิดการบีบอัดเป็นทางเลือกที่ปลอดภัยที่สุด

## การแปลง **Scanned Image PDF** โดยตรง

บางครั้งคุณอาจมี PDF ที่มีภาพสแกนอยู่แล้ว (PDF “เฉพาะภาพ”). เพื่อ **แปลง scanned image pdf** ให้เป็นเวอร์ชันที่ค้นหาได้, คุณสามารถส่ง PDF ทั้งไฟล์ให้ engine แทนการส่งภาพแยกแต่ละไฟล์:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

ธงการตั้งค่าเดียวกัน (`PDF_SEARCHABLE` และ `PdfCompression.NONE`) จะใช้เช่นกัน, ดังนั้นคุณจะได้ **pdf without compression** แม้เริ่มจาก PDF ที่เป็นคอนเทนเนอร์

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

* **ลืมตั้งค่ารูปแบบผลลัพธ์** – engine จะใช้ค่าเริ่มต้นเป็น raster PDF ซึ่งไม่สามารถค้นหาได้ ควรเรียก `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` ก่อน `recognizeToPdf()` เสมอ
* **หน่วยความจำไม่พอเมื่อประมวลผลชุดใหญ่** – โหลดและประมวลผลหน้าเป็นชิ้นส่วน, หรือใช้ streaming API หาก SDK ของคุณมีให้
* **เส้นทางไฟล์ไม่ถูกต้อง** – ใช้เส้นทางแบบ absolute หรือให้แน่ใจว่าไดเรกทอรีทำงานตั้งค่าอย่างถูกต้อง; มิฉะนั้น `pdf.save()` จะโยน `IOException`
* **ไลเซนส์ไม่ได้เปิดใช้งาน** – OCR SDK เชิงพาณิชย์ส่วนใหญ่ต้องการไลเซนส์ที่ถูกต้อง; engine จะโยนข้อยกเว้น runtime หากไม่มี

---

## สรุป

ตอนนี้คุณมีโซลูชันครบถ้วนพร้อมรันที่แสดง **วิธีสร้าง PDF ที่ค้นหาได้** จากภาพสแกน, วิธี **แปลง scanned image PDF**, และอย่างชัดเจน **วิธีปิดการบีบอัด** เพื่อสร้าง **pdf without compression**. ขั้นตอนสำคัญคือ:

1. ตั้งค่ารูปแบบผลลัพธ์เป็น `PDF_SEARCHABLE`.  
2. ปิดการบีบอัด PDF ด้วย `PdfCompression.NONE`.  
3. รัน OCR และบันทึก `PdfDocument`.  
4. บันทึกไฟล์ลงดิสก์.

จากนี้คุณสามารถทดลองกับฟอนต์, เพิ่มลายน้ำ, หรือประมวลผลเป็นชุดทั้งโฟลเดอร์ หากคุณสนใจการเพิ่มแพ็คภาษา OCR, การจัดการ TIFF หลายหน้า, หรือการรวมเวิร์กโฟลว์นี้เข้ากับเว็บเซอร์วิส, ตรวจสอบบทแนะนำที่กำลังจะมาของเราเกี่ยวกับ “การเลือกภาษา OCR ใน Java” และ “Streaming OCR สำหรับชุดเอกสารขนาดใหญ่”.

มีคำถามหรือเจอปัญหา? ฝากคอมเมนต์ด้านล่าง—ขอให้สนุกกับการเขียนโค้ด, และเพลิดเพลินกับ PDF ที่ค้นหาได้ใหม่ของคุณ!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจคของคุณ.

- [จดจำข้อความ PDF – การดำเนินการ OCR ด้วย Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/)
- [OCR จดจำเอกสาร PDF ใน Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [แปลงภาพเป็น PDF C# – บันทึกผลลัพธ์ OCR หลายหน้า](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}