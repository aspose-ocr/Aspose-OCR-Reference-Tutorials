---
category: general
date: 2026-02-25
description: จดจำข้อความจากภาพอย่างรวดเร็วด้วย OCR ที่เร่งด้วย GPU. เรียนรู้การตั้งค่าโหมด
  GPU, โหลดภาพสำหรับ OCR, และดึงข้อความจากไฟล์ TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: th
og_description: จดจำข้อความจากภาพได้ทันทีด้วย OCR ที่เร่งด้วย GPU. คำแนะนำ C# ทีละขั้นตอน
  ครอบคลุมการตั้งค่าโหมด GPU, การโหลดภาพสำหรับ OCR, และการสกัดข้อความจากไฟล์ TIFF.
og_title: รู้จำข้อความจากภาพด้วย OCR ที่เร่งด้วย GPU – คู่มือ C#
tags:
- Aspose OCR
- C#
- GPU computing
title: แยกข้อความจากภาพโดยใช้ OCR ที่เร่งด้วย GPU ใน C#
url: /th/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพด้วย OCR ที่เร่งด้วย GPU ใน C#

เคยต้องการ **จดจำข้อความจากภาพ** แต่ CPU ของคุณทำงานช้าเมื่อสแกนความละเอียดสูงหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่นการแปลงใบแจ้งหนี้เป็นดิจิทัลหรือการเก็บถาวรของหนังสือพิมพ์เก่า—ไฟล์ TIFF เพียงไฟล์เดียวอาจทำให้กระบวนการของคุณหยุดชั่วคราวเป็นหลายนาที ข่าวดีคือ Aspose.OCR ให้คุณสลับโหมดและมอบงานหนักให้ GPU ของคุณ ทำให้การดำเนินการที่ช้าแปรเป็นเกือบทันที

ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด: วิธี **ตั้งค่าโหมด GPU**, วิธี **โหลดภาพสำหรับ OCR**, และวิธี **ดึงข้อความจากไฟล์ TIFF**. เมื่อจบคุณจะมีตัวอย่างที่พร้อมใช้งานและพร้อมผลิตที่คุณสามารถนำไปใส่ในโครงการ .NET 6+ ใดก็ได้.

## ข้อกำหนดเบื้องต้น

- .NET 6 SDK (หรือรุ่นใหม่กว่า) ที่ติดตั้งแล้ว.
- Visual Studio 2022 หรือเครื่องมือแก้ไขใดที่คุณชอบ.
- แพ็กเกจ NuGet ของ Aspose.OCR (`Aspose.OCR`) ที่เพิ่มในโครงการของคุณ.
- GPU ที่รองรับ DirectX 11 หรือใหม่กว่า (GPU สมัยใหม่ส่วนใหญ่ผ่าน).  
  *หากคุณไม่มี GPU คุณยังสามารถรันโค้ดด้วย `GpuMode.Auto`—ไลบรารีจะย้อนกลับไปใช้ CPU โดยอัตโนมัติ.*

> **เคล็ดลับมืออาชีพ:** ตรวจสอบว่าไดรเวอร์ GPU ของคุณเป็นเวอร์ชันล่าสุด; ไดรเวอร์ที่ล้าสมัยอาจทำให้เกิดข้อผิดพลาดการเริ่มต้นที่ไม่ชัดเจน.

## ขั้นตอนที่ 1 – สร้าง OCR engine และตั้งค่าโหมด GPU

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของ `OcrEngine`. วัตถุนี้เก็บการตั้งค่าทั้งหมด รวมถึงว่าตัว engine ควรใช้ GPU หรือไม่.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**ทำไมเรื่องนี้สำคัญ:** การเปิดใช้โหมด GPU จะย้ายการประมวลผลภาพที่ต้องใช้คอมพิวเตอร์หนัก (เช่น การทำไบนารี การกำจัดสัญญาณรบกวน ฯลฯ) ไปยังการ์ดกราฟิก. บน RTX 3060 ระดับกลาง คุณจะเห็น **การเพิ่มความเร็ว 3‑5×** เมื่อเทียบกับการประมวลผลด้วย CPU อย่างเดียว.

## ขั้นตอนที่ 2 – โหลดภาพสำหรับ OCR (ตัวอย่าง TIFF)

Aspose.OCR รองรับหลายรูปแบบ, แต่ TIFF เป็นที่นิยมสำหรับเอกสารสแกนเนื่องจากรักษาคุณภาพแบบไม่มีการสูญเสีย. ใช้ `ImageStream.FromFile` เพื่ออ่านไฟล์เข้าสู่หน่วยความจำ.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**กรณีขอบ:** ไฟล์ TIFF บางไฟล์มีหลายหน้า. `ImageStream.FromFile` จะอ่านเฉพาะหน้าที่แรก. หากคุณต้องการประมวลผลทุกหน้า ให้วนลูปผ่าน `ImageInfo.Pages` และส่งแต่ละหน้าให้ engine แยกกัน.

