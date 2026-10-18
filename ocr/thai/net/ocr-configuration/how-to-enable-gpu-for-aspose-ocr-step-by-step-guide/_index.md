---
category: general
date: 2026-09-08
description: เรียนรู้วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR, รันการประมวลผล OCR แบบชุด,
  และสกัดข้อความจากภาพอย่างมีประสิทธิภาพด้วย .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR. คู่มือนี้แสดงการประมวลผล OCR
  แบบชุด, การสกัดข้อความจากภาพ, และการเลือกอุปกรณ์ GPU ที่เหมาะสมใน .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR – คู่มือเต็ม
url: /th/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีเปิดใช้งาน GPU** เมื่อใช้ Aspose OCR หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาที่ต้องจัดการกับปริมาณเอกสารมหาศาลมักเจออุปสรรคด้านประสิทธิภาพเพราะเครื่องมือ OCR ติดอยู่ที่ CPU. ข่าวดี? การเปิดใช้งานการเร่งความเร็วด้วย GPU นั้นค่อนข้างง่ายและสามารถลดเวลาเพียงไม่กี่วินาทีต่อหน้าได้ ในคู่มือนี้เราจะอธิบาย **วิธีเปิดใช้งาน GPU**, รัน **การประมวลผล OCR แบบชุด**, ดึงข้อความที่ได้รับการจดจำ, และแม้กระทั่งเลือกอุปกรณ์ GPU ที่เหมาะสม. เมื่อจบคุณจะรู้ **วิธีใช้ Aspose** เพื่อการสกัดข้อความ OCR ที่เร็วเหมือนสายฟ้า.

## คำตอบด่วน
- **การเปิดใช้งาน GPU ทำอะไร?** มันย้ายการวิเคราะห์ระดับพิกเซลไปยังการ์ดกราฟิก, ลดเวลาการประมวลผลได้ถึง 80 % สำหรับภาพ 300 dpi ปกติ.  
- **ต้องการไลเซนส์พิเศษหรือไม่?** ไม่, แพคเกจ Aspose.OCR NuGet มาตรฐานรวมการสนับสนุน GPU อยู่แล้ว.  
- **ต้องการเวอร์ชัน .NET ใด?** .NET 6.0 หรือใหม่กว่า; API ใช้คุณลักษณะ C# สมัยใหม่.  
- **สามารถรันบนเครื่องที่มีเฉพาะ CPU ได้หรือไม่?** ได้—หากไม่พบ GPU ที่เข้ากันได้ เครื่องจะกลับไปใช้ CPU โดยอัตโนมัติ.  
- **สามารถประมวลผลภาพได้กี่ภาพพร้อมกัน?** คุณสามารถคิวไฟล์ได้หลายร้อยไฟล์; GPU จะจัดการแบบต่อเนื่องในขณะที่โค้ดของคุณสามารถส่งภาพต่อไปได้ทันทีที่ภาพก่อนหน้าเสร็จ.

## วิธีเปิดใช้งาน GPU คืออะไร?
`how to enable GPU` คือกระบวนการกำหนดค่า `OcrEngine` ของ Aspose OCR ให้ส่งงานประมวลผลภาพไปยังการ์ดกราฟิกที่รองรับ CUDA แทนหน่วยประมวลผลกลาง (CPU). การสลับนี้ควบคุมโดยคุณสมบัติสองตัว: `UseGpu` และ `GpuDeviceId`. การเปิดใช้งานฟล็กนี้จะย้ายการวิเคราะห์พิกเซลที่ใช้คำนวณหนักไปยัง GPU, ซึ่งสามารถจัดการกับพัน ๆ เธรดพร้อมกัน, ลดเวลาการประมวลผลอย่างมาก.  

คลาส `OcrEngine` เป็นส่วนประกอบหลักของ Aspose OCR ที่ทำการวิเคราะห์ภาพและการจดจำข้อความ.

