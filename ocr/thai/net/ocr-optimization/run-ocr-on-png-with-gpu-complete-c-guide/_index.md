---
category: general
date: 2026-01-02
description: รัน OCR บนไฟล์ PNG อย่างรวดเร็วด้วย Aspose OCR และการสนับสนุน GPU. เรียนรู้วิธีจดจำข้อความจากภาพ,
  แยกข้อความจากภาพและตั้งค่าขีดจำกัดหน่วยความจำ GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: th
og_description: ทำ OCR บนไฟล์ PNG อย่างมีประสิทธิภาพโดยใช้ Aspose OCR และการเร่งความเร็วด้วย
  GPU. บทเรียนนี้จะแสดงวิธีการจดจำข้อความจากภาพ, ดึงข้อความจากภาพและควบคุมการใช้หน่วยความจำของ
  GPU.
og_title: เรียกใช้ OCR บน PNG ด้วย GPU – คู่มือ C# ฉบับสมบูรณ์
tags:
- OCR
- C#
- GPU
title: เรียกใช้ OCR บน PNG ด้วย GPU – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# run OCR on PNG with GPU – Complete C# Guide

เคยต้องการ **run OCR on PNG** ไฟล์แต่รู้สึกติดขัดเรื่องประสิทธิภาพหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ กระบวนการจริง ๆ PNG ความละเอียดสูงเพียงไฟล์เดียวก็อาจทำให้เครื่องมือ OCR ที่ทำงานบน CPU ช้าเกินไป ทำให้การค้นหาแบบเร็ว ๆ กลายเป็นการรอคอยเป็นนาที

ข่าวดีคือ Aspose OCR มาพร้อมส่วนขยาย GPU ที่ทำให้คุณ **recognize text from image** ไฟล์ได้ในเวลาเพียงเศษส่วน ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่แสดงให้เห็นอย่างชัดเจนว่าจะ **run OCR on PNG** ด้วย C# อย่างไร, จะ **extract text from image** อย่างไร, และแม้กระทั่งวิธี **set GPU memory limit** เพื่อให้คุณอยู่ในขอบเขตฮาร์ดแวร์ของคุณ

เราจะอธิบาย “วิธีทำ” และ “เหตุผล” ของแต่ละขั้นตอนด้วย เพื่อให้คุณได้โมเดลความคิดที่มั่นคง—not just a copy‑paste snippet.

## สิ่งที่คุณจะได้เรียนรู้

- ข้อกำหนดเบื้องต้นสำหรับการใช้ GPU support ของ Aspose OCR.  
- วิธีโหลด PNG เข้า `Bitmap` และส่งให้เครื่องมือ OCR.  
- วิธีกำหนดค่า `GpuDevice` และ `GpuMemoryLimitMb` เพื่อประสิทธิภาพสูงสุด.  
- วิธี **recognize text from image** และดึงผลลัพธ์เป็นข้อความธรรมดา.  
- เคล็ดลับการจัดการกับกรณีขอบทั่วไป เช่น GPU ที่มีหน่วยความจำต่ำหรือ PNG หลายหน้า.  

เมื่อจบคู่มือนี้คุณจะสามารถ **run OCR on PNG** ไฟล์ด้วยความเร็ว GPU และควบคุมการใช้หน่วยความจำของงาน OCR ของคุณได้อย่างมั่นใจ.

![แผนภาพแสดงการ run OCR บน PNG ด้วยการเร่งความเร็วของ GPU](run-ocr-on-png-diagram.png "ตัวอย่างการ run OCR บน PNG")

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

1. .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วยเช่นกัน).  
2. GPU ของ NVIDIA ที่รองรับ CUDA (ตัวอย่างเลือกดัชนีอุปกรณ์ 0).  
3. แพคเกจ NuGet ของ Aspose.OCR และส่วนขยาย GPU ของมัน (`Aspose.OCR.Extensions`).  
4. PNG ตัวอย่าง (`input.png`) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโปรเจกต์ของคุณ.  

