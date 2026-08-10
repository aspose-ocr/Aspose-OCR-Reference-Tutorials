---
category: general
date: 2026-03-20
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพและกำจัดสัญญาณรบกวนของภาพด้วย Aspose
  OCR คู่มือแบบทีละขั้นตอนนี้ยังแสดงวิธีการเตรียมภาพล่วงหน้าสำหรับ OCR และเพิ่มความแม่นยำของ
  OCR
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: th
og_description: เรียนรู้วิธีการปรับแนวภาพและกำจัดสัญญาณรบกวนด้วย Aspose OCR เพิ่มความแม่นยำของ
  OCR ของคุณในไม่กี่นาที.
og_title: วิธีแก้เอียงภาพ – คู่มือ C# ฉบับสมบูรณ์สำหรับการประมวลผลล่วงหน้า OCR
tags:
- OCR
- C#
- Image Processing
title: วิธีแก้ไขการเอียงของภาพ – คู่มือ C# ฉบับสมบูรณ์สำหรับการเตรียมข้อมูล OCR
url: /th/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการปรับแนวภาพ – คู่มือ C# ฉบับสมบูรณ์สำหรับการเตรียม OCR

เคยสงสัยไหมว่า **how to deskew image** ไฟล์ที่สแกนออกมามีมุมแปลก ๆ? คุณไม่ได้เป็นคนเดียว; นักพัฒนาหลายคนเจอปัญหาเดียวกันเมื่อต้องส่งรูปภาพให้กับเครื่อง OCR. ข่าวดีคือด้วยไม่กี่บรรทัดของ C# และ Aspose OCR คุณสามารถทำให้ภาพตรง, ลดสัญญาณรบกวน, และเพิ่มคอนทราสต์ในขั้นตอนเดียว—ไม่ต้องใช้ Photoshop.

ในบทแนะนำนี้เราจะพาไปดูทุกอย่างที่คุณต้องรู้: ตั้งแต่การโหลดภาพที่เอียง, ไปจนถึง **remove image noise**, **preprocess image for OCR**, และสุดท้าย **recognize text from image** ด้วยคะแนน **improve OCR accuracy** ที่สูง. เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งแปลงสแกนที่ยุ่งเหยิงให้เป็นข้อความที่สะอาดและค้นหาได้.

## สิ่งที่คุณต้องการ

