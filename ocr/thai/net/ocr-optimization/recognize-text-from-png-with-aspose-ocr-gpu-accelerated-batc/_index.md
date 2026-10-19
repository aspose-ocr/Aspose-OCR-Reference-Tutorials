---
category: general
date: 2026-04-01
description: เรียนรู้วิธีจดจำข้อความจากไฟล์ PNG อย่างรวดเร็วโดยตั้งค่า ID ของอุปกรณ์
  GPU และเปิดใช้งานการเร่งความเร็วด้วย GPU ใน Aspose OCR คู่มือ C# ทีละขั้นตอน.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: th
og_description: จดจำข้อความจากไฟล์ PNG อย่างรวดเร็วโดยการตั้งค่า ID ของอุปกรณ์ GPU.
  ทำตามคู่มือ C# ฉบับเต็มนี้เพื่อเปิดใช้งานการเร่งความเร็วด้วย GPU ด้วย Aspose OCR.
og_title: แยกข้อความจาก PNG – บทเรียน OCR ของ Aspose ที่เร่งด้วย GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: แยกข้อความจาก PNG ด้วย Aspose OCR – การสาธิตแบบแบตช์ที่เร่งด้วย GPU
url: /th/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับรู้ข้อความจาก png – คำแนะนำเต็ม C# ที่เร่งด้วย GPU (Batch)

เคยต้อง **รับรู้ข้อความจาก png** ภาพแล้วรู้สึกว่ากระบวนการช้าเกินไปหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาส่วนใหญ่มักเริ่มด้วยการเรียก OCR แบบง่าย ๆ แล้วต้องมองคอนโซลที่ทำงานช้าเหมือนหอยทากเมื่อโฟลเดอร์มีภาพหน้าจอหลายสิบไฟล์  

ข่าวดีคือ Aspose OCR สามารถยกภาระงานหนักไปให้การ์ดจอของคุณทำได้ และด้วยเพียงสองบรรทัดคุณก็สามารถ **set gpu device id** เพื่อเลือก GPU ที่ต้องการได้ ในบทความนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ ซึ่งจะดึงไฟล์ PNG ทุกไฟล์จากโฟลเดอร์ เปิดการเร่งความเร็วด้วย GPU เลือก GPU ตัวแรก แล้วพิมพ์จำนวนอักขระของแต่ละไฟล์

เมื่ออ่านจบแล้วคุณจะได้โปรแกรมที่เป็นอิสระ สามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้ และคุณจะเข้าใจว่าการเปิดใช้งาน GPU มีความสำคัญอย่างไร วิธีจัดการกรณีขอบ และสิ่งที่ควรปรับเพื่อให้ประสิทธิภาพดียิ่งขึ้น

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ .NET Core)  
- แพคเกจ **Aspose.OCR** จาก NuGet – ติดตั้งด้วยคำสั่ง `dotnet add package Aspose.OCR`  
- เครื่องที่มี GPU รองรับ CUDA (ส่วนใหญ่เป็น NVIDIA) พร้อมไดรเวอร์ที่เหมาะสม  
- โฟลเดอร์ที่เต็มไปด้วยภาพ **PNG** ที่ต้องการประมวลผล  

หากคุณไม่คุ้นเคยกับข้อใดข้อหนึ่ง อย่ากังวล ขั้นตอนต่อไปจะให้คำสั่งที่ต้องใช้อย่างละเอียด และเราจะอธิบายวิธีทำเมื่อไม่มี GPU อยู่

## ขั้นตอนที่ 1: เริ่มต้น OcrEngine และเปิดการเร่งความเร็วด้วย GPU  

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ `OcrEngine` แล้วเปิดการสนับสนุน GPU ธงนี้บอกให้ Aspose ใช้ไลบรารี CUDA ที่ทำงานภายใน

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**ทำไมต้องทำเช่นนี้:** หากไม่มี `UseGpuAcceleration` แต่ละภาพจะถูกประมวลผลบน CPU ซึ่งช้ากว่ามากหลายเท่า โดยเฉพาะ PNG ความละเอียดสูง การเปิดใช้งานธงนี้ยังเตรียมเอนจินให้รับค่า GPU เฉพาะในขั้นตอนต่อไปได้

## ขั้นตอนที่ 2: ตั้งค่า GPU Device ID (ไม่บังคับแต่แนะนำ)

หากเครื่องของคุณมี GPU มากกว่าหนึ่งตัว คุณสามารถเลือกใช้ตัวที่ต้องการได้ ID ของอุปกรณ์เริ่มจาก **0** ดังนั้น `0` จะเลือก GPU ตัวแรก, `1` ตัวที่สอง, ฯลฯ

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**เคล็ดลับ:** เมื่อรันบนเซิร์ฟเวอร์ที่แชร์ การกำหนด GPU Device ID อย่างชัดเจนจะช่วยป้องกันงานของคุณไปแย่งทรัพยากรจากกระบวนการอื่น หากคุณละเว้นบรรทัดนี้ Aspose จะเลือกอุปกรณ์เริ่มต้นซึ่งมักจะพอใช้ได้ในระบบที่มี GPU ตัวเดียว

## ขั้นตอนที่ 3: รวบรวมไฟล์ PNG ทั้งหมดจากโฟลเดอร์แบช

ต่อไปเราต้องค้นหา PNG ทุกไฟล์ที่ต้องการทำ OCR วิธี `Directory.GetFiles` จะทำหน้าที่นี้ให้

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**กรณีขอบ:** หากโฟลเดอร์ว่างเปล่า `imageFiles` จะเป็นอาเรย์ว่าง เราจะจัดการในขั้นตอนต่อไปด้วยข้อความแจ้งผู้ใช้ที่เป็นมิตร

