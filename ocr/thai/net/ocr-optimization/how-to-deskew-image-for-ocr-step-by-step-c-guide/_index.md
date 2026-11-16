---
category: general
date: 2026-03-04
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพและการจดจำข้อความจากภาพด้วยการปรับคอนทราสต์เพื่อปรับปรุงความแม่นยำของ
  OCR และเพิ่มประสิทธิภาพภาพสำหรับ OCR.
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: th
og_description: วิธีแก้ไขการเอียงของภาพและเพิ่มประสิทธิภาพผลลัพธ์ OCR เรียนรู้การปรับคอนทราสต์,
  ปรับปรุงความแม่นยำของ OCR, และจดจำข้อความจากภาพด้วยกระบวนการที่นำกลับมาใช้ใหม่ได้
og_title: วิธีแก้ไขการเอียงของภาพ – คู่มือ OCR ด้วย C# อย่างครบถ้วน
tags:
- OCR
- C#
- image‑processing
title: วิธีปรับแนวภาพสำหรับ OCR – คู่มือ C# ทีละขั้นตอน
url: /th/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำให้ภาพไม่เอียง – คู่มือ OCR ด้วย C# อย่างครบถ้วน

เคยสงสัย **วิธีทำให้ภาพไม่เอียง** เพื่อให้เครื่อง OCR อ่านข้อความได้จริงหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่น ใบเสร็จสแกน, สัญญาที่ถ่ายด้วยกล้อง, หรือใบเสร็จที่เบลอจากกล้องโทรศัพท์—ภาพไม่ได้ตั้งตรงอย่างสมบูรณ์ หน้าเอกสารที่เอียงทำให้ตัวจำแนกอักขระทำงานผิดพลาด และผลลัพธ์ก็เป็นข้อความที่ไม่มีความหมาย

ข่าวดีคือ? หากทำให้ภาพไม่เอียง **และ** ปรับคอนทราสต์ คุณสามารถเพิ่ม **ความแม่นยำของ OCR** ได้อย่างมาก ในบทเรียนนี้เราจะเดินผ่านตัวอย่าง C# ที่สมบูรณ์ ซึ่งจะแสดงให้คุณเห็นวิธี **จดจำข้อความจากภาพ** หลังจากใช้ฟิลเตอร์ทำให้ภาพไม่เอียงและเพิ่มคอนทราสต์ เราจะอธิบาย **วิธีปรับคอนทราสต์** อย่างถูกต้อง, พูดถึงกรณีขอบ, และให้ pipeline ที่นำกลับมาใช้ใหม่ได้ซึ่งคุณสามารถใส่ลงในโปรเจกต์ใดก็ได้

## สิ่งที่คุณจะได้รับจากคู่มือนี้

- คำอธิบายที่ชัดเจนว่าทำไมการทำให้ภาพไม่เอียงและคอนทราสต์จึงสำคัญต่อ OCR
- ตัวอย่างโค้ด C# พร้อมรันที่สร้าง pipeline ฟิลเตอร์, เชื่อมต่อกับเครื่อง OCR, และอ่านหลายภาพ
- เคล็ดลับการใช้ pipeline เดียวกันสำหรับหลายไฟล์, การจัดการกรณีล้มเหลว, และการวัดการเพิ่มความแม่นยำ
- ลิงก์ไปยังหัวข้อที่เกี่ยวข้อง เช่น การทำให้ภาพเป็นไบนารี, การกำจัดนอยส์, และ OCR หลายภาษา (ทั้งหมดโดยไม่ต้องออกจากหน้า)

**ข้อกำหนดเบื้องต้น** – คุณต้องมีสภาพแวดล้อม .NET 6+, ไลบรารี OCR ที่รองรับ pipeline ฟิลเตอร์ (เช่น Tesseract‑.NET, IronOCR, หรือ SDK เชิงพาณิชย์ใด ๆ) และ PNG ตัวอย่างสองไฟล์ ไม่ต้องใช้บริการภายนอก

---

## ขั้นตอนที่ 1 – ทำไมการทำให้ภาพไม่เอียงเป็นสิ่งแรกที่ควรทำ

เมื่อหน้าที่สแกนหมุนเพียงไม่กี่องศา, เครื่อง OCR จะเห็น baseline ของแต่ละบรรทัดเป็นมุม. ตัวจำแนกส่วนใหญ่สมมติว่าข้อความเป็นแนวนอน; ความเบี่ยงเบนใด ๆ จะลดคะแนนความมั่นใจและทำให้เกิดข้อผิดพลาดการแทนที่

> **Pro tip:** หากทำได้, ควรถ่ายภาพบนพื้นราบและแสงดี; การแก้ไขด้วยซอฟต์แวร์ไม่สามารถทดแทนข้อมูลที่ดีได้อย่างเต็มที่

ในแง่ของโค้ด, “วิธีทำให้ภาพไม่เอียง” มักหมายถึงการตรวจจับทิศทางของบรรทัดข้อความที่โดดเด่นและหมุนบิตแมพกลับไปที่ 0°. SDK OCR ส่วนใหญ่มี `DeskewFilter` ที่ทำงานนี้โดยอัตโนมัติ

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

