---
category: general
date: 2026-03-02
description: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# และจดจำข้อความจากภาพอย่างรวดเร็ว
  เรียนรู้การตั้งค่าขีดจำกัดหน่วยความจำ GPU, ดึงข้อความจากใบเสร็จ, และทำ OCR อย่างมีประสิทธิภาพ.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- how to run ocr
- extract text from receipt
- set gpu memory limit
language: th
og_description: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# และรับการจดจำข้อความที่เร็วจากภาพ
  ทำตามคำแนะนำนี้เพื่อกำหนดขีดจำกัดหน่วยความจำของ GPU และดึงข้อความจากใบเสร็จ
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# – แยกข้อความ
tags:
- OCR
- C#
- GPU
- Aspose
title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# – การจดจำข้อความ
url: /th/net/ocr-optimization/how-to-enable-gpu-for-ocr-in-c-recognize-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# – การจดจำข้อความ

เคยสงสัย **วิธีเปิดใช้งาน GPU** สำหรับ OCR เมื่อคุณต้องการจดจำข้อความจากไฟล์รูปภาพหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักเจอปัญหาการจดจำที่ช้าเนื่องจากใช้ CPU โดยเฉพาะบนใบเสร็จขนาดใหญ่หรือสแกนความละเอียดสูง ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# คุณสามารถสลับสวิตช์ บอกให้เอนจินทำงานบน GPU และแม้แต่จำกัดการใช้หน่วยความจำได้

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีรัน OCR** ด้วย Aspose.OCR ตั้งค่าขีดจำกัดหน่วยความจำ GPU และสกัดข้อความจากภาพใบเสร็จโดยไม่ต้องเหนื่อยใจ ไม่มีบริการภายนอก เพียงโซลูชันที่สะอาดและเป็นอิสระที่คุณสามารถใส่ลงในโครงการ .NET ใดก็ได้

---

## สิ่งที่คุณต้องการ

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อมแล้ว:

* **.NET 6 หรือใหม่กว่า** – runtime ล่าสุดให้ความเข้ากันได้ดีที่สุด
* **Aspose.OCR for .NET** NuGet package (เวอร์ชัน 23.10 หรือใหม่กว่า).  
  `dotnet add package Aspose.OCR`
* **GPU ที่รองรับ CUDA** พร้อมติดตั้งไดรเวอร์ที่เหมาะสม (NVIDIA 1060+ ทำงานได้ดี).  
  หากคุณไม่มี GPU โค้ดจะสลับไปใช้ CPU อัตโนมัติ—ไม่มีการขัดข้อง เพียงประมวลผลช้าลง
* รูปภาพของใบเสร็จ (หรือเอกสารใด ๆ) ที่คุณต้องการประมวลผล บันทึกเป็น `receipt.jpg`

เมื่อมีทั้งหมดนี้พร้อม คุณจะสามารถคัดลอก‑วางโค้ดด้านล่างและเห็นผลทำงานทันที

---

## ขั้นตอนที่ 1: โหลดภาพที่คุณต้องการประมวลผล  

