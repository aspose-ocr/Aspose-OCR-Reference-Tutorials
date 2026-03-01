---
category: general
date: 2026-02-28
description: สร้าง PDF ที่ค้นหาได้จากไฟล์ TIFF หลายหน้าใน C# คู่มือนี้แสดงวิธีการแปลงภาพเป็น
  PDF ที่ค้นหาได้พร้อมตัวอย่าง OCR ด้วย C# อย่างครบถ้วน
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากไฟล์ TIFF ด้วย Aspose.OCR. ทำตามตัวอย่าง OCR
  ด้วย C# ทีละขั้นตอนเพื่อแปลงภาพเป็น PDF ที่ค้นหาได้.
og_title: สร้าง PDF ที่ค้นหาได้ใน C# – แปลงภาพเป็น PDF ด้วย OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: สร้าง PDF ที่ค้นหาได้ใน C# – แปลงภาพเป็น PDF ด้วย OCR
url: /th/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ใน C# – การแปลงภาพเป็น PDF OCR

เคยต้องการ **สร้าง PDF ที่สามารถค้นหาได้** จากเอกสารสแกนแต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายกระบวนการทำงานของสำนักงาน PDF ที่สามารถค้นหาได้เป็นความแตกต่างระหว่างไฟล์ที่ไม่มีประโยชน์และคลังข้อมูลที่สามารถค้นหาได้  

ในบทแนะนำนี้ เราจะพาคุณผ่าน **c# ocr example** ที่สมบูรณ์ซึ่งแปลงไฟล์ TIFF หลายหน้าเป็น PDF ที่สามารถค้นหาได้ทั้งหมดด้วย Aspose.OCR. เมื่อจบคุณจะรู้วิธี **image to searchable pdf** อย่างแม่นยำ, วิธี **convert tiff to pdf**, และคุณจะได้โค้ดสแนปช็อตที่พร้อมใช้งานที่สามารถใส่ลงในโปรเจค .NET ใดก็ได้

## สิ่งที่คุณจะได้เรียนรู้

* วิธีติดตั้งและอ้างอิง Aspose.OCR ในโปรเจค C#  
* ขั้นตอนที่แม่นยำในการโหลด TIFF, ตั้งค่าภาษา, และเรียก `RecognizeToPdf`  
* ทำไมแต่ละขั้นตอนจึงสำคัญ – ตั้งแต่การจัดการหน่วยความจำจนถึงการเลือกภาษา  
* เคล็ดลับสำหรับการจัดการเอกสารขนาดใหญ่, การแก้ไขปัญหา OCR ที่พบบ่อย, และการขยายโซลูชันไปยังรูปแบบภาพอื่น ๆ  

**Prerequisites** – .NET SDK เวอร์ชันล่าสุด (4.6+ หรือ .NET Core 3.1+), Visual Studio (หรือ IDE ที่คุณชื่นชอบ), และลิขสิทธิ์ Aspose.OCR (รุ่นทดลองฟรีใช้สำหรับทดสอบ) ไม่จำเป็นต้องใช้ไลบรารีภายนอกอื่นใด

---

## สร้าง PDF ที่สามารถค้นหาได้ – ภาพรวม

ในระดับสูง กระบวนการมีลักษณะดังนี้:

1. **Initialize** the `OcrEngine`.  
2. **Load** the source image (a TIFF in our case).  
3. **Configure** language settings for better accuracy.  
4. **Run** OCR and **save** the result directly as a searchable PDF.  

เท่านี้เอง API ของ Aspose ทำงานหนักให้คุณแล้ว คุณจึงไม่ต้องต่อรวมไลบรารี OCR และ PDF แยกกัน

---

## Step 1: Install Aspose.OCR and Set Up Your Project

ขั้นตอนแรก ให้เพิ่มแพ็กเกจ Aspose.OCR ผ่าน NuGet:

```bash
dotnet add package Aspose.OCR
```

หรือ หากคุณชอบใช้ Package Manager Console ใน Visual Studio:

```powershell
Install-Package Aspose.OCR
```

หลังจากแพ็กเกจถูกกู้คืนแล้ว ให้เปิดไฟล์โปรเจคของคุณและตรวจสอบการอ้างอิง:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** ใช้เวอร์ชัน stable ล่าสุด (ตรวจสอบที่เว็บไซต์ Aspose) เพื่อรับการแก้ไขบั๊กและแพ็คเกจภาษาที่ใหม่ที่สุด

---

## Step 2: Convert TIFF to PDF – Loading the Image

ตอนนี้เราจะโหลดไฟล์ TIFF ที่ต้องการทำให้สามารถค้นหาได้ เมธอด `Image.Load` ของ Aspose รองรับ TIFF หลายหน้าโดยอัตโนมัติ

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Why this matters:** การโหลดภาพภายในบล็อก `using` รับประกันว่าทรัพยากรที่ไม่ได้จัดการจะถูกปล่อยออกอย่างทันท่วงที—สำคัญมากเมื่อประมวลผลเอกสารขนาดใหญ่