ฟิลเตอร์ทำงานบนสมมติฐานว่าหน้ากระดาษมีข้อความมากกว่าพื้นหลัง, ซึ่งเป็นความจริงสำหรับเอกสารส่วนใหญ่. หากคุณมีภาพที่มีพื้นที่ว่างมาก, คุณอาจต้องใช้อัลกอริทึมสำรอง—แต่สำหรับ PDF ที่สแกนส่วนใหญ่ค่าเริ่มต้นทำงานได้ดี

---

## ขั้นตอนที่ 2 – เพิ่มคอนทราสต์เพื่อทำให้ตัวอักษรเด่นชัด

คอนทราสต์คือความแตกต่างระหว่างพิกเซลที่มืดที่สุดและสว่างที่สุด. สแกนที่คอนทราสต์ต่ำดูจางและเครื่อง OCR ไม่สามารถบ่งบอกได้ว่าตัวอักษรเริ่มหรือจบที่ไหน. การเพิ่มคอนทราสต์ทำให้ “ความคมชัด” ของการแยกภาพเพิ่มขึ้น, ซึ่ง **ช่วยเพิ่มความแม่นยำของ OCR** ได้

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

ทำไมต้อง 1.2? ในการปฏิบัติ การเพิ่มคอนทราสต์แบบพอประมาณ (10‑30 %) เพียงพอ. หากเพิ่มมากเกินไปจะทำให้รายละเอียดบางอย่างหายไป, โดยเฉพาะฟอนต์บางเบา. คุณสามารถทดลองปรับได้; pipeline ที่เราจะสร้างต่อไปทำให้คุณปรับระดับได้โดยไม่ต้องคอมไพล์แอปใหม่ทั้งหมด

---

## ขั้นตอนที่ 3 – สร้าง Pipeline ฟิลเตอร์ที่นำกลับมาใช้ใหม่ได้

ต่อไปเราจะรวมฟิลเตอร์สองตัวเข้าด้วยกันเป็น pipeline เดียว. วิธีนี้คุณจะ **จดจำข้อความจากภาพ** ด้วยการเตรียมข้อมูลเดียวกันทุกครั้ง, ทำให้ผลลัพธ์สม่ำเสมอ

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**ทำไมต้องใช้ pipeline?**  
- **โมดูลาร์:** เพิ่มหรือเอาฟิลเตอร์ออกได้โดยไม่ต้องแก้ไขการเรียก OCR  
- **ประสิทธิภาพ:** ไลบรารีสามารถทำ batch การดำเนินการ, ลดการใช้หน่วยความจำ  
- **การนำกลับมาใช้ใหม่:** เชื่อมต่อ pipeline เดียวกันกับหลายการเรียก `engine.Recognize`

---

## ขั้นตอนที่ 4 – เชื่อมต่อ Pipeline กับ Engine OCR

OCR ส่วนใหญ่มี property `Filters` หรือเมธอด `SetFilters`. การกำหนด pipeline ที่นี่ทำให้ภาพทุกภาพที่ตามมาผ่านขั้นตอนทำให้ไม่เอียง + คอนทราสต์ ก่อนการวิเคราะห์อักขระจริงเริ่มต้น

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

หากต้องการเปลี่ยนโมเดลภาษา (เช่น English → Spanish) คุณสามารถทำได้ **ก่อน** เชื่อมต่อฟิลเตอร์; ลำดับไม่สำคัญสำหรับขั้นตอนการเตรียมข้อมูล

---

## ขั้นตอนที่ 5 – จดจำข้อความจากภาพแรก

มาลองใช้ pipeline กัน. เราจะโหลด PNG, รัน OCR, และพิมพ์ผลลัพธ์. สังเกตว่าเราใช้ instance `engine` เดียวกัน—ไม่ต้องสร้างฟิลเตอร์ใหม่

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**สิ่งที่คุณควรเห็น:** ข้อความที่เรียงตรง, มีคอนทราสต์ที่ดี, และอักขระที่บิดเบือนน้อยกว่าการสแกนดิบอย่างมาก. หากยังพบข้อผิดพลาด, พิจารณาเพิ่ม `BinarizeFilter` (แปลงเป็นขาว‑ดำบริสุทธิ์) หลังขั้นตอนคอนทราสต์

---

## ขั้นตอนที่ 6 – ใช้ Pipeline เดียวกันกับไฟล์เพิ่มเติม

หนึ่งในข้อได้เปรียบใหญ่ของ pipeline ฟิลเตอร์คือคุณสามารถใช้ซ้ำได้กับหลายไฟล์โดยไม่มีค่าใช้จ่ายเพิ่ม

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

หากคุณมีโฟลเดอร์ที่เต็มไปด้วย PDF ที่สแกน, เพียงวนลูป `Directory.GetFiles(...)` และเรียก `engine.Recognize` ทุกครั้ง. ขั้นตอนทำให้ไม่เอียงและคอนทราสต์จะคงที่, ซึ่งเป็นกุญแจสำคัญในการ **เพิ่มประสิทธิภาพภาพสำหรับ OCR** ในงานแบตช์

