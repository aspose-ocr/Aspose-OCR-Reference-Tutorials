---
category: general
date: 2026-06-28
description: สร้างไฟล์ PDF ที่ค้นหาได้จากไฟล์ TIFF หลายหน้าใน Java ด้วย Aspose OCR.
  เรียนรู้วิธีแปลง TIFF เป็น PDF และเพิ่มชั้นข้อความ OCR ลงใน PDF เพื่อให้ค้นหาได้ทันที.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- add ocr text layer pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพ TIFF ใน Java ด้วย Aspose OCR คู่มือนี้แสดงวิธีแปลง
  TIFF เป็น PDF และเพิ่มชั้นข้อความ OCR ลงใน PDF เพื่อให้เป็นเอกสารที่สามารถค้นหาได้
og_title: สร้าง PDF ที่ค้นหาได้จากไฟล์ TIFF ด้วย Aspose OCR (Java)
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  headline: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  type: TechArticle
- description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  name: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  steps:
  - name: What if my TIFF is single‑page?
    text: The same code works—Aspose treats a single‑page TIFF as a one‑element collection,
      so no extra handling is required.
  - name: Can I control the OCR language?
    text: 'Yes. Before calling `recognizeAndExportPdf`, set the language on the engine:'
  - name: How do I skip embedding the original image to reduce file size?
    text: Just set `pdfOptions.setEmbedOriginalImage(false)`. The PDF will contain
      only the searchable text layer, which dramatically shrinks the file but loses
      the visual representation.
  - name: Is the generated PDF truly searchable on all platforms?
    text: Modern PDF readers (Adobe Acrobat, Foxit, even browsers) honor the text
      layer. Some older, lightweight viewers might ignore it—test on your target platform
      if you’re unsure.
  type: HowTo
tags:
- Aspose OCR
- Java
- PDF Generation
title: สร้าง PDF ที่ค้นหาได้จากไฟล์ TIFF ด้วย Aspose OCR (Java) – คู่มือเต็ม
url: /th/java/ocr-operations/create-searchable-pdf-from-tiff-with-aspose-ocr-java-full-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้จาก TIFF ด้วย Aspose OCR (Java) – คู่มือเต็ม

เคยสงสัยไหมว่า จะ **create searchable PDF** จาก TIFF ที่สแกนโดยไม่ต้องใช้เวลาหลายชั่วโมงกับเครื่องมือของบุคคลที่สาม? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต้องการวิธีที่เชื่อถือได้ในการแปลงไฟล์ภาพขนาดใหญ่ให้เป็น PDF ที่คุณสามารถค้นหาได้จริง

ในบทแนะนำนี้ เราจะพาคุณผ่านโซลูชันที่เป็นขั้นตอนครบวงจร ที่ไม่เพียงแต่ **convert TIFF to PDF** แต่ยัง **add OCR text layer PDF** โดยอัตโนมัติ ทำให้คุณได้เอกสารที่สามารถค้นหาได้จริงในเพียงไม่กี่บรรทัดของ Java.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR สำหรับ Java และใช้ไลเซนส์ (ไม่บังคับแต่แนะนำ).  
- ขั้นตอนที่แน่นอนเพื่อ **convert TIFF to PDF** ด้วย `OcrEngine`.  
- วิธีกำหนดค่า `PdfExportOptions` เพื่อให้ไฟล์ที่สร้างมีชั้นข้อความที่มองไม่เห็นและสามารถค้นหาได้—ซึ่งคือความหมายของ **add OCR text layer PDF** ในการใช้งานจริง.  
- ผลลัพธ์ที่คาดหวังและการตรวจสอบอย่างรวดเร็วเพื่อให้แน่ใจว่าทุกอย่างทำงานถูกต้อง.  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน; เพียงสภาพแวดล้อมการพัฒนา Java พื้นฐาน (JDK 8+ และ IDE ใดก็ได้) ก็เพียงพอ.

---

## ขั้นตอนที่ 1: เตรียมโปรเจกต์ของคุณและใช้ไลเซนส์ Aspose OCR  

ก่อนที่คุณจะเรียกใช้ OCR API ใด ๆ คุณต้องมีไฟล์ JAR ของ Aspose OCR อยู่ใน classpath ของคุณ หากคุณมีไลเซนส์เชิงพาณิชย์ ให้วางไฟล์ `.lic` ไว้ที่ที่เข้าถึงได้และชี้คลาส `License` ไปที่ไฟล์นั้น ขั้นตอนนี้ไม่จำเป็นต้องทำอย่างเคร่งครัด—Aspose จะทำงานในโหมดประเมินผล แต่ไลเซนส์จะลบลายน้ำและเปิดใช้งานฟีเจอร์ทั้งหมด.

