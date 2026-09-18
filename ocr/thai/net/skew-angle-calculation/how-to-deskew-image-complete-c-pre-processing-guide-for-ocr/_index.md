---
category: general
date: 2026-01-13
description: วิธีแก้การเอียงของภาพและลบสัญญาณรบกวนของภาพใน C# – เรียนรู้การเพิ่มความคอนทราสต์ของภาพ,
  การเตรียมภาพสำหรับ OCR, และการใช้ตัวกรองภาพหลายแบบ
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: th
og_description: วิธีแก้ไขการเอียงของภาพและลบสัญญาณรบกวนของภาพใน C# – เรียนรู้การเพิ่มความคมชัดของภาพ,
  การเตรียมภาพสำหรับ OCR, และการใช้ฟิลเตอร์ภาพหลายประเภท
og_title: วิธีแก้ไขการเอียงของภาพ – คู่มือการเตรียมข้อมูล C# ฉบับสมบูรณ์สำหรับ OCR
tags:
- OCR
- C#
- Image Processing
title: วิธีแก้การเอียงของภาพ – คู่มือการเตรียมข้อมูล C# ครบสำหรับ OCR
url: /th/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือการเตรียมข้อมูลล่วงหน้าภาษา C# สำหรับ OCR อย่างครบถ้วน

เคยสงสัย **วิธีแก้ไขการเอียงของภาพ** ก่อนนำเข้าไปยังเครื่อง OCR หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์จริง—สัญญาที่สแกน, ใบเสร็จ, หรือสำเนาโบราณ—ข้อความมักจะเอียงเล็กน้อย, ภาพดูมีเม็ดสี, และคอนทราสต์กระจัดกระจาย ข่าวดีคือ? เพียงไม่กี่บรรทัดของโค้ด C# ก็สามารถทำให้ภาพตรง, กำจัดนอยส์, และเพิ่มคอนทราสต์ ทำให้ OCR ของคุณมีพื้นฐานที่มั่นคง

ในบทแนะนำนี้เราจะเดินผ่าน **ตัวอย่างที่สมบูรณ์และสามารถรันได้** ที่แสดงให้คุณเห็นอย่างชัดเจนว่า **วิธีแก้ไขการเอียงของภาพ** อย่างไร, **กำจัดนอยส์ของภาพ**, **เพิ่มคอนทราสต์ของภาพ**, แล้วจึงรัน OCR ด้วย Aspose.OCR. เมื่อจบคุณจะได้ pipeline ที่สามารถนำกลับมาใช้ใหม่ได้ซึ่งใช้ **หลายฟิลเตอร์ของภาพ** ในการเรียกเดียว—ไม่มีการคาดเดา

## สิ่งที่คุณต้องเตรียม

- **.NET 6+** (หรือเวอร์ชัน .NET ล่าสุด; API ทำงานเช่นเดียวกัน)
- **Aspose.OCR for .NET** NuGet package (`Aspose.OCR` และ `Aspose.OCR.Filters`)
- ตัวอย่างภาพสแกน (เช่น `skewed_noisy.png`) ที่มีการเอียง, นอยส์, และคอนทราสต์ต่ำ
- IDE ที่คุณชื่นชอบ (Visual Studio, Rider, VS Code—เลือกตามความสะดวก)

หากคุณมีโปรเจกต์ตั้งไว้แล้ว เพียงเพิ่มการอ้างอิง NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **เคล็ดลับ:** Aspose มีเวอร์ชันทดลองฟรีพร้อมจำนวนหน้าจำกัด—เหมาะสำหรับลองโค้ดด้านล่าง

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของ OCR Engine

สิ่งแรกที่เราทำคือสร้าง `OcrEngine`. คิดว่าเป็นสมองที่จะอ่านข้อความต่อไป ไม่มีอะไรซับซ้อน แต่เป็นหัวใจสำคัญของทุกอย่างที่ตามมา

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **ทำไมจึงสำคัญ:** การเริ่มต้น engine ครั้งเดียวและใช้ซ้ำสำหรับหลายภาพช่วยลดภาระการโหลดข้อมูลภาษาแบบซ้ำซ้อน