---

## ตัวอย่างทำงานเต็มรูปแบบ – รวมทุกอย่างไว้ด้วยกัน

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และทำงานได้เอง. คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่, เพิ่ม NuGet package ที่เหมาะกับ OCR SDK ของคุณ, แล้วรัน. โปรแกรมจะแสดงข้อความที่จดจำได้จากสองภาพตัวอย่าง

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

หากคุณเปรียบเทียบผลลัพธ์นี้กับการรัน **โดยไม่มี** pipeline ฟิลเตอร์, คุณจะเห็นอักขระหายไป, ตัวเลขผิดตำแหน่ง, หรือบรรทัดที่อ่านไม่ออก. นั่นคือผลกระทบที่วัดได้จากการเรียนรู้ **วิธีทำให้ภาพไม่เอียง** และ **วิธีปรับคอนทราสต์** อย่างถูกต้อง

---

## คำถามทั่วไป & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| *ถ้าภาพแล้วตั้งตรงแล้วล่ะ?* | `DeskewFilter` จะตรวจจับการหมุน 0° และคืนบิตแมพเดิม, ดังนั้นไม่มีค่าใช้จ่ายเพิ่มเติมอย่างมีนัยสำคัญ |
| *สามารถใช้กับ PDF ได้หรือไม่?* | ใช่. OCR SDK ส่วนใหญ่ให้คุณโหลดหน้า PDF เป็น `ImageInfo`. Pipeline เดียวกันทำงานได้เพราะบิตแมพพื้นฐานถูกประมวลผลแบบเดียวกัน |
| *เอกสารของฉันมีข้อความสี—คอนทราสต์จะทำให้สีเสียหายหรือไม่?* | ฟิลเตอร์คอนทราสต์ทำงานบนความสว่าง (luminance), สีจะถูกเก็บไว้แต่เด่นชัดขึ้น. หากต้องการขาว‑ดำบริสุทธิ์, เพิ่ม `BinarizeFilter` หลังคอนทราสต์ |
| *จะวัดการเพิ่มความแม่นยำอย่างไร?* | รัน OCR กับชุดทดสอบก่อนและหลังใช้ pipeline, แล้วคำนวณอัตราข้อผิดพลาดอักขระ (CER) หรืออัตราข้อผิดพลาดคำ (WER). ปกติจะเห็นการลดข้อผิดพลาด 10‑30 % |
| *มีผลต่อประสิทธิภาพหรือไม่?* | การทำให้ไม่เอียงเพิ่มค่าใช้จ่าย CPU เล็กน้อย (มัก < 100 ms ต่อหน้า). คอนทราสต์เป็นการดำเนินการพิกเซลแบบง่าย, ดังนั้นผลกระทบโดยรวมจึงน้อยเมื่อเทียบกับขั้นตอน OCR เอง |

---

## ขั้นตอนต่อไป – ยกระดับ OCR ของคุณ

ตอนนี้คุณรู้แล้ว **วิธีทำให้ภาพไม่เอียง**, **วิธีปรับคอนทราสต์**, และ **วิธีจดจำข้อความจากภาพ** ด้วย pipeline ที่นำกลับมาใช้ใหม่, ลองสำรวจหัวข้อต่อไปนี้:

- **การลดนอยส์** – เพิ่ม `MedianFilter` ก่อนทำให้ไม่เอียงเพื่อทำความสะอาดจุดรบกวน  
- **การทำไบนารี** – แปลงเป็นขาว‑ดำบริสุทธิ์สำหรับภาษาที่มีสคริปต์ซับซ้อน  
- **การประมวลผลหลายหน้า** – วนลูปหน้า PDF และเก็บผลลัพธ์ในดัชนีที่ค้นหาได้  
- **โมเดลภาษา** – สลับระหว่าง `OcrLanguage.English` และ `OcrLanguage.French` แบบไดนามิก  
- **การประมวลผลหลัง OCR** – ใช้ตัวตรวจสอบการสะกดหรือ regex เพื่อแก้ไขการอ่านผิดทั่วไป (เช่น “0” กับ “O”)

ทุกอย่างเหล่านี้สามารถต่อเข้ากับ chain `FilterBuilder` เดียวกัน, ทำให้คุณได้โซลูชันที่โมดูลาร์และดูแลรักษาง่าย ซึ่ง **เพิ่มประสิทธิภาพภาพสำหรับ OCR** ในทุก pipeline การผลิต

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องรู้เกี่ยวกับ **วิธีทำให้ภาพไม่เอียง** สำหรับ OCR, ทำไมการปรับคอนทราสต์เป็นวิธีต้นทุนต่ำแต่ทรงพลังในการ **เพิ่มความแม่นยำของ OCR**, และวิธี **จดจำข้อความจากภาพ** ด้วย pipeline ที่สะอาดและนำกลับมาใช้ใหม่ได้

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}