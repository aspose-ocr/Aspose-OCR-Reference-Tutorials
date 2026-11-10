---
category: general
date: 2026-02-14
description: เรียนรู้วิธีการลบการเอียงจากภาพ, เตรียมภาพสำหรับ OCR, ลดสัญญาณรบกวนในภาพและสกัดข้อความจากภาพโดยใช้
  Aspose OCR ใน C#
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: th
og_description: ลบการเอียงของภาพ, เตรียมภาพสำหรับ OCR และดึงข้อความจากภาพด้วยบทแนะนำขั้นตอนต่อขั้นตอนใน
  C# โดยใช้ Aspose OCR.
og_title: ลบการเอียงจากภาพ – คู่มือการเตรียม OCR อย่างครบถ้วน
tags:
- OCR
- CSharp
- ImageProcessing
title: ลบการเอียงจากภาพ – คู่มือการเตรียม OCR อย่างครบถ้วน
url: /th/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ลบการเอียงของภาพ – คู่มือการเตรียมการ OCR อย่างครบถ้วน

เคยต้องการ **remove skew from image** ก่อนส่งให้เครื่อง OCR หรือไม่? คุณไม่ได้เป็นคนเดียว—เอกสารที่สแกน, ภาพถ่ายใบเสร็จ, หรือสกรีนช็อตมักจะมาพร้อมการเอียง, และมุมเล็กน้อยนั้นสามารถทำให้การจดจำข้อความล้มเหลวได้.  

ข่าวดี? ด้วยฟิลเตอร์ Aspose OCR เพียงไม่กี่ตัว คุณสามารถทำให้ภาพตรง, ลดสัญญาณรบกวน, เพิ่มคอนทราสต์, แล้ว **extract text from image** ในขั้นตอนเดียวที่ต่อเนื่อง. ในคู่มือนี้เราจะเดินผ่านกระบวนการทั้งหมด, ตั้งแต่การโหลดภาพที่เอียงจนถึง **recognize text from document** และพิมพ์ผลลัพธ์.

---

## สิ่งที่คุณจะสร้าง

เมื่อจบบทเรียนนี้คุณจะมีแอปคอนโซล C# ที่พร้อมรันที่:

1. **Removes skew from image** ด้วย `DeskewFilter`.
2. **Reduces noise in image** ด้วย `DenoiseFilter`.
3. **Preprocesses image for OCR** โดยเพิ่มคอนทราสต์.
4. **Recognizes text from document** ผ่าน `Engine` ของ Aspose OCR.
5. **Extracts text from image** และแสดงบนคอนโซล.

ไม่มีบริการภายนอก, เพียงแพคเกจ Aspose OCR NuGet และไม่กี่บรรทัดของโค้ด.

