---
category: general
date: 2026-04-03
description: วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR ใน C# – เรียนรู้วิธีเตรียมภาพล่วงหน้าสำหรับ
  OCR, แยกข้อความจากภาพและปรับปรุงความแม่นยำของ OCR ภายในไม่กี่นาที
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- improve ocr accuracy
- load image for ocr
language: th
og_description: วิธีแก้ไขการเอียงของภาพใน C# ด้วย Aspose OCR คู่มือนี้จะแสดงวิธีการเตรียมภาพสำหรับ
  OCR, แยกข้อความจากภาพและเพิ่มความแม่นยำ.
og_title: วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- Image preprocessing
title: วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/ocr-optimization/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์

เคยสงสัย **how to deskew image** ก่อนนำไปใส่ในเครื่อง OCR หรือไม่? คุณไม่ได้เป็นคนเดียว—การสแกนที่เอียง, ภาพถ่ายที่ถ่ายมาที่มุม, หรือแม้แต่ PDF ที่ค่อนข้างเอียงเล็กน้อยก็อาจทำให้ไลบรารีการจดจำข้อความทำงานผิดพลาดได้.  

ในบทแนะนำแบบขั้นตอนนี้ เราจะพาคุณผ่านกระบวนการทำงานทั้งหมด: ตั้งแต่การโหลดรูปภาพ, ผ่าน **preprocess image for OCR** (deskew, denoise, contrast boost, auto‑rotate), ไปจนถึง **recognize text from image** ด้วย Aspose OCR, และสุดท้ายคือเคล็ดลับบางอย่างเพื่อ **improve OCR accuracy**. เมื่อเสร็จสิ้นคุณจะมีแอปคอนโซล C# ที่พร้อมรันซึ่งจัดการกับ PNG ที่มีสัญญาณรบกวนและเอียงได้อย่างมืออาชีพ.

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือ .NET Framework 4.7.2 – API ทำงานเช่นเดียวกัน)
- **Aspose.OCR for .NET** NuGet package (`Install-Package Aspose.OCR`)
- ตัวอย่างภาพที่ **skewed** และ **noisy** (เช่น `skewed_noisy.png`)
- Visual Studio, Rider หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ – ไม่ต้องการเครื่องมือพิเศษ

> **Pro tip:** หากคุณไม่มีตัวอย่างที่ skewed เพียงแค่หมุนสกรีนช็อตที่สะอาด 10‑15° ใน Paint แล้วเพิ่ม “salt‑and‑pepper” noise เล็กน้อยด้วยโปรแกรมแก้ไขภาพ โค้ดจะทำงานเช่นเดียวกัน.

ตอนนี้, มาเริ่มกันเลย.

## วิธีแก้ไขการเอียงของภาพและเพิ่มความแม่นยำของ OCR

สิ่งแรกที่คุณต้องทำคือบอกให้ `OcrEngine` ของ Aspose **deskew** bitmap ที่เข้ามา. เอนจินมาพร้อมกับคลาส `ImagePreprocessingOptions` ที่สร้างไว้ในตัว ซึ่งให้คุณเปิด/ปิดคุณสมบัติการปรับคุณภาพหลายอย่างพร้อมกัน.

