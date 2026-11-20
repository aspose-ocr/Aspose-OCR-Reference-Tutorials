---
category: general
date: 2026-05-28
description: สร้าง PDF ที่ค้นหาได้โดยใช้ Aspose OCR ใน C# เรียนรู้วิธีทำ OCR บน PDF,
  จดจำข้อความใน PDF, และแปลง PDF ที่สแกนด้วย OCR ให้เป็น PDF ที่ค้นหาได้.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR ใน C# ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อทำ
  OCR บน PDF, จดจำข้อความใน PDF, และจัดการไฟล์ PDF ที่สแกนด้วย OCR.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – รัน OCR บน PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – ทำ OCR บน PDF
url: /th/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR – รัน OCR บน PDF

เคยต้อง **สร้างไฟล์ PDF ที่ค้นหาได้** จากกองเอกสารสแกนหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายกระบวนการทำงานของสำนักงาน สิ่งเดียวที่ขวางคุณจากการมีคลังข้อมูลที่ค้นหาได้เต็มรูปแบบคือเพียงไม่กี่บรรทัดของโค้ดที่รัน OCR บนหน้า PDF  

ในบทแนะนำนี้ เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบ ซึ่งจะแสดงให้คุณเห็นอย่างชัดเจนว่า **สร้าง PDF ที่ค้นหาได้** อย่างไรโดยใช้ไลบรารี Aspose OCR for .NET เมื่อเสร็จสิ้นคุณจะรู้วิธี *รัน OCR บน PDF*, *recognize text PDF* และแปลง *OCR scanned PDF* ให้เป็นเวอร์ชันที่ค้นหาได้โดยไม่ต้องพึ่งบริการของบุคคลที่สาม

> **ข้อกำหนดเบื้องต้น** – .NET SDK เวอร์ชันล่าสุด (แนะนำ 6.0 ขึ้นไป) ใบอนุญาต Aspose.OCR for .NET ที่ถูกต้อง (หรือคีย์ประเมินผลชั่วคราว) และไฟล์ PDF ที่คุณต้องการประมวลผล

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## สิ่งที่คู่มือนี้ครอบคลุม

- การตั้งค่าไลบรารี Aspose OCR ในโปรเจกต์ C#  
- การโหลด PDF ต้นฉบับ (จำนวนหน้าที่ต้องการ)  
- การกำหนดค่าเอนจินให้ส่งออกเป็น **PDF ที่ค้นหาได้**  
- การรันกระบวนการ OCR และบันทึกผลลัพธ์  
- เคล็ดลับสำหรับการจัดการเอกสารหลายหน้า, การเลือกภาษา, และข้อผิดพลาดทั่วไป  

หากคุณทำตามขั้นตอนทั้งหมด คุณจะได้ไฟล์ที่สามารถเปิดด้วย Adobe Reader, กด **Ctrl + F**, และค้นหาคำใดก็ได้ที่ปรากฏในสแกนต้นฉบับได้ทันที

---

## ขั้นตอน 1: ติดตั้ง Aspose OCR for .NET

ก่อนเขียนโค้ดใด ๆ ให้เพิ่มแพ็กเกจ NuGet ลงในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** ใช้แฟล็ก `--version` เพื่อระบุเวอร์ชันล่าสุดที่เสถียร (เช่น `Aspose.OCR 23.10`) ซึ่งจะทำให้เข้ากันได้กับ .NET 6 และใหม่กว่า

---

## ขั้นตอน 2: สร้างอินสแตนซ์ของ OCR Engine

หัวใจของกระบวนการคือ `OcrEngine` คิดว่าเป็นสมองที่อ่านภาพและแปลงเป็นข้อความ การเริ่มต้นใช้งานนั้นง่ายมาก:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

อ็อบเจ็กต์ `OcrEngine` จะเก็บสตรีมภาพอินพุตและการกำหนดค่าที่บอก Aspose ว่าคุณต้องการผลลัพธ์อย่างไร

---