## ขั้นตอนที่ 3 – ทำการจดจำ

เมื่อ engine ถูกตั้งค่าและภาพถูกโหลดแล้ว, เรียก `Recognize()`. เมธอดนี้จะคืนค่าออบเจกต์ `OcrResult` ที่มีผลลัพธ์เป็นข้อความธรรมดาและเมตาดาต้าเพิ่มเติม.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**ถ้าข้อความดูเป็นอักขระผสม?**  
- ตรวจสอบว่าภาพอยู่ในทิศทางที่อ่านได้ (หมุนหากจำเป็น).  
- ปรับตัวเลือกการประมวลผลล่วงหน้า เช่น `ocrEngine.Config.DeskewEnabled = true;`.  
- สำหรับเอกสารหลายภาษา, ตั้งค่า `ocrEngine.Config.Language = Language.English;` หรือ enum ที่เหมาะสม.

## ขั้นตอนที่ 4 – ตรวจสอบผลลัพธ์และจัดการข้อผิดพลาด

การทำงานที่มั่นคงควรตรวจสอบผลลัพธ์ที่เป็น null และจับข้อยกเว้นที่อาจเกิดขึ้น (เช่น ไดรเวอร์ GPU หาย).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**ทำไมต้องห่อไว้?** การเริ่มต้น GPU อาจโยน `DllNotFoundException` หากไม่มีไลบรารีเนทีฟที่จำเป็น. บล็อก catch จะให้เส้นทางการลดระดับอย่างราบรื่น.

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกอย่างเข้าด้วยกัน, นี่คือตัวโปรแกรมเต็มที่คุณสามารถคอมไพล์และรันได้ทันที. แทนที่เส้นทางไฟล์ด้วย TIFF จริงบนเครื่องของคุณ.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

หาก TIFF มีข้อความภาษาอังกฤษที่อ่านได้, คุณจะเห็นอย่างเช่น:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

หากภาพว่างหรืออ่านไม่ออก, คอนโซลจะแจ้งให้คุณตรวจสอบไฟล์ต้นฉบับ.

## คำถามทั่วไป & ความหลากหลาย

| Question | Answer |
|----------|--------|
| **Can I process JPEG or PNG instead of TIFF?** | แน่นอน. `ImageStream.FromFile` ทำงานกับรูปแบบใดก็ได้ที่ Aspose.OCR รองรับ (PNG, JPEG, BMP, ฯลฯ). |
| **What if I have multiple pages in one TIFF?** | วนลูปผ่าน `ImageInfo.Pages` และกำหนดแต่ละหน้าให้กับ `ocrEngine.Image` ก่อนเรียก `Recognize()`. |
| **Do I need a license for Aspose.OCR?** | การประเมินฟรีทำงานได้สูงสุด 100 หน้า. สำหรับการผลิต, ซื้อไลเซนส์เพื่อเอาลายน้ำการประเมินออก. |
| **How do I change the language model?** | ตั้งค่า `ocrEngine.Config.Language = Language.Spanish;` (หรือ enum ที่สนับสนุนอื่น). |
| **Is there a way to get confidence scores?** | เปิด `ocrEngine.Config.EnableConfidence = true;` แล้วตรวจสอบ `result.Confidence` ต่อบรรทัด. |

## สรุป

ตอนนี้คุณรู้วิธี **จดจำข้อความจากภาพ** ด้วย **pipeline OCR ที่เร่งด้วย GPU** ใน C#. ด้วยการ **ตั้งค่าโหมด GPU**, **โหลดภาพสำหรับ OCR**, และ **ดึงข้อความจากไฟล์ TIFF**, คุณได้สร้างโซลูชันที่เร็วและขยายได้พร้อมใช้งานในงานจริง.

ขั้นตอนต่อไป? ลองเชื่อมโค้ดนี้กับตัวสร้าง PDF เพื่อสร้าง PDF ที่ค้นหาได้, หรือส่งสตริงที่ดึงออกไปยัง pipeline การประมวลผลภาษาธรรมชาติ. คุณยังสามารถทดลองใช้ `GpuMode.Auto` เพื่อทำให้แอปของคุณปรับตัวได้ในสภาพแวดล้อมที่ไม่มี GPU.

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้การทำ OCR ของคุณเร็วเหมือนสายฟ้า! 

![จดจำข้อความจากภาพ ตัวอย่าง](https://example.com/ocr-demo.png "จดจำข้อความจากภาพด้วย OCR ที่เร่งด้วย GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}