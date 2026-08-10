---
category: general
date: 2026-04-08
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีการเตรียมภาพล่วงหน้าสำหรับ
  OCR และวิธีการเตรียมภาพเพื่อเพิ่มความแม่นยำ.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# คู่มือนี้แสดงวิธีการเตรียมภาพสำหรับ
  OCR และวิธีการเตรียมภาพเพื่อให้ได้ผลลัพธ์ที่ดีที่สุด.
og_title: ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
tags:
- C#
- OCR
- Aspose
- Image Processing
title: ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์

เคยต้องการ **ดึงข้อความจากรูปภาพ** แต่ผลลัพธ์เต็มไปด้วยข้อผิดพลาดหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่เจอปัญหาเดียวกันเมื่อภาพต้นทางเอียง, มีสัญญาณรบกวน, หรือคอนทราสต์ต่ำ ข่าวดีคือขั้นตอนการเตรียมข้อมูลล่วงหน้าแบบสั้น ๆ สามารถเปลี่ยนภาพที่สั่นคลอนให้เป็นแหล่งข้อมูลที่สะอาดสำหรับ OCR, และ Aspose OCR ทำให้ทุกอย่างง่ายดายเหมือนเค้ก

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างจากโลกจริงที่แสดง **วิธีการเตรียมภาพสำหรับ OCR** ด้วยฟิลเตอร์ในตัวของ Aspose OCR, จากนั้นจริง ๆ **ดึงข้อความจากรูปภาพ** ด้วยเพียงไม่กี่บรรทัดของ C#. เมื่อเสร็จคุณจะมีโปรแกรมพร้อมรัน, เข้าใจว่าทำไมฟิลเตอร์แต่ละตัวถึงสำคัญ, และรู้วิธีปรับแต่ง pipeline ให้เหมาะกับกรณีของคุณเอง

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดยังทำงานบน .NET Framework 4.7+ ด้วย)
- แพคเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- ตัวอย่างรูปภาพที่เอียง, มีสัญญาณรบกวน, หรือคอนทราสต์ต่ำ (เช่น `skewed_noisy.jpg`)
- IDE ใดก็ได้ที่คุณชอบ—Visual Studio, Rider, หรือ VS Code ก็ใช้ได้

ไม่มีไลบรารีเนทีฟเพิ่มเติม, ไม่มีเว็บเซอร์วิส, เพียงแค่ C# ธรรมดา

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – จุดเริ่มต้นสำหรับการดึงข้อความ

ก่อนอื่นสร้างอินสแตนซ์ `OcrEngine` แล้วบอกให้มันรู้ว่าจะค้นหาภาษาอะไร ภาษาอังกฤษเป็นภาษาที่ใช้บ่อยที่สุด, แต่คุณสามารถสลับ `"en"` เป็น `"fr"`, `"de"` หรืออื่น ๆ ได้

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**ทำไมสิ่งนี้ถึงสำคัญ:** เครื่องยนต์เก็บพจนานุกรมภายในและอัลกอริทึมเฉพาะภาษา หากข้ามการตั้งค่าภาษา, Aspose จะใช้ค่าเริ่มต้นเป็นอังกฤษ, แต่การระบุอย่างชัดเจนจะช่วยหลีกเลี่ยงความประหลาดใจเมื่อคุณเปลี่ยน locale ในภายหลัง

## ขั้นตอนที่ 2: สร้าง Pipeline การเตรียมภาพ – วิธีการ Preprocess Image เพื่อผลลัพธ์ที่ดีที่สุด

ตอนนี้เราจะเพิ่มฟิลเตอร์ เหมือนกับชุดเครื่องมือแก้ไขภาพขนาดเล็กที่ทำงานอัตโนมัติก่อนขั้นตอน OCR ฟิลเตอร์สามตัวด้านล่างครอบคลุมปัญหาที่พบบ่อยที่สุด:

| Filter | สิ่งที่แก้ไข | เมื่อควรใช้ |
|--------|--------------|-------------|
| `DeskewFilter` | หมุนภาพกลับเป็นแนวนอน | รูปที่ถ่ายมาที่มุม |
| `DenoiseFilter` | ลดจุดรบกวนและเม็ดสีสุ่ม | ภาพถ่ายในแสงน้อยหรือเอกสารสแกน |
| `ContrastStretchFilter` | เพิ่มคอนทราสต์ ทำให้ข้อความสีเข้มเด่นชัด | พิมพ์ที่ซีดหรือสกรีนช็อตที่สีจาง |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**เคล็ดลับ:** ลำดับสำคัญ ต้องทำ Deskew ก่อน, จากนั้น Denoise, และสุดท้าย Stretch Contrast หากสลับลำดับอาจทำให้เพิ่มสัญญาณรบกวนแทนการลดมัน

## ขั้นตอนที่ 3: รัน OCR – สุดท้ายดึงข้อความจากรูปภาพ

เมื่อ pipeline พร้อม, ส่งพาธของรูปภาพให้ engine. Aspose จะใช้ฟิลเตอร์โดยอัตโนมัติแล้วรันอัลกอริทึมการจดจำ

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

หากไฟล์ไม่พบ, จะเกิด `FileNotFoundException` ชัดเจน นี่คือเหตุผลที่เราแนะนำให้ใช้พาธแบบ absolute ระหว่างการพัฒนา, แล้วเปลี่ยนเป็นพาธ relative หรือค่าคอนฟิกสำหรับการผลิต

## ขั้นตอนที่ 4: แสดงผลลัพธ์ – ดูว่าคุณได้อะไรบ้าง

