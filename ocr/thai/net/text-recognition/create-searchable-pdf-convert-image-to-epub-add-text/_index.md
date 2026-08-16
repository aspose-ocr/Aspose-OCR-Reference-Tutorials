---
category: general
date: 2026-03-13
description: สร้างไฟล์ PDF ที่ค้นหาได้จากภาพใด ๆ ด้วย Aspose OCR. เรียนรู้วิธีแปลงภาพเป็น
  EPUB, เพิ่มข้อความที่ค้นหาได้, และสร้างไฟล์ PDF ที่ค้นหาได้ใน C#
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: th
og_description: สร้างไฟล์ PDF ที่ค้นหาได้จากภาพใด ๆ ด้วย Aspose OCR คู่มือนี้แสดงวิธีแปลงภาพเป็น
  EPUB เพิ่มข้อความที่ค้นหาได้ และสร้างไฟล์ PDF ที่ค้นหาได้ใน C#
og_title: สร้าง PDF ที่ค้นหาได้ – แปลงภาพเป็น EPUB และเพิ่มข้อความ
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: สร้าง PDF ที่ค้นหาได้ – แปลงภาพเป็น EPUB และเพิ่มข้อความ
url: /th/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ – แปลงรูปภาพเป็น EPUB และเพิ่มข้อความ

ต้องการ **สร้าง PDF ที่ค้นหาได้** จากใบเสร็จสแกนหรือรูปภาพใด ๆ หรือไม่? ในบทแนะนำนี้เราจะแสดงวิธีสร้าง PDF ที่ค้นหาได้โดยใช้ Aspose OCR พร้อมกับ **แปลงรูปภาพเป็น EPUB** และ **เพิ่มชั้นข้อความที่สามารถค้นหาได้** — ทั้งหมดในโครงการ C# เดียว  

หากคุณเคยเจอกับ PDF ที่ดูสวยแต่ไม่สามารถค้นหาได้ คุณไม่ได้อยู่คนเดียว ข่าวดีคือชั้นข้อความที่ซ่อนอยู่สามารถเปลี่ยนภาพแบนให้กลายเป็นเอกสารที่ค้นหาได้เต็มรูปแบบ และ Aspose ทำให้กระบวนการนี้ง่ายดายเกือบไม่มีอุปสรรค

## สิ่งที่คุณจะได้เรียนรู้

* วิธีการเริ่มต้น Aspose OCR engine และตั้งค่าภาษา  
* ขั้นตอนที่แน่นอนเพื่อ **แปลงรูปภาพเป็น EPUB** สำหรับการจัดจำหน่าย e‑book  
* วิธีการกำหนดค่า PDF writer เพื่อให้ผลลัพธ์มีชั้นข้อความที่ซ่อนอยู่และสามารถค้นหาได้  
* เคล็ดลับการจัดการกรณีขอบเช่นใบเสร็จหลายหน้า หรือภาษาที่ไม่ใช่ภาษาอังกฤษ  

สิ่งที่คุณต้องมีล่วงหน้าคือสภาพแวดล้อมการพัฒนา .NET (Visual Studio 2022 หรือใหม่กว่า) และแพ็กเกจ Aspose OCR NuGet ไม่มีบริการภายนอก ไม่มีไฟล์กำหนดค่าที่ซับซ้อน—เพียง C# ธรรมดาที่คุณคัดลอก‑วางและรันได้เลย

## ข้อกำหนดเบื้องต้น

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR รองรับ .NET Standard 2.0+ ดังนั้น .NET 6 จะให้การปรับปรุง runtime ล่าสุด |
| Aspose.OCR NuGet package | ให้คลาส `OcrEngine`, `EpubWriter`, และ `PdfWriter` ที่ใช้ในโค้ด |
| An image file (e.g., `receipt.jpg`) | ไฟล์รูปภาพ (เช่น `receipt.jpg`) | แหล่งที่คุณจะทำ OCR บน. รูปภาพ raster ใด ๆ (PNG, JPEG, BMP) ก็ใช้ได้ |
| Basic C# knowledge | ความรู้พื้นฐาน C# | คุณจะอ่านและปรับแต่ง snippet ไม่ได้เรียนภาษาใหม่ตั้งแต่ต้น |

คุณสามารถติดตั้งแพ็กเกจด้วยคำสั่งต่อไปนี้:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** หากคุณใช้ Visual Studio, UI ของ NuGet Package Manager ทำงานเดียวกัน—แค่ค้นหา “Aspose.OCR”

