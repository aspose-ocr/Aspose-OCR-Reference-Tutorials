---
category: general
date: 2026-06-19
description: 'จดจำข้อความจากภาพโดยใช้ Aspose OCR ใน C#: คู่มือขั้นตอนต่อขั้นตอนในการแปลงภาพเป็นข้อความและดึงข้อความจากไฟล์
  JPG.'
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: th
og_description: จดจำข้อความจากภาพด้วย Aspose OCR ใน C# เรียนรู้วิธีตั้งค่าภาษา OCR,
  ดึงข้อความจากไฟล์ JPG, และแปลงภาพเป็นข้อความภายในไม่กี่นาที.
og_title: จดจำข้อความจากภาพใน C# – แปลงภาพเป็นข้อความ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: แยกข้อความจากภาพใน C# – แปลงภาพเป็นข้อความ
url: /th/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพใน C# – แปลงรูปภาพเป็นข้อความ

เคยต้องการ **จดจำข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าห้องสมุดใดจะทำได้โดยไม่ต้องเสียค่าลิขสิทธิ์สูงหรือไม่? คุณไม่ได้เป็นคนเดียว ในบทแนะนำนี้เราจะพาคุณผ่านการใช้โหมด Community ฟรีของ Aspose OCR เพื่อ **แปลงรูปภาพเป็นข้อความ**, ดึงข้อความจากไฟล์ jpg, และแม้กระทั่ง **ตั้งค่าภาษา OCR** สำหรับสถานการณ์หลายภาษา

เราจะครอบคลุมทุกอย่างตั้งแต่การติดตั้งแพ็กเกจ NuGet ไปจนถึงการจัดการกรณีขอบเช่น PDF หลายหน้า หรือรูปภาพความละเอียดต่ำ สุดท้ายคุณจะได้แอปคอนโซลที่สามารถ **ทำ OCR บนไฟล์รูปภาพ** ได้ในพริบตา

## สิ่งที่คุณต้องเตรียม

- .NET 6 SDK หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core 3.1+ ด้วย)  
- Visual Studio 2022 หรือโปรแกรมแก้ไขที่คุณชอบ  
- ไฟล์รูปภาพ (JPG, PNG, BMP…) ที่มีข้อความที่อ่านได้  
- การเชื่อมต่ออินเทอร์เน็ตเพื่อดึงแพ็กเกจ `Aspose.OCR` NuGet  

เท่านี้—ไม่มี DLL เพิ่มเติม ไม่มีบริการภายนอก เพียงแค่ C# แท้ๆ

![ตัวอย่างการจดจำข้อความจากรูปภาพ](https://example.com/ocr-screenshot.png "ตัวอย่างการจดจำข้อความจากรูปภาพ")

*(ภาพหน้าจอแสดงผลลัพธ์คอนโซลหลังจากจดจำ JPG ตัวอย่าง)*

## ขั้นตอน 1: ติดตั้ง Aspose  OCR ผ่าน NuGet

ก่อนอื่นให้เพิ่มไลบรารี Aspose  OCR ไปยังโปรเจกต์ของคุณ เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์และรัน:

```bash
dotnet add package Aspose.OCR
```

แพ็กเกจมาพร้อมกับ **โหมด Community** ที่จำกัดการประมวลผลที่ 100 หน้าต่อการรันหนึ่งครั้ง ซึ่งเหมาะสำหรับการทดลองขนาดเล็ก หากคุณต้องการขีดจำกัดที่สูงขึ้นในภายหลัง สามารถอัปเกรดเป็นไลเซนส์แบบชำระเงินได้โดยไม่ต้องแก้โค้ด

## ขั้นตอน 2: กำหนดค่า OCR Engine (ตั้งค่าภาษา OCR)

ก่อนที่คุณจะ **ทำ OCR บนรูปภาพ** คุณต้องบอกเครื่องมือว่าคาดหวังภาษาที่ใด ค่าเริ่มต้นคืออังกฤษ แต่คุณสามารถสลับเป็นสเปน, ฝรั่งเศส หรือแม้กระทั่งจีนได้ด้วยบรรทัดเดียว

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

ทำไมภาษาถึงสำคัญ? โมเดล OCR ถูกฝึกบนชุดอักขระ; การป้อนเอกสารภาษาฝรั่งเศสให้โมเดลอังกฤษจะทำให้พลาดสำเนียงและลิการ์ การตั้งค่าภาษาให้ถูกต้องจะเพิ่มความแม่นยำอย่างมาก

## ขั้นตอน 3: สร้าง OCR Engine และจดจำรูปภาพ

เมื่อกำหนดค่าพร้อมแล้ว ให้สร้างอินสแตนซ์ของ engine ภายในบล็อก `using` เพื่อให้ทรัพยากรถูกปล่อยอัตโนมัติ จากนั้นเรียก `RecognizeImage` พร้อมพาธไปยัง JPG ของคุณ (หรือรูปแบบที่รองรับใดก็ได้)

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

ข้อควรระวังบางประการ:

- **Thread‑safety:** อินสแตนซ์ `OcrEngine` ไม่ปลอดภัยต่อการทำงานหลายเธรด หากคุณวางแผนจะประมวลผลรูปภาพหลายรูปพร้อมกัน ให้สร้าง engine แยกสำหรับแต่ละเธรด
- **Supported formats:** นอกจาก JPG คุณยังสามารถป้อน PNG, BMP, TIFF, และแม้กระทั่ง PDF วิธีเดียวกันทำงานได้ ดังนั้นคุณสามารถ **ดึงข้อความจาก jpg** หรือรูปภาพราสเตอร์อื่นใดได้เช่นกัน

## ขั้นตอน 4: แสดงข้อความที่จดจำได้ (แปลงรูปภาพเป็นข้อความ)

ตอนนี้ OCR engine ทำงานเสร็จแล้ว ผลลัพธ์จะถูกเก็บไว้ในอ็อบเจ็กต์ `OcrResult` คุณสมบัติ `Text` ของมันจะมีข้อความแบบ plain‑text ของทุกอย่างที่ engine สามารถอ่านได้

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

หากคุณรันโปรแกรมด้วยภาพสกรีนช็อตของใบเสร็จที่ชัดเจน คุณจะเห็นผลลัพธ์ประมาณนี้:

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

นี่คือสาระสำคัญของ **แปลงรูปภาพเป็นข้อความ**—รูปภาพกลายเป็นสตริงที่คุณสามารถเก็บ, ค้นหา หรือส่งต่อให้ระบบอื่นได้

## ขั้นตอน 5: จัดการกับกรณีขอบทั่วไป

### 5.1 รูปภาพความละเอียดต่ำ

ความแม่นยำของ OCR ลดลงอย่างรวดเร็วเมื่อต่ำกว่า 100 dpi หากคุณพบผลลัพธ์เป็นอักขระผสมกัน ให้ลองทำการประมวลผลล่วงหน้ากับรูปภาพ (เพิ่มคอนทราสต์, ปรับขนาด, หรือใช้ฟิลเตอร์ทำให้คม) ก่อนส่งให้ Aspose OCR

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 เอกสารหลายหน้า

แม้ว่าโหมด Community จะจำกัดที่ 100 หน้า คุณก็ยังสามารถประมวลผล PDF หรือ TIFF หลายหน้าได้ Engine จะคืนข้อความต่อเนื่องโดยคงการแบ่งหน้าไว้ด้วย `\f`

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 ภาษาไม่ใช่ภาษาอังกฤษ

สลับค่า enum `Language` ไปเป็นค่าที่รองรับอื่น:

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

อย่าลืมติดตั้งแพ็กเกจภาษาที่เหมาะสมหากคุณต้องการใช้ภาษานอกชุดเริ่มต้น; Aspose มีให้เป็นแพ็กเกจ NuGet แยกต่างหาก

## ขั้นตอน 6: ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือแอปคอนโซลพร้อมคัดลอก‑วางที่ **จดจำข้อความจากรูปภาพ**, **ดึงข้อความจาก jpg**, และ **ตั้งค่าภาษา OCR** ตามที่ต้องการ

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความ “Hello World!”):

