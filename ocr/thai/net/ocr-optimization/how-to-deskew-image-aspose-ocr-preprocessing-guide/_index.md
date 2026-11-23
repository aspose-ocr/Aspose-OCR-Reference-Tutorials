---
category: general
date: 2026-04-29
description: วิธีแก้ไขการเอียงของภาพและเพิ่มความแม่นยำของ OCR ด้วย Aspose OCR – เรียนรู้การกำจัดสัญญาณรบกวน,
  เพิ่มความคอนทราสต์ของภาพ, และสกัดข้อความจากภาพ.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: th
og_description: วิธีแก้ไขการเอียงของภาพและปรับปรุงความแม่นยำของ OCR บทเรียนนี้แสดงวิธีการลบสัญญาณรบกวนจากภาพ
  เพิ่มความคมชัดของภาพ และดึงข้อความจากภาพโดยใช้ Aspose OCR.
og_title: วิธีแก้ไขการเอียงของภาพ – คู่มือ Aspose OCR ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- Image preprocessing
title: วิธีแก้ไขการเอียงของภาพ – คู่มือการเตรียมข้อมูลล่วงหน้าสำหรับ Aspose OCR
url: /th/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือ Aspose OCR ฉบับสมบูรณ์

เคยสงสัยไหมว่า **how to deskew image** ไฟล์ก่อนนำเข้า OCR engine? คุณไม่ได้เป็นคนเดียว การสแกนที่เอียงหรือภาพที่ถ่ายมาที่มุมอาจทำให้การรู้จำข้อความผิดพลาด ทำให้ได้ผลลัพธ์เป็นข้อความสับสน  

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจรที่ไม่เพียงแค่ **how to deskew image** แต่ยัง **remove noise from image**, **boost image contrast**, และสุดท้าย **extract text from image** ด้วย Aspose OCR. เมื่อจบคุณจะเห็นวิธี **improve OCR accuracy** โดยไม่ต้องค้นหาในเอกสาร

> **What you’ll get:** แอปคอนโซล C# ที่พร้อมรัน, คำอธิบายที่ชัดเจนของแต่ละขั้นตอนการเตรียมข้อมูล, และเคล็ดลับเชิงปฏิบัติบางอย่างที่คุณสามารถคัดลอก‑วางไปใช้ในโปรเจกต์ของคุณ

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ด้วย)  
- แพคเกจ NuGet ของ Aspose.OCR (`Install-Package Aspose.OCR`)  
- รูปตัวอย่างที่เอียง มีเสียงรบกวน หรือคอนทราสต์ต่ำ (เช่น `skewed_noisy.jpg`)  
- Visual Studio, VS Code, หรือโปรแกรมแก้ไข C# ที่คุณชอบ  

ไม่ต้องการไลบรารีเนทีฟเพิ่มเติม – Aspose จัดการทุกอย่างในกระบวนการเดียว

---

## วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR

สิ่งแรกที่เราต้องการคือฟิลเตอร์ deskew ที่แก้ไขมุมการหมุน Aspose OCR มาพร้อมกับ `FilterDeskew` ซึ่งวิเคราะห์ baseline ของข้อความและหมุนบิตแมพตามนั้น

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ทำไมเราถึงเริ่มด้วยการแก้ไขการเอียง:**  
หากบรรทัดข้อความไม่เป็นแนวนอน OCR engine จะพยายามตีความอักขระที่เอียงเป็น glyph ที่แตกต่างกัน ทำให้ **improve OCR accuracy** ลดลงอย่างมาก การแก้ไขการเอียงทำให้ baseline เรียงตรง ให้ตัวรับรู้มีพื้นผิวที่สะอาด

> *Pro tip:* หากคุณทราบมุมการหมุนล่วงหน้า (เช่น การสแกนทั้งหมดเอียง 90°) คุณสามารถข้ามฟิลเตอร์และหมุนด้วยตนเอง – จะช่วยเพิ่มประสิทธิภาพเล็กน้อย

---

## การกำจัดเสียงรบกวนจากภาพ – ทำให้การสแกนสะอาด

เสียงรบกวนปรากฏเป็นจุดสีดำหรือสีขาวแบบสุ่ม (รูปแบบ “salt‑and‑pepper” คลาสสิก) และอาจทำให้การแยกอักขระสับสน `FilterDenoise` ใช้ median filter ที่ทำให้จุดเหล่านี้เรียบลงในขณะที่รักษาขอบไว้

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**เมื่อใดควรปรับความแรง:**  
- **Strength = 1** – เมล็ดกรains เบา, การประมวลผลเร็ว.  
- **Strength = 3** – การสแกนที่มีเสียงรบกวนมาก (เช่น เอกสารที่ส่งแฟกซ์).  

