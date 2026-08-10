---
category: general
date: 2026-05-31
description: เรียนรู้วิธีการจดจำข้อความจากภาพใน C# ด้วย Aspose OCR รวมถึงวิธีการดึงข้อความจากไฟล์
  TIFF และการโหลดภาพสำหรับ OCR อย่างมีประสิทธิภาพ
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: th
og_description: คู่มือขั้นตอนการจดจำข้อความจากภาพด้วย Aspose OCR ครอบคลุมการสกัดจากไฟล์
  TIFF และการโหลดภาพอย่างเหมาะสมสำหรับ OCR.
og_title: แยกข้อความจากภาพใน C# โดยใช้ Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: แยกข้อความจากภาพใน C# ด้วย Aspose OCR
url: /th/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพใน C# ด้วย Aspose OCR

เคยต้อง **จดจำข้อความจากรูปภาพ** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรใน C# หรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องจัดการกับเอกสารสแกนหรือไฟล์ TIFF หลายหน้า ในคู่มือนี้เราจะพาคุณผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบที่ **จดจำข้อความจากรูปภาพ** ด้วยไลบรารี Aspose OCR และเรายังจะแสดงวิธี **ดึงข้อความจาก tiff** และวิธีที่ดีที่สุดในการ **โหลดรูปภาพสำหรับ OCR** โดยไม่ต้องเสียศีรษะ

เราจะครอบคลุมทุกอย่างตั้งแต่การติดตั้งแพ็กเกจ NuGet ไปจนถึงการจัดการการเร่งความเร็วด้วย GPU และการกลับไปใช้ CPU เมื่อจำเป็น เมื่อจบบทเรียนนี้คุณจะมีแอปคอนโซลที่พิมพ์ข้อความที่จดจำได้และเวลาการประมวลผล—ไม่มีส่วนที่ขาดหาย ไม่มีการอ้างอิงที่คลุมเครือ

## สิ่งที่คุณจะสร้าง

- แอปคอนโซล .NET ง่าย ๆ ที่โหลดรูปภาพ (รวมถึง TIFF หลายหน้า)  
- เครื่องมือ OCR ที่กำหนดค่าให้ใช้ GPU พร้อมการสำรองด้วย CPU อย่างราบรื่น  
- การดึงข้อความธรรมดาจากรูปภาพและพิมพ์ออกที่คอนโซล  
- ข้อมูลเวลาเพื่อให้คุณเห็นผลกระทบของประสิทธิภาพระหว่าง GPU กับ CPU  

**ข้อกำหนดเบื้องต้น**

- .NET 6 SDK หรือใหม่กว่า (โค้ดทำงานกับ .NET Core และ .NET Framework)  
- ความคุ้นเคยพื้นฐานกับ C# และบรรทัดคำสั่ง  
- การเชื่อมต่ออินเทอร์เน็ตเพื่อดึงแพ็กเกจ Aspose.OCR จาก NuGet  

ถ้าคุณมีทั้งหมดนี้แล้ว มาเริ่มกันเลย

