---
category: general
date: 2026-05-06
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR พร้อมการสนับสนุน GPU เรียนรู้วิธีดึงข้อความอย่างรวดเร็วในบทเรียน
  OCR ด้วย C# ที่ครอบคลุมการตั้งค่า โค้ด และแนวปฏิบัติที่ดีที่สุด.
draft: false
keywords:
- extract text from image
- how to extract text
- c# ocr tutorial
- Aspose OCR GPU
- C# image processing
language: th
og_description: ดึงข้อความจากรูปภาพด้วย Aspose OCR ใน C#. คู่มือนี้แสดงวิธีดึงข้อความอย่างรวดเร็วโดยใช้การเร่งความเร็วด้วย
  GPU และให้คำตอบเกี่ยวกับวิธีดึงข้อความแบบทีละขั้นตอน.
og_title: สกัดข้อความจากภาพใน C# – คอร์ส OCR ฉบับสมบูรณ์
tags:
- OCR
- C#
- Aspose
title: สกัดข้อความจากภาพใน C# – คู่มือ OCR ฉบับสมบูรณ์
url: /th/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน C# – การสอน OCR ฉบับสมบูรณ์

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าห้องสมุดใดจะให้ความเร็ว *และ* ความแม่นยำหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาจำนวนมากเจออุปสรรคนี้เมื่อต้องสร้างสายงานการแปลงเอกสารเป็นดิจิทัล ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถดึงข้อความจากบิตแมปเกือบทุกประเภทได้ และด้วยโค้ดเพียงไม่กี่บรรทัด คุณจะได้การเร่งความเร็วด้วย GPU ทำงานเบื้องหลัง

ใน **C# OCR tutorial** นี้ เราจะพาคุณผ่านทุกอย่างที่ต้องรู้: ตั้งแต่การติดตั้งแพ็กเกจ NuGet, การกำหนดค่าโหมด GPU, จนถึงการจัดการไฟล์ TIFF หลายหน้า ตอนจบคุณจะสามารถตอบคำถามคลาสสิก “วิธีดึงข้อความ” ได้อย่างมั่นใจ และคุณจะมีตัวอย่างพร้อมรันที่สามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณจะได้เรียนรู้

- ขั้นตอนที่แม่นยำ **วิธีดึงข้อความ** จากไฟล์รูปภาพโดยใช้ Aspose OCR
- วิธีเปิดใช้งานการเร่งความเร็วด้วย GPU เพื่อประสิทธิภาพที่สูงขึ้นอย่างมหาศาล
- จุดบกพร่องทั่วไป (เช่น ไดรเวอร์ CUDA หาย) และวิธีแก้ไขอย่างรวดเร็ว
- วิธีขยายโซลูชันสำหรับการประมวลผลเป็นชุดหรือรูปแบบภาพที่ต่างกัน

> **เคล็ดลับมืออาชีพ:** หากคุณอยู่บนเครื่องพัฒนาที่ไม่มี GPU แยกเฉพาะ คุณยังสามารถรันโค้ดในโหมด CPU ได้—แค่ตั้งค่า `UseGpu = false` ส่วนที่เหลือของการสอนจะเหมือนเดิม

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผล |
|-------------|----------------|
| .NET 6.0 หรือใหม่กว่า (หรือ .NET Framework 4.7.2+) | Aspose OCR รองรับรันไทม์สมัยใหม่ |
| Visual Studio 2022 (หรือ IDE ที่คุณชอบ) | ช่วยในการดีบักและการรวม NuGet |
| NVIDIA GPU ที่รองรับ CUDA 11+ (ไม่บังคับแต่แนะนำ) | จำเป็นสำหรับการตั้งค่า `UseGpu = true` |
| Aspose.OCR NuGet package (`Aspose.OCR` and `Aspose.OCR.Gpu`) | ให้เครื่องยนต์ OCR และการสนับสนุน GPU |

หากข้อใดขาดหาย คุณจะเจอข้อผิดพลาดระหว่างคอมไพล์หรือข้อยกเว้นขณะรัน—ไม่ต้องตกใจ การสอนนี้อธิบายวิธีกู้คืน

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ Aspose OCR

เปิดโฟลเดอร์โปรเจกต์ของคุณในเทอร์มินัลและรัน:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

