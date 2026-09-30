---
category: general
date: 2026-01-01
description: วิธีทำ OCR แบบเป็นชุดโดยใช้ Aspose OCR Engine ใน C# เรียนรู้การจดจำข้อความจากภาพและการสกัดข้อความจากไฟล์
  TIFF ด้วยการเร่งความเร็วด้วย GPU
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: th
og_description: วิธีทำ OCR แบบกลุ่มใน C# ด้วย Aspose OCR Engine คู่มือนี้จะแสดงวิธีการจดจำข้อความจากภาพและสกัดข้อความจากไฟล์
  TIFF อย่างมีประสิทธิภาพ
og_title: วิธีทำ OCR แบบเป็นชุดใน C# – คู่มือ Aspose ฉบับสมบูรณ์
tags:
- OCR
- C#
- Aspose
- GPU
title: วิธีทำ OCR แบบแบตช์ใน C# ด้วย Aspose OCR Engine
url: /th/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน C# ด้วย Aspose OCR Engine

เคยสงสัย **วิธีทำ batch OCR** เมื่อคุณมีเอกสารสแกนหลายสิบไฟล์อยู่ในโฟลเดอร์หรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องย้ายจากการจดจำภาพเดียวไปสู่การประมวลผลคอลเลกชันทั้งหมด ข่าวดีคือ Aspose OCR ทำให้เรื่องนี้ง่ายดาย ไม่ว่าจะรันบน CPU หรือใช้ประโยชน์จากการเร่งความเร็วด้วย GPU.

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่ง **จดจำข้อความจากภาพ** และแม้กระทั่ง **ดึงข้อความจากไฟล์ TIFF** เป็นชุดใหญ่ ไม่ต้องพึ่งพา “ดูเอกสาร” แบบคลุมเครือ—เพียงโซลูชันที่ทำงานอิสระที่คุณสามารถคัดลอก‑วางและรันได้ทันที

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ตั้งเป้าหมายที่ .NET 6 แต่ .NET 5 ก็ทำงานได้เช่นกัน).
* แพคเกจ NuGet Aspose.OCR สำหรับ .NET (มีทั้งเวอร์ชัน CPU และ GPU; ติดตั้งเวอร์ชันที่ตรงกับฮาร์ดแวร์ของคุณ).
* โฟลเดอร์ที่มีไฟล์ตัวอย่าง TIFF หรือ PNG จำนวนไม่กี่ไฟล์ที่คุณต้องการประมวลผล.
* Visual Studio 2022 หรือ IDE ใดก็ได้ที่คุณชอบ.

> **เคล็ดลับ:** หากคุณวางแผนใช้เวอร์ชัน GPU ให้ตรวจสอบว่าไดรเวอร์กราฟิกของคุณเป็นเวอร์ชันล่าสุดและ CUDA 11+ ได้ติดตั้งแล้ว. เอนจินจะสลับกลับไปใช้ CPU อัตโนมัติหากไม่พบ GPU ที่เข้ากันได้.

## ขั้นตอนที่ 1 – ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

### H2: สร้าง Console App ใหม่และเพิ่ม Aspose.OCR

เปิดเทอร์มินัล (หรือ Package Manager Console ใน Visual Studio) แล้วรัน:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

หากคุณมีไลเซนส์ที่รองรับ GPU ให้เพิ่มแพคเกจ GPU แทน:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

เท่านี้—โปรเจกต์ของคุณจะอ้างอิงไลบรารี OCR ที่เราจะใช้สำหรับ **batch OCR**.

## ขั้นตอนที่ 2 – เริ่มต้น OCR Engine (CPU หรือ GPU)

### H2: วิธีทำ Batch OCR – การเริ่มต้น Engine

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**ทำไมเรื่องนี้สำคัญ:** การสลับ `UseGpu` ทำให้ Aspose ตัดสินใจเส้นทางที่เร็วที่สุด หาก GPU ไม่พร้อมใช้งาน เอนจินจะเปลี่ยนกลับไปใช้ CPU อย่างเงียบ ๆ ทำให้งาน batch ของคุณไม่หยุดทำงานเนื่องจากขาดฮาร์ดแวร์.

## ขั้นตอนที่ 3 – รวบรวมไฟล์ที่ต้องการประมวลผล

### H2: จดจำข้อความจากภาพ – สร้างรายการไฟล์

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**หมายเหตุกรณีขอบ:** หากคุณมีรูปแบบไฟล์ผสมกัน ให้เปลี่ยนรูปแบบการค้นหาเป็น `"*.*"` แล้วกรองตามส่วนขยายภายในลูป วิธีนี้ทำให้ batch มีความยืดหยุ่น.

## ขั้นตอนที่ 4 – ประมวลผลแต่ละภาพและแสดงตัวอย่าง

### H2: ดึงข้อความจาก TIFF – วนลูปผ่านไฟล์

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**สิ่งที่คุณจะเห็น:** สำหรับแต่ละ TIFF คอนโซลจะพิมพ์ข้อความประมาณ:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