## ทำไมต้องใช้การเร่งความเร็วด้วย GPU กับ Aspose OCR?
Aspose OCR รองรับ **รูปแบบภาพเข้า 50+** และสามารถประมวลผลชุดหลายร้อยหน้าโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ. เมื่อเปิดการเร่งความเร็วด้วย GPU, การทดสอบเบนช์มาร์กแสดงให้เห็น **การลดลง 70 %‑80 %** ของเวลาเฉลี่ยต่อหน้าที่ประมวลผลบน RTX 3080 เมื่อเทียบกับการทำงานบน CPU อย่างเดียว. การเพิ่มความเร็วนี้แปลเป็นค่าใช้จ่ายคลาวด์ที่ต่ำลงและผลลัพธ์ที่ผู้ใช้เห็นเร็วขึ้นในแอปพลิเคชันที่ต้องจัดการเอกสารจำนวนมาก.

## ข้อกำหนดเบื้องต้น
- .NET 6.0 หรือใหม่กว่า (โค้ดใช้ไวยากรณ์ C# สมัยใหม่)  
- แพคเกจ NuGet Aspose.OCR สำหรับ .NET (เวอร์ชัน 23.10 หรือใหม่กว่า)  
- GPU ที่รองรับ CUDA พร้อมติดตั้งไดรเวอร์ที่เหมาะสม (ขั้นต่ำ CUDA 11.0)  
- โฟลเดอร์ที่มีไฟล์ตัวอย่าง `.tif` สำหรับการรันแบบชุด  

หากคุณมีพื้นฐานเหล่านี้ครบแล้ว, ไปต่อกันเลย.

## วิธีเปิดใช้งาน GPU ใน Aspose OCR
โหลดเครื่องมือ OCR, เปิดโหมด GPU, และเลือกดัชนีอุปกรณ์ตามต้องการ.  

`OcrEngine` เป็นคลาสหลักของ Aspose OCR ที่ทำการวิเคราะห์ภาพและการจดจำข้อความ.  

การเปิดใช้งาน GPU เป็นการดำเนินการสองขั้นตอน: ตั้งค่า `UseGpu = true` และเมื่อมีหลาย GPU, กำหนด `GpuDeviceId` ที่ต้องการ. ย่อหน้านี้อธิบายกระบวนการทั้งหมดใน 45 คำ.  

สิ่งแรกที่คุณต้องบอก `OcrEngine` ให้ใช้ GPU คือการทำผ่านคุณสมบัติสองอย่างง่าย: `UseGpu` และโดยเลือก `GpuDeviceId`. การตั้งค่า `UseGpu` เป็น `true` จะสลับเครื่องมือไปยังโหมด GPU, ส่วน `GpuDeviceId` ให้คุณเลือกว่า GPU ใด (หากมีหลายตัว) จะทำงานหนัก.  

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

> **ทำไมเรื่องนี้สำคัญ** – เวอร์ชัน CPU ประมวลผลแต่ละพิกเซลแบบต่อเนื่อง, ซึ่งอาจเป็นคอขวดสำหรับภาพความละเอียดสูง. เวอร์ชัน GPU รันพัน ๆ เธรดพร้อมกัน, ลดเวลาต่อหน้าอย่างมาก.

### ภาพรวมเชิงภาพ  

![แผนภาพแสดงวิธีที่เครื่องมือ OCR โอนงานไปยัง GPU เมื่อกำหนด “วิธีเปิดใช้งาน gpu”](/images/enable-gpu-diagram.png){: .center .responsive alt="วิธีเปิดใช้งาน gpu"}

[แผนภาพแสดงวิธีที่เครื่องมือ OCR โอนงานไปยัง GPU เมื่อกำหนด “วิธีเปิดใช้งาน gpu”](/images/enable-gpu-diagram.png)

*(หากคุณไม่สามารถดูภาพได้, เพียงจินตนาการแผนผังที่เครื่องมือ OCR ส่งบัฟเฟอร์ภาพไปยังคอร์ของ CUDA.)*

## วิธีรันการประมวลผล OCR แบบชุดกับ Aspose
`Recognize` method ของ `OcrEngine` ประมวลผลภาพและคืนค่า `OcrResult` ที่มีข้อความที่สกัดและเมตาดาต้า. คุณสามารถประมวลผลโฟลเดอร์ทั้งหมดโดยวนลูปผ่านรายการเส้นทางไฟล์. เครื่องมือจะคิวภาพแต่ละภาพไปยัง GPU โดยอัตโนมัติ, ทำให้ pipeline ทำงานต่อเนื่องในขณะที่แอปพลิเคชันของคุณยังคงส่งไฟล์ใหม่. วิธีนี้ทำให้คุณจัดการกับ TIFF หลายร้อยไฟล์ได้อย่างมีประสิทธิภาพ, โดย GPU ทำงานหนักแบบขนาน.  

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

> **เคล็ดลับ** – สำหรับชุดที่ใหญ่มาก, พิจารณาใช้ `Parallel.ForEach` ร่วมกับ `ocrEngine.Clone()` เพื่อหลีกเลี่ยงปัญหาความปลอดภัยของเธรด. เมธอด `Clone` สร้างสำเนาแบบตื้นของเครื่องมือที่ยังชี้ไปยังคอนเท็กซ์ GPU เดียวกัน.

### ผลลัพธ์ที่คาดหวัง

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

หากตัวเลขดูสมเหตุสมผล, **การประมวลผล OCR แบบชุด** ของคุณทำงานและ GPU กำลังถูกใช้งาน.

## วิธีสกัดข้อความจากภาพ – รับผลลัพธ์
`OcrResult` คืออ็อบเจ็กต์ที่เก็บผลลัพธ์ OCR, รวมถึงข้อความที่จดจำ, คะแนนความมั่นใจ, และข้อมูลการจัดวาง. เมธอด `Recognize` คืนค่าอ็อบเจ็กต์ `OcrResult`. ดึงข้อความธรรมดาจากคุณสมบัติ `Text` และเขียนลงไฟล์เพื่อใช้ต่อในขั้นตอนถัดไป. การเก็บข้อความ OCR ช่วยให้การประมวลผลต่อ (การทำดัชนีการค้นหา, การทำเหมืองข้อมูล, ฯลฯ) ทำได้โดยไม่ต้องรันเครื่องมือใหม่และให้บันทึกถาวรสำหรับการดีบัก.  

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

> **ทำไมต้องสกัดเป็นไฟล์?** – การเก็บข้อความ OCR ช่วยให้การประมวลผลต่อ (การทำดัชนีการค้นหา, การทำเหมืองข้อมูล, ฯลฯ) ทำได้โดยไม่ต้องรันเครื่องมือใหม่. มันยังให้บันทึกถาวรสำหรับการดีบัก.

## วิธีตั้งค่าอุปกรณ์ GPU เพื่อประสิทธิภาพสูงสุด
`CudaDeviceInfo` ให้ข้อมูลเกี่ยวกับ GPU ที่รองรับ CUDA ที่ติดตั้งในระบบ. เมื่อมีหลาย GPU, ใช้ `GpuDeviceId` เพื่อเลือกอันที่ดีที่สุด. ดัชนีสอดคล้องกับลำดับที่ `CudaDeviceInfo.GetDevices()` คืนค่า. การเลือกอุปกรณ์ที่เหมาะสมทำให้คุณใช้ GPU ที่ทรงพลังที่สุดและหลีกเลี่ยงการแย่งทรัพยากรกับงานอื่นบนการ์ดรอง.  

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

> **กรณีขอบ** – GPU รุ่นเก่าบางรุ่นไม่รองรับเวอร์ชัน CUDA ที่ต้องการ. ในสถานการณ์นั้น, `UseGpu = true` จะกลับไปใช้ CPU อย่างเงียบ, ดังนั้นควรตรวจสอบ `ocrEngine.IsGpuEnabled` หลังการเริ่มต้นเสมอ.

## วิธีใช้ Aspose OCR ในโครงการจริง
เมื่อรวมทุกอย่างเข้าด้วยกัน, นี่คือตัวอย่างแอปพลิเคชันคอนโซลขนาดกะทัดรัดพร้อมรันที่แสดง **วิธีเปิดใช้งาน GPU**, รัน **การประมวลผล OCR แบบชุด**, สกัดข้อความ, และให้คุณเลือกอุปกรณ์ GPU. ตัวอย่างนี้สร้าง `OcrEngine`, เปิดใช้งาน GPU, แสดงรายการอุปกรณ์ที่มี, ประมวลผลแต่ละภาพ, และเขียนข้อความที่จดจำได้ลงไฟล์ `.txt` ควบคู่กับภาพต้นฉบับ.  

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

1. ติดตั้งแพคเกจ NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. แทนที่เส้นทางใน `imageFiles` ด้วยตำแหน่งของไฟล์ `.tif` ของคุณเอง.  
3. สร้างและรัน: `dotnet run`.  

คุณควรเห็นรายการ GPU, ตามด้วยบรรทัดสำหรับแต่ละภาพที่รายงานจำนวนอักขระและเส้นทางของไฟล์ `.txt` ที่สร้างขึ้น.

## คำถามทั่วไป & ปัญหาที่พบบ่อย

- **ทำงานบนเครื่องที่มีเฉพาะ CPU ได้หรือไม่?**  
  ใช่—หาก `UseGpu` เป็น `true` แต่ไม่พบ GPU ที่เข้ากันได้, Aspose จะกลับไปใช้ CPU. คุณสามารถตรวจสอบโหมดผ่าน `ocrEngine.IsGpuEnabled`.

- **ถ้าได้รับข้อผิดพลาด “CUDA driver version is insufficient” จะทำอย่างไร?**  
  อัปเดตไดรเวอร์ NVIDIA ของคุณเป็นเวอร์ชันล่าสุดที่ตรงกับชุดเครื่องมือ CUDA ที่มาพร้อมกับ Aspose. ไลบรารีต้องการอย่างน้อย CUDA 11.0 สำหรับฟีเจอร์ GPU ล่าสุด.

- **สามารถประมวลผล PDF โดยตรงได้หรือไม่?**  
  Aspose OCR ทำงานกับภาพราสเตอร์. แปลงหน้าของ PDF เป็นภาพก่อน (เช่น ใช้ Aspose.PDF) แล้วจึงส่งให้เครื่องมือ OCR.

- **จะเพิ่มความแม่นยำบนสแกนที่มีสัญญาณรบกวนอย่างไร?**  
  เปิดใช้งานตัวเลือกการเตรียมข้อมูลล่วงหน้าเช่น `ocrEngine.Preprocess = true` หรือใช้ภาพความละเอียดสูงกว่า (300 dpi หรือมากกว่า). การเร่งความเร็วด้วย GPU ยังคงใช้ได้.

## คำถามที่พบบ่อย

**ถาม: จำเป็นต้องมีไลเซนส์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?**  
**ตอบ:** ใช่, จำเป็นต้องมีไลเซนส์ Aspose.OCR เชิงพาณิชย์สำหรับการใช้งานในระบบผลิต, มีรุ่นทดลองฟรีสำหรับการประเมิน.

**ถาม: โมเดล GPU ใดที่รองรับอย่างเป็นทางการ?**  
**ตอบ:** GPU ของ NVIDIA ที่รองรับ CUDA 11.0 หรือใหม่กว่า, เช่น RTX 2060, RTX 3070, RTX 4090, และซีรีส์ Tesla ที่สอดคล้อง.

**ถาม: สามารถรันโค้ดนี้ใน ASP.NET Core web API ได้หรือไม่?**  
**ตอบ:** แน่นอน. อินสแตนซ์ `OcrEngine` เดียวกันสามารถใช้ซ้ำได้ระหว่างคำขอ; เพียงตรวจสอบความปลอดภัยของเธรดโดยการคล cloning เครื่องมือต่อคำขอ.

**ถาม: Aspose OCR รองรับเอกสารหลายภาษาได้หรือไม่?**  
**ตอบ:** ใช่, คุณสามารถตั้งค่า `ocrEngine.Language = Language.English | Language.Spanish` เพื่อเปิดการจดจำหลายภาษาพร้อมกัน.

**ถาม: ขนาดภาพสูงสุดที่ GPU สามารถจัดการได้คือเท่าไหร่?**  
**ตอบ:** เครื่องมือสตรีมข้อมูลภาพ, ดังนั้นคุณสามารถประมวลผลภาพขนาดสูงสุด 10,000 × 10,000 พิกเซลโดยไม่ทำให้หน่วยความจำ GPU หมด, แม้ว่าประสิทธิภาพอาจแตกต่าง.

---

**อัปเดตล่าสุด:** 2026-09-08  
**ทดสอบด้วย:** Aspose.OCR 23.10 สำหรับ .NET  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [วิธีใช้ OCR ใน C เพื่อสกัดข้อความจากภาพด้วยการเร่งความเร็ว GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [สกัดข้อความจากภาพด้วย Aspose OCR GPU C Guide](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [ลบพื้นหลัง OCR ด้วย Aspose OCR คู่มือ GPU ฉบับสมบูรณ์](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}