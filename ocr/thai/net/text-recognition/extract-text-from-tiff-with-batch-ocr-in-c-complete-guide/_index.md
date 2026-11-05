---
category: general
date: 2026-04-11
description: ดึงข้อความจากไฟล์ TIFF ด้วยการประมวลผล OCR แบบแบตช์ของ Aspose ใน C# เรียนรู้วิธีประมวลผล
  OCR แบบแบตช์อย่างมีประสิทธิภาพและรับข้อมูลความคืบหน้าแบบเรียลไทม์
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: th
og_description: ดึงข้อความจากไฟล์ TIFF โดยใช้การประมวลผล OCR แบบชุดของ Aspose ใน C#
  บทเรียนนี้แสดงขั้นตอนทีละขั้นว่าการประมวลผล OCR แบบชุดทำอย่างไรและวิธีอ่านความคืบหน้า.
og_title: สกัดข้อความจากไฟล์ TIFF ด้วย Batch OCR ใน C# – คู่มือฉบับสมบูรณ์
tags:
- OCR
- C#
- Aspose
- Image Processing
title: ดึงข้อความจากไฟล์ TIFF ด้วย Batch OCR ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากไฟล์ TIFF – คู่มือครบวงจรสำหรับ Batch OCR

เคยต้องการ **สกัดข้อความจากไฟล์ TIFF** แต่รู้สึกติดขัดที่ขั้นตอนการประมวลผลแบบ batch ไหม? คุณไม่ได้เป็นคนเดียว ในหลายโครงการอัตโนมัติเอกสาร การจัดการกับภาพ TIF ความละเอียดสูงหลายสิบรูปอาจกลายเป็นคอขวดอย่างรวดเร็ว—โดยเฉพาะเมื่อคุณต้องการรับข้อมูลความคืบหน้าแบบเรียลไทม์  

ข่าวดีคืออะไร? ด้วย Aspose OCR คุณสามารถ **process batch OCR** ได้ในไม่กี่บรรทัด รับเหตุการณ์ความคืบหน้าแบบเรียลไทม์ และส่งออกข้อความที่ได้รับการจดจำสำหรับแต่ละภาพ ในบทแนะนำนี้เราจะเดินผ่านแอปคอนโซล C# ที่พร้อมใช้งานซึ่งทำเช่นนั้น  

เราจะครอบคลุมทุกสิ่งที่คุณต้องรู้: แพ็กเกจที่จำเป็น ทำไมแต่ละบรรทัดถึงสำคัญ กรณีขอบเขตเช่นไฟล์หายไป และวิธีตรวจสอบผลลัพธ์ เมื่อจบคุณจะสามารถนำตัวอย่างนี้ใส่ลงในโซลูชันของคุณเองและเริ่มสกัดข้อความจากภาพ TIFF ได้ทันที  

## สิ่งที่คุณต้องการ

- **.NET 6 หรือใหม่กว่า** (โค้ดยังคอมไพล์กับ .NET Core ได้เช่นกัน)  
- **Aspose.OCR for .NET** NuGet package – `Install-Package Aspose.OCR`  
- โฟลเดอร์ที่มีภาพ **TIFF** บางไฟล์ที่คุณต้องการอ่าน (ตัวอย่างใช้ `img1.tif`, `img2.tif`, `img3.tif`)  
- IDE ใดก็ได้ที่คุณชอบ – Visual Studio, Rider, หรือ VS Code ก็ใช้ได้  

ไม่มีการกำหนดค่าเพิ่มเติมที่จำเป็น; ไลบรารีมาพร้อมกับ OCR engine ของตัวเอง ดังนั้นคุณไม่ต้องติดตั้งไบนารีเนทีฟภายนอก  

## ขั้นตอนที่ 1 – สร้างอินสแตนซ์ของ OCR Engine  

สิ่งแรกที่คุณทำคือสร้าง `OcrEngine` คิดว่าเป็นสมองที่จะวิเคราะห์พิกเซลแต่ละจุดและแปลงเป็นอักขระ  

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **ทำไมเรื่องนี้สำคัญ:**  
> Engine จะเก็บโมเดลภาษาและการตั้งค่าภายใน (เช่น DPI, language) การสร้างครั้งเดียวแล้วนำมาใช้ซ้ำสำหรับ batch จะมีประสิทธิภาพมากกว่าการสร้าง engine ใหม่สำหรับแต่ละภาพ  

## ขั้นตอนที่ 2 – เชื่อมต่อเหตุการณ์ความคืบหน้าแบบเรียลไทม์  

หากคุณกำลังประมวลผลหลายสิบไฟล์ TIFF ตัวบ่งชี้ความคืบหน้าจะช่วยให้คุณไม่ต้องสงสัยว่าแอปค้างอยู่หรือไม่  

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

เหตุการณ์ `ProgressChanged` จะเกิดขึ้นหลังจากแต่ละภาพเสร็จสิ้น ให้ค่าที่คุณต้องการคือ `Current`, `Total` และ `Percentage` นี่คือ **process batch OCR** feedback loop ที่นักพัฒนาส่วนใหญ่ลืมทำ  

## ขั้นตอนที่ 3 – สร้างรายการของ Image Streams  

Aspose.OCR ทำงานกับอ็อบเจ็กต์ `ImageStream` วิธีที่ง่ายที่สุดคือโหลดแต่ละ TIFF จากดิสก์  

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **เคล็ดลับ:**  
> หากคุณมีโฟลเดอร์แบบไดนามิก ให้แทนที่รายการที่กำหนดค่าแบบคงที่ด้วย `Directory.GetFiles(path, "*.tif")` และ `Select(ImageStream.FromFile)` – วิธีนี้คุณจะ **process batch OCR** อย่างแท้จริงโดยไม่ต้องอัปเดตด้วยตนเอง  