แพ็กเกจสองตัวนี้ให้ฟังก์ชัน OCR หลักพร้อมชั้นการเร่งความเร็วด้วย GPU หลังการติดตั้ง คุณจะเห็น assembly ที่อ้างอิงในไฟล์ `.csproj` ของคุณ

## ขั้นตอนที่ 2: กำหนดค่า OCR Settings สำหรับ GPU

ตอนนี้เราจะสร้างอ็อบเจกต์ `OcrEngineSettings` และบอกให้เอนจิ้นใช้ GPU นี่คือจุดที่ **ดึงข้อความจากรูปภาพ** ได้รับการเพิ่มประสิทธิภาพ

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Required for GPU acceleration

// Configure OCR to run on the first available GPU (device ID 0)
var ocrSettings = new OcrEngineSettings
{
    UseGpu = true,          // Turn on GPU acceleration
    GpuDeviceId = 0         // Optional: specify which GPU to use
};
```

> **เหตุผลที่สำคัญ:** การเปิดใช้งาน GPU จะย้ายงานหนัก (การเตรียมพิกเซล, การสรุปผลแบบนิวรัล) จาก CPU ไปยังการ์ดกราฟิก ทำให้เวลาในการประมวลผลลดจากวินาทีเป็นมิลลิวินาที

หากคุณไม่มี GPU ที่เข้ากันได้ เพียงตั้งค่า `UseGpu = false` เอนจิ้นจะกลับไปใช้โหมด CPU โดยไม่ต้องแก้ไขโค้ดใด ๆ

## ขั้นตอนที่ 3: เริ่มต้น OCR Engine

เมื่อการตั้งค่าพร้อมแล้ว ให้สร้างอินสแตนซ์ของ `OcrEngine` อ็อบเจกต์นี้เก็บการกำหนดค่าและจะถูกใช้ซ้ำสำหรับแต่ละภาพที่คุณประมวลผล

```csharp
// Create the OCR engine with the previously defined settings
var ocrEngine = new OcrEngine(ocrSettings);
```

คุณอาจสงสัยว่าทำไมต้องแยกการตั้งค่าออกจากเอนจิ้น คำตอบคือความยืดหยุ่น—โดยสลับ `ocrSettings` คุณสามารถใช้อินสแตนซ์ `ocrEngine` เดียวกันกับหลายไฟล์ได้ และสลับระหว่าง GPU กับ CPU ได้ตามต้องการ

## ขั้นตอนที่ 4: จดจำข้อความจากภาพของคุณ

นี่คือหัวใจของกระบวนการ **วิธีดึงข้อความ** เราเรียก `RecognizeImage` และส่งพาธของไฟล์ที่ต้องการวิเคราะห์ เมธอดจะคืนค่า `OcrResult` ที่บรรจุสตริงที่ดึงออกมาและคะแนนความมั่นใจ

```csharp
// Replace with the actual path to your image file
string imagePath = @"C:\Images\sample_multi_page.tif";

// Perform OCR – this will extract text from the image
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

> **กรณีขอบ:** หากภาพเป็นไฟล์ TIFF หลายหน้า Aspose OCR จะประมวลผลแต่ละหน้าโดยอัตโนมัติและต่อผลลัพธ์เข้าด้วยกัน หากต้องการผลลัพธ์ต่อหน้า ให้ตรวจสอบ `ocrResult.PageResults`

## ขั้นตอนที่ 5: แสดงหรือบันทึกข้อความที่ดึงออกมา

สุดท้าย ให้แสดงผลลัพธ์บนคอนโซล, เขียนลงไฟล์, หรือส่งต่อไปยังระบบอื่น สำหรับการสอนนี้เราจะพิมพ์ออกเท่านั้น