## ขั้นตอนที่ 2: โหลดภาพสแกนดิบจากดิสก์

ต่อไปเราจะดึงภาพจากดิสก์ เมธอด `OcrImage.FromFile` จะอ่านไฟล์เข้าสู่รูปแบบที่ Aspose สามารถจัดการได้

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **กรณีพิเศษ:** หากภาพของคุณอยู่ในรูปแบบที่ไม่เป็นมาตรฐาน (TIFF, BMP) Aspose ยังรองรับได้ แต่คุณอาจต้องแปลงเป็น PNG ก่อนเพื่อความสอดคล้อง

## ขั้นตอนที่ 3: สร้าง Pipeline การเตรียมข้อมูลล่วงหน้า (Deskew → Denoise → Contrast)

นี่คือจุดที่เราตอบคำถามหลัก **วิธีแก้ไขการเอียงของภาพ** พร้อมกับ **กำจัดนอยส์ของภาพ** และ **เพิ่มคอนทราสต์ของภาพ** API เชิง fluent ของ Aspose ให้เราสามารถเชื่อมต่อฟิลเตอร์ต่อกัน ทำให้โค้ดอ่านเหมือนประโยค

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### สิ่งที่แต่ละฟิลเตอร์ทำ

| ฟิลเตอร์ | วัตถุประสงค์ | ผลกระทบทั่วไป |
|----------|----------------|----------------|
| **DeskewFilter** | ค้นหามุมของบรรทัดข้อความและหมุนภาพให้เป็นแนวนอน | กำจัดการเอียงที่ทำให้ OCR สับสน, ลดอัตราความผิดพลาดประมาณ 30‑50 % |
| **DenoiseFilter** | ใช้อัลกอริทึมการทำให้เรียบที่รักษาขอบภาพไว้ขณะกำจัดนอยส์แบบสุ่ม | ทำความสะอาดใบเสร็จสแกนหรือภาพที่ถ่ายในแสงน้อย, ทำให้ตัวอักษรชัดเจนขึ้น |
| **ContrastFilter** | ขยายฮิสโตแกรมให้ส่วนมืดเข้มขึ้นและส่วนสว่างสว่างขึ้น | ปรับความแตกต่างระหว่างข้อความและพื้นหลัง, มีประโยชน์อย่างยิ่งกับเอกสารที่ซีด |

> **ทำไมต้องเชื่อมต่อกัน?** การทำ Deskew ก่อนทำให้ Denoise ทำงานบนภาพที่มีการจัดแนวถูกต้อง; การเพิ่มคอนทราสต์เป็นขั้นตอนสุดท้ายทำให้ข้อความที่ทำความสะอาดแล้วโดดเด่นต่อ OCR engine

## ขั้นตอนที่ 4: ทำ OCR บนภาพที่ผ่านการประมวลผลแล้ว

เมื่อภาพตรง, สะอาด, และคอนทราสต์สูงแล้ว เราจะส่งต่อให้ OCR engine เราจะใช้ข้อมูลภาษาอังกฤษ, แต่ Aspose รองรับกว่า 150 ภาษา

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

หากต้องการใช้ภาษาอื่น เพียงเปลี่ยน `OcrLanguage.English` เป็นค่า enum ที่เหมาะสม (เช่น `OcrLanguage.Spanish`)

## ขั้นตอนที่ 5: แสดงข้อความที่ได้รับการจดจำ