---

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดทำงานกับ .NET Core และ .NET Framework ด้วยเช่นกัน).
- Visual Studio 2022 หรือเครื่องมือแก้ไขใด ๆ ที่คุณชอบ.
- ติดตั้ง Aspose.OCR สำหรับ .NET (`dotnet add package Aspose.OCR`).
- ภาพตัวอย่าง (`skewed_noisy.jpg`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้.

ถ้าคุณมีทั้งหมดนี้, ไปกันเลย.

---

## ขั้นตอนที่ 1: โหลดภาพต้นฉบับ

สิ่งแรกที่เราต้องการคือ `ImageStream` ที่ชี้ไปยังไฟล์ที่เราต้องการทำความสะอาด.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **ทำไมสิ่งนี้สำคัญ:** `ImageStream` ทำหน้าที่เป็นนามธรรมของบิตแมปพื้นฐาน, ทำให้ฟิลเตอร์ Aspose ทำงานได้โดยที่คุณไม่ต้องจัดการข้อมูลพิกเซลดิบ.

---

## ขั้นตอนที่ 2: สร้าง Pipeline การเตรียมการ (Remove Skew & Reduce Noise)

แทนที่จะเรียกใช้ฟิลเตอร์แต่ละตัวแยกกัน, Aspose ให้คุณเชื่อมต่อพวกมันใน `ImageProcessingPipeline`. สิ่งนี้ทำให้โค้ดเป็นระเบียบและรับประกันว่าการดำเนินการเกิดขึ้นตามลำดับที่ถูกต้อง.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### ทำไมลำดับจึงสำคัญ

1. **Deskew first** – การทำให้ภาพตรงก่อนการลดสัญญาณรบกวนจะป้องกันไม่ให้ฟิลเตอร์สัญญาณรบกวนมองขอบเอียงเป็นศิลปวัตถุ.  
2. **Denoise second** – เมื่อภาพอยู่ในระดับที่เรียบ, อัลกอริทึมสามารถแยกสัญญาณจากเม็ดเกรนได้ดีขึ้น.  
3. **Contrast boost last** – การเพิ่มคอนทราสต์หลังจากภาพสะอาดแล้วจะเพิ่มความอ่านได้ของ OCR สูงสุดโดยไม่ทำให้สัญญาณรบกวนเพิ่มขึ้น.

---

## ขั้นตอนที่ 3: ใช้ Pipeline และรับภาพที่ทำความสะอาดแล้ว

ตอนนี้เราจะรัน pipeline กับสตรีมต้นฉบับ.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

ในขั้นตอนนี้ภาพได้ถูก deskewed, denoised, และมีคอนทราสต์สูงขึ้น—เหมาะอย่างยิ่งสำหรับ OCR.

---

## ขั้นตอนที่ 4: เริ่มต้น OCR Engine และจดจำข้อความ

เมื่อมีภาพที่บริสุทธิ์ในมือ เราก็สามารถส่งให้ Aspose OCR ได้ในที่สุด.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **เคล็ดลับ:** หากคุณต้องการการปรับแต่งตามภาษา, `Engine` รองรับคุณสมบัติ `Language` (เช่น `ocrEngine.Language = Language.English;`). สำหรับเอกสารที่ใช้ตัวอักษรละตินส่วนใหญ่ค่าเริ่มต้นทำงานได้ดี.

---

## ขั้นตอนที่ 5: แสดงข้อความที่สกัดออกมา

`Console.WriteLine` อย่างรวดเร็วจะแสดงผลลัพธ์.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

เมื่อคุณรันโปรแกรม คุณควรเห็นเนื้อหาข้อความของ `skewed_noisy.jpg` แสดงบนเทอร์มินัล—สะอาด, อ่านง่าย, และพร้อมสำหรับการประมวลผลต่อไป.

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมคัดลอกและวาง. บันทึกเป็น `Program.cs`, แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริง, แล้วรัน `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับใบเสร็จง่าย):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

หากผลลัพธ์ดูเป็นอักษรผิด, ตรวจสอบอีกครั้งว่าพาธของภาพถูกต้องและไฟล์ต้นฉบับมีข้อความที่อ่านได้จริง.

---

## คำถามทั่วไป & กรณีขอบ

### ถ้าภาพถูกหมุน 90° แทนการเอียงเล็กน้อย?

`DeskewFilter` จัดการกับมุมเล็ก (±15°). สำหรับการหมุนเต็ม, เรียก `new RotateFilter { Angle = 90 }` ก่อนขั้นตอน deskew.

### ภาพของฉันเป็นรูปแบบ PNG—มีอะไรเปลี่ยนแปลงไหม?

ไม่มี. `ImageStream.FromFile` ตรวจจับรูปแบบอัตโนมัติ, ดังนั้น PNG, JPEG, BMP, หรือ TIFF ทำงานแบบเดียวกัน.

### ฉันจะปรับความแรงของการลดสัญญาณรบกวนได้อย่างไร?

`DenoiseFilter` มีคุณสมบัติ `Strength` (0‑100). ค่าที่สูงกว่าจะลบเม็ดเกรนมากขึ้นแต่อาจทำให้รายละเอียดบางอย่างเบลอ. ทดลองค่าประมาณ 30‑50 สำหรับเอกสารที่มีข้อความมาก.

### ฉันต้องการประมวลผลหลายไฟล์—ฉันสามารถใช้ pipeline ซ้ำได้ไหม?

แน่นอน. สร้าง `processingPipeline` ครั้งเดียว, แล้ววนลูปแต่ละไฟล์:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

การใช้ `Engine` ตัวเดียวกันซ้ำยังช่วยเพิ่มประสิทธิภาพ.

---

## เคล็ดลับระดับมืออาชีพสำหรับ OCR ที่พร้อมใช้งานในผลิตภัณฑ์

- **Cache the pipeline**: การสร้างฟิลเตอร์ซ้ำหลายครั้งอาจมีค่าใช้จ่ายสูงในสถานการณ์ที่ต้องประมวลผลจำนวนมาก.  
- **Set OCR language**: `ocrEngine.Language = Language.Spanish;` สำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษ.  
- **Handle empty results**: ตรวจสอบเสมอว่า `ocrResult.Text?.Length > 0` ก่อนดำเนินการต่อ.  
- **Log intermediate images**: การบันทึก `cleanedImage` ลงดิสก์ (`cleanedImage.Save("debug.png");`) ช่วยให้คุณปรับพารามิเตอร์ฟิลเตอร์ได้ละเอียด.

---

## สรุป

เราได้แสดงวิธี **remove skew from image**, **reduce noise in image**, และ **preprocess image for OCR** ด้วย pipeline ฟิลเตอร์ที่ทรงพลังของ Aspose OCR, จากนั้น **recognize text from document** และสุดท้าย **extract text from image**. ทั้งหมดนี้ทำได้ในไม่เกิน 50 บรรทัดของ C# และง่ายต่อการขยายสำหรับการประมวลผลเป็นชุด, โมเดลภาษาที่กำหนดเอง, หรือฟิลเตอร์เพิ่มเติม.  

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเพิ่ม `BinarizeFilter` เพื่อบังคับให้ผลลัพธ์เป็นสีขาว‑ดำ, หรือทดลองระดับต่าง ๆ ของ `ContrastBoostFilter` เพื่อดูว่ามันส่งผลต่อความแม่นยำของการจดจำอย่างไร. ยิ่งคุณทดลองกับ pipeline มากเท่าไหร่, คุณก็จะเข้าใจว่าฟิลเตอร์แต่ละตัวมีส่วนช่วยให้ได้ผล OCR ที่สะอาดแค่ไหน.  

ขอให้สนุกกับการเขียนโค้ด, และขอให้ภาพของคุณอยู่ตรงเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}