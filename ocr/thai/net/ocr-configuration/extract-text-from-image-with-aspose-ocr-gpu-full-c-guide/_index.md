---
category: general
date: 2026-04-06
description: ดึงข้อความจากรูปภาพโดยใช้ Aspose OCR GPU ใน C#. เรียนรู้วิธีโหลดรูปภาพจากไฟล์และตั้งค่าขีดจำกัดหน่วยความจำ
  GPU ในคู่มือขั้นตอนต่อขั้นตอนนี้.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR GPU ใน C# เรียนรู้วิธีโหลดภาพจากไฟล์และตั้งค่าขีดจำกัดหน่วยความจำ
  GPU ในคู่มือขั้นตอนต่อขั้นตอนนี้.
og_title: สกัดข้อความจากภาพด้วย Aspose OCR GPU – คู่มือ C# เต็มรูปแบบ
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: ดึงข้อความจากภาพด้วย Aspose OCR GPU – คู่มือ C# เต็ม
url: /th/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Aspose OCR GPU – คู่มือเต็ม C#

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่รู้สึกติดขัดเมื่อต้องการประสิทธิภาพสูงหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจอปัญหาเดียวกันเมื่อ OCR กลายเป็นคอขวด ในบทเรียนนี้เราจะสาธิตวิธีดึงข้อความจากรูปภาพโดยใช้ Aspose OCR GPU runtime, โหลดรูปจากไฟล์, และแม้แต่ตั้งค่าขีดจำกัดหน่วยความจำ GPU เพื่อควบคุมทรัพยากรอย่างแม่นยำ

เราจะเดินผ่านตัวอย่าง C# ที่พร้อมรันครบถ้วน, อธิบายว่าทำไมบรรทัดแต่ละบรรทัดถึงสำคัญ, และชี้ให้เห็นข้อผิดพลาดทั่วไปที่อาจเจอ หลังจากนี้คุณจะมีพื้นฐานที่มั่นคงสำหรับสร้าง pipeline OCR ที่เร็วและขยายได้บน GPU

## สิ่งที่คู่มือนี้ครอบคลุม

- **ข้อกำหนดเบื้องต้น**: .NET 6+ (หรือ .NET Framework 4.6+), แพคเกจ NuGet Aspose.OCR, ไดรเวอร์ GPU ที่รองรับ
- **โค้ดขั้นตอน‑โดย‑ขั้นตอน** ที่โหลดรูปจากไฟล์, ตั้งค่า Aspose OCR GPU engine, และดึงข้อความ
- **ทำไม** คุณอาจต้องตั้งค่าขีดจำกัดหน่วยความจำ GPU และวิธีทำอย่างปลอดภัย
- **การจัดการกรณีขอบ**: รูปความละเอียดต่ำ, ไม่มี GPU, และการแก้ไขคะแนนความมั่นใจ
- **ขั้นตอนต่อไป**: การประมวลผลเป็นชุด, การรวมกับ ASP.NET Core, และการสลับกลับไปใช้ CPU หากจำเป็น

> **เคล็ดลับมืออาชีพ:** หากคุณไม่แน่ใจว่า GPU ของคุณกำลังทำงานหรือไม่ ให้ตรวจสอบตัวตรวจสอบกิจกรรม GPU (เช่น NVIDIA‑SMI) ขณะ OCR ทำงาน คุณจะเห็นการเพิ่มขึ้นของการใช้หน่วยความจำที่ตรงกับขีดจำกัดที่คุณตั้งไว้

---

![แผนภาพแสดงกระบวนการดึงข้อความจากรูปภาพโดยใช้ Aspose OCR GPU engine](extract-text-from-image-aspose-ocr-gpu.png "ดึงข้อความจากรูปภาพโดยใช้ Aspose OCR GPU")

## ขั้นตอนที่ 1: เริ่มต้น Aspose OCR Engine สำหรับการประมวลผลด้วย GPU

สิ่งแรกที่คุณต้องมีคืออินสแตนซ์ `OcrEngine` ที่รู้ว่าจะทำงานบน GPU Aspose มีออบเจ็กต์ `OcrEngineSettings` ที่สะอาดตาซึ่งคุณสามารถระบุ runtime ได้

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**ทำไมจึงสำคัญ:** โดยค่าเริ่มต้น Aspose OCR จะถอยกลับไปใช้ CPU ซึ่งอาจพอรับรูปขนาดเล็กได้แต่จะช้าอย่างน่าเจ็บปวดสำหรับภาพความละเอียดสูง การตั้งค่า `Runtime = OcrRuntime.Gpu` อย่างชัดเจนจะย้ายงานหนักไปที่การ์ดกราฟิก ทำให้คุณเห็นการเพิ่มความเร็วอย่างชัดเจน

## ขั้นตอนที่ 2: (เลือกทำ) ตั้งค่าขีดจำกัดหน่วยความจำ GPU

หากคุณทำงานบนเวิร์กสเตชันที่แชร์หรือคอนเทนเนอร์ที่มีทรัพยากร GPU จำกัด คุณสามารถกำหนดขีดจำกัดหน่วยความจำที่ OCR engine ใช้ได้ การทำเช่นนี้จะป้องกันการล่มจาก out‑of‑memory และทำให้กระบวนการอื่นทำงานได้อย่างราบรื่น

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**เมื่อใดควรใช้:**  
- **สภาพแวดล้อมแบบหลายผู้เช่า** ที่หลายบริการใช้ GPU ร่วมกัน  
- **pipeline CI/CD** ที่จัดสรรหน่วยความจำ GPU คงที่ต่อแต่ละงาน  

