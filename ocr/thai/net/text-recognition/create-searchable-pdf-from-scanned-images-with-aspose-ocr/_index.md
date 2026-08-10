---
category: general
date: 2026-02-27
description: สร้าง PDF ที่ค้นหาได้จาก PDF ที่สแกนในไม่กี่วินาทีด้วย Aspose OCR. เรียนรู้วิธีแปลง
  PDF ที่สแกน, แปลง PDF ด้วย OCR, และดึงข้อความจาก PDF อย่างง่ายดาย.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้ทันที บทแนะนำนี้แสดงวิธีแปลง PDF สแกน, แปลง PDF
  ด้วย OCR, และสกัดข้อความจาก PDF ด้วย Aspose OCR.
og_title: สร้าง PDF ที่ค้นหาได้ – คู่มือ Aspose OCR อย่างรวดเร็ว
tags:
- Aspose OCR
- C#
- PDF processing
title: สร้าง PDF ที่ค้นหาได้จากภาพสแกนด้วย Aspose OCR
url: /th/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากภาพสแกนด้วย Aspose OCR

เคยต้อง **สร้าง PDF ที่ค้นหาได้** จากใบแจ้งหนี้ที่เป็นกระดาษเท่านั้นแต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? ด้วย Aspose OCR คุณสามารถ **สร้าง PDF ที่ค้นหาได้** ได้ในไม่กี่บรรทัดของ C#—ไม่ต้องใช้บริการภายนอก ไม่ต้องคัดลอก‑วางด้วยตนเอง  

ในคู่มือนี้เราจะพาคุณผ่านทุกขั้นตอนที่จำเป็นเพื่อ **แปลงไฟล์ pdf ที่สแกน** ให้เป็น PDF ที่ค้นหาได้เต็มรูปแบบ อธิบายว่าทำไมแต่ละขั้นตอนจึงสำคัญ และแม้กระทั่งแสดงวิธี **ดึงข้อความจาก pdf** หากคุณต้องการสตริงดิบแทนการสร้าง PDF สุดท้าย เมื่อเสร็จแล้วคุณจะได้โค้ดส่วนนำกลับมาใช้ใหม่ที่จัดการกับปัญหา “PDF ที่มีเฉพาะภาพ” อย่างทั่วไปและเคล็ดลับสำหรับกรณีขอบ

![สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR](image-placeholder.png "สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR")

## สิ่งที่คุณต้องมี

- .NET 6.0 หรือใหม่กว่า (API ทำงานบน .NET Core, .NET Framework, และ .NET 5+)
- Visual Studio 2022 (หรือโปรแกรมแก้ไขใดก็ได้ที่คุณชอบ)
- แพคเกจ NuGet ของ Aspose OCR (`Aspose.OCR`) – เราจะติดตั้งในขั้นตอนแรก
- ไฟล์ PDF ที่สแกน (เฉพาะภาพ) ที่คุณต้องการแปลงเป็น **PDF ที่ค้นหาได้**

เท่านี้—ไม่ต้องใช้เครื่องมือ OCR เพิ่มเติม ไม่ต้องกังวลเรื่องลิขสิทธิ์สำหรับการทดลองใช้งาน  

ตอนนี้ไปเริ่มกันเลย

## ขั้นตอนที่ 1: ติดตั้งไลบรารี Aspose OCR (และเคล็ดลับสั้น)

ก่อนที่โค้ดใดจะทำงาน ไลบรารีต้องถูกอ้างอิงไว้ เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรันคำสั่ง:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** หากคุณใช้ Package Manager ของ Visual Studio ค้นหา “Aspose.OCR” แล้วคลิก **Install**. เวอร์ชันทดลองใช้งานฟรีรองรับได้สูงสุด 20 หน้า ซึ่งเหมาะสำหรับการทดสอบ

การติดตั้งแพคเกจจะทำให้คุณเข้าถึง `OcrEngine`, `OcrLanguage`, และ `OcrOutputFormat`—สามคลาสที่เราจะใช้เพื่อ **ocr convert pdf**.

## ขั้นตอนที่ 2: ตั้งค่า OCR Engine (สร้าง PDF ที่ค้นหาได้ – การตั้งค่าพื้นฐาน)

Engine ต้องรู้ว่าจะจดจำภาษาอะไรและต้องการรูปแบบผลลัพธ์อะไร ในกรณีของเราต้องการ PDF ภาษาอังกฤษที่สามารถค้นหาได้

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

ทำไมต้องตั้งค่า `Language` อย่างชัดเจน? ความแม่นยำของ OCR ลดลงอย่างมากเมื่อ Engine พยายามเดาภาษา โดยเฉพาะกับเอกสารที่มีตัวเลขหรือสคริปต์ผสม การกำหนดเป็นภาษาอังกฤษจะให้ชั้นข้อความที่สะอาดขึ้น ซึ่งต่อมาจะช่วยให้ขั้นตอน **extract text from pdf** ทำงานได้ดีขึ้น

## ขั้นตอนที่ 3: แปลง PDF ที่สแกนเป็น PDF ที่ค้นหาได้

เมื่อ Engine พร้อมแล้ว ให้ชี้ไปที่ไฟล์ต้นฉบับและบอกที่อยู่ของไฟล์ผลลัพธ์ การเรียกครั้งเดียวนี้ทำงานหนักทั้งหมด: แปลงแต่ละหน้าเป็น raster, รัน OCR, แล้วเขียน PDF ใหม่พร้อมชั้นข้อความที่มองไม่เห็น

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