- .NET 6 หรือใหม่กว่า (โค้ดใช้ไวยากรณ์ `using var` ซึ่งรองรับตั้งแต่ C# 8)
- แพคเกจ NuGet ของ Aspose OCR (`Aspose.OCR`) – ติดตั้งโดยใช้ `dotnet add package Aspose.OCR`
- รูปตัวอย่างที่เอียงและมีสัญญาณรบกวน (เช่น `skewed_noisy.png`)
- IDE หรือโปรแกรมแก้ไขที่คุณชอบ (Visual Studio, VS Code, Rider… คุณเลือก)

> **เคล็ดลับ:** หากคุณไม่มีไฟล์ตัวอย่าง เพียงหมุนภาพหน้าจอที่ชัดเจนหลายองศาและเพิ่มสัญญาณรบกวน “salt‑and‑pepper” ด้วยโปรแกรมแก้ไขภาพ. ขั้นตอนทำงานเช่นเดียวกัน.

## ขั้นตอนที่ 1: วิธีการปรับแนวภาพด้วย Deskew Filter

สิ่งแรกที่เราทำคือแก้ไขการหมุน. Aspose มี `DeskewFilter` ที่สามารถตรวจจับมุมโดยอัตโนมัติได้จนถึง `MaxAngle` ที่กำหนดได้. การตั้งค่าเป็น **5°** เป็นค่าเริ่มต้นที่ปลอดภัยสำหรับเอกสารสแกนส่วนใหญ่.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**ทำไมเรื่องนี้สำคัญ:**  
หากข้อความเอียง อัลกอริทึม OCR อาจตีความอักขระผิด—เช่น “l” กลายเป็น “i”. ด้วยการ **deskewing** ก่อน คุณจะให้เครื่องทำงานบนผืนผ้าใบที่ตรง.

## ขั้นตอนที่ 2: การลบสัญญาณรบกวนภาพด้วย Despeckle

การสแกนจากโทรศัพท์ราคาถูกหรือสแกนเนอร์เก่า ๆ มักมีจุดรบกวนที่ดูเหมือนจุดสุ่ม. จุดเหล่านั้นทำให้ตัวจดจำอักขระสับสน. `DespeckleFilter` ทำให้ภาพเรียบขึ้นโดยคงขอบไว้.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

หากคุณต้องการ **remove image noise** อย่างเข้มข้นขึ้น ให้เพิ่มค่า `Strength` เป็น 3 หรือ 4—แต่ระวังการสูญเสียเส้นบาง.

## ขั้นตอนที่ 3: การเตรียมภาพสำหรับ OCR – เพิ่มคอนทราสต์

การสแกนที่คอนทราสต์ต่ำ (สีเทาอ่อนบนกระดาษสีขาว) อาจทำให้ OCR พลาดตัวอักษรที่จาง. `ContrastFilter` ขยายช่วงโทน ทำให้พิกเซลสีเข้มเข้มขึ้นและพิกเซลสีอ่อนอ่อนขึ้น.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**กรณีขอบ:** หากภาพต้นฉบับของคุณมีคอนทราสต์สูงอยู่แล้ว การใช้ฟิลเตอร์นี้อาจทำให้รายละเอียดจางหาย. ในกรณีนั้น ตั้งค่า `Level` เป็น `1.0` (ปิดการทำงานโดยอ้อม).

## ขั้นตอนที่ 4: โหลดและทำความสะอาดภาพต้นฉบับ

ตอนนี้เราจะโหลดภาพจริงและรันผ่านขั้นตอนที่เราสร้างขึ้น.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **หมายเหตุ:** เมธอด `Apply` จะคืนค่าอ็อบเจ็กต์ `Image` ใหม่; ภาพต้นฉบับจะไม่ถูกเปลี่ยน. ทำให้คุณเปรียบเทียบ “ก่อน” และ “หลัง” ได้ง่ายหากต้องการดีบักกระบวนการ.

## ขั้นตอนที่ 5: จดจำข้อความจากภาพด้วย Aspose OCR

เมื่อมีภาพที่ตรง, ปราศจากสัญญาณรบกวน, และคอนทราสต์สูงในมือ เราจะส่งต่อให้กับเครื่อง OCR.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**สิ่งที่คุณควรเห็น:** คอนโซลจะแสดงเนื้อหาข้อความของการสแกนต้นฉบับ, ปกติจะมีการจดจำผิดพลาดน้อยกว่ามากเมื่อเทียบกับการป้อนไฟล์ดิบโดยตรง.

## ขั้นตอนที่ 6: ตรวจสอบและปรับปรุงความแม่นยำของ OCR

แม้จะมีขั้นตอนที่มั่นคง บางอักขระอาจยังผิดพลาด—โดยเฉพาะหากฟอนต์ต้นฉบับแปลก. นี่คือเคล็ดลับเร็ว ๆ เพื่อ **improve OCR accuracy**:

| ปัญหา | วิธีแก้เร็ว |
|-------|-----------|
| เครื่องหมายวรรคตอนเล็กหายไป | เพิ่ม `BinaryThresholdFilter` ก่อนขั้นตอนคอนทราสต์ |
| หลายภาษา (เช่น English + Spanish) | ตั้งค่า `ocrEngine.Language = Language.English | Language.Spanish;` |
| พื้นหลังสีเข้มมาก | กลับสีภาพ (`new InvertFilter()`) ก่อน deskew |
| เอกสารขนาดใหญ่ | ประมวลผลหน้าแบบขนาน (`Parallel.ForEach`) เพื่อเร่งความเร็ว |

ลองทดลองเปลี่ยนลำดับของฟิลเตอร์; บางครั้งการใช้ **contrast** ก่อน **despeckle** ให้ผลลัพธ์ดีกว่าในสแกนคุณภาพต่ำ.

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจคคอนโซลใหม่. มันรวมทุกส่วนที่เราพูดถึง พร้อมกับการตรวจสอบความปลอดภัยสองสามอย่าง.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความ “Hello World!”):

```
=== OCR Output ===

Hello World!
```

หากคุณเห็นอักขระแปลก ๆ ให้ตรวจสอบลำดับของ pipeline อีกครั้งหรือเพิ่มค่า `DespeckleFilter.Strength`.

## สรุป

เราได้ครอบคลุม **how to deskew image**, **remove image noise**, **preprocess image for OCR**, และสุดท้าย **recognize text from image** ด้วย Aspose OCR—พร้อมคำนึงถึง **improve OCR accuracy**. ตัวอย่างที่สมบูรณ์และสามารถรันได้แสดงทุกขั้นตอนในบริบท, เพื่อให้คุณสามารถนำไปใส่ในโปรเจค .NET ใดก็ได้และเริ่มดึงข้อความทันที.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองขยาย pipeline เพื่อรองรับ PDF หลายหน้า, หรือทดลองใช้ language pack สำหรับเอกสารหลายภาษา. แนวคิดเดียวกันใช้ได้—เพียงสลับ `Language` flag และอาจเพิ่ม `RotateFilter` สำหรับหน้าที่กลับหัว.

มีคำถามหรือภาพที่ยากต่อการจัดการ? แสดงความคิดเห็นด้านล่าง, แล้วเราจะช่วยแก้ไขร่วมกัน. Happy coding!

![ตัวอย่างการปรับแนวภาพ](/images/deskew-example.png "ภาพประกอบของการปรับแนวภาพโดยใช้ Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}