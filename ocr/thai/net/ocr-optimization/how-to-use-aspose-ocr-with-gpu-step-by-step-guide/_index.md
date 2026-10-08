---
category: general
date: 2026-02-09
description: วิธีใช้ Aspose OCR พร้อมการเร่งความเร็วด้วย GPU ใน C#. เรียนรู้การจดจำข้อความจากไฟล์
  jpg, การสกัดข้อความจากภาพ, และการเปิดใช้งาน GPU ในเวลาเพียงไม่กี่นาที.
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: th
og_description: วิธีใช้ Aspose OCR กับ GPU ใน C# คู่มือนี้จะแสดงวิธีการจดจำข้อความจากไฟล์
  JPG และสกัดข้อความจากภาพโดยใช้การเร่งความเร็วด้วย GPU.
og_title: วิธีใช้ Aspose OCR กับ GPU – คู่มือการเขียนโปรแกรมแบบครบถ้วน
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: วิธีใช้ Aspose OCR กับ GPU – คู่มือขั้นตอนโดยละเอียด
url: /th/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose OCR กับ GPU – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้องประมวลผลกองใบแจ้งหนี้ที่สแกนหลายแผ่นอย่างรวดเร็ว แต่ CPU ทำงานช้าอยู่หรือไม่? นั่นคือปัญหาที่พบบ่อยเมื่อคุณพยายาม **how to use aspose** สำหรับ OCR ในระดับใหญ่ ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างจริงที่แสดง **how to use aspose** เพื่อจดจำข้อความจากไฟล์ jpg, ดึงข้อความจากรูปภาพ, และใช้ประโยชน์จาก GPU อย่างเต็มที่

คิดว่าเป็นการเดินผ่านแบบพักกาแฟ—ไม่มีส่วนเกิน เพียงขั้นตอนที่คุณสามารถคัดลอก‑วางลงใน Visual Studio แล้วดูผลลัพธ์ที่น่าตื่นเต้น เมื่อเสร็จคุณจะได้แอปคอนโซล C# ที่ทำงานได้บนเครื่อง Windows สมัยใหม่ใด ๆ ที่มี GPU ของ NVIDIA หรือ AMD

![วิธีใช้ Aspose OCR กับ GPU](/images/aspose-gpu-example.png)

## สิ่งที่คุณต้องการ

- **.NET 6.0** (หรือใหม่กว่า) – โค้ดนี้ตั้งเป้าหมายที่ .NET 6 แต่ทำงานได้กับ .NET 5 และ .NET Framework 4.8 ด้วยการปรับแต่งเล็กน้อย
- **Aspose.OCR for .NET** NuGet package – ติดตั้งโดยใช้ `dotnet add package Aspose.OCR`
- เครื่องที่ **GPU‑enabled** – บทแนะนำนี้แสดงวิธี **how to enable gpu** และ **how to set gpu** ขีดจำกัดหน่วยความจำของ GPU แต่โค้ดจะสลับไปใช้ CPU อย่างราบรื่นหากไม่พบ GPU ที่เข้ากันได้
- รูปภาพเช่น `invoice_01.jpg` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้

มีครบหรือยัง? ดีมาก, มาเริ่มกันเลย

## วิธีใช้ Aspose OCR กับ GPU – การตั้งค่าเริ่มต้น

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ OCR engine และบอกให้ใช้ GPU ขั้นตอนนี้สำคัญมาก เพราะหากไม่ได้ตั้งค่าสถานะนี้ Aspose จะใช้การประมวลผลด้วย CPU ซึ่งทำให้ประสิทธิภาพที่เราต้องการหายไป

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**ทำไมจึงสำคัญ:** การเปิดใช้ GPU จะย้ายคอร์การประมวลผลภาพที่หนักไปยังกราฟิกโปรเซสเซอร์ ซึ่งเร็วกว่า CPU ประมาณ 10‑20× สำหรับภาพขนาดใหญ่ `GpuMemoryLimit` เป็นวาล์วความปลอดภัย; ตั้งค่าเป็น 1024 MB จะทำงานได้ดีกับการ์ดระดับกลางส่วนใหญ่พร้อมกับทำให้แอปตอบสนองได้ดี

> **เคล็ดลับ:** หากคุณรันแอปบนเครื่องที่ไม่มี GPU ที่เข้ากันได้ Aspose จะสลับไปใช้โหมด CPU อัตโนมัติและบันทึกคำเตือน ไม่เกิดการขัดข้อง เพียงแค่รันช้าลงเท่านั้น

## Recognize Text from JPG – Loading the Image

ตอนนี้ engine พร้อมแล้ว เราต้องป้อนภาพให้มัน ตัวอย่างใช้ JPEG เพราะ **recognize text from jpg** เป็นสถานการณ์ทั่วไปสำหรับใบแจ้งหนี้, ใบเสร็จ, และหนังสือเดินทาง

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**ทำไมต้องตรวจสอบไฟล์:** ไฟล์หายเป็นสาเหตุที่พบบ่อยที่สุดของข้อผิดพลาดระหว่างรันในตัวอย่างสั้น ๆ การจัดการล่วงหน้าจะทำให้บทแนะนำนี้เป็นมิตรต่อผู้เริ่มต้น

## Extract Text from Image – Running the OCR Engine