หากคุณละเว้นบรรทัดนี้ Aspose จะใช้หน่วยความจำตามที่ต้องการ ซึ่งไม่มีปัญหาในเวิร์กสเตชันที่มี GPU เฉพาะ

## ขั้นตอนที่ 3: โหลดรูปจากไฟล์

ต่อไปเราต้องนำรูปเข้ามาในหน่วยความจำ Aspose OCR ทำงานกับ `System.Drawing.Image` ดังนั้นเราจะใช้ `Image.FromFile` ตรวจสอบให้แน่ใจว่าเส้นทางชี้ไปยังไฟล์ที่มีอยู่ มิฉะนั้นจะเกิดข้อยกเว้น

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**ทำไมการโหลดจากไฟล์ถึงสำคัญ:** นักพัฒนาหลายคนพยายามส่งอาร์เรย์ไบต์โดยตรง ซึ่งทำงานได้แต่เพิ่มขั้นตอนการแปลงที่ไม่จำเป็น การใช้ `Image.FromFile` ทำให้กระบวนการตรงไปตรงมา และคำสั่ง `using` รับประกันว่าการเชื่อมต่อไฟล์จะถูกปล่อยอย่างทันท่วงที

## ขั้นตอนที่ 4: รัน OCR และดึงผลลัพธ์

เมื่อ engine ตั้งค่าเรียบร้อยและรูปถูกโหลดแล้ว เราก็สามารถดึงข้อความได้เมธอด `Recognize` จะคืนค่า `OcrResult` ที่ประกอบด้วยข้อความดิบและคะแนนความมั่นใจ

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**ทำความเข้าใจผลลัพธ์:**  
- `Confidence` มีค่าอยู่ระหว่าง 0 ถึง 1 คะแนนความมั่นใจ 0.95 (หรือ 95 %) มักหมายถึง OCR ถูกต้องมาก  
- `Text` มีการขึ้นบรรทัดใหม่ตามที่ปรากฏในรูป ซึ่งสะดวกต่อการประมวลผลต่อไป

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และจัดการกรณีขอบ

### ตรวจสอบระดับความมั่นใจ

หากความมั่นใจต่ำกว่าเช่น 80 % คุณอาจต้องสลับไปใช้การประมวลผลด้วย CPU หรือทำการปรับภาพล่วงหน้า (เช่น การทำไบนารีไลเซชัน)

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### จัดการกรณีไม่มี GPU

ไม่ใช่ทุกเครื่องจะมี GPU ที่รองรับ Aspose จะโยน `OcrException` หากไม่สามารถเริ่มต้น runtime ของ GPU ได้

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### รูปความละเอียดสูง

รูปขนาดใหญ่มาก (เช่น กว้าง > 4000 px) สามารถใช้หน่วยความจำ GPU มาก หากคุณถึงขีดจำกัดที่ตั้งไว้ก่อนหน้า Aspose จะตัดการประมวลผล ในกรณีนี้ให้ลดขนาดรูปก่อน:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมครบถ้วนที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้ รวมทุกขั้นตอน การจัดการข้อผิดพลาด และตรรกะสลับกลับไปใช้ CPU หากจำเป็น

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

หากความมั่นใจต่ำกว่าขีดจำกัด คุณจะเห็นข้อความสลับไปใช้ CPU เพิ่มเติม

---

## สรุป

ตอนนี้คุณรู้ **วิธีดึงข้อความจากรูปภาพ** ด้วย Aspose OCR GPU engine, **วิธีโหลดรูปจากไฟล์**, และเหตุผลที่ควร **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** สำหรับงานผลิตจริง ตัวอย่างข้างต้นเป็นโซลูชันที่ทำงานได้เต็มรูปแบบและอ้างอิงได้ซึ่งคุณสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

ต่อไปคุณอาจพิจารณา:

- **การประมวลผลเป็นชุด**: วนลูปโฟลเดอร์รูปภาพและบันทึกผลลง CSV  
- **การรวมกับ ASP.NET Core**: เปิด API endpoint ที่รับรูปอัปโหลดและคืนค่า OCR text  
- **การปรับจูนประสิทธิภาพ**: ทดลองค่า `GpuMemoryLimit` ต่าง ๆ และตรวจสอบการใช้ GPU เพื่อหาจุดที่เหมาะที่สุด

ปรับโค้ดให้เข้ากับสถานการณ์ของคุณได้เลย—ไม่ว่าจะเป็นการสร้าง pipeline ดิจิไทซ์เอกสาร, แอปแปลแบบเรียลไทม์, หรือบริการสแกนใบเสร็จ หลักการพื้นฐานยังคงเหมือนเดิม: เริ่มต้น GPU engine, จัดการหน่วยความจำอย่างชาญฉลาด, และตรวจสอบความมั่นใจเสมอ

มีคำถามหรือเจอปัญหา? แสดงความคิดเห็นด้านล่างและมาช่วยกันแก้ไขกันเถอะ. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}