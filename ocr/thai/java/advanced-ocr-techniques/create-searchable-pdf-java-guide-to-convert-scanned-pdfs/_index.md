---
category: general
date: 2026-02-22
description: สร้าง PDF ที่ค้นหาได้จาก PDF ที่สแกนโดยใช้ Aspose OCR ใน Java เรียนรู้การแปลง
  PDF ที่สแกน, การบีบอัดภาพใน PDF, และการจดจำ OCR ของ PDF อย่างมีประสิทธิภาพ.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: th
og_description: สร้าง PDF ที่ค้นหาได้จาก PDF ที่สแกนโดยใช้ Aspose OCR ใน Java คำแนะนำแบบขั้นตอนนี้แสดงวิธีแปลง
  PDF ที่สแกน, บีบอัดภาพใน PDF, และทำการจดจำข้อความด้วย OCR ของ PDF.
og_title: สร้าง PDF ที่ค้นหาได้ – คู่มือ Java เพื่อแปลง PDF สแกน
tags:
- Java
- OCR
- PDF
- Aspose
title: สร้าง PDF ที่ค้นหาได้ – คู่มือ Java สำหรับแปลง PDF สแกน
url: /th/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ – คู่มือ Java สำหรับแปลง PDF สแกน

เคยต้องการ **create searchable PDF** จากกองเอกสารสแกนหรือไม่? มันเป็นปัญหาที่พบบ่อย—PDF ของคุณดูดี แต่คุณไม่สามารถกด *Ctrl + F* เพื่อค้นหาอะไรได้ ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ Java และ Aspose OCR คุณสามารถเปลี่ยน PDF ที่เป็นภาพเท่านั้นให้เป็นไฟล์ที่ค้นหาได้เต็มรูปแบบ, **convert scanned PDF** เป็นข้อความ, และแม้กระทั่งลดขนาดผลลัพธ์โดย **compressing PDF images**.  

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้ครบถ้วน, อธิบายว่าการตั้งค่าแต่ละอย่างสำคัญอย่างไร, และแสดงวิธีปรับกระบวนการสำหรับกรณีขอบเช่นการสแกนหลายหน้า หรือภาพความละเอียดต่ำ. เมื่อจบคุณจะมีโค้ดสั้น ๆ ที่พร้อมใช้งานในสภาพการผลิตที่ **recognize pdf ocr** อย่างเชื่อถือได้และสร้างเอกสารที่ค้นหาได้อย่างเป็นระเบียบ.

---

## สิ่งที่คุณต้องการ

- **Java 17** (หรือ JDK เวอร์ชันล่าสุด; API ไม่ขึ้นกับ JDK)  
- ไลบรารี **Aspose.OCR for Java** – สามารถดึงจาก Maven Central (`com.aspose:aspose-ocr`)  
- PDF สแกน (เฉพาะภาพ) ที่คุณต้องการทำให้ค้นหาได้  
- IDE หรือโปรแกรมแก้ไขข้อความที่คุณถนัด (IntelliJ, VS Code, Eclipse…)

ไม่มีเฟรมเวิร์กหนัก, ไม่มีบริการภายนอก—เพียง Java แท้ ๆ และ JAR ของบุคคลที่สามเดียว.

![ตัวอย่างการสร้าง PDF ที่ค้นหาได้](placeholder-image.png "ภาพประกอบของ PDF ที่ค้นหาได้ซึ่งสร้างจากเอกสารสแกน")

*ข้อความแทนภาพ:* **create searchable pdf** แสดงภาพก่อน‑และ‑หลังของ PDF สแกนที่ถูกแปลงเป็นข้อความที่ค้นหาได้.

---