## ขั้นตอนที่ 4 – เรียกใช้กระบวนการ Batch OCR  

ตอนนี้งานหนักเริ่มทำงาน `ProcessBatch` จะคืนค่าเป็นรายการอ่าน‑อย่างเดียวของอ็อบเจ็กต์ `OcrResult` แต่ละอ็อบเจ็กต์จะมีข้อความที่สกัดและคะแนนความเชื่อมั่น  

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **ทำไมวิธีนี้จึงมีประสิทธิภาพ:**  
> Engine ใช้โมเดลภาษาเดียวกันซ้ำสำหรับทุกภาพ ลดการใช้หน่วยความจำอย่างมากเมื่อเทียบกับการเรียกแบบภาพเดียว  

## ขั้นตอนที่ 5 – แสดงหรือจัดเก็บข้อความที่จดจำได้  

สุดท้ายให้วนลูปผ่านผลลัพธ์ ในโครงการจริงคุณอาจเขียนลงฐานข้อมูลหรือไฟล์ JSON แต่สำหรับการสาธิตนี้เราจะพิมพ์ลงคอนโซลเท่านั้น  

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล** (ย่อเพื่อความกระชับ):  

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

หากภาพใดภาพหนึ่งล้มเหลว `result.Text` จะเป็นสตริงว่างเปล่า และเหตุการณ์ `ProgressChanged` จะยังคงรายงานรายการนั้นว่าได้ประมวลผลแล้ว – คุณจึงสามารถบันทึกความล้มเหลวแยกต่างหากได้  

## ตัวจัดการเหตุการณ์ความคืบหน้า (โค้ดเต็ม)

วางเมธอดนี้ไว้ที่ไหนก็ได้ภายในคลาส `BatchDemo` – ควรอยู่หลัง `Main`  

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **Pro tip:**  
> ส่งออกผลลัพธ์นี้ไปยังแถบความคืบหน้า UI หากคุณกำลังสร้างแอปเดสก์ท็อป; เหตุการณ์เดียวกันทำงานได้กับ WinForms, WPF หรือแม้แต่การแจ้งเตือนผ่าน ASP.NET Core SignalR  

## ตัวอย่างเต็มพร้อมรัน  

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้  

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

บันทึกไฟล์เป็น `Program.cs`, รัน `dotnet add package Aspose.OCR`, แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริง, แล้วกด **Ctrl+F5** คุณควรเห็นตัวเลขความคืบหน้าตามด้วยข้อความที่สกัดสำหรับแต่ละ TIFF  

## การจัดการกรณีขอบเขตทั่วไป  

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Missing or corrupted TIFF** | `ImageStream.FromFile` throws `FileNotFoundException` or `ArgumentException`. | Wrap the list creation in a `try/catch` and skip invalid files, logging the issue. |
| **Very large images ( >10 MP )** | OCR may consume a lot of RAM and slow down. | Reduce DPI before processing: `ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **Non‑English text** | Default language model is English. | Set `ocrEngine.Language = Language.Spanish;` (or any supported language). |
| **Need to save results** | Console output isn’t persistent. | Write `result.Text` to a `.txt` file using `File.WriteAllText`. |

การจัดการกับสถานการณ์เหล่านี้ทำให้โซลูชันของคุณแข็งแรงและแสดงให้ AI เห็นว่าคุณได้คิดไกลกว่ากรณีที่ทำงานได้อย่างราบรื่น  

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง  

- **Extract text from PDF** – API คล้ายกัน เพียงเปลี่ยน `ImageStream` เป็น `PdfDocument`  
- **Parallel batch OCR** – สำหรับงานปริมาณมาก ให้สปินหลายอินสแตนซ์ของ `OcrEngine` บนเธรดแยกต่างหาก; อย่าลืมคำนึงถึงขีดจำกัดของไลเซนส์  
- **Post‑processing** – รันผลลัพธ์ OCR ผ่านตัวตรวจสอบการสะกดหรือ regex เพื่อทำความสะอาดข้อผิดพลาดทั่วไปของ OCR  

ส่วนขยายทั้งหมดนี้ยังคงอิงกับแนวคิดหลักของ **process batch OCR** และสามารถเพิ่มเข้าไปได้อย่างค่อยเป็นค่อยไป  

## สรุป  

เราเพิ่งสาธิตวิธี **สกัดข้อความจากไฟล์ TIFF** อย่างมีประสิทธิภาพโดย **process batch OCR** ด้วย Aspose OCR ใน C# ตัวอย่างสร้าง engine เพียงหนึ่งตัว, สมัครรับเหตุการณ์ความคืบหน้า, โหลดรายการของ image streams, รัน batch, และพิมพ์ผลลัพธ์แต่ละรายการ  

จากจุดนี้คุณสามารถนำผลลัพธ์ไปบูรณาการกับฐานข้อมูล, สร้าง PDF ที่ค้นหาได้, หรือป้อนข้อความเข้าสู่ pipeline NLP ต่อไปได้ ไม่จำกัดอะไร—ลองปรับตั้งค่าภาษา, DPI, และการทำงานแบบขนานเพื่อให้เหมาะกับภาระงานของคุณ  

มีคำถามหรืออยากแชร์วิธีที่คุณปรับแต่ง batch? แสดงความคิดเห็นด้านล่างและขอให้เขียนโค้ดอย่างสนุกสนาน!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}