![โค้ด C# เพื่อจดจำข้อความจากรูปภาพด้วย Aspose OCR](image.png "โค้ด C# เพื่อจดจำข้อความจากรูปภาพด้วย Aspose OCR")

## ขั้นตอนที่ 1 – จดจำข้อความจากรูปภาพ: ตั้งค่าเครื่องมือ OCR

ก่อนอื่นเราต้องสร้างอินสแตนซ์ `OcrEngine` Aspose OCR ให้คุณเลือกอุปกรณ์ประมวลผล—GPU เพื่อความเร็ว, CPU เป็นเครือข่ายสำรอง เครื่องมือยังรับค่าคำแนะนำเรื่องขีดจำกัดหน่วยความจำ ซึ่งเป็นประโยชน์บนเครื่องที่แชร์ทรัพยากร

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
การเลือก `OcrDevice.Gpu` สามารถลดเวลาการจดจำได้หลายวินาทีสำหรับรูปภาพขนาดใหญ่ โดยเฉพาะ TIFF หลายหน้า `GpuMemoryLimit` ป้องกันแอปของคุณไม่ให้ใช้หน่วยความจำ GPU ทั้งหมดบนเครื่องที่แชร์

## ขั้นตอนที่ 2 – โหลดรูปภาพสำหรับ OCR (รองรับ TIFF)

ต่อไปเราจะส่งรูปภาพให้กับเครื่องมือ Aspose `ImageStream.FromFile` รองรับ **ทุก** ฟอร์แมตที่ไลบรารีสนับสนุน—TIFF, PNG, JPEG, ตามที่คุณต้องการ ขั้นตอนนี้ตอบโจทย์ความต้องการ **โหลดรูปภาพสำหรับ OCR** โดยตรง

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**เคล็ดลับ:** หากคุณทำงานกับ TIFF หลายหน้า Aspose จะจัดการแต่ละหน้าเป็นเฟรมแยกจากกันโดยอัตโนมัติและเครื่องมือจะประมวลผลต่อเนื่อง ไม่ต้องเขียนโค้ดเพิ่มเติม

## ขั้นตอนที่ 3 – เรียกใช้การจดจำและ **ดึงข้อความจาก tiff**

เมื่อเครื่องมือพร้อมและรูปภาพถูกโหลดแล้ว เราจะเริ่มกระบวนการ OCR วิธี `Recognize` จะคืนค่า `OcrResult` ที่มีข้อความธรรมดา, คะแนนความเชื่อมั่น, และรายละเอียดเวลา

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**การจัดการกรณีขอบ:**  
หาก GPU ไม่พร้อมใช้งาน `engine.Recognize()` ยังทำงานได้เพราะเครื่องมือจะสลับไปใช้ CPU อย่างเงียบ คุณสามารถตรวจสอบ `engine.Device` หลังการจดจำเพื่อบันทึกว่าอุปกรณ์ใดถูกใช้จริง

## ขั้นตอนที่ 4 – ดึงข้อความธรรมดาที่จดจำได้

การดึงข้อความทำได้ง่าย—อ่านค่า `Text` property นี่คือจุดที่เราจบการ **ดึงข้อความจาก tiff** (หรือรูปภาพอื่น) และแสดงให้ผู้ใช้เห็น

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

คุณจะเห็นอักขระดิบ ๆ พร้อมการขึ้นบรรทัดใหม่ตามที่ปรากฏในรูปต้นฉบับ หากต้องการผลลัพธ์ที่มีโครงสร้างมากขึ้น (เช่น JSON หรือ CSV) คุณสามารถสำรวจ `result.Regions` และ `result.Lines` ได้ แต่ข้อความธรรมดามักเพียงพอสำหรับสคริปต์เร็ว ๆ

## ขั้นตอนที่ 5 – วัดเวลาการประมวลผลและจัดการการสำรอง GPU

ประสิทธิภาพเป็นสิ่งสำคัญโดยเฉพาะเมื่อคุณต้องประมวลผลหลายสิบหน้า คุณสมบัติ `ProcessingTime` บอกเวลาที่ OCR ใช้จริง ไม่ว่าจะรันบน GPU หรือ CPU

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**ทำไมคุณควรใส่ใจ:**  
หากสังเกตเห็นเวลาเพิ่มขึ้น คุณอาจต้องปรับ `GpuMemoryLimit` หรือสลับไปใช้ CPU อย่างชัดเจน (`Device = OcrDevice.Cpu`) ในทางกลับกัน ผลลัพธ์ภายในวินาทีเดียวบน TIFF ขนาดใหญ่หมายความว่า GPU ของคุณทำงานได้ดี

## ตัวอย่างเต็มพร้อมรัน

คัดลอกโค้ดด้านล่างไปยังโปรเจกต์คอนโซลใหม่ (`dotnet new console -n OcrDemo`) แล้วรัน `dotnet add package Aspose.OCR` จากนั้นเปลี่ยน `YOUR_DIRECTORY/sample_multi_page.tif` ให้เป็นพาธของรูปภาพของคุณ

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัดทอนเพื่อความกระชับ):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

หากเครื่องของคุณไม่มี GPU ที่รองรับ เวลาอาจยาวขึ้นหลายวินาทีเล็กน้อย แต่ข้อความยังคงถูกดึงออกมาได้อย่างถูกต้อง

## คำถามที่พบบ่อยและข้อควรระวัง

- **ถ้ารูปภาพใหญ่เกิน (มากกว่า 10 MB) จะทำอย่างไร?**  
  ลดความละเอียดก่อนส่งให้เครื่องมือ หรือเพิ่ม `GpuMemoryLimit` หากมี VRAM เพียงพอ  
- **สามารถประมวลผลหลายรูปภาพในลูปได้หรือไม่?**  
  ทำได้แน่นอน เพียงใช้อินสแตนซ์ `OcrEngine` เดียวกันและกำหนด `ImageStream` ใหม่ในแต่ละรอบ  
- **ต้องทำการ Dispose อะไรบ้างหรือไม่?**  
  `OcrEngine` implements `IDisposable` ใช้บล็อก `using` เพื่อจัดการทรัพยากรอย่างสะอาด โดยเฉพาะเมื่อใช้ GPU  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **รองรับภาษานอกเหนือจากอังกฤษหรือไม่?**  
  ตั้งค่า `engine.Language = OcrLanguage.Spanish` (หรือภาษาที่สนับสนุนอื่น) ก่อนเรียก `Recognize()`  

## สรุป

ตอนนี้คุณมีโซลูชันครบวงจรที่ **จดจำข้อความจากรูปภาพ** ใน C# ด้วย Aspose OCR บทเรียนนี้ได้อธิบายวิธี **โหลดรูปภาพสำหรับ OCR**, วิธี **ดึงข้อความจาก tiff**, และวิธีวัดประสิทธิภาพพร้อมการสำรอง GPU อย่างราบรื่น

ต่อจากนี้คุณอาจ:

- ทดลองกับฟอร์แมตรูปภาพต่าง ๆ (BMP, PDF) เพื่อดูว่า Aspose จัดการอย่างไร  
- สำรวจ `result.Regions` เพื่อรับข้อมูล bounding‑box หากต้องการจัดการเลย์เอาต์อย่างละเอียด


## คุณควรเรียนรู้อะไรต่อไป?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}