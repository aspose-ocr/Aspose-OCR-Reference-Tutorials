---
category: general
date: 2026-04-01
description: ทำการเตรียมภาพสำหรับ OCR เพื่อปรับปรุงความแม่นยำของ OCR เรียนรู้วิธีการใช้การปรับแนวอัตโนมัติ,
  การลดสัญญาณรบกวน, และการแปลงเป็นสีขาว‑ดำด้วย Aspose.OCR.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy
- black and white OCR
- Aspose OCR preprocessing
- image deskew C#
- OCR noise reduction
language: th
og_description: ทำการประมวลผลภาพล่วงหน้าสำหรับ OCR เพื่อปรับปรุงความแม่นยำของ OCR
  คู่มือแบบขั้นตอนต่อขั้นตอนนี้แสดงการแก้ไขการเอียงอัตโนมัติ, การลดสัญญาณรบกวน, และการแปลงเป็นสีขาว‑ดำด้วย
  C#
og_title: เตรียมภาพล่วงหน้าสำหรับ OCR – เพิ่มความแม่นยำด้วย Aspose.OCR
tags:
- OCR
- C#
- Image Processing
title: เตรียมภาพสำหรับ OCR – เพิ่มความแม่นยำด้วย Aspose.OCR
url: /th/net/ocr-optimization/preprocess-image-for-ocr-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เตรียมภาพสำหรับ OCR – เพิ่มความแม่นยำด้วย Aspose.OCR

เคยสงสัยไหมว่าทำไมผลลัพธ์ OCR ของคุณถึงดูเป็นกองอักขระสับสนแม้ว่าภาพต้นฉบับจะดูดี? คุณอาจพลาดขั้นตอนสำคัญ: **preprocess image for OCR**.  
ในบทเรียนนี้เราจะพาไปดูวิธีทำความสะอาดภาพที่เอียงหรือมีสัญญาณรบกวนเพื่อให้เครื่องอ่านได้อย่างมืออาชีพ. เมื่อทำครบคุณจะเห็นการกระโดดขึ้นอย่างชัดเจนใน **improve OCR accuracy** และคุ้นเคยกับเทคนิค **black and white OCR** ที่ Aspose.OCR ทำให้เป็นเรื่องง่าย.

## สิ่งที่คุณจะได้เรียนรู้

เราจะครอบคลุมตั้งแต่การติดตั้งแพคเกจ NuGet ของ Aspose.OCR ไปจนถึงการกำหนดค่า `PreprocessOptions` ที่ทำการ auto‑deskew, denoise, และ binarize ภาพของคุณ. คุณยังจะได้รับเคล็ดลับการจัดการกรณีขอบ – เช่น การหมุนมากเกินไปหรือสแกนที่คอนทราสต์ต่ำ – เพื่อให้คุณรักษาคุณภาพการจดจำได้สูงไม่ว่ากรณีใด. ไม่ต้องอ้างอิงเอกสารภายนอก; โซลูชันทั้งหมดอยู่ที่นี่.

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (ตัวอย่างคอมไพล์ด้วย .NET 6, แต่เวอร์ชันเก่าก็ทำงานได้)
- ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ใดก็ได้ที่คุณชอบ)
- ไฟล์ภาพที่เอียงหรือมีสัญญาณรบกวน (เราจะเรียกมันว่า `skewed_noisy.jpg`)

ถ้าคุณมีทั้งหมดนี้แล้ว, ไปต่อกันเลย.

## เตรียมภาพสำหรับ OCR – ทำไมการ Pre‑Processing ถึงสำคัญ

ลองนึกถึงเครื่อง OCR เป็นผู้อ่านที่เข้มงวด: ถ้าหน้ากระดาษเอียง, มีจุดรบกวน, หรือสีเทามากเกินไป, มันจะติดขัดกับคำ. การ Pre‑Processing จัดการกับศัตรูสามประการทั่วไป:

1. **Rotation** – Auto‑deskew ทำให้หน้ากระดาษตรงแนวนอน.  
2. **Noise** – Denoising กำจัดพิกเซลรบกวนที่อาจดูเหมือนอักขระ.  
3. **Contrast** – Binarizing (การแปลงเป็นสีขาว‑ดำ) ให้เครื่องแยกพื้นหน้า‑หลังได้ชัดเจน.

รวมกันเป็นกระดูกสันหลังของเวิร์กโฟลว์ใด ๆ ที่ต้องการ **improve OCR accuracy**.