## ขั้นตอน 1 – สร้าง PDF ที่ค้นหาได้ด้วย Aspose OCR

สิ่งแรกที่เราต้องการคืออินสแตนซ์ `OcrEngine` ที่รู้ว่าจะจดจำภาษาอะไร ภาษาอังกฤษเป็นค่าเริ่มต้น แต่คุณสามารถเปลี่ยนเป็นภาษาฝรั่งเศส, เยอรมัน ฯลฯ ได้โดยตั้งค่า `ocrEngine.Language`

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

ทำไมต้องเริ่มต้น engine ก่อน? engine จะเก็บโมเดลการจดจำไว้ในหน่วยความจำ ดังนั้นการสร้างเพียงครั้งเดียวและนำมาใช้ซ้ำกับหลายรูปภาพจะช่วยประหยัด CPU และ RAM ในงานแบชขนาดใหญ่ คุณจะคงอินสแตนซ์เดียวตลอดการทำงาน

## ขั้นตอน 2 – โหลดรูปภาพและทำ OCR

ต่อไปเราจะชี้ engine ไปที่ไฟล์ที่ต้องการประมวลผล `ImageStream.FromFile` จะอ่านรูปภาพเข้าสู่รูปแบบที่ OCR engine เข้าใจ

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **What if the image is multi‑page?**  
> Aspose OCR สามารถจัดการกับ TIFF หลายหน้าได้โดยอัตโนมัติ เพียงส่งพาธของไฟล์ TIFF ไป; engine จะวนผ่านแต่ละหน้าโดยอัตโนมัติ

## ขั้นตอน 3 – แปลงรูปภาพเป็น EPUB

หากคุณต้องการเวอร์ชัน e‑book ของเอกสารที่สแกน Aspose ทำให้เป็นบรรทัดเดียว `EpubWriter` ใช้อินสแตนซ์ `OcrEngine` เดียวกัน หมายความว่าผลลัพธ์ OCR จะถูกนำกลับมาใช้โดยไม่ต้องประมวลผลเพิ่มเติม

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

ทำไมต้องส่งออกเป็น EPUB? EPUB เป็นฟอร์แมตที่รีฟลว์ได้—เหมาะกับเครื่องอ่านบนมือถือ ข้อความ OCR จะสามารถเลือกได้ และรูปภาพต้นฉบับจะคงเป็นพื้นหลัง เพื่อรักษาลักษณะของสแกนต้นฉบับ

## ขั้นตอน 4 – เพิ่มชั้นข้อความที่ค้นหาได้ลงใน PDF

ต่อไปคือส่วนที่จริง ๆ แล้ว **สร้าง PDF ที่ค้นหาได้** โดยเปิดใช้งาน `AddSearchableTextLayer` PDF writer จะฝังชั้นข้อความที่มองไม่เห็นซึ่งสะท้อนผลลัพธ์ OCR ผู้ใช้สามารถค้นหา, คัดลอก หรือไฮไลท์ข้อความได้เหมือน PDF ปกติ

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Common pitfall:** หากลืมตั้งค่า `AddSearchableTextLayer` จะได้ PDF ที่ดูเหมือนกันแต่ไม่มีข้อความที่ค้นหาได้ ตรวจสอบค่าสถานะนี้เสมอเมื่อคุณต้องการเอกสารที่สามารถค้นหาได้

## ขั้นตอน 5 – ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือแอปคอนโซลที่พร้อมใช้งาน คุณสามารถวางลงในโครงการ .NET ใหม่และรันได้ทันที

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

* `receipt.epub` – ไฟล์ EPUB ที่คุณสามารถเปิดใน Calibre, Apple Books หรือ e‑reader ใด ๆ  
* `receipt_searchable.pdf` – PDF ที่คุณสามารถกด **Ctrl + F** เพื่อค้นหาคำใด ๆ ที่ปรากฏในรูปภาพต้นฉบับ  

หากคุณเปิด PDF ใน Adobe Acrobat และดู **File → Properties → Description** คุณจะเห็นสตรีมข้อความที่ซ่อนอยู่ภายใต้แท็บ **Fonts** ยืนยันว่าชั้นข้อความที่ค้นหาได้มีอยู่จริง

## คำถามทั่วไปและกรณีขอบ

**ถาม: วิธีนี้ทำงานกับภาษาที่ไม่ใช่ภาษาอังกฤษหรือไม่?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}