---
category: general
date: 2026-04-08
description: สร้าง PDF ที่ค้นหาได้อย่างรวดเร็วและเรียนรู้วิธีบีบอัดภาพใน PDF, ฝังฟอนต์ใน
  PDF และจดจำข้อความจากภาพใน C# ด้วย Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: th
og_description: สร้าง PDF ที่ค้นหาได้อย่างรวดเร็วด้วย Aspose.OCR เรียนรู้การบีบอัดภาพใน
  PDF, ฝังฟอนต์ใน PDF, และการจดจำข้อความจากภาพในบทเรียนเดียว
og_title: สร้าง PDF ที่ค้นหาได้ – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose.OCR
- C#
- PDF Generation
title: สร้าง PDF ที่ค้นหาได้ – คู่มือ C# ครบสำหรับแปลงภาพเป็น PDF
url: /th/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ – คู่มือ C# ฉบับสมบูรณ์

ต้องการ **create searchable pdf** จากภาพสแกนหรือไม่? คุณไม่ได้เป็นคนเดียวที่มองดู PNG ขนาดใหญ่และสงสัยว่าจะเปลี่ยนเป็นเอกสารที่มีน้ำหนักเบาและสามารถค้นหาข้อความได้อย่างไร ข่าวดีคือด้วย Aspose.OCR คุณทำได้ในไม่กี่บรรทัด และคุณยังจะได้เรียนรู้วิธี **compress PDF images**, **embed fonts PDF**, และ **recognize text image** อย่างไม่ต้องเหนื่อยเลย.

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การโหลดภาพ, การรัน OCR, การปรับแต่งตัวเลือกการบันทึก PDF, จนถึงการเขียน PDF ที่ค้นหาได้ลงดิสก์ สุดท้ายคุณจะมีเมธอดพร้อมใช้ที่สามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้ พร้อมกับเคล็ดลับระดับมืออาชีพสำหรับกรณีขอบที่คุณอาจเจอในภายหลัง.

## สิ่งที่คุณต้องการ

- **.NET 6+** (โค้ดทำงานบน .NET Framework 4.7 ด้วยเช่นกัน แต่เราจะตั้งเป้าหมายที่ .NET 6 เพื่อไวยากรณ์สมัยใหม่).  
- **Aspose.OCR for .NET** – ติดตั้งผ่าน NuGet: `Install-Package Aspose.OCR`.  
- ไฟล์ภาพ (PNG, JPEG, TIFF) ที่มีข้อความที่คุณต้องการทำให้สามารถค้นหาได้.  
- ความอยากรู้อยากเห็นเล็กน้อย – ส่วนที่เหลือจะอธิบายด้านล่าง.

> **Pro tip:** หากคุณกำลังวางแผนประมวลผลหลายสิบหน้า พิจารณาใช้ instance ของ `OcrEngine` เพียงหนึ่งเดียวซ้ำเพื่อหลีกเลี่ยงภาระการโหลดข้อมูลภาษาซ้ำๆ.

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – Recognize Text Image

สิ่งแรกที่เราต้องการคือ OCR engine ที่สามารถอ่านอักขระจากบิตแมพต้นฉบับ Aspose.OCR ให้คุณระบุภาษา (English, French, ฯลฯ) และคืนค่าอ็อบเจกต์ `OcrResult` ที่บรรจุทั้งข้อความดิบและข้อมูลภาพ.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
- การตั้งค่าภาษาเพิ่มความแม่นยำอย่างมาก; engine จะโหลดพจนานุกรมเฉพาะภาษาภายใน.  
- `OcrResult` ไม่ได้เก็บเฉพาะสตริงที่สกัดออกมาเท่านั้น แต่ยังเก็บบิตแมพพื้นฐาน ซึ่งเราจะฝังลงใน PDF ในภายหลังเพื่อให้เอกสารคงความเหมือนภาพสแกนต้นฉบับ.

## ขั้นตอนที่ 2: กำหนดค่า PDF Save Options – Compress PDF Images & Embed Fonts

PDF ที่ค้นหาได้โดยพื้นฐานคือ PDF ปกติที่มีชั้นข้อความที่มองไม่เห็นอยู่บนภาพสแกน หากคุณละเลยการบีบอัด ไฟล์สุดท้ายอาจใหญ่โต `PdfSaveOptions` class ให้การควบคุมละเอียดเกี่ยวกับคุณภาพภาพ, การฝังฟอนต์, และว่าฟอนต์ควรทำ subset หรือไม่.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**ทำไมคุณควร embed fonts PDF:**  
เมื่อเปิด PDF บนระบบที่ไม่มีฟอนต์เดียวกันกับที่ใช้ในชั้น OCR ข้อความอาจแสดงเป็นอักขระผิดรูป การฝังฟอนต์รับประกันความถูกต้องของการแสดงผลข้ามแพลตฟอร์ม ซึ่งสำคัญสำหรับเอกสารทางกฎหมายหรือเอกสารสำรอง.

