---
category: general
date: 2026-03-23
description: สร้างไฟล์ PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose OCR. เรียนรู้วิธีแปลงไฟล์
  TIFF เป็น PDF ด้วยการบีบอัดสูงและจดจำข้อความในภาพภายในไม่กี่นาที.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Aspose OCR บทเรียนนี้แสดงวิธีแปลง
  TIFF เป็น PDF เพิ่มชั้นข้อความที่ค้นหาได้ และใช้การบีบอัดสูง
og_title: สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- PDF generation
title: สร้าง PDF ที่ค้นหาได้จากภาพ – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คู่มือ C# ฉบับสมบูรณ์

เคยต้อง **สร้าง searchable pdf** จากเอกสารสแกนแต่ไม่รู้จะเริ่มอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อต้องแปลง TIFF สแกนเป็น PDF ที่ค้นหาได้ ข่าวดีคือ ด้วย Aspose OCR คุณสามารถ **convert tiff to pdf**, ใส่ชั้นข้อความซ่อนบนภาพ, และแม้กระทั่งบีบอัดไฟล์ด้วยตัวเลือก **high compression pdf**, ทั้งหมดในไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การติดตั้งแพ็กเกจ NuGet ที่จำเป็น, โหลดภาพ TIFF, ทำการจดจำข้อความ, และสุดท้ายส่งออกเป็น PDF ที่ค้นหาได้. เมื่อเสร็จคุณจะได้แอปคอนโซลที่ **recognize image text** และสร้าง PDF ที่กะทัดรัด, ค้นหาได้ พร้อมสำหรับการทำดัชนี. ไม่ต้องใช้เครื่องมือเพิ่มเติม, ไม่ต้องทำ OCR ด้วยตนเอง—แค่โค้ดสะอาดและคำอธิบายสั้น ๆ.

## ข้อกำหนดเบื้องต้น & สิ่งที่คุณต้องมี

- **.NET 6+** (หรือ .NET Framework 4.6+). API ทำงานได้ทั้งสอง, แต่ .NET 6 มีการปรับปรุง runtime ล่าสุด.  
- **Visual Studio 2022** หรือ IDE ใดก็ได้ที่คุณชอบ.  
- แพ็กเกจ NuGet **Aspose.OCR** และ **Aspose.OCR.Gpu** (แพ็กเกจ GPU เป็นตัวเลือกเสริมที่ช่วยเร่งการจดจำบนฮาร์ดแวร์ที่รองรับ).  
- ไฟล์ TIFF ตัวอย่าง (เช่น `invoice.tif`) ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม.  

หากคุณมีทั้งหมดแล้ว, ดำเนินต่อไป. หากยังไม่มี, ขั้นตอนการติดตั้งด้านล่างจะครอบคลุมทุกอย่าง.

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ Aspose OCR

เริ่มต้นโดยเปิดโฟลเดอร์โปรเจกต์ของคุณในเทอร์มินัลและรัน:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

คำสั่งเหล่านี้จะดึงเอาเอนจิน OCR หลักและไลบรารีเร่งความเร็วด้วย GPU. ส่วน GPU ไม่ได้บังคับใช้; หากไม่พบ GPU ที่รองรับ เอนจินจะสลับไปใช้โหมด CPU.

> **เคล็ดลับ:** เมื่อทำงานในสภาพแวดล้อมการผลิต, ให้ล็อคเวอร์ชันแพ็กเกจใน `csproj` เพื่อหลีกเลี่ยงการเปลี่ยนแปลงที่ทำให้โค้ดพังโดยไม่คาดคิด.

## ขั้นตอนที่ 2: ตั้งค่า Skeleton ของโปรเจกต์

สร้างแอปคอนโซลใหม่ (หากคุณยังไม่มี):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

แทนที่ `Program.cs` ที่สร้างอัตโนมัติด้วยโค้ดเต็มที่จะแสดงต่อไป. โปรแกรมจะ:

1. Initialise an `OcrEngine` with GPU support.  
2. Load the TIFF image.  
3. Run OCR and abort gracefully on failure.  
4. Configure **PdfExportOptions** for a searchable layer and **high compression**.  
5. Write the output file.

## ขั้นตอนที่ 3: เขียนโค้ดเต็ม (Full Example)

ด้านล่างเป็นไฟล์ซอร์ส **ทั้งหมด**. คัดลอก‑วางลงใน `Program.cs`. คอมเมนต์อธิบาย “ทำไม” ของแต่ละบรรทัด, ไม่ใช่แค่ “ทำอะไร”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **GPU acceleration** สามารถลดเวลาการจดจำจากวินาทีเป็นมิลลิวินาทีบนการ์ดสมัยใหม่—เหมาะสำหรับการประมวลผลจำนวนมาก.  
- **IncludeTextLayer** ฝังข้อความที่ได้จาก OCR ไว้เป็นชั้นซ่อน, ทำให้โปรแกรมอ่าน PDF สามารถค้นหาเอกสารได้โดยไม่เปลี่ยนแปลงลักษณะภาพ.  
- **High compression** ใช้การบีบอัด Flate (ZIP) กับสตรีมภาพ, ซึ่งเป็นการบีบอัดแบบ lossless แต่ลดขนาดไฟล์ได้อย่างมาก—เหมาะสำหรับการเก็บสำเนาใบแจ้งหนี้หลายพันฉบับ.

