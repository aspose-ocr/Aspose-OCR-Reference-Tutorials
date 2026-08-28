---
category: general
date: 2025-12-30
description: วิธีเปิดใช้งาน GPU ใน Aspose OCR สำหรับการประมวลผล OCR แบบกลุ่มและการสกัดข้อความ
  OCR เรียนรู้วิธีตั้งค่าอุปกรณ์ GPU และการใช้ Aspose อย่างมีประสิทธิภาพ
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: th
og_description: วิธีเปิดใช้งาน GPU ใน Aspose OCR. ทำตามคู่มือนี้เพื่อการประมวลผล OCR
  แบบชุด, การสกัดข้อความ OCR, การตั้งค่าอุปกรณ์ GPU, และเรียนรู้วิธีใช้ Aspose.
og_title: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR – บทเรียนเต็ม
tags:
- Aspose
- OCR
- GPU
- C#
title: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR – คู่มือขั้นตอนโดยละเอียด
url: /th/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีเปิดใช้งาน GPU** เมื่อใช้ Aspose OCR หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาที่ต้องจัดการกับเอกสารจำนวนมหาศาลมักเจอขีดจำกัดด้านประสิทธิภาพเพราะเครื่องมือ OCR ทำงานอยู่บน CPU ข่าวดีคือ การเปิดใช้งานการเร่งความเร็วด้วย GPU ทำได้ค่อนข้างง่ายและสามารถลดเวลาในการประมวลผลต่อหน้าได้หลายวินาที ในคู่มือนี้เราจะอธิบาย **วิธีเปิดใช้งาน GPU**, การทำ **การประมวลผล OCR แบบชุด**, การดึงข้อความที่ได้รับการจดจำ, และแม้กระทั่งการเลือกอุปกรณ์ GPU ที่เหมาะสม เมื่ออ่านจบคุณจะรู้ **วิธีใช้ Aspose** เพื่อดึงข้อความ OCR อย่างรวดเร็ว

## สิ่งที่คู่มือนี้ครอบคลุม

เราจะเริ่มด้วยการตั้งค่าไลบรารี Aspose OCR, จากนั้นเปิดใช้งานการสนับสนุน GPU, และสุดท้ายรันชุดไฟล์ภาพ TIFF ผ่านเอนจิน ระหว่างทางเราจะอธิบายว่าทำไมคุณอาจต้อง **ตั้งค่าอุปกรณ์ GPU** ด้วยตนเอง, สิ่งที่ควรระวัง, และวิธีตรวจสอบว่าการดึงข้อความทำงานจริงหรือไม่ ไม่มีเอกสารภายนอก เพียงโซลูชันที่คัดลอก‑วางได้ครบถ้วนที่คุณสามารถรันได้ทันที

