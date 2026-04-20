---
category: general
date: 2026-02-28
description: ทำการเตรียมภาพ OCR ด้วย C# เพื่อปรับปรุงความแม่นยำของ OCR. เรียนรู้วิธีโหลดภาพด้วย
  C# และรัน OCR บนภาพโดยใช้ตัวกรอง OCR ของ Aspose.
draft: false
keywords:
- preprocess image OCR
- load image c#
- recognize text from image
- improve ocr accuracy
- run OCR on image
language: th
og_description: ทำการเตรียมภาพ OCR ใน C# เพื่อปรับปรุงความแม่นยำของ OCR. ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อโหลดภาพด้วย
  C# และรัน OCR บนภาพด้วย Aspose.
og_title: การเตรียมภาพ OCR ใน C# – เพิ่มความแม่นยำอย่างรวดเร็ว
tags:
- C#
- OCR
- Image Processing
title: การเตรียมภาพ OCR ใน C# – คู่มือฉบับสมบูรณ์เพื่อเพิ่มความแม่นยำ
url: /th/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-to-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพ OCR ใน C# – คู่มือฉบับสมบูรณ์เพื่อเพิ่มความแม่นยำ

เคยสงสัยไหมว่า **preprocess image OCR** จะทำอย่างไรให้การสกัดข้อความแม่นยำ? คุณไม่ได้เป็นคนเดียว ภาพที่มีเสียงรบกวนหรือเอียงอาจทำให้เครื่อง OCR ที่สมบูรณ์กลายเป็นเกมเดา ซึ่งน่าหงุดหงิดเมื่อคุณต้องการข้อมูลที่เชื่อถือได้อย่างรวดเร็ว ในบทแนะนำนี้เราจะพาไปผ่านโซลูชันเชิงปฏิบัติที่ไม่เพียงแต่ *loads image C#* แต่ยัง **improve OCR accuracy** ด้วยการใช้ฟิลเตอร์อัจฉริยะก่อนที่คุณจะ **run OCR on image** ไฟล์

เราจะครอบคลุมทุกอย่างตั้งแต่การตั้งค่า Aspose.OCR, การเพิ่มฟิลเตอร์การเตรียมภาพที่เหมาะสม, จนถึงการ **recognize text from image** และพิมพ์ผลลัพธ์ ในตอนจบคุณจะได้สคริปต์ที่พร้อมใช้งานและพร้อมผลิตที่สามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือ .NET Framework 4.7+ – API ทำงานเช่นเดียวกัน)
- **Aspose.OCR for .NET** – แพคเกจ NuGet (`Aspose.OCR`) ที่มาพร้อมฟิลเตอร์ที่ทรงพลัง
- ภาพตัวอย่างที่มีเสียงรบกวน, หมุน, หรือคอนทราสต์ต่ำ (เช่น `noisy_rotated.jpg`)
- Visual Studio, Rider หรือเครื่องมือแก้ไข C# ที่คุณชอบ

ไม่มีบริการภายนอก, ไม่มีคีย์คลาวด์—เพียงโค้ด C# แท้ที่ทำงานบนเครื่องเท่านั้น

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และเพิ่ม Namespaces

แรกเริ่ม ดึงไลบรารีจาก NuGet:

```bash
dotnet add package Aspose.OCR
```