## ขั้นตอน 3: โหลด PDF ต้นฉบับ (รัน OCR บน PDF)

Aspose OCR สามารถรับ PDF โดยตรง; มันจะดึงแต่ละหน้าเป็นภาพภายในระบบ แทนที่พาธตัวอย่างด้วยตำแหน่งของเอกสารสแกนของคุณ:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **ทำไมวิธีนี้ถึงใช้ได้:** เมธอด `ImageStream.FromFile` จะตรวจจับรูปแบบ PDF โดยอัตโนมัติและเตรียมการแสดงผลแบบเรสเตอร์สำหรับ OCR ไม่ต้องทำขั้นตอนแปลงเพิ่มเติม

---

## ขั้นตอน 4: กำหนดรูปแบบผลลัพธ์และภาษา

ที่นี่เราบอก Aspose ว่าต้องการอะไร การตั้งค่า `OutputFormat` เป็น `SearchablePdf` จะสั่งให้เอนจินฝังข้อความที่รู้จำไว้ด้านหลังภาพหน้าเดิม ทำให้ได้ **PDF ที่ค้นหาได้** คุณยังสามารถเลือกภาษาเพื่อเพิ่มความแม่นยำได้ – ภาษาอังกฤษเป็นค่าเริ่มต้น แต่คุณสามารถสลับเป็นฝรั่งเศส, เยอรมัน ฯลฯ

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

หากต้องประมวลผลเอกสารสองภาษา คุณสามารถรวมภาษาต่าง ๆ ด้วยการใช้แฟล็กของ enum `Language`

---

## ขั้นตอน 5: รันกระบวนการ OCR – Recognize Text PDF

ตอนนี้งานหนักเริ่มทำงาน เมธอด `Recognize` จะสแกนทุกหน้า, ดึง glyphs, และสร้างสตรีม PDF ภายในที่มีทั้งภาพต้นฉบับและชั้นข้อความที่มองไม่เห็น นี่คือขั้นตอนที่เราทำ *recognize text PDF*

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **คำถามทั่วไป:** *ถ้า PDF มี 200 หน้า จะทำอย่างไร?*  
> เอนจินจะประมวลผลหน้าเป็นลำดับและสตรีมผลลัพธ์ ทำให้การใช้หน่วยความจำคงที่ อย่างไรก็ตาม สำหรับไฟล์ขนาดใหญ่มาก คุณอาจต้องเพิ่มการตั้งค่า `MemoryLimit` ใน `ocrEngine.Configuration`

---

## ขั้นตอน 6: บันทึก PDF ที่ค้นหาได้

สุดท้าย ให้เขียนผลลัพธ์ลงดิสก์ เมธอด `Save` จะบันทึกสตรีมภายในเป็นไฟล์ใหม่ที่คุณสามารถเปิดด้วยโปรแกรมดู PDF ใดก็ได้

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

รันโปรแกรม (`dotnet run`) แล้วดูคอนโซลยืนยันการสร้างไฟล์ เปิด `handbook_searchable.pdf` แล้วลองค้นหาคำที่คุณรู้ว่ามีในสแกนต้นฉบับ – คุณจะเห็นผลลัพธ์ทันที

---

## การจัดการกรณีขอบและสถานการณ์ขั้นสูง

### หลายภาษา (OCR Scanned PDF)

หาก PDF ต้นฉบับของคุณมีทั้งภาษาอังกฤษและสเปน ให้รวมภาษาดังนี้:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR จะสลับพจนานุกรมแบบไดนามิก เพิ่มความแม่นยำสำหรับเอกสารหลายภาษา

### PDF ที่มีรหัสผ่าน