หากสิ่งใดเหล่านี้ฟังดูไม่คุ้นเคย ไม่ต้องกังวล—เราจะระบุทางเลือกที่เกี่ยวข้อง.

---

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และส่วนขยาย GPU

สิ่งแรกที่ต้องทำ ก่อนอื่น หากไม่มีไลบรารีที่ถูกต้อง โค้ดส่วนอื่นจะไม่คอมไพล์.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` แพคเกจจะดึงไบนารี CUDA เนทีฟที่จำเป็นสำหรับการเร่งความเร็วด้วย GPU.  
*Pro tip:* หากคุณอยู่บนเครื่องที่ไม่มี GPU คุณยังคงสามารถคอมไพล์โปรเจกต์ได้; เพียงตั้งค่า `PreferGpu = false` ในภายหลัง.

---

## ขั้นตอนที่ 2 – โหลด PNG ที่ต้องการประมวลผล

ตอนนี้เราจริง ๆ **run OCR on PNG** โดยการโหลดเข้า `Bitmap`. ขั้นตอนนี้ตรงไปตรงมาแต่ควรสังเกตสั้น ๆ: `Bitmap` ต้องการเส้นทางไฟล์ ดังนั้นตรวจสอบให้แน่ใจว่าเส้นทางถูกต้องสัมพันธ์กับไฟล์ executable ของคุณ.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

หาก PNG มีขนาดใหญ่ผิดปกติ (เช่น > 5000 px ด้านหนึ่ง) คุณอาจต้องลดขนาดลงก่อนเพื่อหลีกเลี่ยงการใช้หน่วยความจำ GPU จนเต็ม นั่นคือจุดที่ตัวเลือก **set GPU memory limit** มีประโยชน์ในภายหลัง.

---

## ขั้นตอนที่ 3 – สร้างและกำหนดค่า OCR Engine สำหรับการใช้ GPU

นี่คือหัวใจของบทแนะนำ: การกำหนดค่า OCR engine เพื่อ **recognize text from image** ด้วย GPU. มีสองคุณสมบัติที่สำคัญ:

- `GpuDevice` – เลือกอุปกรณ์ CUDA ที่จะใช้.  
- `GpuMemoryLimitMb` – จำกัดจำนวนหน่วยความจำ GPU ที่ engine สามารถจัดสรรได้.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**ทำไมต้องตั้งค่าขีดจำกัดหน่วยความจำ?** GPU บางรุ่นแชร์หน่วยความจำกับจอแสดงผลหรือทำงานหลายงานพร้อมกัน การจำกัดการจัดสรรจะช่วยป้องกันการล่มจาก out‑of‑memory โดยเฉพาะเมื่อประมวลผล PNG จำนวนมากพร้อมกัน.

---

## ขั้นตอนที่ 4 – กำหนด Recognition Options (ภาษา & การตั้งค่า GPU Preference)

อ็อบเจกต์ `RecognitionOptions` บอก engine ว่าต้องการค้นหาภาษาอะไรและจะ **prefer GPU** แม้สำหรับภาพขนาดเล็ก สำหรับเอกสารภาษาอังกฤษส่วนใหญ่นี้เพียงพอ แต่คุณสามารถเปลี่ยน `Language.English` เป็นภาษาที่รองรับอื่น ๆ ได้.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

หากคุณต้องการ **extract text from image** ในภาษาที่ไม่ใช่ภาษาอังกฤษ เพียงเปลี่ยนค่า enum `Language`. ไลบรารีนี้รองรับหลายสิบภาษาโดยไม่ต้องตั้งค่าเพิ่มเติม.

---

## ขั้นตอนที่ 5 – เรียกใช้ OCR และดึงผลลัพธ์

เมื่อทุกอย่างเชื่อมต่อเรียบร้อย การเรียกสุดท้ายเป็นบรรทัดเดียวที่จริง ๆ แล้ว **run OCR on PNG** และคืนค่าอ็อบเจกต์ผลลัพธ์ที่มีข้อมูลครบ.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` มีไม่เพียงแต่ข้อความธรรมดา (`ocrResult.Text`) แต่ยังรวมถึงคะแนนความเชื่อมั่น, กล่องขอบเขต, และแม้กระทั่งภาพต้นฉบับที่มีการไฮไลท์คำ—มีประโยชน์หากต้องการดีบักหรือแสดงผลการสกัด.