## ขั้นตอนที่ 4: รันแอปและตรวจสอบผลลัพธ์

เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์และรัน:

```bash
dotnet run
```

หากทุกอย่างตั้งค่าอย่างถูกต้อง, คุณจะเห็น:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

เปิด `invoice.pdf` ด้วยโปรแกรมอ่าน PDF ใดก็ได้ (Adobe Acrobat, Edge, หรือแม้กระทั่งเบราว์เซอร์). ลองค้นหาคำที่คุณรู้ว่ามีใน TIFF ต้นฉบับ—เช่น “Total”. ตัวอ่านควรไฮไลต์คำนั้นแม้ว่าจะเป็นส่วนของภาพ. นั่นคือสัญญาณของ **searchable pdf**.

### ขนาดไฟล์ที่คาดหวัง

ใบแจ้งหนี้สแกนทั่วไป (≈300 KB TIFF) มักจะลดลงเป็น **≈80 KB** หลังจากใช้ `PdfCompression.High`. ขนาดที่แน่นอนขึ้นอยู่กับความซับซ้อนของภาพ, แต่คุณจะเห็นการลดลงอย่างชัดเจน.

## ขั้นตอนที่ 5: ความแปรผันทั่วไป & กรณีขอบ

| Situation | What to Adjust | Why |
|-----------|----------------|-----|
| **No GPU available** | Change `new OcrEngine(GpuMode.Enabled)` to `new OcrEngine(GpuMode.Disabled)` | Prevents the engine from attempting GPU initialization, which can cause a brief delay. |
| **Multiple pages (multi‑page TIFF)** | Set `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Loads all frames; Aspose will process each page and generate a multi‑page PDF. |
| **Need OCR language other than English** | `ocrEngine.Language = Language.French;` (or any supported language) | Improves accuracy for non‑English documents. |
| **Want a visible text overlay instead of hidden layer** | `pdfExportOptions.IncludeTextLayer = false;` and manually add `TextFragment` objects. | Useful when you want the OCR text to appear as selectable text on top of the image. |
| **Ultra‑small PDFs** | Combine `PdfCompression.High` with `ImageResolution = 150` DPI before recognition. | Lower DPI reduces image data, further shrinking the PDF at the cost of visual fidelity. |

> **Note:** Always test edge cases on a small sample before scaling to production. OCR accuracy can vary with image quality, noise, and language.

## ขั้นตอนที่ 6: เคล็ดลับสำหรับการใช้งานระดับ Production

1. **Error Logging** – Replace `Console.WriteLine` with a proper logging framework (Serilog, NLog) for easier diagnostics.  
2. **Batch Processing** – Wrap the core logic in a method that accepts input/output paths, then iterate over a directory of TIFF files.  
3. **Async I/O** – While Aspose OCR itself is synchronous, loading and saving files can be async to keep UI threads responsive.  
4. **Security** – If you expose this functionality via a web API, validate file paths and limit file sizes to prevent abuse.  
5. **Version Pinning** – Use exact version numbers (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) to guarantee consistent behaviour across builds.

## สรุป

เราตอนนี้ได้สร้าง **โซลูชันครบวงจร** ที่ **create searchable pdf** จากภาพสแกน, **convert tiff to pdf**, และทำได้ด้วยการตั้งค่า **high compression pdf** พร้อมกับ **recognize image text** อย่างแม่นยำ. ผลลัพธ์ **searchable pdf from image** มีน้ำหนักเบา, ค้นหาได้, และพร้อมสำหรับกระบวนการต่อไปเช่นการทำดัชนี, การเก็บถาวร, หรือ e‑discovery.

มีใบแจ้งหนี้หลายชุด? ใส่เมธอดนี้ในลูป, ชี้ไปที่โฟลเดอร์, แล้วให้ Aspose OCR ทำงานหนักให้. อยากทดลองระดับการบีบอัดหรือแพ็คเกจภาษาอื่น? โค้ดเป็นโมดูลาร์พอที่จะสลับตัวเลือกเหล่านั้นได้ในไม่กี่วินาที.

---

*พร้อมจะก้าวต่อ?* ลองเพิ่มลายน้ำ, ฝังเมตาดาต้า, หรือแม้กระทั่งต่อ PDF ที่ผ่านการ OCR หลายไฟล์เข้าด้วยกัน. ชุด Aspose มีส่วนขยายมากมาย—สำรวจเอกสารและต่อเนื่องไป. Happy coding!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}