```java
// Apply your Aspose OCR license (optional for full features)
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **เคล็ดลับมืออาชีพ:** เก็บไฟล์ไลเซนส์ไว้ไกลจากระบบควบคุมเวอร์ชันของคุณเพื่อหลีกเลี่ยงการเปิดเผยโดยบังเอิญ.

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของ OCR Engine  

การสร้างอ็อบเจกต์ `OcrEngine` เป็นการก้าวแรกที่แท้จริงสู่การ **create searchable pdf**. Engine นี้เก็บการตั้งค่า OCR ทั้งหมดและจะใช้ในการแปลงต่อไป.

```java
// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

ทำไมต้องใช้ engine แยก? มันทำให้คุณสามารถใช้การตั้งค่าเดียวกันกับหลายไฟล์ได้ ซึ่งสะดวกเมื่อคุณประมวลผลหลายสิบไฟล์ TIFF เป็นชุด.

## ขั้นตอนที่ 3: โหลด Multi‑Page TIFF ของคุณ  

Aspose OCR ทำให้การโหลด TIFF หลายหน้าเป็นเรื่องง่าย เพียงเพิ่มเส้นทางไฟล์ลงในอ็อบเจกต์ `OcrInput`; ไลบรารีจะตรวจจับและจัดคิวทุกหน้าโดยอัตโนมัติ.

```java
// Load a multi‑page TIFF image as OCR input
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically
```

หากคุณต้องการ **convert TIFF to PDF** ทีละหน้า คุณก็สามารถเรียก `ocrInput.add(pageStream)` ภายในลูป—Aspose จะถือแต่ละการเรียกเป็นหน้าที่แยกกัน.

## ขั้นตอนที่ 4: กำหนดค่า PDF Export Options – การเพิ่มชั้นข้อความ OCR  

นี่คือจุดที่เวทมนตร์เกิดขึ้นสำหรับ **add OCR text layer pdf**. โดยการสลับแฟล็กสองสามตัว คุณบอกให้ Aspose ฝังบิตแมปต้นฉบับ (เพื่อรักษาความคมชัดของภาพ) *และ* สร้างชั้นข้อความที่ซ่อนอยู่ซึ่งเครื่องมือค้นหาสามารถทำดัชนีได้.

```java
// Configure PDF export options
PdfExportOptions pdfOptions = new PdfExportOptions();
pdfOptions.setEmbedOriginalImage(true);      // keep the bitmap as background
pdfOptions.setCreateSearchablePdf(true);     // generate hidden text layer for search
pdfOptions.setAuthor("John Doe");
pdfOptions.setTitle("OCR Output");
```

- `setEmbedOriginalImage(true)`: ทำให้ PDF มีลักษณะเหมือนภาพสแกนต้นฉบับอย่างแม่นยำ.  
- `setCreateSearchablePdf(true)`: สร้างการซ้อนทับข้อความที่มองไม่เห็น—นี่คือหัวใจของ **add OCR text layer pdf**.  
- คุณสามารถเพิ่มเมตาดาต้า (ผู้เขียน, ชื่อเรื่อง, หัวข้อ) ตามที่แสดง; จะช่วยในการจัดการเอกสารในภายหลัง.

## ขั้นตอนที่ 5: รัน OCR และส่งออก PDF ที่สามารถค้นหาได้  

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน เมธอด `recognizeAndExportPdf` ทำงานหนัก: มันรัน OCR บนแต่ละหน้าของ TIFF, เขียนภาพที่มองเห็นได้, และซ้อนทับข้อความที่สามารถค้นหาได้.

```java
// Perform OCR recognition and export the result as a searchable PDF
ocrEngine.recognizeAndExportPdf(
    ocrInput,
    "YOUR_DIRECTORY/searchable.pdf",
    pdfOptions
);

System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
```

เมื่อคอนโซลพิมพ์ข้อความสำเร็จ คุณเพิ่ง **create searchable pdf** จากไฟล์ TIFF เปิด `searchable.pdf` ที่ได้ในโปรแกรมดู PDF ใดก็ได้ กด `Ctrl+F` แล้วลองค้นหาคำที่ปรากฏในภาพต้นฉบับ—ควรพบได้ทันที.

## การตรวจสอบผลลัพธ์ – รายการตรวจสอบอย่างรวดเร็ว  

1. **ความคมชัดของภาพ** – PDF ควรดูเหมือน TIFF ต้นฉบับอย่างแม่นยำ (ขอบคุณ `setEmbedOriginalImage`).  
2. **การค้นหา** – ใช้ฟังก์ชันค้นหาของโปรแกรมดู; ชั้นข้อความที่ซ่อนควรให้ผลลัพธ์ที่ตรงกัน.  
3. **เมตาดาต้า** – เปิดคุณสมบัติของ PDF เพื่อตรวจสอบผู้เขียนและชื่อเรื่องที่คุณตั้งไว้ก่อนหน้า.  