```csharp
// Show the extracted text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

เมื่อคุณรันโปรแกรม คุณควรเห็นอะไรบางอย่างเช่น:

```
=== OCR Output ===
Invoice #12345
Date: 04/30/2026
Total: $1,250.00
...
```

นั่นคือช่วงเวลาที่คุณ **ดึงข้อความจากรูปภาพ** สำเร็จโดยใช้ Aspose OCR

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นแอปคอนโซลที่พร้อมรันครบทุกส่วน คัดลอก‑วางลงในไฟล์ `Program.cs` ใหม่และกด **F5**

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Required for GPU acceleration

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure OCR settings (GPU enabled)
            var ocrSettings = new OcrEngineSettings
            {
                UseGpu = true,          // Turn on GPU acceleration
                GpuDeviceId = 0         // Optional: specify which GPU to use
            };

            // 2️⃣ Initialize the OCR engine with those settings
            var ocrEngine = new OcrEngine(ocrSettings);

            // 3️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY\sample_multi_page.tif";

            // 4️⃣ Perform OCR – this extracts the text
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Output the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมกับใบแจ้งหนี้ที่พิมพ์ชัดเจนจะให้ข้อความแบบ plain‑text ของฟิลด์ในใบแจ้งหนี้ หากภาพเบลอหรือภาษาที่ใช้ไม่ได้รับการสนับสนุน `ocrResult.Text` อาจมีอักขระแปลก ๆ — ปรับการเตรียมภาพ (เช่น การทำไบนารี) หรือสลับไปใช้โมเดลภาษาที่ต่างกันเพื่อความแม่นยำที่ดีกว่า

## คำถามทั่วไป & การแก้ไขปัญหา

**ถาม: แอปของฉันพังด้วยข้อความ “CUDA driver not found”.**  
ตอบ: ตรวจสอบว่าได้ติดตั้ง CUDA 11+ แล้วและไดรเวอร์ GPU ตรงกับเวอร์ชัน CUDA คุณสามารถรัน `nvidia-smi` จากพรอมต์เพื่อยืนยันว่าไดรเวอร์ปรากฏ

**ถาม: จะประมวลผลโฟลเดอร์เต็มของภาพอย่างไร?**  
ตอบ: ห่อการเรียก `RecognizeImage` ไว้ในลูป `foreach (var file in Directory.GetFiles(folder, "*.tif"))` อย่าลืมใช้อินสแตนซ์ `ocrEngine` เดียวกันเพื่อประสิทธิภาพ

**ถาม: สามารถดึงข้อความจาก PDF ได้หรือไม่?**  
ตอบ: ไม่ได้โดยตรงกับ Aspose OCR แต่คุณสามารถแปลงหน้าของ PDF เป็นภาพก่อน (ใช้ Aspose.PDF หรือไลบรารีอื่น) แล้วจึงส่งภาพเหล่านั้นเข้าสู่ขั้นตอน OCR

**ถาม: ถ้าต้องการดึงข้อความในภาษาที่ไม่ใช่อังกฤษจะทำอย่างไร?**  
ตอบ: ตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish` (หรือภาษาอื่นที่รองรับ) ก่อนเรียก `RecognizeImage`

## การขยายการสอน

- **การประมวลผลเป็นชุด:** ผสานโค้ดกับ `Parallel.ForEach` เพื่อประมวลผลหลายคอร์เมื่อไม่มี GPU
- **การประมวลผลหลังจาก OCR:** ใช้ regular expressions ทำความสะอาดหมายเลขโทรศัพท์, วันที่, หรือค่าเงิน
- **การบูรณาการ:** ส่งสตริงที่ดึงออกไปยังฐานข้อมูลหรือดัชนี Azure Cognitive Search เพื่อทำเอกสารให้ค้นหาได้

## สรุป

คุณมี **C# OCR tutorial** ที่ครบถ้วนแล้ว ซึ่งแสดง **วิธีดึงข้อความ** จากภาพโดยใช้การเร่งความเร็วด้วย GPU และจัดการไฟล์หลายหน้าอย่างราบรื่น ด้วยการทำตามขั้นตอนข้างต้น คุณสามารถรวม Aspose OCR เข้าในโปรเจกต์ .NET ใดก็ได้และเริ่มแปลงรูปภาพเป็นข้อความที่ค้นหาและแก้ไขได้ในเวลาอันสั้น

พร้อมรับความท้าทายต่อไปหรือยัง? ลองสลับฟล็ก GPU ปิดเพื่อดูความแตกต่างของประสิทธิภาพ หรือทดลองกับรูปแบบภาพอื่น ๆ เช่น PNG หรือ JPEG ไม่มีขีดจำกัด—ขอให้สนุกกับการเขียนโค้ด!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}