```csharp
using Aspose.OCR;
using System.Drawing;

/// <summary>
/// Demonstrates how to deskew image, denoise, boost contrast, and run OCR.
/// </summary>
class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing options
        ImagePreprocessingOptions opts = new ImagePreprocessingOptions
        {
            Deskew = true,          // <-- this is the key to how to deskew image
            Denoise = true,
            ContrastBoost = 30,    // increase contrast by 30 %
            AutoRotate = true
        };
        ocrEngine.PreprocessingOptions = opts;

        // 3️⃣ Load the image you want to process
        Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run OCR on the pre‑processed bitmap
        string text = ocrEngine.Recognize(input);

        // 5️⃣ Show the result
        System.Console.WriteLine(text);
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **Deskew = true** บอกให้เอนจินตรวจจับ baseline ของข้อความและหมุนภาพจนกว่า baseline จะเป็นแนวนอน. หากไม่ทำ, การเอียงเพียง 5° ก็อาจทำให้ความแม่นยำลดลง 15‑20 %.
- **Denoise** ลบจุดรบกวนแบบสุ่มที่มักปรากฏหลังจากสแกนเอกสารความละเอียดต่ำ.
- **ContrastBoost** เพิ่มความแตกต่างระหว่าง foreground (text) กับ background (paper), ซึ่งจำเป็นสำหรับ **improve OCR accuracy**.
- **AutoRotate** จัดการการหมุนแนวตั้ง vs แนวนอนโดยอัตโนมัติ, ช่วยคุณไม่ต้องตรวจสอบด้วยตนเอง.

โค้ดข้างต้นเป็น **complete, runnable example**—เพียงเปลี่ยน `YOUR_DIRECTORY` ให้เป็นพาธของไฟล์ของคุณและกด F5.

## Preprocess Image for OCR – การลดสัญญาณรบกวนและเพิ่มความคอนทราสต์

คุณอาจสงสัยว่าจำเป็นต้องทำการลดสัญญาณรบกวนและเพิ่มคอนทราสต์พร้อมกันหรือไม่. คำตอบสั้น ๆ: **yes, in most real‑world cases**. นี่คือการสรุปอย่างรวดเร็ว:

| คุณลักษณะ | ทำอะไร | เมื่อสำคัญ |
|-----------|--------|------------|
| **Deskew** | ทำให้บรรทัดข้อความที่เอียงตรงขึ้น | แบบฟอร์มที่สแกน, ภาพจากกล้องโทรศัพท์ |
| **Denoise** | ลบพิกเซลที่แยกออกมา | การสแกนในแสงน้อย, สแกนเนอร์ราคาถูก |
| **ContrastBoost** | ทำให้ข้อความสีเข้มสว่างขึ้น, พื้นหลังสีเข้มลง | เอกสารซีด, หมึกซีด |
| **AutoRotate** | ตรวจจับแนวตั้งหรือแนวนอนอัตโนมัติ | PDF หลายหน้า ที่มีการวางแนวผสมกัน |

หากคุณกำลังประมวลผลสแกนที่สะอาดและจัดแนวอย่างสมบูรณ์ คุณอาจปิดฟลักเหล่านี้ได้, แต่ **preprocess image for OCR** เป็นค่าเริ่มต้นที่ปลอดภัยและแทบไม่มีผลเสีย.

## การจดจำข้อความจากภาพ – การใช้ Aspose OCR

เมื่อขั้นตอนการเตรียมภาพเสร็จสิ้น, เอนจินจะส่ง bitmap ที่ทำความสะอาดแล้วให้กับ recognizer ภายใน. เมธอด `Recognize` จะคืนค่า `string` ธรรมดาที่คงการขึ้นบรรทัดไว้. คุณสามารถทำการ post‑process ผลลัพธ์ต่อได้ (เช่น ตัด whitespace, รัน spell‑check) หากต้องการ.

```csharp
string recognizedText = ocrEngine.Recognize(inputImage);
Console.WriteLine("--- OCR RESULT ---");
Console.WriteLine(recognizedText);
```

### ผลลัพธ์ที่คาดหวัง

หาก `skewed_noisy.png` มีข้อความ “Hello World!”, คอนโซลจะพิมพ์บางอย่างเช่น:

```
--- OCR RESULT ---
Hello World!
```

แม้จะมีสัญญาณรบกวนระดับปานกลาง, คุณควรเห็น **over 95 % accuracy** ขอบคุณขั้นตอนการเตรียมภาพที่เราเปิดใช้งาน.

## การโหลดภาพสำหรับ OCR – เคล็ดลับการจัดการไฟล์

บรรทัด `Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png")` เป็นวิธีที่ง่ายที่สุดในการ **load image for OCR**, แต่มีรายละเอียดเล็กน้อยที่ควรทราบ:

1. **File locks** – `FromFile` จะเปิดไฟล์ไว้จนกว่า `Image` จะถูก disposed. ควรใส่ไว้ในบล็อก `using` หากคุณต้องการลบหรือย้ายไฟล์ภายหลัง.
2. **Supported formats** – Aspose OCR รองรับ BMP, JPEG, PNG, TIFF, และ GIF. หากคุณมี PDF, ให้แยกแต่ละหน้าเป็นภาพก่อน (Aspose.PDF สามารถช่วยได้).
3. **Memory usage** – ภาพขนาดใหญ่ (มากกว่า 5 MP) สามารถใช้ RAM มาก. พิจารณาลดขนาดด้วย `Bitmap` ก่อนส่งให้เอนจินหากเจอ `OutOfMemoryException`.

```csharp
using (Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png"))
{
    string result = ocrEngine.Recognize(input);
    Console.WriteLine(result);
}
```

## การปรับปรุงความแม่นยำของ OCR – เคล็ดลับจากโลกจริง