หากการตรวจสอบใดล้มเหลว ให้ตรวจสอบอีกครั้งว่า `setCreateSearchablePdf(true)` ถูกเปิดใช้งานและไลเซนส์ของคุณ (ถ้ามี) ไม่ได้อยู่ในโหมดประเมินผลที่มีข้อจำกัด.

## กรณีขอบและคำถามทั่วไป  

### ถ้า TIFF ของฉันเป็นหน้าเดียว?  

โค้ดเดียวกันทำงาน—Aspose จะถือ TIFF หน้าเดียวเป็นคอลเลกชันที่มีหนึ่งองค์ประกอบ ดังนั้นไม่ต้องการการจัดการเพิ่มเติม.

### ฉันสามารถควบคุมภาษาของ OCR ได้หรือไม่?  

ได้. ก่อนเรียก `recognizeAndExportPdf` ให้ตั้งค่าภาษาบน engine:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.English);
```

แทนที่ `English` ด้วย enum ของภาษาที่รองรับใดก็ได้.

### ฉันจะข้ามการฝังภาพต้นฉบับเพื่อทำให้ไฟล์ขนาดเล็กลงได้อย่างไร?  

เพียงตั้งค่า `pdfOptions.setEmbedOriginalImage(false)` PDF จะมีเฉพาะชั้นข้อความที่สามารถค้นหาได้ ซึ่งทำให้ไฟล์ลดขนาดอย่างมากแต่จะสูญเสียการแสดงผลภาพ.

### PDF ที่สร้างขึ้นสามารถค้นหาได้จริงบนทุกแพลตฟอร์มหรือไม่?  

โปรแกรมอ่าน PDF สมัยใหม่ (Adobe Acrobat, Foxit, แม้กระทั่งเบราว์เซอร์) จะรับรองชั้นข้อความ บางโปรแกรมอ่านเก่า ๆ หรือเบาอาจละเลย—ทดสอบบนแพลตฟอร์มเป้าหมายของคุณหากไม่แน่ใจ.

## ตัวอย่างการทำงานเต็มรูปแบบ  

ด้านล่างเป็นคลาส Java ที่สมบูรณ์พร้อมรัน แทนที่เส้นทาง placeholder ด้วยเส้นทางจริง, เพิ่มไฟล์ JAR ของ Aspose OCR ไปยังโปรเจกต์ของคุณ, แล้วคลิกรัน.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license (optional for full features)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load a multi‑page TIFF image as OCR input
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically

        // Step 4: Configure PDF export options
        PdfExportOptions pdfOptions = new PdfExportOptions();
        pdfOptions.setEmbedOriginalImage(true);    // keep the bitmap as background
        pdfOptions.setCreateSearchablePdf(true);   // generate hidden text layer for search
        pdfOptions.setAuthor("John Doe");
        pdfOptions.setTitle("OCR Output");

        // Step 5: Perform OCR recognition and export the result as a searchable PDF
        ocrEngine.recognizeAndExportPdf(
            ocrInput,
            "YOUR_DIRECTORY/searchable.pdf",
            pdfOptions
        );

        System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง (คอนโซล):**

```
Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf
```

เปิด `searchable.pdf` แล้วลองค้นหาคำใดก็ได้ที่ปรากฏใน TIFF ต้นฉบับ— voilà, คุณได้ **create searchable pdf** อย่างสำเร็จ!

## สรุป  

เราเพิ่งอธิบายวิธีที่ครบถ้วนและพร้อมใช้งานในระดับผลิตเพื่อ **create searchable PDF** จาก TIFF ด้วย Aspose OCR สำหรับ Java โดยการกำหนดค่า `PdfExportOptions` คุณจะได้ **add OCR text layer PDF** โดยอัตโนมัติ ทำให้ภาพคงที่กลายเป็นเอกสารที่สามารถค้นหาได้ทันที  

หากคุณพร้อมจะก้าวต่อไป ลองทดลองกับ:

- **convert TIFF to PDF** ด้วยขนาดหน้าที่กำหนดเองหรือการตั้งค่า DPI.  
- เพิ่มลายน้ำหรือลายเซ็นดิจิทัลหลังการ OCR.  
- ประมวลผลหลายไฟล์ TIFF ในโฟลเดอร์ด้วยลูป `for` ง่าย ๆ  

แต่ละส่วนขยายเหล่านี้สร้างบนแนวคิดหลักที่เราได้อธิบายไว้ ดังนั้นคุณจะพบว่าการเปลี่ยนแปลงเป็นไปอย่างราบรื่น  

มีคำถามหรือเจอปัญหา? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ

- [จดจำข้อความ PDF – การทำงาน OCR ด้วย Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/)
- [OCR การจดจำเอกสาร PDF ใน Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [วิธี OCR PDF ใน .NET ด้วย Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}