```
=== OCR Output ===
Hello World!
```

รันโปรแกรมด้วย `dotnet run` แล้วคุณจะเห็นคอนโซลแสดงสตริงที่ดึงออกมา

## เคล็ดลับมืออาชีพ & ข้อผิดพลาดทั่วไป

- **เคล็ดลับมืออาชีพ:** ห่อการเรียก OCR ด้วยบล็อก `try/catch` เพื่อจัดการไฟล์เสียหายอย่างราบรื่น  
- **ระวัง:** รูปภาพที่มีลายน้ำหรือสัญญาณรบกวนพื้นหลังมาก; สิ่งเหล่านี้มักทำให้ engine สับสน  
- **คำแนะนำ:** หากต้องประมวลผลไฟล์หลายไฟล์ ให้วนลูปผ่านรายการในไดเรกทอรีและใช้ `OcrEngine` ตัวเดียวกัน—แค่จำไว้ว่าต้องรีเซ็ตการตั้งค่าต่อภาพทุกครั้ง  
- **จำไว้:** ขีดจำกัด 100 หน้าในโหมด Community เป็นต่อการรันหนึ่งครั้ง ไม่ใช่ต่อไฟล์ แบ่ง PDF ขนาดใหญ่ออกหากถึงขีดจำกัด

## สรุป

ตอนนี้คุณมีโค้ดสแนปช็อตที่พร้อมใช้งานในระดับผลิตภัณฑ์ที่ **จดจำข้อความจากรูปภาพ** ด้วย Aspose OCR ใน C# ตั้งแต่การติดตั้งแพ็กเกจ NuGet ไปจนถึง **ตั้งค่าภาษา OCR**, การจัดการรูปภาพความละเอียดต่ำ, และสุดท้าย **แปลงรูปภาพเป็นข้อความ** ทุกขั้นตอนถูกครอบคลุมแล้ว อย่ากลัวจะทดลอง—เปลี่ยนภาษา, ป้อน PNG, หรือเชื่อมต่อผลลัพธ์เข้ากับดัชนีการค้นหา

ต่อไปคุณอาจสำรวจ **ดึงข้อความจาก jpg** ในระดับใหญ่โดยผสานโค้ดนี้เข้าไปใน Azure Function หรือเจาะลึกคุณลักษณะขั้นสูงของ Aspose OCR เช่น การวิเคราะห์เลย์เอาต์และการจดจำลายมือ ความเป็นไปได้ไม่มีที่สิ้นสุด และพื้นฐานที่คุณสร้างวันนี้จะทำให้การต่อยอดเป็นเรื่องง่าย

ขอให้เขียนโค้ดสนุกและภาพของคุณอ่านออกได้เสมอ!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบทางเลือกในโปรเจกต์ของคุณเอง

- [ดึงข้อความจากรูปภาพ C# พร้อมการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [จดจำข้อความจากรูปภาพด้วย Aspose OCR สำหรับหลายภาษา](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [ดึงข้อความจากรูปภาพ – การเพิ่มประสิทธิภาพ OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}