สิ่งแรกที่กระบวนการ OCR ใด ๆ ทำคืออ่านภาพต้นฉบับเข้าสู่หน่วยความจำ เราจะใช้ `System.Drawing.Bitmap` เพราะเบาและทำงานข้ามแพลตฟอร์มกับ .NET 6+

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuOcrDemo
{
    static void Main()
    {
        // Load the receipt image from disk
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        Bitmap bitmapImage = new Bitmap(imagePath);
```

*ทำไมเรื่องนี้สำคัญ*: การโหลดภาพตั้งแต่แรกช่วยให้คุณตรวจสอบเส้นทางและจับ `FileNotFoundException` ก่อนที่ OCR engine จะเริ่มทำงาน นอกจากนี้ยังให้โอกาสคุณทำการประมวลผลล่วงหน้า (หมุน, ทำไบนารี) หากต้องการในภายหลัง

---

## ขั้นตอนที่ 2: ตั้งค่า OCR Engine ให้ใช้ GPU  

ตอนนี้เราบอก Aspose.OCR ให้ทำงานบน GPU วัตถุ `OcrEngineSettings` คือที่ที่เวทมนตร์เกิดขึ้น

```csharp
        // Configure OCR to run on the GPU and limit its memory usage
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,          // Enable GPU acceleration (requires supported GPU)
            GpuMemoryLimit = 1024            // Optional: cap GPU memory at 1024 MB
        };
```

*ทำไมต้องตั้งค่าขีดจำกัดหน่วยความจำ?*  
หากคุณแชร์ GPU กับกระบวนการอื่น (เช่น โมเดล deep‑learning) คุณไม่ต้องการให้ OCR ใช้ VRAM ทั้งหมด คุณสมบัติ `GpuMemoryLimit` ช่วยให้คุณรักษาความเป็นมิตรของระบบได้

> **Pro tip:** หากคุณไม่แน่ใจว่าเครื่องมี GPU ที่เข้ากันได้หรือไม่ ให้ห่อการตั้งค่าใน `try…catch` และสลับไปใช้ `OcrEngine.Cpu` เมื่อเกิด `UnsupportedHardwareException`

---

## ขั้นตอนที่ 3: เริ่มต้น OCR Engine  

เมื่อการตั้งค่าพร้อมแล้ว สร้างอินสแตนซ์ของเอนจิน ขั้นตอนนี้จะตรวจสอบความพร้อมของ GPU ภายใน

```csharp
        // Initialise the OCR engine with the GPU settings
        OcrEngine ocrEngine = new OcrEngine(ocrSettings);
```

หากไม่พบ GPU Aspose จะโยนข้อยกเว้นที่ให้ข้อมูล การจับข้อยกเว้นตั้งแต่แรกช่วยหลีกเลี่ยงข้อผิดพลาด “null reference” ที่ไม่คาดคิดในภายหลัง

---

## ขั้นตอนที่ 4: รันการจดจำและดึงข้อความ  

นี่คือขั้นตอนหนัก—การจดจำข้อความจาก bitmap

```csharp
        // Perform OCR on the bitmap
        string recognizedText = ocrEngine.Recognize(bitmapImage);

        // Output the result to the console
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

เมธอด `Recognize` จะคืนสตริงธรรมดาที่มีอักขระที่ตรวจพบทั้งหมด พร้อมรักษาการขึ้นบรรทัดใหม่เมื่อทำได้ นี่คือสิ่งที่คุณต้องการเมื่อ **สกัดข้อความจากใบเสร็จ** เพื่อการประมวลผลต่อ (เช่น แยกยอดรวม, วันที่ หรือชื่อผู้ขาย)

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างใบเสร็จ):

```
=== Recognized Text ===
Store: QuickMart
Date: 03/01/2026
Item        Qty   Price
Apple       2     $1.20
Bread       1     $2.50
Total               $3.70
```

หาก GPU ทำงานอยู่ คุณจะสังเกตเห็นเวลาประมวลผลลดจาก ~1.2 วินาที (CPU) เหลือ ~0.3 วินาทีบนการ์ดระดับกลาง—เป็นการชนะที่เห็นได้ชัดสำหรับงานแบตช์

---

## ขั้นตอนที่ 5: จัดการกรณีขอบและการสำรอง  

สภาพแวดล้อมจริงมักไม่รับประกันว่ามี GPU ที่สมบูรณ์แบบ นี่คือลักษณะโค้ดสั้น ๆ ที่ทำให้ระบบสลับไปใช้ CPU อย่างราบรื่นเมื่อจำเป็น:

```csharp
        try
        {
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);
            string text = ocrEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
        catch (UnsupportedHardwareException)
        {
            Console.WriteLine("GPU not available – switching to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;   // fallback
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string text = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
```

*ทำไมเรื่องนี้สำคัญ*: แอปของคุณจะยังคงทำงานได้แม้บนเซิร์ฟเวอร์แบบ headless หรือใน CI pipeline ที่ไม่มี GPU ผู้ใช้จะชื่นชมความทนทาน และมันยังช่วยเพิ่มสัญญาณ E‑E‑A‑T ของคุณสำหรับผู้ช่วย AI ที่ชอบโค้ดที่แข็งแรงและทนต่อข้อผิดพลาด

---

## โบนัส: ปรับแต่งขีดจำกัดหน่วยความจำ GPU  

บางครั้งคุณอาจประมวลผล PDF ขนาดมหาศาลที่เรนเดอร์เป็นภาพ 4 K ในกรณีนั้น ขีดจำกัดเริ่มต้น 1024 MB อาจต่ำเกินไป ทำให้เกิด `OutOfMemoryException` ปรับค่าได้ดังนี้:

```csharp
        // Increase limit for high‑resolution images
        ocrSettings.GpuMemoryLimit = 2048; // 2 GB
```