## ขั้นตอนที่ 4: ประมวลผลแต่ละภาพและแสดงจำนวนอักขระที่รับรู้ได้

นี่คือลูปหลัก สำหรับ PNG แต่ละไฟล์เราจะเรียก `Recognize` แล้วพิมพ์ชื่อไฟล์พร้อมความยาวของข้อความที่ดึงออกมา

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**สิ่งที่คุณจะเห็น:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

หากภาพไม่มีข้อความ จำนวนจะเป็น `0` ซึ่งเป็นพฤติกรรมปกติสำหรับสกรีนช็อตที่เป็นกราฟิกอย่างเดียว

## ขั้นตอนที่ 5: รันโปรแกรมและตรวจสอบการใช้ GPU  

คอมไพล์ไฟล์ (`dotnet build`) แล้วรัน (`dotnet run`) ขณะคอนโซลเลื่อน คุณสามารถเปิดเครื่องมือมอนิเตอร์ GPU (เช่น NVIDIA Smi) เพื่อตรวจดูการใช้ GPU ที่พุ่งขึ้นชั่วครู่สำหรับแต่ละภาพ หากไม่เห็นการทำงานใด ๆ ให้ตรวจสอบว่า:

1. ติดตั้งไดรเวอร์ CUDA แล้วหรือยัง  
2. `UseGpuAcceleration` ถูกตั้งค่าเป็น `true`  
3. `GpuDeviceId` ที่กำหนดตรงกับ GPU จริง  

หาก GPU ไม่พร้อมใช้งาน Aspose จะสลับกลับไปใช้ CPU โดยอัตโนมัติ แต่คุณจะเสียประสิทธิภาพที่ได้จาก GPU

## ความแปรผันทั่วไป & เคล็ดลับ  

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน |
|-----------|-------------------|
| **รูปแบบภาพต่างกัน** (เช่น JPEG) | เปลี่ยน pattern การค้นหาเป็น `*.jpg` หรือ `*.*` Aspose จะยังคงรับรู้ข้อความได้ |
| **ขนาดแบชใหญ่มาก** (หลายพันไฟล์) | ประมวลผลเป็นชิ้นย่อยเพื่อหลีกเลี่ยงความกดดันของหน่วยความจำ: แบ่ง `imageFiles` เป็นอาเรย์ย่อย |
| **ต้องการข้อความจริง ไม่ใช่แค่ความยาว** | แทนที่ `ocrResult.Text.Length` ด้วย `ocrResult.Text` ใน `WriteLine` |
| **รันบนเซิร์ฟเวอร์แบบ headless** | ตรวจให้แน่ใจว่าเซิร์ฟเวอร์มีไดรเวอร์ GPU; หากไม่มีให้ตั้ง `UseGpuAcceleration = false` เพื่อหลีกเลี่ยงข้อผิดพลาด |
| **มีหลาย GPU ต้องการกระจายโหลด** | ใช้ลูป `ocrEngine.GpuDeviceId = i % gpuCount` ภายใน `foreach` เพื่อสลับอุปกรณ์ |

## ผลลัพธ์ที่คาดหวัง & การตรวจสอบ  

เมื่อทุกอย่างทำงานได้ คอนโซลจะพิมพ์ชื่อไฟล์ตามด้วยจำนวนอักขระ ตามที่แสดงในตัวอย่างก่อนหน้า หากต้องการตรวจสอบผล OCR จริง ๆ คุณสามารถพิมพ์ข้อความออกมาชั่วคราวได้:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

แค่จำไว้ว่าให้ลบหรือคอมเมนต์บรรทัดนั้นเมื่อทำแบชขนาดใหญ่; การพิมพ์หลายพันบรรทัดจะทำให้เทอร์มินัลอัดแน่น

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

บันทึกเป็น `GpuBatchDemo.cs` แล้วรัน `dotnet add package Aspose.OCR` จากนั้น `dotnet run` คุณควรเห็นจำนวนอักขระปรากฏอย่างรวดเร็วสำหรับแต่ละ PNG ด้วยความเร่งของ GPU

## สรุป  

ตอนนี้คุณรู้วิธี **รับรู้ข้อความจาก png** อย่างมีประสิทธิภาพโดยเปิดการเร่งความเร็วด้วย GPU และ **set gpu device id** อย่างชัดเจนใน Aspose OCR โปรแกรมที่คัดลอก‑วางได้เต็มรูปแบบนี้จัดการการค้นหาโฟลเดอร์, ตรวจสอบกรณีขอบ, และให้ฟีดแบ็กทันทีเกี่ยวกับประสิทธิภาพ OCR  

ขั้นตอนต่อไป? ลองเปลี่ยนการเรียก `Recognize` เป็น `ocrEngine.RecognizeAsync` หากต้องการประมวลผลแบบไม่บล็อก, หรือทดลองตัวเลือกการเตรียมภาพล่วงหน้า (เช่น การทำไบนารี) ที่ Aspose มีให้ คุณอาจส่งผลลัพธ์ OCR ไปยังฐานข้อมูลหรือดัชนีการค้นหาเพื่อสร้างระบบค้นหาเต็มข้อความได้  

มีคำถามเกี่ยวกับการจัดการ PDF หลายหน้า หรืออยากเปรียบเทียบ Aspose OCR กับ Tesseract? แสดงความคิดเห็นหรือสำรวจบทเรียนอื่น ๆ ของเราเกี่ยวกับ **batch OCR C#**, **เคล็ดลับประสิทธิภาพ OCR**, และ **การประมวลผลภาพด้วย GPU** ขอให้สนุกกับการเขียนโค้ด!  

![Console output showing recognised character counts for PNG files – recognize text from png using GPU acceleration](image-placeholder.png "ตัวอย่างผลลัพธ์การรับรู้ข้อความจาก png ด้วยการเร่ง GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}