จากนั้นนำเข้า Namespaces ที่จำเป็นที่ส่วนหัวของไฟล์ของคุณ:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;
```

> **เคล็ดลับ:** หากคุณใช้ .NET 6 กับ top‑level statements คุณสามารถวางคำสั่ง `using` ไว้หลังบล็อก `global using` เพื่อให้โค้ดดูสะอาดขึ้น

## ขั้นตอนที่ 2: สร้าง OCR Engine และแนบฟิลเตอร์การเตรียมภาพ

หัวใจของ **preprocess image OCR** คือสายการทำงานของฟิลเตอร์ ฟิลเตอร์ที่มีประสิทธิภาพสองตัวคือ `DeskewFilter` (หมุนภาพอัตโนมัติ) และ `DenoiseFilter` (ลบจุดรบกวน) การเพิ่มฟิลเตอร์เหล่านี้ตั้งแต่ต้นจะทำให้ engine ทำงานบนผืนผ้าใบที่สะอาดขึ้น

```csharp
// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Attach filters to boost accuracy
ocrEngine.Filters.Add(new DeskewFilter());   // Auto‑rotate
ocrEngine.Filters.Add(new DenoiseFilter()); // Reduce visual noise
```

ทำไมต้องใช้ฟิลเตอร์เหล่านี้? ข้อความเอียงมักทำให้การแยกอักขระผิดพลาด, ส่วนพิกเซลสุ่มอาจถูกเข้าใจเป็น glyphs. ด้วยการ **improve OCR accuracy** ด้วยการ deskew และ denoise, คุณจะให้สัญญาณที่ชัดเจนกว่ากับ recognizer

## ขั้นตอนที่ 3: โหลดภาพที่คุณต้องการประมวลผล

ตอนนี้เราจะ **load image C#** แบบสไตล์ C#. เมธอด `Image.Load` ของ Aspose.OCR รองรับเส้นทางไฟล์, สตรีม, หรือแม้กระทั่ง `Bitmap`. นี่คือวิธีที่ง่ายที่สุดโดยใช้ไฟล์:

```csharp
// Step 3: Load the source image (replace with your own path)
using var sourceImage = Image.Load(@"C:\Images\noisy_rotated.jpg");
```

> **กรณีพิเศษ:** หากภาพของคุณอยู่ใน memory stream (เช่นอัปโหลดผ่าน API) ให้ใช้ `Image.Load(stream)` แทน สายฟิลเตอร์ทำงานเช่นเดียวกัน

## ขั้นตอนที่ 4: รัน OCR บนภาพที่ผ่านการกรอง

เมื่อ engine ถูกตั้งค่าและโหลดภาพแล้ว ถึงเวลาที่จะ **run OCR on image** เมธอด `Recognize` จะคืนค่า `OcrResult` ที่มีข้อความที่สกัดออกมา, คะแนนความมั่นใจ, และแม้กระทั่ง bounding boxes หากคุณต้องการใช้ในภายหลัง

```csharp
// Step 4: Perform OCR on the preprocessed image
var ocrResult = ocrEngine.Recognize(sourceImage);
```

หากคุณต้องการค่าความมั่นใจดิบของแต่ละบรรทัด คุณสามารถตรวจสอบ `ocrResult.Lines` – แต่ละบรรทัดมี property `Confidence` นั่นเป็นประโยชน์เมื่อคุณต้องการทำเครื่องหมายผลลัพธ์ที่ความมั่นใจต่ำเพื่อการตรวจสอบด้วยมือ

## ขั้นตอนที่ 5: แสดงข้อความที่ได้รับการจดจำ

สุดท้าย แสดงข้อความหรือเขียนลงไฟล์ สำหรับการสาธิตอย่างรวดเร็ว เราจะพิมพ์ลงคอนโซล:

```csharp
// Step 5: Show the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