![ตัวอย่างการเตรียมภาพสำหรับ OCR](https://example.com/ocr-preprocess.png "ตัวอย่างการเตรียมภาพสำหรับ OCR")

*(ข้อความแทนภาพ: “ตัวอย่างการเตรียมภาพสำหรับ OCR แสดงก่อนและหลังการทำ Binarization”)*

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR

เริ่มต้นด้วยการดาวน์โหลดไลบรารี. เปิดเทอร์มินัล (หรือ Package Manager Console) แล้วรัน:

```bash
dotnet add package Aspose.OCR
```

หรือ, ถ้าคุณชอบใช้ UI ของ Visual Studio, คลิกขวาที่ **Dependencies → Manage NuGet Packages**, ค้นหา **Aspose.OCR**, แล้วคลิก **Install**. แพคเกจนี้รวมทุกอย่างที่คุณต้องการ, รวมถึง namespace `Filters` ที่ใช้สำหรับการ Pre‑processing.

## ขั้นตอนที่ 2: สร้าง OCR Engine

เมื่อไลบรารีพร้อม, เราสามารถสร้างอินสแตนซ์ `OcrEngine` ได้. วัตถุนี้เป็นจุดเริ่มต้นสำหรับการจดจำทั้งหมด.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

ทำไมต้องสร้าง Engine ก่อน? Engine จะเก็บการตั้งค่าทั่วไป (ภาษา, ภูมิภาค, ฯลฯ) และสำคัญที่สุดคือ `PreprocessOptions` ที่เราจะกำหนดต่อไป.

## ขั้นตอนที่ 3: กำหนดค่า Preprocess Options

นี่คือจุดที่เวทมนต์เกิดขึ้น. เราจะเปิดใช้สามแฟล็ก:

- `AutoDeskew` – ตรวจจับและแก้ไขการหมุนโดยอัตโนมัติ.
- `DenoiseLevel = DenoiseLevel.Medium` – สมดุลระหว่างการทำความสะอาดสัญญาณรบกวนและการรักษารายละเอียดละเอียด.
- `Binarize` – บังคับให้ผลลัพธ์เป็นสีขาว‑ดำ, วิธี **black and white OCR** แบบคลาสสิก.

```csharp
// Step 3: Set up preprocessing to clean the image
PreprocessOptions preprocessOptions = new PreprocessOptions
{
    AutoDeskew = true,                     // Correct rotation automatically
    DenoiseLevel = DenoiseLevel.Medium,   // Reduce noise while preserving details
    Binarize = true                        // Convert to black‑and‑white for better recognition
};

// Attach options to the engine
ocrEngine.PreprocessOptions = preprocessOptions;
```

**ทำไมต้องตั้งค่าแบบนี้?** Auto‑deskew จัดการกับการเอียงทั่วไป (สูงสุดประมาณ ~15°). ระดับ Medium สำหรับการสแกนเอกสารทั่วไป; คุณสามารถเปลี่ยนเป็น `High` สำหรับสแกนที่มีสัญญาณรบกวนมาก, แต่ต้องระวังการสูญเสียอักขระเล็ก. การ Binarization เป็นหัวใจของ **black and white OCR** — มันลบกราเดียนสีเทาอ่อนที่ทำให้เครื่องสับสน.

## ขั้นตอนที่ 4: รันการจดจำบนภาพที่มีสัญญาณรบกวน

เมื่อ Engine พร้อม, ส่งพาธของภาพที่มีปัญหาให้มัน. เมธอด `Recognize` จะคืนค่าเป็นอ็อบเจกต์ `OcrResult` ที่บรรจุข้อความที่สกัดและคะแนนความเชื่อมั่น.

```csharp
// Step 4: Recognize text from a skewed and noisy image
// Replace the path with your actual image location
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

// Output the raw text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

ถ้าทุกอย่างทำงานเรียบร้อย, คุณควรเห็นบล็อกข้อความที่สะอาดในคอนโซล. Engine ยังเปิดให้เข้าถึง `ocrResult.Confidence` หากคุณต้องการตัวเลขวัด **improve OCR accuracy**.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และปรับแต่งเพื่อความแม่นยำที่ดียิ่งขึ้น

การเห็นผลลัพธ์เป็นเรื่องดี, แต่คุณอาจยังพบการอ่านผิดบางส่วน — โดยเฉพาะกับฟอนต์แปลก. นี่คือเช็คลิสต์สั้น ๆ:

1. **ตรวจสอบ Confidence** – ค่าต่ำกว่า 0.7 มักบ่งบอกพื้นที่ที่มีปัญหา. คุณสามารถบันทึกค่าเหล่านี้และตัดสินใจว่าจะทำ Pre‑process ใหม่ด้วย `DenoiseLevel` ที่สูงขึ้นหรือไม่.
2. **ปรับ Threshold ของ Binarization** – Aspose ให้คุณส่งค่า Threshold ที่กำหนดเองผ่าน `PreprocessOptions.BinarizationThreshold`. ค่าต่ำจะเก็บสีเทามากกว่า, ค่าสูงจะทำให้สีขาว‑ดำเข้มข้นกว่า.
3. **Crop หรือ Resize** – ถ้าภาพใหญ่เกินไป, ลดขนาดลงประมาณ ~150 DPI ก่อนส่งให้ Engine; จะช่วยเร่งการประมวลผลและอาจเพิ่มความแม่นยำได้.

```csharp
// Example: Increase denoise for a very dirty scan
ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;

// Re‑run recognition
var refinedResult = ocrEngine.Recognize("YOUR_DIRECTORY/very_dirty.jpg");
Console.WriteLine(refinedResult.Text);
```

## โบนัส: ใช้ Black and White OCR เพื่อผลลัพธ์ที่ดีกว่า

บางครั้งคุณอาจได้ยินนักพัฒนาบอกว่า “ใช้ Grayscale ก็พอ” — แต่วิธี **black and white OCR** มักให้ผลดีกว่า, โดยเฉพาะเมื่อแหล่งข้อมูลมีแสงไม่สม่ำเสมอ. การบังคับให้เป็นภาพไบนารีจะลบเงาอ่อนที่เครื่องอาจเข้าใจว่าเป็นอักขระ.

หากคุณต้องการทดลองต่อ, คุณสามารถสร้างภาพไบนารีด้วยตนเองแล้วส่งให้ Engine:

```csharp
// Generate a binary bitmap manually (optional)
Bitmap binaryBitmap = ocrEngine.PreprocessOptions.ApplyFilters(
    Image.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg")
);

// Pass the bitmap directly
var bitmapResult = ocrEngine.Recognize(binaryBitmap);
Console.WriteLine(bitmapResult.Text);
```

วิธีนี้ให้คุณควบคุมขั้นตอน Pre‑processing ทั้งหมด, ซึ่งมีประโยชน์เมื่อคุณต้องรวมฟิลเตอร์กำหนดเองหรือไลบรารีภาพของบุคคลที่สาม.

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน, นี่คือแอปคอนโซลที่พร้อมรันที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์ C# ใหม่:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (auto‑deskew, denoise, binarize)
        PreprocessOptions preprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,
            DenoiseLevel = DenoiseLevel.Medium,
            Binarize = true
        };
        ocrEngine.PreprocessOptions = preprocessOptions;

        // 3️⃣ Recognize the image (replace with your file path)
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);

        // 5️⃣ Optional: tweak settings if confidence is low
        if (ocrResult.Confidence < 0.7)
        {
            Console.WriteLine("\nLow confidence detected – increasing denoise level.");
            ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;
            var retryResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");
            Console.WriteLine("=== Refined Output ===");
            Console.WriteLine(retryResult.Text);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวังในคอนโซล**

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.

=== Refined Output ===
The quick brown fox jumps over the lazy dog.
```

*ข้อความจริงของคุณจะต่างกันแน่นอน, แต่คุณควรเห็นรูปแบบที่สะอาดเช่นเดียวกัน.*

## สรุป

เราได้แสดงวิธี **preprocess image for OCR** ด้วย Aspose.OCR, และอธิบายว่าขั้นตอนแต่ละอย่าง — auto‑deskew, denoise, และการแปลงเป็นสีขาว‑ดำ — มีบทบาทสำคัญในการ **improve OCR accuracy**. ด้วยโค้ดที่ให้ไว้ คุณจะได้ผลลัพธ์ที่เชื่อถือได้บนสแกนที่เอียงหรือมีสัญญาณรบกวนโดยไม่ต้องค้นหาเอกสารเพิ่มเติม.

ต่อไปคุณจะทำอะไร? ลองผสาน pipeline นี้กับการตั้งค่าภาษาเฉพาะ (เช่น `ocrEngine.Language = Language.English`) หรือส่งบิตแมพที่ทำความสะอาดแล้วไปยังโมเดล NLP ต่อไป. คุณยังสามารถทดลองปรับ `BinarizationThreshold` เพื่อจูนเอฟเฟกต์ **black and white OCR** สำหรับใบเสร็จที่คอนทราสต์ต่ำหรือโน้ตมือเขียน.

หากคุณเจอปัญหาใด ๆ หรือมีเทคนิคของคุณเองในการเพิ่มความแม่นยำของ OCR, อย่าลังเลที่จะแสดงความคิดเห็น. Happy coding, และขอให้ข้อความของคุณอ่านได้ชัดเจนเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}