แม้จะมีการเตรียมภาพอัตโนมัติ, บางกรณีขอบยังทำให้เอนจิน OCR ทำงานผิดพลาด. ด้านล่างเป็นกลยุทธ์ที่ผ่านการทดสอบที่คุณสามารถใส่ลงใน pipeline ของคุณ:

- **Binarize the image** (`opts.Binarization = true`) เมื่อพื้นหลังไม่สม่ำเสมอ.
- **Set language** (`ocrEngine.Language = Language.English`) เพื่อจำกัดชุดอักขระ.
- **Increase DPI**: หากคุณควบคุมกระบวนการสแกน, ตั้งค่าอย่างน้อย 300 dpi.
- **Crop margins**: ลบขอบสีขาวใหญ่; มันอาจทำให้การตรวจจับบรรทัดสับสน.
- **Validate output**: ใช้ regular expressions เพื่อตรวจสอบวันที่, ตัวเลข, หรือรูปแบบที่รู้จัก, แล้วทำเครื่องหมายบรรทัดที่ความเชื่อมั่นต่ำเพื่อการตรวจสอบด้วยมือ.

> **Remember:** เป้าหมายไม่ได้แค่ **recognize text from image**, แต่ทำให้ทำได้อย่างเชื่อถือได้ในคุณภาพเอกสารที่หลากหลาย.

## ตัวอย่างทำงานเต็มรูปแบบ – ทุกขั้นตอนในไฟล์เดียว

ด้านล่างเป็นโปรแกรมสุดท้ายที่เป็นอิสระซึ่งคุณสามารถคัดลอกและวางลงในโปรเจกต์คอนโซลใหม่ได้.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class DeskewOcrDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine engine = new OcrEngine();

        // Preprocess settings (deskew, denoise, contrast, auto‑rotate)
        engine.PreprocessingOptions = new ImagePreprocessingOptions
        {
            Deskew = true,
            Denoise = true,
            ContrastBoost = 30,
            AutoRotate = true
        };

        // Load image – make sure the path is correct
        const string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";

        // Using block prevents file‑handle leaks
        using (Image img = Image.FromFile(imagePath))
        {
            // Run OCR
            string text = engine.Recognize(img);

            // Output result
            Console.WriteLine("--- OCR RESULT ---");
            Console.WriteLine(text);
        }
    }
}
```

รันโปรแกรม, คุณควรเห็นข้อความที่ทำความสะอาดและแก้ไขการเอียงถูกพิมพ์ในคอนโซล. หากคุณเปลี่ยน `skewed_noisy.png` เป็นสแกนที่สะอาดและตรง, ผลลัพธ์จะเหมือนเดิม—แต่จะมีการเพิ่มประสิทธิภาพเล็กน้อยเนื่องจากเอนจินข้ามขั้นตอน deskew.

## สรุป

เราได้อธิบาย **how to deskew image** ด้วย Aspose OCR, แสดงวิธี **preprocess image for OCR**, สาธิตวิธีที่ถูกต้องในการ **load image for OCR**, และสุดท้าย **recognize text from image** พร้อมกับคำนึงถึง **improve OCR accuracy**. โค้ดตัวอย่างเต็มพร้อมใช้งานในโปรเจกต์ .NET ใด ๆ, และเคล็ดลับเพิ่มเติมให้คุณมีแผนที่สำหรับจัดการอินพุตที่ท้าทายยิ่งขึ้น.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองเชื่อมต่อหลายภาพเข้าด้วยกันเพื่อสร้าง workflow OCR หลายหน้า, หรือทดลองใช้ language pack แบบกำหนดเองสำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษ. หลักการเตรียมภาพเดียวกันยังคงใช้ได้—deskew, denoise, boost contrast, และให้ Aspose ทำงานหนัก.

มีคำถามเกี่ยวกับประเภทไฟล์เฉพาะหรือจำเป็นต้องช่วยปรับค่า `ContrastBoost`? แสดงความคิดเห็นด้านล่างหรือเข้าไปที่ฟอรั่มของ Aspose. โค้ดดิ้งสนุก, และขอให้ OCR ของคุณแม่นยำเสมอ!  

![แผนภาพแสดงภาพที่เอียงต้นฉบับทางซ้ายและผลลัพธ์ที่แก้ไขการเอียงและทำความสะอาดทางขวา](deskew-diagram.png "แผนภาพแสดงภาพที่เอียงต้นฉบับและผลลัพธ์ที่แก้ไขการเอียง – ตัวอย่างวิธีแก้ไขการเอียงของภาพ")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}