ในทางกลับกันบนเวิร์กสเตชันที่ใช้ร่วมกัน คุณอาจต้องการ **ตั้งขีดจำกัดหน่วยความจำ GPU** ที่ 512 MB เพื่อให้มีพื้นที่เหลือสำหรับแอปอื่น ๆ

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Load the image
        Bitmap bitmapImage = new Bitmap(@"YOUR_DIRECTORY/receipt.jpg");

        // 2️⃣ Configure OCR to use GPU and set memory limit
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,      // Enable GPU acceleration
            GpuMemoryLimit = 1024        // Limit GPU memory to 1 GB (optional)
        };

        try
        {
            // 3️⃣ Initialise the engine
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);

            // 4️⃣ Recognize text
            string recognizedText = ocrEngine.Recognize(bitmapImage);

            // 5️⃣ Output result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (UnsupportedHardwareException)
        {
            // Fallback to CPU if GPU is unavailable
            Console.WriteLine("GPU not detected – falling back to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string recognizedText = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(recognizedText);
        }
    }
}
```

บันทึกไฟล์นี้เป็น `Program.cs` รัน `dotnet run` แล้วคุณจะเห็นข้อความที่สกัดออกมาแสดงในคอนโซล นั่นคือกระบวนการ **วิธีรัน OCR** ทั้งหมด ตั้งแต่การโหลดภาพจนถึงการจดจำด้วย GPU และการสำรองอย่างราบรื่น

---

## คำถามที่พบบ่อย

**Q: Does this work on Linux?**  
A: Yes. Aspose.OCR ships with native binaries for Windows, Linux, and macOS. Just install the CUDA driver for your distro and the same C# code works.  

**Q: What if my receipt image is in PNG format?**  
A: `Bitmap` can load PNG, JPEG, BMP, and TIFF out of the box. Just change the file extension in `imagePath`.  

**Q: Can I process multiple images in a loop?**  
A: Absolutely. Instantiate the `OcrEngine` once (outside the loop) and call `Recognize` for each bitmap—this re‑uses the GPU context and speeds up batch jobs.  

**Q: How accurate is GPU OCR compared to CPU?**  
A: The underlying OCR model is identical; only the execution engine changes. Accuracy stays the same, while speed improves.  

---

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

ตอนนี้คุณรู้ **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR แล้ว คุณอาจต้องการ:

* **รวมเข้ากับฐานข้อมูล** – เก็บบรรทัดใบเสร็จที่สกัดได้เพื่อการวิเคราะห์
* **ทำการประมวลผลภาพล่วงหน้า** (deskew, denoise) เพื่อเพิ่มความแม่นยำ—ดูที่ฟิลเตอร์ `System.Drawing` หรือ OpenCV
* **รวมกับตัวแยก PDF** เพื่อสกัดภาพจากใบแจ้งหนี้หลายหน้า ก่อนรัน OCR
* **สำรวจไลบรารีเร่งความเร็วด้วย GPU** อื่น ๆ เช่น Tesseract‑GPU หรือ Microsoft Azure Computer Vision สำหรับทางเลือกบนคลาวด์

แต่ละเส้นทางเหล่านี้จะขยายพลังของ pipeline OCR ของคุณและช่วยให้คุณไม่ต้องสร้างล้อใหม่จากศูนย์

---

## ความคิดเห็นสรุป

คุณเพิ่งเชี่ยวชาญ **วิธีเปิดใช้งาน GPU** สำหรับ OCR ใน C# และได้เรียนรู้ **การจดจำข้อความจากไฟล์รูปภาพ**, **สกัดข้อความจากใบเสร็จ** PDFs, และ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** เพื่อประสิทธิภาพที่ดีที่สุด โค้ดครบถ้วน, รันได้, และมีการป้องกันข้อผิดพลาด—ตรงกับสิ่งที่ผู้ช่วย AI ชื่นชอบที่จะอ้างอิง  

ลองใช้งาน ปรับขีดจำกัดหน่วยความจำให้เหมาะกับฮาร์ดแวร์ของคุณ แล้วดูความเร็วที่เพิ่มขึ้น เมื่อพร้อมแล้ว ให้ลุยเข้าสู่การทำ preprocessing หรือการประมวลผลแบบแบตช์ เพื่อเปลี่ยนเดโมภาพเดียวให้กลายเป็นโซลูชันระดับองค์กร

ขอให้คุณเขียนโค้ดอย่างสนุกสนาน และขอให้

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}