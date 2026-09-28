---
category: general
date: 2025-12-29
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพ, ลบพื้นหลังและดึงข้อความด้วย Aspose
  OCR. โค้ด C# ทีละขั้นตอนเพื่อเตรียมภาพสำหรับ OCR และจดจำข้อความจากภาพ.
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: th
og_description: วิธีแก้ไขการเอียงของภาพและเพิ่มความแม่นยำของ OCR. ปฏิบัติตามคู่มือนี้เพื่อกำจัดพื้นหลัง,
  เตรียมภาพสำหรับ OCR และจดจำข้อความจากภาพโดยใช้ Aspose.
og_title: วิธีทำให้ภาพตรง – การสอนการเตรียมข้อมูล OCR ด้วย C#
tags:
- Aspose OCR
- C#
- Image preprocessing
title: วิธีแก้การเอียงของภาพ – คู่มือ C# ฉบับสมบูรณ์สำหรับการเตรียม OCR
url: /th/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือ C# ฉบับสมบูรณ์สำหรับการเตรียมข้อมูล OCR

เคยสงสัยไหมว่า **วิธีแก้ไขการเอียงของภาพ** ที่สแกนออกมาดูเหมือนโปสการ์ดบิดเบี้ยว? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ ภาพต้นฉบับมักจะเอียง มีเสียงรบกวน หรือมีพื้นหลังเป็นลายจุดสีที่ทำให้ OCR ทำงานลำบาก  

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันที่ใช้งานได้จริง ไม่เพียงแค่ **วิธีแก้ไขการเอียงของภาพ** แต่ยังรวมถึง **วิธีลบพื้นหลัง**, **วิธีสกัดข้อความ**, และสุดท้าย **การจดจำข้อความจากภาพ** ด้วย Aspose OCR สำหรับ .NET เมื่อจบคุณจะได้โปรแกรม C# ที่พร้อมรันเพื่อเตรียมภาพสำหรับ OCR และคืนข้อความที่สะอาดและค้นหาได้

## สิ่งที่คุณต้องมี

- .NET 6 SDK หรือใหม่กว่า (โค้ดทำงานได้บน .NET Core และ .NET Framework ทั้งหมด)  
- Visual Studio 2022 (หรือโปรแกรมแก้ไขที่คุณชอบ)  
- แพ็กเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- ตัวอย่างภาพที่เอียงและมีเสียงรบกวน (เช่น `skewed_noisy.jpg`)  

เท่านี้—ไม่มีไลบรารีเนทีฟเพิ่มเติม ไม่มีเครื่องมือบรรทัดคำสั่งที่ยุ่งยาก มาเริ่มกันเลย

## ขั้นตอนที่ 1 – โหลดภาพอินพุต (เริ่มต้นวิธีแก้ไขการเอียงของภาพ)

สิ่งแรกที่ต้องทำคือโหลดภาพเข้าสู่หน่วยความจำ เมธอด `Image.Load` ของ Aspose OCR รับพาธไฟล์และคืนอ็อบเจ็กต์ `Image` ที่คุณสามารถจัดการได้

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดภาพทำให้เรามีตัวจับเพื่อใช้กับการแปลงต่อ ๆ ไป ทั้งการแก้ไขการเอียงและการลบพื้นหลัง

## ขั้นตอนที่ 2 – แก้ไขการเอียงของภาพ (วิธีแก้ไขการเอียงของภาพในทางปฏิบัติ)

Aspose OCR มีฟิลเตอร์ `Deskew` ที่ตรวจจับมุมเอียงอัตโนมัติได้จนถึงค่าขีดจำกัดที่กำหนด ที่นี่เรากำหนดให้สูงสุด **5°** เพราะเอกสารสแกนส่วนใหญ่ไม่เกินค่านี้

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **เคล็ดลับ:** หากเอกสารของคุณหมุนเกิน 5° ให้เพิ่มค่า `angleThreshold` เป็น 10 หรือ 15 ได้เลย อัลกอริทึมยังคงทำงานเร็วแม้กับมุมที่ใหญ่ขึ้น

## ขั้นตอนที่ 3 – ลดสัญญาณรบกวนในภาพที่แก้ไขการเอียงแล้ว

สัญญาณรบกวนเป็นศัตรูลับของความแม่นยำ OCR การทำการลดสัญญาณรบกวนอย่างง่ายช่วยลบจุดรบกวนโดยไม่ทำให้ตัวอักษรเบลอ

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **ทำงานอย่างไรภายใน:** ฟิลเตอร์ใช้การเบลอแบบมีเดียนที่รักษาขอบ (ตัวอักษร) ไว้ในขณะที่ลดพิกเซลที่แยกเดี่ยวออกไป

## ขั้นตอนที่ 4 – ลบพื้นหลัง (วิธีลบพื้นหลังอย่างมีประสิทธิภาพ)

พื้นหลังที่อ่อนหรือมีลายจุดอาจทำให้เครื่อง OCR สับสน เมธอด `RemoveBackground` ของ Aspose OCR จะแยกข้อความพื้นหน้าออกจากพื้นหลัง

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **ทำไมต้องลบพื้นหลัง?** การเพิ่มคอนทราสต์ระหว่างข้อความและพื้นผิวทำให้เครื่องสามารถแยกอักขระได้แม่นยำขึ้นโดยตรง ซึ่งช่วยปรับปรุงผลลัพธ์ของ **วิธีสกัดข้อความ** ให้ดียิ่งขึ้น

## ขั้นตอนที่ 5 – เริ่มต้นเครื่อง OCR