## ขั้นตอนที่ 1 – เริ่มต้น OCR Engine  

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine`. คิดว่าเป็นสมองที่จะวิเคราะห์บิตแมปแต่ละภาพภายใน PDF และส่งออกอักขระ Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **เคล็ดลับ:** หากคุณวางแผนจะประมวลผล PDF จำนวนมากต่อเนื่อง, ให้ใช้ `OcrEngine` ตัวเดียวซ้ำแทนการสร้างใหม่ทุกครั้ง. จะช่วยประหยัดมิลลิวินาทีและลดการใช้หน่วยความจำ.

---

## ขั้นตอนที่ 2 – ตั้งค่า PDF‑Specific OCR Options  

Aspose ให้คุณปรับจูนวิธีการสร้าง PDF ผลลัพธ์. การตั้งค่าสามตัวด้านล่างเป็นที่มีผลมากที่สุดสำหรับ **compress pdf images** พร้อมคงความสามารถในการค้นหา.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi เป็นจุดที่ลงตัว; ค่าใต้มักทำให้เร็วขึ้นแต่อาจพลาดฟอนต์ขนาดเล็ก.  
- **CompressImages** – เปิดการบีบอัด PNG แบบไม่มีการสูญเสีย; PDF ที่ค้นหาได้จะคมชัดแต่ไฟล์เบากว่า.  
- **EmbedOriginalImages** – หากไม่เปิดฟลักนี้เอนจินจะลบภาพราสเตอร์เดิม, เหลือเพียงข้อความที่มองไม่เห็น. การเก็บภาพไว้ทำให้ PDF มีลักษณะเหมือนสแกนเดิม, ซึ่งหลายทีม compliance ต้องการ.

---

## ขั้นตอนที่ 3 – โหลด PDF สแกนของคุณเข้าสู่ `OcrInput`  

Aspose อ่านไฟล์ต้นทางผ่านตัวห่อ `OcrInput`. คุณสามารถเพิ่มหลายไฟล์ได้, แต่ในตัวอย่างนี้เรามุ่งเน้นที่ **image PDF** เพียงไฟล์เดียว.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **ทำไมไม่ส่ง `File` ตรง ๆ?** การใช้ `OcrInput` ให้ความยืดหยุ่นในการต่อหลาย PDF หรือแม้กระทั่งผสานไฟล์ภาพ (PNG, JPEG) ก่อน OCR. นี่เป็นรูปแบบที่แนะนำเมื่อคุณ **convert scanned pdf** ที่อาจกระจายอยู่หลายแหล่ง.

---

## ขั้นตอนที่ 4 – ทำ OCR และรับ PDF ที่ค้นหาได้เป็น Byte Array  

ตอนนี้จุดมุ่งหมายเกิดขึ้น. เอนจินวิเคราะห์แต่ละหน้า, รัน OCR, และสร้าง PDF ใหม่ที่มีทั้งภาพต้นฉบับและชั้นข้อความที่ซ่อนอยู่.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

หากคุณต้องการข้อความดิบสำหรับการใช้งานอื่น (เช่น การทำดัชนี), สามารถเรียก `ocrEngine.recognize(ocrInput)` ซึ่งจะคืนค่า `String`. แต่สำหรับเป้าหมาย **create searchable pdf** เราต้องการอาร์เรย์ไบต์เพื่อบันทึกลงดิสก์.

---

## ขั้นตอนที่ 5 – บันทึก PDF ที่ค้นหาได้ลงดิสก์  

สุดท้าย, เขียนอาร์เรย์ไบต์ลงไฟล์. NIO ของ Java ทำให้เป็นบรรทัดเดียว.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

เมื่อคุณเปิด `searchable_output.pdf` ใน Adobe Acrobat หรือโปรแกรมอ่านสมัยใหม่อื่น ๆ, คุณจะสังเกตว่าตอนนี้สามารถเลือก, คัดลอก, และค้นหาข้อความได้—ตรงกับที่การแปลง **image pdf to text** สัญญาไว้.

---

## แปลง PDF สแกนเป็นข้อความด้วย OCR (เลือกทำ)

บางครั้งคุณต้องการเพียงข้อความธรรมดาที่สกัดออกมา, ไม่ใช่ PDF ใหม่. คุณสามารถใช้เอนจินเดียวกันได้:

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

ส่วนโค้ดนี้แสดงให้เห็นว่าการ **recognize pdf ocr** สำหรับการประมวลผลต่อไป เช่น การป้อนดัชนีการค้นหา หรือการวิเคราะห์ภาษาธรรมชาติ ทำได้ง่ายแค่ไหน.

---

## บีบอัดภาพ PDF เพื่อให้ไฟล์เล็กลง  

หากสแกนต้นทางของคุณใหญ่ (เช่น 600 dpi สีเต็ม), PDF ที่ค้นหาได้อาจยังคงหนัก. นอกจากฟลัก `setCompressImages(true)`, คุณยังสามารถลดขนาดภาพก่อน OCR ได้ด้วยตนเอง:

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

การลด DPI จะทำให้ขนาดไฟล์ประมาณครึ่งหนึ่ง, แต่ควรทดสอบความอ่านได้—ฟอนต์บางตัวอาจอ่านไม่ออกเมื่อ DPI ต่ำกว่า 150. การตัดสินใจระหว่าง **compress pdf images** กับความแม่นยำของ OCR ขึ้นอยู่กับข้อจำกัดด้านพื้นที่จัดเก็บของคุณ.

---

## อธิบายการตั้งค่า Recognize PDF OCR  

| การตั้งค่า                | ผลต่อผลลัพธ์                         | กรณีการใช้งานทั่วไป                                   |
|------------------------|------------------------------------------|----------------------------------------------------|
| `setOutputDpi(int)`    | ควบคุมความละเอียดของ raster ที่ OCR สร้างผลลัพธ์ | คลังเก็บคุณภาพสูง (300 dpi) vs. PDF เว็บเบา (150 dpi) |
| `setCompressImages`    | เปิดการบีบอัด PNG                      | เมื่อคุณต้องส่ง PDF ทางอีเมลหรือเก็บบนคลาวด์ |
| `setEmbedOriginalImages`| เก็บภาพสแกนต้นฉบับไว้                | เอกสารทางกฎหมายหรือ compliance ที่ต้องคงลักษณะเดิม |
| `setLanguage` (optional) | บังคับโมเดลภาษา (เช่น "eng")          | คอร์ปัสหลายภาษา ที่การตรวจจับอัตโนมัติอาจผิดพลาด |

การเข้าใจ “โนบ” เหล่านี้ช่วยให้คุณ **recognize pdf ocr** อย่างชาญฉลาดและหลีกเลี่ยงกับดัก “ข้อความเบลอ”.

---

## Image PDF to Text – ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง  

1. **สแกนความละเอียดต่ำ** – ความแม่นยำของ OCR ลดลงอย่างชัดเจนเมื่อต่ำกว่า 150 dpi. ควรอัปสแคลภาพต้นทางก่อนส่งให้ Aspose, หรือขอ DPI สูงขึ้นจากเครื่องสแกน.  
2. **หน้าหมุน** – หากหน้าถูกสแกนเอียง, เปิด auto‑rotate: `pdfOcrOptions.setAutoRotate(true);`.  
3. **PDF ที่เข้ารหัส** – เอนจินไม่สามารถอ่านไฟล์ที่มีรหัสผ่าน; ต้องถอดรหัสก่อนด้วย `PdfDocument` จาก Aspose.PDF.  
4. **ผสม raster และ text** – บาง PDF มีชั้นข้อความซ่อนอยู่แล้ว. การรัน OCR อีกครั้งอาจทำให้ข้อความซ้ำซ้อน. ใช้ `PdfOcrOptions.setSkipExistingText(true);` เพื่อคงชั้นเดิมไว้.

การจัดการกับปัญหาเหล่านี้ทำให้สายงาน **create searchable pdf** ของคุณแข็งแรงแม้ในสภาพเอกสารจริง.

---

## ตัวอย่างทำงานเต็มรูปแบบ (ทุกขั้นตอนในไฟล์เดียว)

ด้านล่างเป็นคลาส Java เต็มที่คุณสามารถคัดลอก‑วางลงใน IDE ของคุณ. แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริงของคุณ.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}