อ็อบเจ็กต์ `OcrResult` มีข้อความดิบ, คะแนนความเชื่อมั่น, และแม้กระทั่ง bounding box ของแต่ละคำ สำหรับการสาธิตอย่างรวดเร็วเราจะพิมพ์ข้อความไปที่คอนโซล

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

เมื่อรันโปรแกรม, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบคุณภาพของภาพอีกครั้งหรือทดลองเพิ่มฟิลเตอร์อื่น (เช่น `BinarizationFilter` สำหรับภาพไบนารี)

## ตัวอย่างทำงานเต็มรูปแบบ – คัดลอก‑วางและรัน

ด้านล่างเป็นโปรแกรมครบชุดที่ทำงานได้เอง เพียงเปลี่ยน `YOUR_DIRECTORY/skewed_noisy.jpg` ให้เป็นพาธจริงของภาพทดสอบของคุณ

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** – คอนโซลจะพิมพ์ข้อความแบบ plain‑text ของสิ่งที่อยู่ในภาพ หากภาพมีป้ายง่าย ๆ ที่เขียนว่า “OpenAI”, คุณจะเห็นคำนั้นโดยไม่มีสัญลักษณ์เพิ่มเติม

## กรณีขอบและวิธีปรับแต่ง Pipeline

### 1️⃣ รูปภาพมืดมาก

หากฟิลเตอร์คอนทราสต์ไม่พอ, ให้เพิ่ม `BrightnessCorrectionFilter` ด้านหน้า:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ เอกสารหลายภาษา

ตั้งค่า `Language = "en+fr"` (Aspose รองรับรหัสภาษาแยกด้วยคอมม่า) และเพิ่ม `LanguageDetectionFilter` หากต้องการให้ engine ตรวจจับอัตโนมัติ

### 3️⃣ PDF ขนาดใหญ่ที่แปลงเป็นภาพ

การประมวลผล PDF พันหน้าหนึ่งภาพต่อครั้งอาจช้า ใช้ `Parallel.ForEach` เพื่อรัน OCR บนหลายภาพพร้อมกัน, แต่จำไว้ว่า `OcrEngine` ไม่ปลอดภัยต่อการทำงานหลายเธรด—ต้องสร้างอินสแตนซ์แยกสำหรับแต่ละเธรด

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ การรับ Bounding Boxes

หากต้องการตำแหน่งของแต่ละคำ (เช่นเพื่อไฮไลท์), ตรวจสอบ `ocrResult.Regions`. แต่ละ region มีพิกัด `Rectangle` ที่คุณสามารถส่งต่อไปยัง UI overlay

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## ข้อผิดพลาดทั่วไป (และวิธีหลีกเลี่ยง)

- **Skipping the Deskew step** – แม้เพียงการเอียง 2 องศาก็ทำให้คะแนนความเชื่อมั่นลดลง 20 % . ควรเพิ่ม `DeskewFilter` เสมอเมื่อแหล่งข้อมูลไม่ได้จัดแนวอย่างสมบูรณ์
- **Using JPEG with heavy compression** – ศูนย์บีบอัดทำให้เกิด artefacts ที่คล้ายสัญญาณรบกวน; เปลี่ยนเป็น PNG หรือ TIFF เพื่อ OCR ที่ดีกว่า
- **Hard‑coding paths** – พาธ relative ทำงานในเครื่องท้องถิ่น, แต่ใน pipeline CI/CD ควรอ่านตำแหน่งภาพจากคอนฟิกหรือ environment variables

## การทดสอบการตั้งค่า

1. รันโปรแกรมด้วยภาพที่สะอาดและคอนทราสต์สูง. คุณควรได้ข้อความเกือบสมบูรณ์แบบ
2. เปลี่ยนเป็นภาพที่มีสัญญาณรบกวนและเอียง. ตรวจสอบว่าผลลัพธ์ดีขึ้นหลังจากเพิ่มฟิลเตอร์สามตัว
3. ทดลองลบฟิลเตอร์หนึ่งตัวต่อครั้งเพื่อดูผลกระทบ—ช่วยให้คุณเข้าใจ *ทำไม* แต่ละขั้นตอนถึงสำคัญ

## สรุป

เราได้สาธิตวิธี **ดึงข้อความจากรูปภาพ** ด้วย Aspose OCR, และแสดงวิธี **เตรียมภาพสำหรับ OCR** ที่ใช้ได้ในหลายสถานการณ์จริง โดยการเชื่อมต่อ `DeskewFilter`, `DenoiseFilter`, และ `ContrastStretchFilter` คุณจะให้ engine มี “ผืนผ้าใบ” ที่สะอาด, ซึ่งทำให้ความแม่นยำเพิ่มขึ้นอย่างมาก

จากนี้คุณสามารถสำรวจฟิลเตอร์ขั้นสูงเพิ่มเติม, จัดการเอกสารหลายหน้า, หรือผสานผล OCR เข้ากับดัชนีการค้นหา ไม่ว่าคุณจะเลือกทำอะไร, รูปแบบหลัก—initialize, preprocess, recognize, and consume—ยังคงเหมือนเดิม

พร้อมจะก้าวต่อ? ลองเพิ่ม `BinarizationFilter` สำหรับสแกนขาว‑ดำ, หรือเชื่อมผลลัพธ์กับฐานข้อมูลเพื่อ PDF ที่ค้นหาได้. Happy coding, และขอให้ทุกภาพที่คุณส่งให้ Aspose คืนข้อความที่คมชัดและอ่านง่าย!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}