เมื่อมีภาพในมือ ขั้นตอนต่อไปคือการรันกระบวนการ OCR นี่คือจุดที่ Aspose ทำงานหนักและคืนค่าอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความธรรมดา, คะแนนความเชื่อมั่น, และแม้แต่ bounding box หากคุณต้องการใช้ในภายหลัง

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**สิ่งที่คุณจะเห็น:** คอนโซลจะแสดงอักขระดิบที่ Aspose ตรวจจับได้ สำหรับใบแจ้งหนี้ที่สะอาด คุณอาจได้ผลลัพธ์ประมาณนี้:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน คุณอาจต้องปรับคุณภาพของภาพหรือเปิดใช้งานตัวเลือกการเตรียมล่วงหน้าเพิ่มเติม (เช่น deskew, binarization) สิ่งเหล่านี้อยู่นอกขอบเขตของคู่มือสั้น ๆ นี้แต่มีเอกสารอธิบายใน API ของ Aspose

## How to Enable GPU – Configuring the Engine

คุณอาจสงสัย **how to enable gpu** สำหรับ Aspose หากพลาดขั้นตอนแรก คำตอบคือการสลับฟล็อก `UseGpu` ในอ็อบเจ็กต์การตั้งค่าของ engine ตามที่แสดงไว้ก่อนหน้านี้ นี่คือโค้ดสั้น ๆ ที่คุณสามารถวางลงในโปรเจกต์ใด ๆ ก็ได้

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

เบื้องหลัง Aspose จะโหลดไลบรารี CUDA/OpenCL ที่ตรงกับฮาร์ดแวร์ของคุณ หาก runtime ไม่พบไลบรารีเหล่านั้น จะบันทึกคำเตือนและสลับไปใช้ CPU ไม่ต้องทำการติดตั้งเพิ่มเติมสำหรับ Windows ส่วนใหญ่

## How to Set GPU – Fine‑Tuning Memory Usage

บางครั้งคุณอาจเจอข้อผิดพลาด “out of memory” บน GPU ระดับต่ำ นี่คือจุดที่ **how to set gpu** ขีดจำกัดหน่วยความจำมีประโยชน์ คุณสมบัติ `GpuMemoryLimit` รับค่าจำนวนเต็มเป็นเมกะไบต์

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**เมื่อใดควรปรับ:** หากคุณประมวลผลหลายภาพพร้อมกัน ให้ลดขีดจำกัดเพื่อไม่ให้การ์ดเต็มเกินไป ในทางกลับกัน หากคุณใช้เวิร์กสเตชันที่มี VRAM 8 GB คุณสามารถเพิ่มค่าได้ถึง 4096 MB เพื่อเร่งการประมวลผลเป็นชุด

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมสมบูรณ์ที่คุณสามารถคัดลอกไปสร้างโปรเจกต์คอนโซลใหม่ (`dotnet new console`) ได้ รวมทุกส่วนที่เราได้พูดถึงแล้ว พร้อมการจัดการข้อผิดพลาดเล็กน้อยเพื่อความทนทาน

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรัน `dotnet run` คอนโซลจะพิมพ์ข้อความดิบที่ดึงจาก `invoice_01.jpg` หากภาพมีข้อความพิมพ์ที่ชัดเจน ผลลัพธ์จะเกือบเหมือนกับเอกสารต้นฉบับ

## ปัญหาที่พบบ่อย & วิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้เร็ว |
|-------|--------|-------------|
| **GPU not detected** | ไดรเวอร์ CUDA หายหรือ GPU ไม่รองรับ | ติดตั้งไดรเวอร์ NVIDIA/AMD ล่าสุด; ตรวจสอบด้วย `nvidia-smi` หรือคำสั่งเทียบเท่า |
| **Out‑of‑memory error** | `GpuMemoryLimit` สูงเกินกว่าการ์ดจะรับได้ | ลดขีดจำกัดลงเหลือ 512 MB หรือ น้อยกว่า |
| **Garbage output** | JPG ความละเอียดต่ำหรือบีบอัดหนัก | ใช้ภาพต้นฉบับคุณภาพสูงขึ้นหรือเปิด `ocrEngine.Preprocessing.Deskew = true` |
| **Null `ocrResult`** | การโหลดสตรีมภาพล้มเหลว | ตรวจสอบเส้นทางไฟล์อีกครั้งและให้แน่ใจว่าไฟล์ไม่ถูกล็อก |

การจัดการปัญหาเหล่านี้ล่วงหน้าจะช่วยคุณหลีกเลี่ยงการตามรอย stack trace ที่ซับซ้อนได้ในภายหลัง

## ขั้นตอนต่อไป

ตอนนี้คุณได้เชี่ยวชาญ **how to use aspose** สำหรับ OCR เร็วแล้ว คุณอาจอยากสำรวจต่อ:

- **Batch processing** – วนลูปผ่านไดเรกทอรีของ JPGs และบันทึกผลลัพธ์แต่ละไฟล์เป็นไฟล์ `.txt`
- **Structured extraction** – ใช้ `ocrResult.Regions` เพื่อรับ bounding box และดึงฟิลด์เฉพาะ เช่น หมายเลขใบแจ้งหนี้
- **Hybrid CPU/GPU mode** – ใช้ CPU สำหรับภาพขนาดเล็กและสลับไปใช้ GPU เฉพาะไฟล์ขนาดใหญ่เพื่อสมดุลความเร็วและหน่วยความจำ

ส่วนขยายทั้งหมดนี้สร้างบนพื้นฐานเดียวกันที่คุณเพิ่งตั้งค่าเสร็จ และเป็นหัวข้อที่ยอดเยี่ยมสำหรับการผจญภัยในบทแนะนำครั้งต่อไปของคุณ

---

*Happy coding! หากคุณเจออุปสรรคใด ๆ ฝากคอมเมนต์ด้านล่างหรือแจ้งในฟอรั่มชุมชน Aspose GPU พร้อมแล้ว — มาทำ OCR ให้เร็วเหมือนสายฟ้า*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}