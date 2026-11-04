---
category: general
date: 2026-03-07
description: เรียนรู้วิธีการปรับแนวภาพให้ตรง, เพิ่มความคมชัด, และดึงข้อความจากการสแกนโดยใช้
  Aspose OCR. ทำ OCR บนภาพด้วยตัวอย่าง C# เต็มรูปแบบและโหลดภาพสำหรับ OCR ได้อย่างง่ายดาย.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: th
og_description: เรียนรู้วิธีแก้ไขการเอียงของภาพ, เพิ่มความคมชัด, และดึงข้อความจากการสแกนโดยใช้
  Aspose OCR ใน C#. ทำ OCR บนภาพด้วยโค้ดทีละขั้นตอน.
og_title: วิธีทำให้ภาพไม่เอียงและรัน OCR ด้วย C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- OCR
- Image Processing
title: วิธีแก้ไขการเอียงของภาพและทำ OCR ด้วย C# – คู่มือครบถ้วน
url: /th/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพและรัน OCR ใน C# – คู่มือฉบับสมบูรณ์

หากคุณเคยสงสัย **how to deskew image** ก่อนรัน OCR, คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะพาคุณผ่านการเพิ่มคอนทราสต์, การโหลดภาพสำหรับ OCR, และสุดท้าย **extracting text from scan** ด้วย Aspose OCR.  

ไม่ว่าคุณจะกำลังดิจิไทซ์ใบเสร็จเก่า, ทำความสะอาดสัญญาที่สแกน, หรือแค่ต้องการวิธีที่เชื่อถือได้ในการอ่านข้อความจากรูปที่เอียง, ขั้นตอนด้านล่างครอบคลุมทุกอย่างที่คุณต้องการ. ไม่มีของเกินจำเป็น—เพียงตัวอย่างทำงานที่คุณสามารถคัดลอก‑วางลงใน Visual Studio.  

## สิ่งที่คุณจะได้ทำ

* แก้ไขการเอียงสูงสุด 30° (นี่คือส่วนของ **how to deskew image**).  
* เพิ่มคอนทราสต์ของภาพเพื่อให้ขอบอักขระคมชัดขึ้น (**how to boost contrast**).  
* โหลดรูปของคุณเข้าสู่เครื่อง OCR (**load image for OCR**).  
* รันกระบวนการจดจำและ **extract text from scan**.  

ทั้งหมดนี้ทำงานกับแพคเกจ Aspose.OCR .NET NuGet รุ่นล่าสุด (v23.11 ณ เวลาที่เขียน).  

---

![ตัวอย่างการแก้ไขการเอียงของภาพ](/images/deskew-example.png "วิธีแก้ไขการเอียงของภาพ")