สุดท้าย เราจะพิมพ์ผลลัพธ์ลงคอนโซล ในแอปพลิเคชันจริงคุณอาจบันทึกลงไฟล์, ฐานข้อมูล, หรือส่งต่อข้อความไปยัง pipeline NLP ต่อไป

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมเต็มรูปแบบกับใบเสร็จที่เอียงทั่วไปจะให้ผลลัพธ์ประมาณนี้:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ให้ตรวจสอบภาพต้นฉบับ—การเบลอมากเกินไปหรือความมืดสุดขีดอาจต้องการการเตรียมเช่น `SharpenFilter`)

![ตัวอย่างการแก้ไขการเอียงของภาพ](images/deskewed_example.png "วิธีแก้ไขการเอียงของภาพ – ก่อนและหลังการประมวลผล")

*ภาพด้านบนแสดงสแกนที่เอียงอยู่ด้านซ้ายและเวอร์ชันที่ถูกแก้ไข, กำจัดนอยส์, และเพิ่มคอนทราสต์ด้านขวา*

## เคล็ดลับเพิ่มเติม & ข้อผิดพลาดทั่วไป

### 1. เมื่อมุมการเอียงมากเกินไป

หากเอกสารถูกเอียงมากกว่า 30°, `DeskewFilter` อาจทำงานได้ยาก ในกรณีนั้นให้หมุนภาพด้วยตนเองก่อน:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. การจัดการภาพสี

ฟิลเตอร์ทำงานบนภาพระดับสีเทาภายใน, แต่คุณสามารถบังคับให้แปลงเป็นสีเทาได้:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. ปรับความแรงของ Denoise

`DenoiseFilter` รับพารามิเตอร์ `strength` แบบเลือก (0‑100). ค่าที่สูงกว่าจะกำจัดนอยส์มากขึ้นแต่ก็อาจทำให้รายละเอียดบางอย่างเบลอ

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. การใช้หลายฟิลเตอร์ของภาพนอกเหนือจากพื้นฐาน

Aspose มีฟิลเตอร์เพิ่มเติมมากมาย: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter` เป็นต้น คุณสามารถผสมและจับคู่เพื่อสร้าง pipeline ที่เหมาะกับประเภทเอกสารของคุณ

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดที่พร้อมใส่ลงในโปรเจกต์คอนโซล

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

รันโปรแกรมด้วย `dotnet run`. หากทุกอย่างตั้งค่าเรียบร้อย คอนโซลจะแสดงข้อความที่สะอาดและอ่านง่ายจากภาพที่เคยเอียงและมีนอยส์เดิมของคุณ

## สรุป

เราได้อธิบาย **วิธีแก้ไขการเอียงของภาพ** ด้วย C# พร้อมกับ **กำจัดนอยส์ของภาพ**, **เพิ่มคอนทราสต์ของภาพ**, และ **เตรียมภาพสำหรับ OCR** ด้วยการเชื่อมต่อ **หลายฟิลเตอร์ของภาพ** จุดสำคัญคือ pipeline การเตรียมข้อมูลที่จัดลำดับอย่างเหมาะสมสามารถเพิ่มความแม่นยำของ OCR อย่างมหาศาล—มักเปลี่ยนสแกนที่อ่านยากให้เป็นข้อความที่ชัดเจน

พร้อมก้าวต่อไปหรือยัง? ลองเปลี่ยน `ContrastFilter` เป็น `BinarizeFilter` เพื่อดูว่าการแปลงเป็นสีขาว‑ดำส่งผลอย่างไร, หรือทดลองใช้ `ResizeFilter` เพื่อป้อนภาพความละเอียดสูงเข้าสู่ engine. รูปแบบเดียวกันใช้ได้กับฟิลเตอร์ใดก็ได้, ดังนั้นคุณจึงมีพื้นฐานที่ยืดหยุ่นสำหรับโครงการ OCR ทั้งหมดในอนาคต

มีคำถามเกี่ยวกับการจัดการ PDF, OCR หลายภาษา, หรือการรวมเข้ากับ ASP.NET API? แสดงความคิดเห็นด้านล่างและขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}