หาก PDF ต้นฉบับมีหลายหน้า Aspose OCR จะประมวลผลต่อเนื่องโดยคงรูปแบบเดิมไว้ ไฟล์ผลลัพธ์สามารถเปิดด้วยโปรแกรมดู PDF ใดก็ได้; คุณจะสังเกตว่าตอนนี้สามารถเลือกและค้นหาคำที่เคยเป็นเพียงรูปภาพได้แล้ว

### ตรวจสอบผลลัพธ์ (ดึงข้อความจาก PDF)

เพื่อให้แน่ใจว่าการแปลงสำเร็จ คุณอาจต้องดึงข้อความออกมาทางโปรแกรม:

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

โค้ดส่วนนี้แสดงวิธี **extract text from pdf** หลังขั้นตอน OCR ซึ่งเป็นประโยชน์สำหรับการทำดัชนีหรือส่งเนื้อหาเข้าเครื่องมือค้นหา โปรดทราบว่าคุณต้องใช้แพคเกจ `Aspose.PDF` แยกต่างหากสำหรับส่วนนี้; มันเป็นส่วนเสริมที่เบา

## ขั้นตอนที่ 4: จัดการกับกรณีขอบที่พบบ่อยเมื่อคุณ **Convert Image PDF**

แม้กระบวนการพื้นฐานจะทำงานกับ PDF ส่วนใหญ่ แต่ไฟล์ในโลกจริงอาจมีความท้าทายต่าง ๆ:

| สถานการณ์ | สาเหตุ | วิธีแก้ |
|-----------|--------|----------|
| **หน้าหมุน** | เครื่องสแกนบางครั้งหมุนหน้าอัตโนมัติ 90° | ตั้งค่า `ocrEngine.RotatePages = true` ก่อนเรียก `RecognizePdf` |
| **หลายภาษา** | ใบแจ้งหนี้อาจมีคำภาษาฝรั่งเศสหรือเยอรมัน | ใช้ `OcrLanguage.Multilingual` หรือรวมหลายภาษาโดยใช้ `|` (เช่น `OcrLanguage.English | OcrLanguage.French`) |
| **ไฟล์ขนาดใหญ่ (> 100 หน้า)** | ข้อจำกัดของเวอร์ชันทดลองอาจหยุดการประมวลผลกลางไฟล์ | ซื้อไลเซนส์หรือแบ่ง PDF เป็นชิ้นย่อยด้วย `Aspose.Pdf` ก่อนทำ OCR |
| **สแกนความละเอียดต่ำ** | ตัวอักษรเบลอ ทำให้ OCR แม่นยำลดลง | เพิ่ม DPI ด้วย `ocrEngine.ImageResolution = 300` (ค่าเริ่มต้นคือ 200) |

การจัดการกับสถานการณ์เหล่านี้จะทำให้ **ocr convert pdf** ของคุณคงความเสถียรในสภาพการผลิต

## ขั้นตอนที่ 5: ทำอัตโนมัติกระบวนการทั้งหมด (ห่อเป็นเมธอด)

หากคุณกำลังสร้างบริการประมวลผลใบแจ้งหนี้ คุณอาจต้องการเมธอดที่นำกลับมาใช้ใหม่ นี่คือเวอร์ชันกะทัดรัดที่รับพาธอินพุตและเอาต์พุต จัดการการหมุนหน้า และคืนค่าข้อความที่ดึงออกมา

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

จากนั้นคุณสามารถเรียกใช้ได้ดังนี้:

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

นี่คือเวิร์กโฟลว์ **convert image pdf** → **searchable PDF** ที่ครบถ้วน ทั้งหมดห่ออยู่ในเมธอดเดียวที่คุณสามารถใส่ลงในบริการ ASP.NET Core หรือแอปคอนโซลใดก็ได้

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานบน macOS/Linux ได้หรือไม่?**  
A: ได้แน่นอน. Runtime .NET 6 และ Aspose OCR เป็นแบบข้ามแพลตฟอร์ม ดังนั้นโค้ดเดียวกันทำงานบน Windows, macOS, และคอนเทนเนอร์ Linux

**Q: ถ้าฉันต้องการแค่ข้อความและไม่สนใจ PDF ที่ค้นหาได้?**  
A: ข้ามขั้นตอน `OutputFormat` แล้วตั้งค่า `OutputFormat = OcrOutputFormat.Text`. Engine จะคืนข้อความธรรมดาโดยตรง

**Q: สามารถคงเมตาดาต้าของ PDF ต้นฉบับได้หรือไม่?**  
A: ได้. หลังการแปลง คุณสามารถคัดลอกเมตาดาต้าจากอ็อบเจ็กต์ `Document` ต้นฉบับไปยังอ็อบเจ็กต์ใหม่โดยใช้ `doc.Info.Title`, `doc.Info.Author` เป็นต้น

**Q: มีขีดจำกัดจำนวนหน้าไหม?**  
A: เวอร์ชันทดลองฟรีจำกัดที่ 20 หน้าต่อเอกสาร. ไลเซนส์เต็มจะยกข้อจำกัดนี้ออก

## สรุป

ตอนนี้คุณรู้วิธี **create searchable PDF** 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}