## ขั้นตอนที่ 3: บันทึกผลลัพธ์เป็น Searchable PDF – Image to Searchable PDF

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน: นำ `OcrResult` ไปใช้กับ `PdfSaveOptions` ของเราและเขียนไฟล์ เมธอด `SaveAsSearchablePdf` ทำงานหนัก—สร้างชั้นข้อความที่ซ่อนอยู่ซึ่งสะท้อนผลลัพธ์ OCR ขณะยังคงรักษาภาพต้นฉบับ.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมคอนโซลแบบ self‑contained ที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซล .NET ใหม่ มันสมมติว่าภาพอยู่ในโฟลเดอร์ชื่อ `YOUR_DIRECTORY` ที่สัมพันธ์กับไฟล์ executable.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

การรันโปรแกรมจะสร้าง `output.pdf` ที่คุณสามารถเปิดด้วย Adobe Reader, Foxit หรือโปรแกรมดู PDF ใดก็ได้และค้นหาคำที่เคยอยู่ในภาพได้ทันที.

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ – การค้นหาทำงานหรือไม่?

หลังจากไฟล์ถูกสร้างขึ้น เปิดไฟล์และลองใช้ฟังก์ชันค้นหาในตัว (Ctrl + F) หากคุณสามารถหาคำเช่น “invoice”, “date”, หรือ “total” ได้ คุณได้สร้าง **searchable PDF** สำเร็จแล้ว.

หากการค้นหาไม่ให้ผลลัพธ์ใดเลย:

1. **Check OCR accuracy** – อาจภาพต้นฉบับมีความละเอียดต่ำ พิจารณาเพิ่ม DPI ก่อน OCR (Aspose ให้คุณตั้งค่า `Resolution` บน engine).  
2. **Confirm font embedding** – เปิดคุณสมบัติของ PDF แล้วดูที่ *Fonts*; คุณควรเห็นฟอนต์ที่ฝังอยู่แสดงอยู่.  
3. **Inspect image compression** – `ImageQuality` ที่ต่ำมากอาจทำให้ชั้นภาพไม่สามารถอ่านได้ ซึ่งบางครั้งทำให้เครื่องมือ downstream สับสน.

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องปรับ | เหตุผล |
|----------|----------------|-----|
| **Multi‑page TIFF** | วนลูปแต่ละเฟรม, เรียก `RecognizeImage` ต่อหน้า, จากนั้นใช้ `PdfSaveOptions` กับ `AppendMode = true`. | ทำให้แต่ละหน้าที่สแกนเป็นหน้า searchable ของตนเอง. |
| **Non‑English language** | เปลี่ยน `Language = "fr"` (หรือรหัส ISO ที่เหมาะสม) และอาจจัดหาพจนานุกรมกำหนดเอง. | ปรับปรุงการรับรู้สำหรับอักขระที่มีสำเนียงและ glyph เฉพาะภาษา. |
| **Very large images** | ลดขนาดบิตแมพก่อน OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | ลดการใช้หน่วยความจำและเร่งความเร็ว OCR โดยไม่สูญเสียความแม่นยำมากเกินไป. |
| **Need OCR confidence** | เข้าถึง `ocrResult.RecognizedWords` และตรวจสอบคุณสมบัติ `Confidence`. | ช่วยให้คุณทำเครื่องหมายคำที่ความมั่นใจต่ำเพื่อการตรวจสอบด้วยมือ. |

## เคล็ดลับประสิทธิภาพ

- **Reuse the `OcrEngine`** เมื่อประมวลผลชุดไฟล์ – มันแคชข้อมูลภาษา.  
- **Parallelize** ขั้นตอนการรับรู้ด้วย `Parallel.ForEach` หากคุณใช้เครื่องหลายคอร์, แต่ให้การเขียน PDF เป็นแบบต่อเนื่องเพื่อหลีกเลี่ยงความขัดแย้งในการเข้าถึงไฟล์.  
- **Tune `ImageQuality`**: 85‑90 ให้ภาพใกล้เคียงไม่มีการสูญเสีย, ส่วน 60‑70 มักเพียงพอสำหรับเอกสารที่มีข้อความเป็นส่วนใหญ่.

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **create searchable pdf** จากภาพโดยใช้ Aspose.OCR พร้อมทั้งเรียนรู้วิธี **compress pdf images**, **embed fonts pdf**, และ **recognize text image** อย่างมีประสิทธิภาพ ตัวอย่างโค้ดเต็มพร้อมใช้งานในโปรเจกต์ C# ใดก็ได้ และเคล็ดลับเพิ่มเติมจะช่วยให้คุณปรับโซลูชันให้เหมาะกับงานที่ใหญ่ขึ้นหรือภาษาต่างๆ.

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเพิ่มลายน้ำ, ผสานหลาย PDF ที่ searchable, หรือรวมขั้นตอนนี้เข้ากับเว็บ API เพื่อให้ผู้ใช้อัปโหลดสแกนและรับ PDF ที่ searchable ทันที ความเป็นไปได้ไม่มีที่สิ้นสุด และด้วยพื้นฐานที่พร้อมคุณจะพบว่าการขยาย workflow เป็นเรื่องง่าย.

ขอให้เขียนโค้ดอย่างสนุกสนาน และขอให้ PDF ของคุณเล็ก, searchable, และแสดงผลอย่างสมบูรณ์!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}