เมื่อภาพตรง, สะอาด, และคอนทราสต์สูง เราจะสร้างอินสแตนซ์ของเครื่อง OCR ไม่ต้องตั้งค่าเพิ่มเติมสำหรับสคริปต์ละตินพื้นฐาน แต่คุณสามารถสลับภาษาได้หากต้องการ

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **หมายเหตุ:** Aspose OCR รองรับมากกว่า 100 ภาษา หากต้องการรองรับหลายภาษา ให้ตั้งค่า `ocrEngine.Language = OcrLanguage.YourLanguage;` ก่อนทำการจดจำ

## ขั้นตอนที่ 6 – จดจำข้อความจากภาพ (วิธีสกัดข้อความ)

เมื่อเครื่องพร้อม ให้นำภาพที่ผ่านการเตรียมส่งเข้าไป เมธอด `Recognize` จะคืนอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความดิบและคะแนนความเชื่อมั่น

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **ข้อมูลเชิงลึกของผลลัพธ์:** `ocrResult.Text` มีสตริงข้อความธรรมดา ส่วน `ocrResult.Confidence` (หากเรียกดู) จะบอกระดับความมั่นใจของเครื่องต่อแต่ละบรรทัด

## ขั้นตอนที่ 7 – แสดงผลข้อความที่จดจำได้

สุดท้าย พิมพ์ข้อความที่สกัดออกมาที่คอนโซล—หรือบันทึกลงไฟล์, ฐานข้อมูล, หรือที่ใดก็ได้ตามกระบวนการทำงานของคุณ

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

โปรแกรมเต็มรูปแบบพร้อมรันแล้ว สร้างและรันโปรเจกต์ คุณจะเห็นข้อความที่สะอาดและอ่านง่าย แม้ภาพต้นฉบับจะเริ่มจากการเอียงและมีสัญญาณรบกวน

![ตัวอย่างการแก้ไขการเอียงของภาพ](/images/deskew-demo.png "สาธิตการแก้ไขการเอียงของภาพโดยใช้ Aspose OCR")

*ภาพหน้าจอด้านบนแสดงภาพก่อนและหลังการแก้ไขการเอียงของภาพ เพื่อแสดงผลของขั้นตอนการเตรียมข้อมูล*

## กรณีขอบและคำถามที่พบบ่อย

### ถ้าภาพหมุนเกิน 5° จะทำอย่างไร?
เพิ่มค่า `angleThreshold` ในการเรียก `Deskew` อัลกอริทึมยังคงตรวจจับมุมที่ถูกต้องได้ เพียงแต่ขยายช่วงการค้นหาให้กว้างขึ้น

### เอกสารของฉันมีข้อความสี—`RemoveBackground` จะทำให้สีหายไปหรือไม่?
`RemoveBackground` ทำงานบนความสว่าง (luminance) ดังนั้นข้อความสีจะถูกแปลงเป็นระดับสีเทาก่อนทำความสะอาด หากต้องการรักษาสีสำหรับการประมวลผลต่อไป ให้ข้ามขั้นตอนนี้และใช้การลดสัญญาณรบกวนอย่างเดียว

### จะจัดการกับ PDF หลายหน้าอย่างไร?
แปลงแต่ละหน้าของ PDF เป็นภาพ (เช่น ใช้ Aspose.PDF) แล้วส่งภาพแต่ละหน้าผ่านขั้นตอนเดียวกัน ทำลูป遍历หน้าต่าง ๆ และต่อข้อความจาก `ocrResult.Text` เข้าด้วยกัน

### สามารถปรับปรุงความแม่นยำสำหรับโน้ตมือเขียนได้หรือไม่?
ลองเปิดใช้งาน `ocrEngine.Options.UseNeuralNetwork = true;` (มีในเวอร์ชันใหม่ของ Aspose) และเพิ่มความละเอียดของภาพเป็นอย่างน้อย 300 dpi ก่อนทำการประมวลผล

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นไฟล์ซอร์สทั้งหมดพร้อมคำสั่ง `using` ที่จำเป็นและคอมเมนต์ ให้นำไปวางในโปรเจกต์คอนโซลใหม่แล้วกด **F5**

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับใบแจ้งหนี้ง่าย)

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ตรวจสอบให้แน่ใจว่าภาพต้นฉบับชัดเจนพอและมุมการแก้ไขการเอียงไม่เกินค่าขีดจำกัดที่คุณตั้งไว้

## สรุป

เราได้อธิบาย **วิธีแก้ไขการเอียงของภาพ** ทีละขั้นตอน แสดง **วิธีลบพื้นหลัง** สาธิต **วิธีสกัดข้อความ** ด้วยการเตรียมข้อมูลล่วงหน้า และสุดท้ายใช้ Aspose OCR เพื่อ **จดจำข้อความจากภาพ** ทั้งหมดอยู่ในโปรแกรม C# กะทัดรัดที่คุณสามารถต่อยอดเป็นการประมวลผลเป็นชุด, แปลง PDF, หรือรวมเข้าในระบบจัดการเอกสารขนาดใหญ่ได้

พร้อมรับความท้าทายต่อไปหรือยัง? ลองป้อนโฟลเดอร์ที่มี PDF สแกนเข้าไปในขั้นตอนนี้ หรือทดลองตั้งค่าการลดสัญญาณรบกวนต่าง ๆ เพื่อดูว่ามันส่งผลต่อคะแนนความเชื่อมั่นอย่างไร ยิ่งคุณเล่นกับพารามิเตอร์มากเท่าไหร่ คุณก็จะเข้าใจการแลกเปลี่ยนระหว่างความเร็วและความแม่นยำได้ดียิ่งขึ้น

มีคำถามหรือภาพที่ยังไม่ทำงาน? แสดงความคิดเห็นด้านล่าง แล้วเรามาช่วยกันแก้ไขกันเถอะ โค้ดดิ้งให้สนุกและขอให้ผลลัพธ์ OCR ของคุณใสเหมือนคริสตัลเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}