คุณควรเห็นประโยคที่สะอาดและอ่านง่ายหากการเตรียมภาพทำงาน หากผลลัพธ์ยังดูเป็นอักขระผสมแป้น ให้พิจารณาเพิ่มฟิลเตอร์เช่น `ContrastAdjustmentFilter` หรือ `BinarizationFilter`—Aspose มีชุดฟิลเตอร์ครบ

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรันที่เชื่อมทุกขั้นตอนเข้าด้วยกัน คัดลอกและวางลงในโปรเจกต์คอนโซลใหม่แล้วกด **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with helpful filters
        var ocrEngine = new OcrEngine();
        ocrEngine.Filters.Add(new DeskewFilter());   // Auto‑rotate the image
        ocrEngine.Filters.Add(new DenoiseFilter()); // Remove visual noise

        // 2️⃣ Load the image you want to process
        using var preprocessedImage = Image.Load(@"C:\Images\noisy_rotated.jpg");

        // 3️⃣ Run OCR on the filtered image
        var ocrResult = ocrEngine.Recognize(preprocessedImage);

        // 4️⃣ Output the recognized text
        System.Console.WriteLine("=== OCR Result ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
=== OCR Result ===
The quick brown fox jumps over the lazy dog.
```

หากรูปต้นฉบับมีประโยคดังกล่าว ฟิลเตอร์ควรจะลบความเบลอและทำให้ข้อความตรงขึ้น ทำให้ engine อ่านได้อย่างสมบูรณ์

## ปัญหาที่พบบ่อย & วิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ภาพเบลอยังอ่านไม่ได้** | การใช้ Denoise เพียงอย่างเดียวไม่สามารถกู้รายละเอียดที่หายไปได้. | เพิ่ม `SharpnessFilter` หรือขยายขนาดภาพก่อน OCR. |
| **ข้อความยังเอียง** | Deskew อาจต้องการการตรวจจับมุมที่แรงขึ้น. | ใช้ `DeskewFilter` พร้อมกำหนด `AngleThreshold` เอง (เช่น `new DeskewFilter(0.5)` ). |
| **คะแนนความมั่นใจต่ำ** | คอนทราสต์ของภาพต่ำเกินไป. | ใส่ `ContrastAdjustmentFilter` หรือ `BinarizationFilter`. |
| **ข้อผิดพลาด Out‑of‑memory** | ภาพขนาดใหญ่มากใช้ RAM มาก. | ลดขนาดด้วย `ResizeFilter` ก่อนประมวลผล. |

## เมื่อใดควรใช้ฟิลเตอร์เพิ่มเติม

Aspose.OCR มาพร้อมกับฟิลเตอร์หลากหลาย: `GammaCorrectionFilter`, `ColorInversionFilter`, `CropFilter` และอื่น ๆ หากกระบวนการทำงานของคุณเกี่ยวกับเอกสารสแกนที่มีลายน้ำ ให้ลองใช้ `CropFilter` เพื่อตัดขอบที่มีเสียงรบกวนออก สำหรับภาพที่ถ่ายในแสงน้อย `GammaCorrectionFilter` สามารถทำให้ข้อความสว่างขึ้นโดยไม่ทำให้พื้นหลังสว่างเกินไป

## ขั้นตอนต่อไป: ไปไกลกว่าการ OCR พื้นฐาน

ตอนนี้คุณได้เชี่ยวชาญ **preprocess image OCR** แล้ว ลองพิจารณาการขยายต่อไปนี้:

- **Batch processing** – วนลูปผ่านโฟลเดอร์ของภาพ, ใช้สายฟิลเตอร์เดียวกัน.
- **Language selection** – ตั้งค่า `ocrEngine.Language = OcrLanguage.English;` สำหรับโครงการหลายภาษา.
- **Export to structured formats** – ใช้ `ocrResult.ToJson()` หรือเขียนเป็น CSV สำหรับการวิเคราะห์ต่อไป.
- **Integrate with Azure Blob Storage** – ดึงภาพโดยตรงจากคลาวด์, เตรียมภาพ, แล้วเก็บข้อความที่สกัดกลับไป.

## สรุป

เราได้อธิบายขั้นตอนการทำงาน **preprocess image OCR** อย่างครบถ้วนใน C# โดยการสร้าง `OcrEngine`, แนบ `DeskewFilter` และ `DenoiseFilter`, โหลดรูปภาพ, และในที่สุด **recognize text from image**, คุณสามารถ **improve OCR accuracy** อย่างมากและ **run OCR on image** ไฟล์ได้อย่างเชื่อถือได้ โค้ดนี้เป็นอิสระเต็มรูปแบบ ทำงานกับ .NET เวอร์ชันล่าสุด และสามารถขยายต่อสำหรับงานแบบแบตช์, รองรับหลายภาษา, หรือการผสานกับคลาวด์

ลองใช้กับสแกนที่มีเสียงรบกวนของคุณ—ปรับพารามิเตอร์ฟิลเตอร์, อาจเพิ่ม `ContrastAdjustmentFilter`, แล้วดูข้อความที่ปรากฏขึ้น หากเจอปัญหาใด ๆ เอกสาร Aspose.OCR (ค้นหา “Aspose OCR filters”) จะเป็นคู่มือที่ดี แต่กรณีส่วนใหญ่ถูกครอบคลุมไว้ที่นี่

ขอให้เขียนโค้ดอย่างสนุกสนาน และขอให้ OCR ของคุณใสเหมือนคริสตัล!

![preprocess image OCR example](/images/ocr-preprocess-example.png "Illustration of preprocessing steps for OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}