ตัวอย่างนี้ยืนยันว่า batch ทำงานสำเร็จโดยไม่ต้องเปิดไฟล์แต่ละไฟล์ด้วยตนเอง.

## ขั้นตอนที่ 5 – บันทึกผลลัพธ์ (ไม่บังคับแต่เป็นประโยชน์)

### H3: เก็บผลลัพธ์ OCR เป็นไฟล์ข้อความ

หากคุณต้องการข้อความเต็มสำหรับการประมวลผลต่อไป ให้เพิ่มโค้ดนี้ภายในลูป `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

ตอนนี้แต่ละไฟล์ TIFF จะมีไฟล์ `.txt` คู่ที่บรรจุผลลัพธ์ OCR ทั้งหมด—เหมาะสำหรับการทำดัชนี การค้นหา หรือป้อนเข้าสู่โมเดลภาษา.

## ขั้นตอนที่ 6 – รันเดโมและตรวจสอบ

1. สร้างโปรเจกต์: `dotnet build`.
2. เรียกใช้: `dotnet run --project GpuBatchDemo.csproj`.

คุณควรเห็นบรรทัดตัวอย่างที่พิมพ์บนคอนโซล และ (หากคุณเพิ่มขั้นตอนเสริม) ไฟล์ `.txt` ชุดหนึ่งอยู่ข้างไฟล์ภาพต้นฉบับ.

### H3: ปัญหาที่พบบ่อยและวิธีแก้

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|-------------------|--------|
| **`ocrResult.Text` ว่าง** | ภาพมืดเกินไปหรือ DPI ต่ำ | ทำการประมวลผลล่วงหน้าภาพ (เพิ่มคอนทราสต์, ขยายขนาด) หรือกำหนด `ocrEngine.Settings.PreprocessImage = true`. |
| **ข้อผิดพลาด GPU “CUDA driver version is insufficient”** | ไดรเวอร์ล้าสมัย | อัปเดตไดรเวอร์ GPU หรือกำหนด `UseGpu = false` เพื่อบังคับใช้ CPU. |
| **ข้อยกเว้น “File not found”** | ตัวคั่นเส้นทางไม่ถูกต้องบน Linux/macOS | ใช้ `Path.Combine` หรือเครื่องหมายทับหน้า (`/`). |

## ขั้นตอนที่ 7 – ขยายขนาด (เกินกว่าจำนวนไฟล์เล็กน้อย)

เมื่อคุณย้ายจากจำนวน TIFF เพียงไม่กี่ไฟล์ไปสู่หลายพันไฟล์ ให้พิจารณา:

* **การประมวลผลแบบขนาน:** ห่อ `foreach` ด้วย `Parallel.ForEach` (ตรวจสอบว่าอินสแตนซ์ของ engine ปลอดภัยต่อเธรด; หากไม่เช่นนั้นให้สร้างหนึ่งอินสแตนซ์ต่อเธรด).
* **I/O แบบแบ่งเป็นชั้น:** อ่านภาพเป็นชุดเพื่อหลีกเลี่ยงการใช้ RAM จนเต็ม.
* **การบันทึก:** เขียนความคืบหน้าไปยังไฟล์ล็อก; ช่วยให้สามารถทำต่อหลังจากการล่ม.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **จำไว้:** หน่วยความจำ GPU ถูกแชร์กัน ดังนั้นการสร้างงาน GPU ขนานมากเกินไปอาจทำให้ช้าลง ทดสอบด้วยจำนวนเธรดไม่กี่ตัวก่อน.

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

การรันโปรแกรมนี้จะ **จดจำข้อความจากภาพ**, **ดึงข้อความจาก TIFF**, และสาธิต **วิธีทำ batch OCR** อย่างมีประสิทธิภาพ.

## สรุป

ตอนนี้คุณมีตัวอย่างครบวงจรของ **วิธีทำ batch OCR** ใน C# ด้วยเอ็นจิน OCR ของ Aspose. บทแนะนำครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโปรเจกต์, การสลับการเร่งความเร็วด้วย GPU, การสร้างรายการไฟล์, การประมวลผลแต่ละภาพ, และการบันทึกผลลัพธ์ ไม่ว่าคุณจะดึงข้อความจากไฟล์ TIFF หรือรูปแบบภาพอื่น ๆ รูปแบบเดียวกันก็ใช้ได้—เพียงเปลี่ยนส่วนขยายไฟล์.

พร้อมก้าวต่อไปหรือยัง? ลองผสานผลลัพธ์ OCR กับดัชนีการค้นหา, ป้อนข้อความเข้าสู่โมเดลภาษาใหญ่, หรือทดลองประมวลผลแบบขนานเพื่อประหยัดหลายนาทีจาก batch ขนาดใหญ่. ไม่มีขีดจำกัด, และคุณมีพื้นฐานที่จะต่อยอด.

มีคำถามหรืออยากแชร์เทคนิค batch‑OCR ของคุณ? แสดงความคิดเห็นด้านล่าง—ขอให้เขียนโค้ดอย่างสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}