*ภาพด้านบนแสดงเอกสารที่สแกนก่อนและหลังการแก้ไขการเอียง.*

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย).  
* Visual Studio 2022 (หรือ IDE C# ใดก็ได้ที่คุณชอบ).  
* แพคเกจ Aspose.OCR NuGet – ติดตั้งโดยใช้ `dotnet add package Aspose.OCR`.  

เท่านี้เอง ไม่ต้องบริการภายนอก ไม่ต้องคีย์ API.

---

## วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR

สิ่งแรกที่เราทำคือสร้าง **ImageProcessingPipeline** และเพิ่ม `DeskewFilter`. ตัวกรองจะตรวจจับมุมของบรรทัดข้อความหลักโดยอัตโนมัติและหมุนภาพกลับเป็นแนวนอน.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
การสแกนที่เอียงทำให้เครื่อง OCR สับสนเพราะอักขระไม่ตรงกับเส้นฐานอีกต่อไป. `DeskewFilter` วิเคราะห์ฮิสโตแกรมของภาพ, ค้นหามุม, และหมุนภาพ, ซึ่งทำให้ความแม่นยำของการจดจำเพิ่มขึ้นอย่างมาก.

> **เคล็ดลับ:** หากคุณทราบว่าเอกสารของคุณไม่เอียงเกิน 15°, ตั้งค่า `MaxAngle = 15` เพื่อเร่งการประมวลผล.

---

## วิธีเพิ่มคอนทราสต์เพื่อการจดจำที่ดียิ่งขึ้น

หลังจากแก้ไขการเอียง, ขั้นตอนต่อไปคือทำให้ข้อความเด่นชัด. `ContrastBoostFilter` ขยายช่วงความเข้มของพิกเซล, ซึ่งเป็นประโยชน์อย่างยิ่งสำหรับการพิมพ์ที่ซีด.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**ทำไมจึงช่วยได้:**  
การสแกนที่คอนทราสต์ต่ำทำให้เกิดอักขระสีเทาที่อาจถูกตัวแปลงเป็นไบนารีตีดเป็นพื้นหลัง. การเพิ่มคอนทราสต์ทำให้พิกเซลสีเข้มเข้มขึ้นและพิกเซลสีอ่อนอ่อนขึ้น, ให้ `BinarizationFilter` ถัดไปมีพื้นผิวที่สะอาดขึ้น.

---

## ทำ OCR บนภาพ – การโหลดไฟล์

ตอนนี้ภาพได้ผ่านการเตรียมล่วงหน้าแล้ว, เราต้อง **load image for OCR**. Aspose มีตัวช่วย `ImageStream.FromFile` ที่สะดวก.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

หากภาพของคุณอยู่ในสตรีม (เช่นอัปโหลดผ่านเว็บ API), คุณสามารถใช้ `ImageStream.FromStream(yourStream)` แทนได้. เครื่องยนต์รองรับ BMP, JPEG, PNG, TIFF, และอื่น ๆ อีกมาก.

---

## รันกระบวนการจดจำและ **extract text from scan**

เมื่อทุกอย่างเชื่อมต่อแล้ว, การเรียก `Recognize()` จะทำงานหนัก. หลังจากเรียก, ข้อความที่จดจำได้จะพร้อมใช้งานผ่าน `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับใบแจ้งหนี้ง่าย):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบลำดับของ pipeline อีกครั้ง—แก้เอียงก่อน, จากนั้นลดนอยส์, เพิ่มคอนทราสต์, และสุดท้ายไบนารีตีด. การสลับลำดับอาจทำให้ผลลัพธ์แย่ลง.

---

## ข้อผิดพลาดทั่วไปและกรณีขอบ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| **ผลลัพธ์ว่าง** | ภาพมืดเกินไปหรือสว่างเกินไปสำหรับวิธีไบนารีตีดเริ่มต้น. | เพิ่ม `ContrastBoostFilter.Strength` หรือเปลี่ยนเป็น `BinarizationMethod.Otsu`. |
| **ข้อความบางส่วนหาย** | ยังมีนอยส์เหลืออยู่หลังการลดนอยส์. | ใช้ `DenoiseLevel.Medium` สำหรับภาพที่น้อยนอยส์, หรือเพิ่ม `DenoiseFilter` ตัวที่สอง. |
| **ทิศทางการหมุนผิด** | เอกสารมีการวางแนวผสม (เช่น ภาพถ่ายของหน้าที่หมุน). | ตั้งค่า `DeskewFilter.MaxAngle` ต่ำลงด้วยตนเองและหมุนภาพล่วงหน้าด้วย `ImageProcessor.Rotate`. |
| **ประสิทธิภาพช้าลง** | ชุดใหญ่ของภาพความละเอียดสูง. | ลดขนาดภาพ (`ImageProcessor.Resize`) ก่อน pipeline, หรือประมวลผลแบบขนาน (`Parallel.ForEach`). |

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

บันทึกไฟล์นี้เป็น `Program.cs`, รัน `dotnet run`, และดูคอนโซลพิมพ์ผลลัพธ์ **extract text from scan**.  

---

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

* **Batch processing** – ห่อหุ้มตรรกะข้างต้นในลูปเพื่อจัดการหลายสิบไฟล์.  
* **Custom language packs** – หากคุณต้องการอ่านสคริปต์ที่ไม่ใช่ละติน, โหลดโมเดลภาษาโดยใช้ `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF output** – ผสาน Aspose.PDF กับ OCR เพื่อฝังข้อความที่ค้นหาได้โดยตรงลงในไฟล์ PDF.  
* **Performance tuning** – ทดลองจัดลำดับ `ImageProcessingPipeline`; บางครั้งการลดนอยส์ก่อนการแก้เอียงให้ผลลัพธ์เร็วขึ้นในภาพที่มีนอยส์.  

ทั้งหมดนี้สร้างบนแนวคิดหลักที่เราได้ครอบคลุม: **how to deskew image**, **how to boost contrast**, **load image for OCR**, **perform OCR on image**, และสุดท้าย **extract text from scan**.

---

## สรุป

เราเพิ่งแสดงวิธีที่สมบูรณ์และพร้อมใช้งานในผลิตภัณฑ์เพื่อ **how to deskew image** และรัน OCR ใน C#. ด้วยการต่อเชื่อม filter การแก้เอียง, ขั้นตอนการลดนอยส์, การเพิ่มคอนทราสต์, และ binarizer, คุณจะได้อินพุตที่สะอาดซึ่งทำให้ Aspose OCR สามารถ **extract text from scan** ได้อย่างเชื่อถือได้.  

ลองรันโค้ด, ปรับพารามิเตอร์ของ filter ให้เหมาะกับเอกสารของคุณ, แล้วคุณจะเห็นว่าความแม่นยำของการจดจำเพิ่มขึ้นเร็วแค่ไหน. มีคำถาม? แสดงความคิดเห็นได้เลย, และขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}