**ผลลัพธ์ที่คาดหวัง** (สำหรับ PNG ตัวอย่างที่มีข้อความ “Hello World”):

```
=== OCR Output ===
Hello World
```

หากข้อความแสดงเป็นอักขระผสมกัน ตรวจสอบอีกครั้งว่า PNG ไม่เสียหายและขีดจำกัดหน่วยความจำ GPU ไม่ต่ำเกินไปสำหรับขนาดภาพ.

---

## ขั้นตอนที่ 6 – การจัดการกรณีขอบและเคล็ดลับปฏิบัติที่ดีที่สุด

### GPU ที่มีหน่วยความจำต่ำ

หากคุณพบข้อยกเว้นเช่น `CudaException: out of memory` ให้ลดค่า `GpuMemoryLimitMb` หรือแบ่ง PNG เป็นหลายส่วนก่อนประมวลผล การแบ่งส่วนสามารถทำได้ด้วย `Graphics.DrawImage` บนคลอนของ `Bitmap`.

### การประมวลผล PNG หลายไฟล์ในชุดเดียว

เมื่อประมวลผลโฟลเดอร์ของ PNG ให้ใช้ instance ของ `OcrEngine` เดียวกันซ้ำ—การเริ่มต้นเพียงครั้งเดียวช่วยลดการสลับคอนเท็กซ์ของ GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### การสำรองกลับไปใช้ CPU

หากไม่มี GPU ให้ตั้งค่า `PreferGpu = false` เพียงอย่างเดียว Engine จะสำรองกลับไปใช้ CPU โดยอัตโนมัติโดยไม่ต้องแก้ไขโค้ด.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มรูปแบบที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้ รวมทุกขั้นตอนข้างต้นพร้อมการตรวจสอบความปลอดภัยบางอย่าง.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

บันทึกไฟล์เป็น `Program.cs`, รัน `dotnet run`, แล้วคุณควรเห็นข้อความที่สกัดออกมาถูกพิมพ์บนคอนโซล.

---

## สรุป

เราได้แสดงวิธี **run OCR on PNG** ไฟล์โดยใช้ส่วนขยาย GPU ของ Aspose OCR, วิธี **recognize text from image**, และวิธี **extract text from image** พร้อมควบคุม **set GPU memory limit**. ด้วยการกำหนดค่า `GpuDevice` และ `GpuMemoryLimitMb` คุณจะทำให้แอปพลิเคชันของคุณเร็วและเสถียร แม้บน GPU ที่มีสเปคปานกลาง.

จากนี้คุณอาจ:

- ทดลองใช้ภาษาอื่น (`Language.French`, `Language.Spanish`).  
- ผสานขั้นตอน OCR เข้ากับ pipeline การประมวลผลเอกสารที่ใหญ่ขึ้น.  
- เพิ่มการประมวลผลหลัง เช่น การตรวจสอบการสะกดหรือการสกัดเอนทิตี้ เพื่อทำให้ข้อความดิบดูเรียบร้อย.  

จำไว้ว่า สิ่งสำคัญไม่ใช่แค่โค้ด แต่คือการเข้าใจว่าทำไมแต่ละการตั้งค่าถึงสำคัญ เมื่อคุณรู้วิธี **set GPU memory limit** และเมื่อควรสำรองกลับไปใช้ CPU คุณจะสร้างโซลูชัน OCR ที่ขยายตัวได้อย่างราบรื่น.

มีคำถามเกี่ยวกับขนาด PNG เฉพาะ, TIFF หลายหน้า, หรือการแก้ไขข้อผิดพลาดของ GPU? แสดงความคิดเห็นด้านล่าง แล้วขอให้โค้ดสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}