> **ข้อกำหนดเบื้องต้น**  
> - .NET 6.0 หรือใหม่กว่า (โค้ดใช้ไวยากรณ์ C# สมัยใหม่)  
> - NuGet package Aspose.OCR for .NET (เวอร์ชัน 23.10 หรือใหม่กว่า)  
> - GPU ที่รองรับ CUDA พร้อมไดรเวอร์ที่เหมาะสมติดตั้งไว้  
> - โฟลเดอร์ที่มีไฟล์ `.tif` ตัวอย่างหลายไฟล์สำหรับการรันแบบชุด  

หากคุณมีสิ่งเหล่านี้ครบแล้ว ไปต่อกันเลย

## วิธีเปิดใช้งาน GPU ใน Aspose OCR

สิ่งแรกที่ต้องทำคือบอกให้ `OcrEngine` ใช้ GPU ทำได้โดยการตั้งค่าคุณสมบัติสองอย่าง: `UseGpu` และ (ถ้าต้องการ) `GpuDeviceId` การตั้งค่า `UseGpu` เป็น `true` จะสลับเอนจินไปยังโหมด GPU ส่วน `GpuDeviceId` ให้คุณเลือก GPU ใด (หากมีมากกว่าหนึ่ง) ที่จะทำงานหนัก

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **ทำไมเรื่องนี้ถึงสำคัญ** – เวอร์ชัน CPU ประมวลผลพิกเซลทีละหนึ่ง ซึ่งอาจเป็นคอขวดสำหรับภาพความละเอียดสูง ส่วนเวอร์ชัน GPU จะรันหลายพันเธรดพร้อมกัน ลดเวลาต่อหน้าอย่างมหาศาล

### ภาพรวมเชิงภาพ  

![Diagram showing how the OCR engine offloads work to the GPU when “how to enable gpu” is set](/images/enable-gpu-diagram.png){: .center .responsive alt="วิธีเปิดใช้งาน GPU"}

*(หากคุณไม่เห็นภาพนี้ ให้จินตนาการเป็นแผนผังที่ OCR engine ส่งบัฟเฟอร์ภาพไปยังคอร์ CUDA)*

## การประมวลผล OCR แบบชุดกับ Aspose

ตอนนี้เอนจินพร้อมใช้ GPU แล้ว ให้เราป้อนรายการไฟล์ให้มัน การประมวลผลแบบชุดง่ายเพียงวนลูปผ่าน `List<string>` ที่บรรจุพาธของภาพ เนื่องจากเราใช้ GPU เอนจินจะจัดคิวแต่ละภาพไปยังอุปกรณ์โดยอัตโนมัติ ทำให้ pipeline ทำงานต่อเนื่อง

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **เคล็ดลับระดับมืออาชีพ** – หากต้องจัดการชุดข้อมูลขนาดใหญ่มากจริง ๆ ให้พิจารณาใช้ `Parallel.ForEach` ร่วมกับ `ocrEngine.Clone()` เพื่อหลีกเลี่ยงปัญหา thread‑safety วิธี `Clone` จะสร้างสำเนาแบบตื้นของเอนจินที่ยังคงชี้ไปยังคอนเท็กซ์ GPU เดียวกัน

### ผลลัพธ์ที่คาดหวัง

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

หากตัวเลขดูสมเหตุสมผล แสดงว่า **การประมวลผล OCR แบบชุด** ทำงานและ GPU กำลังถูกใช้

## การดึงข้อความ OCR – รับผลลัพธ์

เมธอด `Recognize` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความดิบ, คะแนนความเชื่อมั่น, และแม้กระทั่ง bounding box หากคุณต้องการ ดึงข้อความธรรมดาออกมาและบันทึกลงไฟล์เพื่อให้คุณตรวจสอบการดึงข้อมูลได้

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **ทำไมต้องดึงไปยังไฟล์?** – การเก็บข้อความ OCR ไว้ช่วยให้ขั้นตอนต่อไป (เช่น การทำดัชนีการค้นหา, การทำเหมืองข้อมูล ฯลฯ) ทำได้โดยไม่ต้องรันเอนจินซ้ำ อีกทั้งยังเป็นบันทึกถาวรสำหรับการดีบัก

## ตั้งค่าอุปกรณ์ GPU เพื่อประสิทธิภาพสูงสุด

หากเครื่องของคุณมี GPU หลายตัว—เช่น RTX แยกสำหรับ ML และกราฟิกการ์ดแบบบูรณาการ—คุณควรตรวจสอบให้แน่ใจว่าเลือกอุปกรณ์ที่ถูกต้อง `GpuDeviceId` รับค่าเต็มจำนวนที่สอดคล้องกับดัชนีอุปกรณ์ที่ `CudaDeviceInfo.GetDevices()` รายงาน

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **กรณีขอบ** – GPU รุ่นเก่าบางรุ่นอาจไม่รองรับเวอร์ชัน CUDA ที่ต้องการ ในสถานการณ์นั้น `UseGpu = true` จะสลับกลับไปใช้ CPU อย่างเงียบ ๆ ดังนั้นควรตรวจสอบ `ocrEngine.IsGpuEnabled` หลังการเริ่มต้นเสมอ

## วิธีใช้ Aspose OCR ในโครงการจริง

รวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างแอปพลิเคชันคอนโซลขนาดกะทัดรัดที่พร้อมรัน แสดง **วิธีเปิดใช้งาน GPU**, รัน **การประมวลผล OCR แบบชุด**, ดึงข้อความ, และให้คุณเลือกอุปกรณ์ GPU

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### การรันตัวอย่าง

1. ติดตั้ง NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`  
2. แก้ไขพาธใน `imageFiles` ให้ชี้ไปยังไฟล์ `.tif` ของคุณเอง  
3. สร้างและรัน: `dotnet run`  

คุณจะเห็นรายการ GPU ตามด้วยบรรทัดสำหรับแต่ละภาพที่รายงานจำนวนอักขระและพาธของไฟล์ `.txt` ที่สร้างขึ้น

## คำถามที่พบบ่อย & ข้อควรระวัง

- **ทำงานได้บนเครื่องที่มีเฉพาะ CPU หรือไม่?**  
  ใช่—หาก `UseGpu` เป็น `true` แต่ไม่พบ GPU ที่เข้ากันได้ Aspose จะสลับกลับไปใช้ CPU คุณสามารถตรวจสอบโหมดได้ผ่าน `ocrEngine.IsGpuEnabled`

- **ถ้าเจอข้อผิดพลาด “CUDA driver version is insufficient” ควรทำอย่างไร?**  
  อัปเดตไดรเวอร์ NVIDIA ของคุณให้เป็นเวอร์ชันล่าสุดที่ตรงกับ CUDA toolkit ที่มาพร้อมกับ Aspose ไลบรารีต้องการอย่างน้อย CUDA 11.0 สำหรับฟีเจอร์ GPU ล่าสุด

- **สามารถประมวลผล PDF โดยตรงได้หรือไม่?**  
  Aspose OCR ทำงานกับภาพเรสเตอร์เท่านั้น ให้แปลงหน้าของ PDF เป็นภาพก่อน (เช่น ใช้ Aspose.PDF) แล้วจึงส่งเข้า OCR engine

- **จะปรับปรุงความแม่นยำบนสแกนที่มีสัญญาณรบกวนอย่างไร?**  
  เปิดใช้งานตัวเลือกการเตรียมข้อมูลล่วงหน้า เช่น `ocrEngine.Preprocess = true` หรือใช้ภาพความละเอียดสูงกว่า (300 dpi หรือมากกว่า) การเร่งด้วย GPU ยังทำงานต่อไป

## สรุป

เราได้ครอบคลุม **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR, แสดงขั้นตอน **การประมวลผล OCR แบบชุด**, สาธิต **การดึงข้อความ OCR**, และอธิบายวิธี **ตั้งค่าอุปกรณ์ GPU** เพื่อประสิทธิภาพสูงสุด ด้วยตัวอย่างโค้ดเต็มรูปแบบ คุณสามารถรวม OCR ที่เร็วด้วย GPU เข้าไปในโครงการ .NET ใดก็ได้และตอบคำถาม “วิธีใช้ Aspose” อย่างมั่นใจ

พร้อมก้าวต่อไปหรือยัง? ลองเพิ่มการตรวจจับภาษา, ส่งข้อความที่ดึงมาเข้าสู่ดัชนีการค้นหา, หรือทดลองสเกลหลาย GPU สำหรับคลังเอกสารขนาดมหาศาล ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณผสาน API ที่แข็งแกร่งของ Aspose กับพลังของ GPU สมัยใหม่

ขอให้เขียนโค้ดสนุกและ OCR ของคุณทำงานเร็วเท่าที่ GPU จะทำได้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}