เมื่อทำงานกับ PDF ที่มีการป้องกัน ให้ส่งรหัสผ่านก่อนเรียก `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

หากรหัสผ่านไม่ถูกต้อง `Recognize` จะโยน `InvalidPasswordException`; การจับข้อยกเว้นนี้ทำให้คุณสามารถขอให้ผู้ใช้ใส่รหัสผ่านใหม่ได้

### ควบคุมคุณภาพภาพ

DPI ที่สูงให้ผลลัพธ์ OCR ดีกว่าแต่ใช้หน่วยความจำมากขึ้น หากพบอักขระผิดรูป ให้ปรับ DPI:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### โหมดใบอนุญาต vs การประเมินผล

ในโหมดประเมินผล จะมีลายน้ำปรากฏบนทุกหน้า เพื่อเอาออก ให้ใช้ใบอนุญาตของคุณก่อนเรียก OCR ใด ๆ:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## เคล็ดลับระดับมืออาชีพสำหรับการใช้งานจริง

- **การประมวลผลเป็นชุด:** ห่อโลจิกหลักไว้ในลูป `foreach` ที่วนผ่านรายการ PDF ปล่อย `OcrEngine` หลังจากแต่ละไฟล์เพื่อคืนทรัพยากรเนทีฟ  
- **การบันทึก:** ใช้ `ocrEngine.Configuration.Logger` เพื่อเก็บสถิติ OCR รายละเอียด (เช่น ตัวอักษรที่รู้จำต่อวินาที) มีประโยชน์มากเมื่อแก้ปัญหาความแม่นยำต่ำ  
- **การปรับประสิทธิภาพ:** สำหรับเซิร์ฟเวอร์หลายคอร์ สร้างอ็อบเจ็กต์ `OcrEngine` แยกตามเธรด; ไลบรารีปลอดภัยต่อเธรดเมื่อแต่ละอินสแตนซ์แยกจากกัน  
- **การจัดการข้อผิดพลาด:** ควรล้อมรอบ `Recognize` และ `Save` ด้วยบล็อก `try/catch` เสมอ ข้อยกเว้นที่พบบ่อยได้แก่ `FileNotFoundException`, `OutOfMemoryException`, และ `UnsupportedFormatException`

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (คอนโซล):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

เปิดไฟล์ที่ได้, กด **Ctrl + F**, คุณจะสามารถค้นหาคำใดก็ได้ที่ปรากฏในหน้าสแกนต้นฉบับ นั่นคือความมหัศจรรย์ของการแปลง *OCR scanned PDF* ให้เป็น **PDF ที่ค้นหาได้**

---

## สรุป

เราได้สาธิตวิธี **สร้าง PDF ที่ค้นหาได้** ด้วย Aspose OCR for .NET ครอบคลุมตั้งแต่การติดตั้งแพ็กเกจจนถึงการจัดการ PDF หลายภาษาและ PDF ที่มีรหัสผ่าน ด้วยขั้นตอนเหล่านี้คุณสามารถ *รัน OCR บน PDF* ได้อย่างมั่นใจ, *recognize text PDF* อย่างแม่นยำ, และแปลง *OCR scanned PDF* ใด ๆ ให้เป็นทรัพย์สินที่ค้นหาได้เต็มที่

### ต่อไปคุณควรทำอะไร?

- สำรวจ API **aspose ocr pdf** เพิ่มเติม: ดึงข้อความธรรมดา, ส่งออกเป็น DOCX, หรือสร้าง PDF ที่ค้นหาได้เป็นชุดใหญ่  
- ผสานผลลัพธ์ PDF ที่ค้นหาได้กับ Aspose.PDF เพื่อเพิ่มบุ๊กมาร์คหรือวอเตอร์มาร์ค  
- ทดลองตั้งค่า DPI ต่าง ๆ หรือพจนานุกรม OCR แบบกำหนดเองสำหรับฟอนต์เฉพาะ

อย่าลังเลที่จะปรับแต่งตัวอย่างนี้, ผสานเข้ากับสายงานจัดการเอกสารของคุณ, หรือถามคำถามในคอมเมนต์ ขอให้สนุกกับการเขียนโค้ดและเปลี่ยนสแกนที่อ่านไม่ได้ให้กลายเป็นทองคำที่ค้นหาได้!

## บทแนะนำที่เกี่ยวข้อง

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}