การเพิ่มความแรงมากเกินไปอาจทำให้เส้นบางเบลอ ซึ่งอาจ *hurt* **improve OCR accuracy**. ทดสอบค่าต่าง ๆ บนตัวอย่างที่เป็นตัวแทน

---

## การเพิ่มคอนทราสต์ของภาพ – เน้นอักขระที่จาง

ภาพที่คอนทราสต์ต่ำ (เช่น ใบเสร็จที่ซีด) มักทำให้ OCR engine พลาด glyph ที่บางเบา `FilterContrastBoost` ขยายฮิสโตแกรมทำให้พิกเซลสีเข้มเข้มขึ้นและพิกเซลสีอ่อนอ่อนขึ้น

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**ทำไมคอนทราสต์ถึงสำคัญ:**  
คอนทราสต์ที่สูงขึ้นทำให้สัญญาณต่อสัญญาณรบกวนดีขึ้น ทำให้ recognizer แบบ neural ของ Aspose แยก “I” จาก “l” ได้ง่ายขึ้น อย่างไรก็ตาม การบูสต์เกินไปอาจทำให้ภาพอิ่มเกินไป ทำให้ไล่โทนสีเรียบกลายเป็นขอบคมที่ดูเหมือน artefacts ควรหาจุดสมดุล; 1.5‑2.0 เป็นจุดเริ่มต้นที่ดี

---

## การสกัดข้อความจากภาพ – ขั้นตอน OCR สุดท้าย

ตอนนี้ภาพตรง, สะอาด, และคมชัด OCR engine สามารถทำงานได้ เมธอด `Recognize` จะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่มีข้อความดิบ, คะแนนความเชื่อมั่น, และแม้แต่ bounding box หากคุณต้องการ

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Sample output** (สมมติว่าภาพต้นฉบับมีข้อความ “Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

หากคุณพบอักขระหายไป ตรวจสอบ pipeline การเตรียมข้อมูลอีกครั้ง – บางทีภาพอาจยังต้องการการกำจัดเสียงรบกวนที่แรงขึ้นหรือระดับคอนทราสต์ที่ต่างออกไป  

> *Common question:* “ถ้าฉันต้องการรู้จำภาษาที่ไม่ใช่ภาษาอังกฤษล่ะ?”  
> เพียงตั้งค่า `ocrEngine.Language = Language.English;` เป็นภาษาที่รองรับอื่น (เช่น `Language.French`). ขั้นตอนการเตรียมข้อมูลยังคงเหมือนเดิม

---

## การปรับปรุง OCR Accuracy – การปรับแต่งเพิ่มเติม

แม้จะมี pipeline ที่สมบูรณ์แล้ว การปรับเพิ่มเล็กน้อยก็สามารถผลักดัน **improve OCR accuracy** ไปได้อีก

| เคล็ดลับ | เมื่อใช้ | วิธี |
|-----|--------------|-----|
| **Binary Thresholding** | การสแกนที่มืดมากหรือสว่างมาก | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | ฟอนต์ขนาดเล็ก (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | ตัวอักษรที่รู้จัก (เฉพาะตัวเลข ฯลฯ) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | การประมวลผลเป็นชุด | Loop over each page and reuse the same pipeline. |

จำไว้ว่า: ฟิลเตอร์เพิ่มแต่ละตัวจะเพิ่มเวลาในการประมวลผล ดังนั้นเปิดใช้งานเฉพาะที่คุณต้องการจริง ๆ

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บ `skewed_noisy.jpg`

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Expected result:** ข้อความที่สะอาดและตรงพิมพ์ออกที่คอนโซล, มีการจดจำผิดน้อยกว่าการป้อนไฟล์ดิบโดยตรงเข้า `ocrEngine.Recognize`

---

## สรุป

เราได้ครอบคลุม **how to deskew image**, วิธี **remove noise from image**, วิธี **boost image contrast**, และสุดท้ายวิธี **extract text from image** ด้วย Aspose OCR. การเชื่อมต่อฟิลเตอร์เหล่านี้จะทำให้คุณเห็นการเพิ่มขึ้นอย่างชัดเจนใน **improve OCR accuracy**, โดยเฉพาะกับการสแกนคุณภาพต่ำ  

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองป้อน PDF หลายหน้าเข้าสู่ pipeline เดียวกัน หรือทดลองปรับค่า threshold สำหรับการ binarization. หลักการเดียวกันใช้ได้ – แก้ไขการเอียง, ทำความสะอาด, เพิ่มความสว่าง, แล้วจดจำ  

มีคำถามหรือกรณีแปลก ๆ ไหม? แสดงความคิดเห็นและเรามาแก้ไขด้วยกัน. Happy coding!  

![how to deskew image example](deskew-example.png "how to deskew image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}