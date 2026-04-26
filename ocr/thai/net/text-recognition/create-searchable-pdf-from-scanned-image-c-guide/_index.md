---
category: general
date: 2026-04-26
description: สร้างไฟล์ PDF ที่ค้นหาได้จากภาพสแกนโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีแปลงภาพสแกน
  ดึงข้อความ และสร้าง PDF ที่ค้นหาได้อย่างรวดเร็ว.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพสแกนโดยใช้ Aspose OCR. โค้ด C# ทีละขั้นตอนเพื่อแปลง,
  ดึงข้อความ, และสร้าง PDF ที่ค้นหาได้.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพสแกน – คู่มือ C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: สร้าง PDF ที่ค้นหาได้จากภาพสแกน – คู่มือ C#
url: /th/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากภาพสแกน – คำแนะนำ C#

เคยต้อง **สร้าง PDF ที่ค้นหาได้** จากสัญญากระดาษ, ใบเสร็จ, หรือเอกสารเก่า ๆ ไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่มักเจออุปสรรคนี้เมื่อลูกค้าส่งกองไฟล์สแกน TIFF มาและต้องการ PDF ที่ค้นหาได้เป็นผลลัพธ์สุดท้าย  

ในบทเรียนนี้เราจะสาธิต **วิธี OCR เอกสาร** และเปลี่ยนภาพสแกนให้เป็น **PDF ที่ค้นหาได้** ด้วย Aspose OCR for .NET. เมื่อทำตามจนจบแล้วคุณจะสามารถ **แปลงไฟล์ภาพสแกน**, **ดึงข้อความจากภาพ**, และแม้กระทั่งจัดการกับ TIFF หลายหน้าได้โดยไม่ต้องกังวล

## สิ่งที่คุณต้องเตรียม

ก่อนจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (API ทำงานกับ .NET Core, .NET Framework, และ .NET 5+)  
* ใบอนุญาต Aspose OCR ที่ถูกต้อง หรือคุณยินดีใช้เวอร์ชันทดลองพร้อมลายน้ำ  
* ติดตั้งแพคเกจ NuGet `Aspose.OCR` (`dotnet add package Aspose.OCR`)  
* ไฟล์ TIFF ตัวอย่าง (เช่น `contract_scan.tif`) ที่ต้องการแปลงเป็น PDF ที่ค้นหาได้  

เท่านี้—ไม่ต้องใช้ไลบรารีเพิ่มเติม, ไม่ต้องตั้งค่าซับซ้อน พร้อมหรือยัง? ไปกันเลย

![ตัวอย่างการสร้าง PDF ที่ค้นหาได้](create-searchable-pdf.png "ตัวอย่างการสร้าง PDF ที่ค้นหาได้")

## ขั้นตอนที่ 1 – เริ่มต้น OCR Engine (Create Searchable PDF)

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ `OcrEngine`. วัตถุนี้ทำหน้าที่อ่านบิตแมพ, ระบุอักขระ, และส่งคืนข้อความให้คุณ  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**ทำไมต้องตั้งค่าภาษา?**  
หากปล่อยไว้เป็นค่าเริ่มต้น, Aspose จะพยายามตรวจสอบทุกชุดภาษาซึ่งทำให้ช้าลง การระบุ `Language.Latin` จะบอกให้เอนจินโฟกัสที่อักษรละติน, ทำให้เร็วขึ้นและแม่นยำมากขึ้นสำหรับสัญญาที่เป็นภาษาอังกฤษ

## ขั้นตอนที่ 2 – โหลดภาพสแกนของคุณ (Convert Scanned Image)

ต่อไปเราจะส่งภาพให้เอนจินประมวลผล. Aspose รองรับการอ่านจากพาธไฟล์, สตรีม, หรือแม้กระทั่ง `byte[]`. เพื่อความง่ายเราจะใช้ `ImageStream.FromFile`  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

หากคุณต้อง **แปลง TIFF เป็น PDF** ในภายหลัง, จำไว้ว่า TIFF หลายหน้าจะถูกจัดการโดยอัตโนมัติ—แต่ละเฟรมจะกลายเป็นหน้า PDF แยกกัน

## ขั้นตอนที่ 3 – รัน OCR และดึงข้อความ (Extract Text From Image)

การรัน OCR เพียงเรียก `Recognize`. เอนจินจะคืนค่า `RecognitionResult` ที่มีข้อความธรรมดา, คะแนนความเชื่อมั่น, และข้อมูลการจัดวาง  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**เคล็ดลับ:** หากคุณต้องการเพียงข้อความ (ไม่ต้องการ PDF), สามารถหยุดที่นี่และบันทึก `extractedText` ลงไฟล์ `.txt`. แต่ส่วนใหญ่เป้าหมายของเราคือ PDF ที่ค้นหาได้, ดังนั้นเราจะดำเนินต่อ

## ขั้นตอนที่ 4 – บันทึกเป็น PDF ที่ค้นหาได้ (Create Searchable PDF)

