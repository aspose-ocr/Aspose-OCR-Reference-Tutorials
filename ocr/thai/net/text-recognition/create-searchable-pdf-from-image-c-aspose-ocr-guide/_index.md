---
category: general
date: 2026-05-06
description: สร้างไฟล์ PDF ที่ค้นหาได้จากรูปภาพโดยใช้ Aspose OCR ใน C# เรียนรู้การแปลง
  PNG เป็น PDF, ดึงข้อความจากรูปภาพและสร้าง PDF ที่ค้นหาได้.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose OCR ใน C# บทเรียนขั้นตอนต่อขั้นตอนนี้แสดงวิธีแปลง
  PNG เป็น PDF, ดึงข้อความจากภาพ, และสร้าง PDF ที่ค้นหาได้.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพ – คู่มือ C# Aspose OCR
tags:
- Aspose
- C#
- OCR
- PDF
title: สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คู่มือ OCR ด้วย C# ของ Aspose
url: /th/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คำแนะนำ C# Aspose OCR

เคยต้องการ **create searchable PDF** จากรูปสแกนแต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? บางทีคุณอาจมีใบเสร็จ PNG, JPEG ของสัญญา, หรือบิตแมปใด ๆ ที่คุณต้องการแปลงเป็น PDF ที่คุณสามารถค้นหาได้ นี่เป็นปัญหาที่พบบ่อย โดยเฉพาะเมื่อคุณต้องจัดการกับสแกนเก่าที่นั่งอยู่ในโฟลเดอร์โดยไม่มีการใช้งาน

ข่าวดีคือด้วย Aspose OCR คุณสามารถ **convert image to PDF**, ดึงข้อความที่ซ่อนอยู่ออกมา และได้เอกสารที่ค้นหาได้เต็มรูปแบบ—ทั้งหมดในไม่กี่บรรทัดของ C# ในคู่มือนี้เราจะยังแสดงวิธี **convert png to PDF**, **extract text from image**, และแม้กระทั่งกรณีขอบของการจัดการกับ TIFF หลายหน้า โดยตอนจบคุณจะมีโซลูชันที่พร้อมใช้งานซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณต้องการ

- **.NET 6+** (โค้ดทำงานบน .NET Framework 4.6+ ด้วย)
- **Visual Studio 2022** หรือ IDE ที่คุณชอบ
- **Aspose.OCR** NuGet package (จะดึง Aspose.PDF มาให้โดยอัตโนมัติ)
- ไฟล์รูปภาพ (PNG, JPEG, BMP, TIFF) ที่คุณต้องการแปลงเป็น PDF ที่ค้นหาได้

ไม่มีเทคนิคการให้ลิขสิทธิ์เพิ่มเติม ไม่มีบริการภายนอก—เพียงอ้างอิง NuGet เพียงหนึ่งรายการและเวลาเขียนโค้ดไม่กี่นาที

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ NuGet Aspose.OCR

ก่อนอื่นให้เพิ่มไลบรารีลงในโปรเจกต์ของคุณ เปิด Package Manager Console แล้วรัน:

```powershell
Install-Package Aspose.OCR
```

> **เคล็ดลับ:** หากคุณใช้ .NET CLI คำสั่งที่เทียบเท่าคือ `dotnet add package Aspose.OCR`.

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine

การสร้างอินสแตนซ์ของ `OcrEngine` คือประตูสู่การทำ OCR ทั้งหมด คิดว่าเป็นสมองที่จะมองรูปของคุณและเริ่ม “อ่าน” ตัวอักษร

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

คุณอาจสงสัย *ทำไมไม่เรียกเมธอดสแตติกโดยตรง?* วิธีการเชิงวัตถุทำให้คุณปรับตั้งค่าต่าง ๆ ได้ในภายหลัง (ภาษา, ความละเอียด ฯลฯ) โดยไม่ต้องเปลี่ยนโฟลว์โดยรวม

## ขั้นตอนที่ 3: โหลดรูปภาพที่คุณต้องการแปลง

นี่คือจุดที่เราจะ **convert image to PDF** อย่างแท้จริง—โดยส่งบิตแมปเข้าไปใน OCR engine แทนที่ `"YOUR_DIRECTORY/input.png"` ด้วยพาธจริงของไฟล์ของคุณ

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

หากคุณมีสถานการณ์ **convert png to pdf** เพียงชี้ไปที่ไฟล์ PNG สำหรับ TIFF หลายหน้า Aspose.OCR จะจัดการแต่ละเฟรมเป็นหน้าแยกโดยอัตโนมัติ

## ขั้นตอนที่ 4: รัน OCR และดึงข้อความ (ถ้าต้องการ)

การเรียก `Recognize()` ทำงานหนัก: วิเคราะห์รูป, ตรวจจับอักขระ, และคืนผลลัพธ์ที่เป็นโครงสร้าง คุณสามารถเก็บข้อความไว้สำหรับบันทึก, การทำดัชนีการค้นหา, หรือแสดงผล

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Why extract text?** แม้ว่าเราจะฝังข้อความลงใน PDF ขั้นสุดท้ายแล้ว แต่การมีสตริงดิบก็อาจมีประโยชน์สำหรับการตรวจสอบหรือการวิเคราะห์