---

## Step 3: Image to Searchable PDF – OCR Engine Configuration

ก่อนที่เราจะรัน OCR เราจะบอกเอนจินว่าคาดว่าจะใช้ภาษาอะไร ภาษาอังกฤษทำงานได้ในหลายกรณี แต่คุณสามารถสลับเป็นค่า `OcrLanguage` ใดก็ได้

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Expert note:** การเลือกภาษาที่ถูกต้องจะลดการรับรู้ผิดพลาดอย่างมหาศาล หากคุณมีหลายภาษา สามารถรวมกันด้วยตัวดำเนินการ `|` เช่น `OcrLanguage.English | OcrLanguage.French`

---

## Step 4: C# OCR Example – Recognize and Save

เมื่อเอนจินพร้อมแล้ว ให้เรียก `RecognizeToPdf` เมธอดนี้จะเขียน PDF ที่สามารถค้นหาได้โดยตรงลงดิสก์ พร้อมฝังเลเยอร์ข้อความที่มองไม่เห็นไว้ด้านหลังภาพต้นฉบับ

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

หลังจากบรรทัดนี้ทำงานเสร็จ `output.pdf` จะประกอบด้วยหน้าต่าง ๆ ของ TIFF ดั้งเดิมพร้อมกับข้อความซ่อนที่โปรแกรมอ่าน PDF ใดก็สามารถค้นหาได้

---

## Step 5: C# Image to PDF – Verify the Result

มาทดสอบว่าทุกอย่างทำงานถูกต้องหรือไม่ เปิด PDF ที่สร้างขึ้นใน Adobe Reader (หรือโปรแกรมดูอื่น) แล้วลองค้นหาคำที่คุณรู้ว่ามีอยู่ในไฟล์ TIFF ต้นฉบับ

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

หากการค้นหาตอบสนอง คุณได้ **create searchable pdf** จากภาพสำเร็จแล้ว หากไม่พบผล ให้ตรวจสอบการตั้งค่าภาษา หรือคุณภาพของไฟล์ TIFF ต้นฉบับอีกครั้ง

---

## Full Working Example

รวมทุกส่วนเข้าด้วยกัน นี่คือแอปคอนโซลแบบ self‑contained ที่คุณสามารถคอมไพล์และรันได้:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Expected output** (in the console):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

เปิด `output.pdf` แล้วคุณควรจะพิมพ์คำใดคำหนึ่งจาก TIFF ดั้งเดิมในช่องค้นหาของโปรแกรมดูและเห็นผลลัพธ์ที่ไฮไลท์

---

![ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้](placeholder-image.png){: .align-center alt="ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้"}

*ภาพหน้าจอด้านบนแสดง PDF ที่สามารถค้นหาได้เปิดอยู่ในโปรแกรมดูพร้อมกับเลเยอร์ข้อความที่ซ่อนอยู่ทำงานอยู่*

---

## Common Questions & Edge Cases

### What if my TIFF is huge (hundreds of pages)?

Aspose.OCR จะสตรีมหน้าทีละหน้า แต่คุณอาจยังเจอขีดจำกัดของหน่วยความจำ พิจารณาประมวลผล TIFF เป็นชุดย่อย:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

ภายหลังให้รวม PDF แต่ละหน้าด้วยไลบรารี PDF (เช่น Aspose.PDF)

### Can I output to a different format, like searchable DOCX?

ได้—ใช้ `RecognizeToDocument` แทน `RecognizeToPdf` API มีโครงสร้างเดียวกับเมธอด PDF เพียงเปลี่ยนส่วนขยายไฟล์เป้าหมาย

### How do I handle languages other than English?

เปลี่ยน `OcrLanguage.English` เป็นค่า enum ที่เหมาะสม เช่น `OcrLanguage.Spanish` คุณยังสามารถรวมหลายภาษาได้:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### What about password‑protected PDFs?

หลังจากขั้นตอน OCR คุณสามารถเปิด PDF ที่สร้างขึ้นด้วย Aspose.PDF และทำการเข้ารหัส:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Recap

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **create searchable PDF** จากภาพ TIFF ด้วย C# ตั้งแต่การติดตั้ง Aspose.OCR, การโหลดภาพ, การตั้งค่าภาษา, การรัน OCR, จนถึงการตรวจสอบผลลัพธ์ที่สามารถค้นหาได้ ตอนนี้คุณมี **c# ocr example** ที่แข็งแรงและสามารถปรับใช้กับรูปแบบอื่น ๆ ได้  

หากคุณพร้อมก้าวต่อไป ลอง:

* **Convert TIFF to PDF** สำหรับเอกสารที่ไม่ต้องการค้นหา (เพียงข้ามขั้นตอน OCR)  
* ทดลองกับ **image to searchable pdf**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}