Aspose ทำขั้นตอนสุดท้ายให้เรียบง่าย: เพียงเรียก `Save` ด้วย `SaveFormat.PdfSearchable`. ภายในไลบรารีจะฝังข้อความที่ดึงมาเป็นเลเยอร์ที่มองไม่เห็นในขณะที่ยังคงรักษารูปภาพต้นฉบับไว้  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

เมื่อเปิด `contract_searchable.pdf` ด้วยโปรแกรมดู PDF ใด ๆ, คุณจะสามารถเลือก, คัดลอก, และค้นหาข้อความได้—ตรงกับที่ลูกค้าคาดหวังจาก “PDF ที่ค้นหาได้”

## การจัดการ TIFF หลายหน้า (Convert Tiff to PDF)

หากไฟล์ต้นทางของคุณมีหลายหน้า, Aspose จะถือแต่ละเฟรมเป็นหน้าแยกโดยอัตโนมัติ ไม่ต้องเขียนลูปเพิ่ม แต่คุณอาจต้องการกำหนด DPI หรือคุณภาพของภาพสำหรับแต่ละหน้า:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

หลังจากตั้งค่าตัวเลือกเหล่านี้, ทำซ้ำ **ขั้นตอนที่ 2** สำหรับแต่ละเฟรม, หรือเพียงชี้ `ImageStream.FromFile` ไปที่ TIFF หลายหน้าและให้ Aspose จัดการให้

## ข้อผิดพลาดทั่วไปและวิธีแก้

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| ข้อความแสดงเป็นอักขระผิดหรือหายไป | ตั้งค่าภาษาไม่ถูกต้อง | ตั้งค่า `ocrEngine.Language` ให้เป็นชุดภาษาที่ตรงกัน (เช่น `Language.German`) |
| PDF มีขนาดใหญ่ (10 MB สำหรับสแกนหน้าเดียว) | การบีบอัดภาพเริ่มต้นต่ำ | ปรับ `ocrEngine.ImageProcessingOptions.Compression` เป็น `Jpeg` และกำหนดค่า `Quality` ที่เหมาะสม (0‑100) |
| OCR ทำงานช้า | ใช้การตรวจจับภาษาด้วยค่า `Auto` เริ่มต้น | ระบุภาษาที่คาดว่าจะใช้โดยชัดเจน |
| ไม่มีเลเยอร์ที่ค้นหาได้ | บันทึกด้วย `SaveFormat.Pdf` แทน `PdfSearchable` | ใช้ `PdfSearchable` |

## ตัวอย่างครบวงจร (Full End‑to‑End Example)

รวมทุกขั้นตอนเข้าด้วยกัน, นี่คือแอปคอนโซลที่พร้อมรันและคัดลอกไปวางใน Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**สิ่งที่คุณจะเห็น:**  
* หน้าต่างคอนโซลที่พิมพ์ข้อความบางส่วนจาก OCR  
* ไฟล์ `contract_searchable.pdf` อยู่ข้างไฟล์ TIFF ดั้งเดิม เปิดไฟล์, กด **Ctrl + F**, ค้นหาคำใดก็ได้ที่ปรากฏในสแกนต้นฉบับ—สำเร็จแล้ว

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

* **วิธี OCR เอกสารเป็นชุด** – ห่อโค้ดด้านบนในลูป `foreach` เพื่อประมวลผลโฟลเดอร์ทั้งหมด  
* **แปลงรูปแบบภาพสแกนอื่น ๆ** (PNG, JPEG) – API เดียวกันทำงานได้; เพียงเปลี่ยนนามสกุลไฟล์  
* **ดึงข้อความจากภาพเพื่อการวิเคราะห์ต่อ** – ส่ง `result.Text` ไปยัง pipeline การประมวลผลภาษาธรรมชาติ  
* **ปรับขนาด PDF** – สำรวจ `PdfSaveOptions` เพื่อบีบอัดภาพเพิ่มเติมหรือฝังฟอนต์เฉพาะเมื่อจำเป็น  

ลองทำตามไอเดียเหล่านี้, แล้วคุณจะกลายเป็นผู้เชี่ยวชาญที่ทุกคนเรียกหาเมื่อมีคำขอ “แปลงสแกนนี้เป็น PDF ที่ค้นหาได้”

---

### TL;DR

คุณได้เรียนรู้วิธี **สร้าง PDF ที่ค้นหาได้** จากภาพสแกนด้วย Aspose OCR ใน C#. ขั้นตอนคือ: เริ่มต้นเอนจิน, โหลดภาพ, รัน OCR, และบันทึกด้วย `PdfSearchable`. ปรับตั้งค่าภาษา, DPI, และการบีบอัดเพื่อจัดการกรณีพิเศษ, แล้วคุณก็พร้อม **แปลงภาพสแกน**, **ดึงข้อความจากภาพ**, และแม้กระทั่ง **แปลง TIFF เป็น PDF** ในระดับใหญ่แล้ว. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}