## ขั้นตอนที่ 5: กำหนดค่า PDF Options สำหรับเอกสารที่ค้นหาได้

Aspose.PDF ให้เราโหมดพิเศษ `PdfSaveOptions` ที่ชื่อ **CreateSearchablePdf** ซึ่งบอกไลบรารีให้ฝังข้อความ OCR เป็นเลเยอร์ที่มองไม่เห็นอยู่ด้านหลังภาพ ทำให้ PDF สามารถค้นหาได้

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

หากคุณต้องการ PDF ที่มีเพียงภาพอย่างเดียว (ไม่มีข้อความซ่อน) คุณสามารถสลับเป็น `PdfSaveOptions.CreatePdf()` ได้ แต่สำหรับเป้าหมายของเรา—**create searchable PDF**—โหมดค้นหาได้คือสิ่งที่สำคัญ

## ขั้นตอนที่ 6: บันทึก PDF ที่ค้นหาได้ลงดิสก์

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน เมธอด `SavePdf` จะเขียนภาพและข้อความซ่อนลงในไฟล์เดียว

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

ในขั้นตอนนี้คุณจะได้ **searchable PDF** ที่สามารถเปิดด้วย Adobe Reader, พิมพ์คำในช่องค้นหา, และกระโดดไปยังตำแหน่งที่ตรงกันทันที—แม้หน้าที่มองเห็นยังคงเป็นภาพสแกนเดิม

## ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกส่วนเข้าด้วยกัน นี่คือแอปคอนโซลที่พร้อมรัน คัดลอก‑วางลงในโปรเจกต์ C# ใหม่ ปรับพาธไฟล์ แล้วกด **F5**

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรม คอนโซลจะแสดงผลประมาณนี้:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

และใน `YOUR_DIRECTORY` คุณจะพบ `output.pdf` เปิดไฟล์นั้น กด **Ctrl F**, พิมพ์ “Invoice”, แล้วคุณจะกระโดดตรงไปยังคำนั้น—แม้หน้าดูเหมือนสแกนแบน

## การจัดการกับความแตกต่างทั่วไป

### การแปลงหลายรูปภาพพร้อมกัน

หากคุณมีโฟลเดอร์เต็มไปด้วย PNGs และต้องการ PDF ที่ค้นหาได้ไฟล์เดียว ให้วนลูปไฟล์และเพิ่มแต่ละไฟล์เป็นหน้าแยก:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

คุณยังสามารถใช้ `PdfFileEditor` จาก Aspose.PDF เพื่อรวม PDF ชั่วคราวหลายไฟล์เป็นไฟล์สุดท้ายหนึ่งไฟล์ได้

### การจัดการกับสแกนความละเอียดต่ำ

ความแม่นยำของ OCR ลดลงเมื่อ DPI ของภาพต่ำกว่า 150 ก่อนส่งภาพเข้า OCR คุณสามารถอัปสเกลภาพได้:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### การเลือกภาษาเฉพาะ

หากเอกสารของคุณไม่ใช่ภาษาอังกฤษ ให้ตั้งค่าภาษา ก่อนเรียก `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

การปรับแต่งเหล่านี้ทำให้ **extract text from image** ทำงานอย่างเชื่อถือได้ในหลายสถานการณ์

## ผลลัพธ์ภาพ

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*ภาพหน้าจอด้านบนแสดง PDF ที่ภาพมองเห็นได้ แต่เลเยอร์ข้อความสามารถค้นหาได้*

## สรุป

คุณมีสูตรครบถ้วนพร้อมใช้งานในระดับ production เพื่อ **create searchable PDF** จากรูปภาพใด ๆ ด้วย Aspose OCR และ C# เราได้อธิบายวิธี **convert image to PDF**, **extract text from image**, และแม้กระทั่งกรณีขอบ **convert png to pdf** และ **ocr image to pdf** โค้ดเป็นอิสระเต็มรูปแบบ ทำงานบน .NET runtime ใดก็ได้ และสามารถขยายเป็นการประมวลผลเป็นชุดหรือสนับสนุนภาษาที่กำหนดเองได้

ต่อไปคุณจะทำอะไร? ลองเพิ่มลายน้ำ, เข้ารหัส PDF, หรือส่งข้อความที่ดึงออกไปยังดัชนีการค้นหาอย่าง Elasticsearch ความเป็นไปได้ไม่มีที่สิ้นสุด และรูปแบบเดียวกัน—load → recognize → save—จะช่วยคุณในทุก workflow ที่ขับเคลื่อนด้วย OCR

หากคุณเจอปัญหาใดหรือมีกรณีการใช้งานที่น่าสนใจอยากแชร์ คอมเมนต์ด้านล่างได้เลย ขอให้เขียนโค้ดสนุกสนานและเพลิดเพลินกับการเปลี่ยนสแกนที่ดื้อดึงให้กลายเป็นทองคำที่ค้นหาได้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}