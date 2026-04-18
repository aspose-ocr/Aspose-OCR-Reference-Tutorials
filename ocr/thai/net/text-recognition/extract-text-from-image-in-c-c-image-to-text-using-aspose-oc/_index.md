---
category: general
date: 2026-04-17
description: ดึงข้อความจากรูปภาพด้วย Aspose OCR ใน C# เรียนรู้วิธีอ่านข้อความจาก PNG,
  แปลงรูปภาพเป็นข้อความ, และโหลดรูปภาพสำหรับ OCR ภายในไม่กี่นาที.
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: th
og_description: ดึงข้อความจากภาพด้วย Aspose OCR ใน C# บทเรียนนี้แสดงวิธีอ่านข้อความจาก
  PNG, แปลงภาพเป็นข้อความ, และโหลดภาพสำหรับ OCR อย่างมีประสิทธิภาพ.
og_title: สกัดข้อความจากภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- Image Processing
title: สกัดข้อความจากภาพใน C# – แปลงภาพเป็นข้อความด้วย Aspose OCR
url: /th/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพใน C# – คู่มือ Aspose OCR ฉบับสมบูรณ์

เคยต้องการ **สกัดข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารีใด? คุณไม่ได้เป็นคนเดียว นักพัฒนาจำนวนมากเจออุปสรรคนี้เมื่อมีภาพ PNG, ใบแจ้งหนี้ที่สแกน, หรือป้ายหลายภาษาและต้องการแปลงพิกเซลเป็นข้อความที่สามารถค้นหาได้  

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันแบบทำมือที่ทำให้คุณ **อ่านข้อความจาก PNG**, **แปลงรูปภาพเป็นข้อความ**, และ **โหลดรูปภาพสำหรับ OCR** ด้วย Aspose OCR—ทั้งหมดใน C# สมัยใหม่ที่สะอาดและทันสมัย เมื่อจบคุณจะได้โปรแกรมพร้อมรันที่สามารถใส่ลงในโครงการ .NET ใดก็ได้

## สิ่งที่คุณจะได้เรียนรู้

- วิธีโหลดไฟล์รูปภาพสำหรับ OCR (ขั้นตอน “โหลดรูปภาพสำหรับ OCR”)  
- วิธีกำหนดค่า Aspose OCR สำหรับกลุ่มภาษาที่ต้องการ  
- วิธีสกัดสตริงที่ได้รับการจดจำและแสดงผลในคอนโซล  
- เคล็ดลับการจัดการหลายภาษา, ไฟล์ขนาดใหญ่, และการจัดการหน่วยความจำ  

ไม่ต้องอ้างอิงเอกสารภายนอก; ทุกอย่างที่คุณต้องการอยู่ในโค้ดสแนปด้านล่าง

## ข้อกำหนดเบื้องต้น

- .NET 6+ SDK (หรือ .NET Core 3.1+ – API เหมือนกัน)  
- Visual Studio 2022, VS Code, หรือ IDE ที่คุณชอบ  
- แพ็กเกจ NuGet **Aspose.OCR** (ติดตั้งด้วย `dotnet add package Aspose.OCR`)  

ถ้าคุณมีทั้งหมดนี้แล้ว, ไปกันเลย

![Extract text from image using Aspose OCR in C#](https://example.com/aspsoe-ocr-demo.png "extract text from image using Aspose OCR")

## ขั้นตอนที่ 1 – โหลดรูปภาพสำหรับ OCR

สิ่งแรกที่ต้องทำคือให้เครื่อง OCR มีอะไรให้อ่าน Aspose OCR รองรับหลายรูปแบบ, แต่ PNG เป็นตัวเลือกทั่วไปสำหรับสกรีนช็อตและกราฟิกที่สแกน

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดรูปภาพอย่างถูกต้องทำให้เอนจินเห็นข้อมูลพิกเซลที่คุณคาดหวัง หากส่งสตรีมที่เสียหาย การจดจำจะล้มเหลวโดยไม่มีข้อความแจ้ง

## ขั้นตอนที่ 2 – สร้างและกำหนดค่า OCR Engine

ต่อไปให้สร้างอินสแตนซ์ของ `OcrEngine` คุณสามารถตั้งค่ากลุ่มภาษาเพิ่มเติมได้; สำหรับสคริปต์ตะวันตกส่วนใหญ่ค่าเริ่มต้นทำงานได้, แต่หากต้องจัดการกับ Cyrillic, Arabic, หรืออักษรเอเชีย คุณควรบอกเอนจินล่วงหน้า

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **เคล็ดลับระดับมืออาชีพ:** การตั้งค่าภาษาให้แคบลงจะทำให้เอนจินค้นหาชุดอักขระที่จำกัด, ซึ่งช่วยเร่งการจดจำและเพิ่มความแม่นยำ

## ขั้นตอนที่ 3 – ทำ OCR และสกัดข้อความ

ตอนนี้งานหนักเริ่มทำงานแล้ว เรียก `Recognize` พร้อมภาพที่โหลดไว้ก่อนหน้า, จากนั้นอ่านคุณสมบัติ `Text` จากผลลัพธ์

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### ผลลัพธ์ที่คาดหวัง

หาก `sample.png` มีข้อความ “Hello, World!” คุณจะเห็น:

```
=== OCR Output ===
Hello, World!
```

หากภาพซับซ้อนกว่า (เช่น ใบเสร็จหลายบรรทัด) เอนจินจะคงการขึ้นบรรทัด, ให้คุณได้บล็อกข้อความพร้อมประมวลผลต่อ

## ขั้นตอนที่ 4 – รวมทุกอย่างเป็นโปรแกรมสมบูรณ์

ด้านล่างเป็นแอปพลิเคชันคอนโซลแบบครบวงจรที่คุณสามารถคัดลอกและวางลงในโปรเจกต์ C# ใหม่ได้ มีการจัดการข้อผิดพลาดและคอมเมนต์อธิบายแต่ละส่วน

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

เรียกใช้โปรแกรม (`dotnet run` จากโฟลเดอร์โปรเจกต์) แล้วดูคอนโซลพิมพ์สตริงที่สกัดออกมา นั่นคือขั้นตอน **สกัดข้อความจากรูปภาพ** ทั้งหมดในโค้ดไม่ถึง 30 บรรทัด

## ขั้นตอนที่ 5 – รูปแบบทั่วไป & กรณีขอบ

### อ่านข้อความจาก PNG เทียบกับรูปแบบอื่น

แม้ว่าตัวอย่างจะใช้ PNG, Aspose OCR ยังรองรับ JPEG, BMP, TIFF, และ GIF เพียงเปลี่ยนนามสกุลไฟล์; การเรียก `OcrImage.FromFile` เดิมทำงานได้โดยไม่ต้องแก้ไข

### แปลงรูปภาพเป็นข้อความใน Web API

หากต้องการเปิดให้บริการฟังก์ชันนี้ผ่าน endpoint HTTP, คุณสามารถรับไฟล์อัปโหลด `IFormFile`, แปลงสตรีมเป็น `OcrImage` ด้วย `OcrImage.FromStream`, แล้วคืนสตริงเป็น JSON โลจิก OCR ยังคงเหมือนเดิม

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### จัดการรูปภาพขนาดใหญ่

รูปภาพความละเอียดสูงอาจใช้หน่วยความจำมาก วิธีที่เป็นประโยชน์คือย่อขนาดรูปก่อนส่งให้เอนจิน:

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### เอกสารหลายภาษา

หากเอกสารผสม English กับ Cyrillic ให้รวมแฟล็กภาษาต่าง ๆ:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

เอนจินจะพยายามจดจำอักขระจากทั้งสองชุด

### ปล่อยทรัพยากร

คำสั่ง `using` รอบ `OcrEngine` รับประกันว่าทรัพยากรเนทีฟจะถูกปล่อยออก หากลืมทำเช่นนี้อาจทำให้เกิดการรั่วของหน่วยความจำ, โดยเฉพาะในบริการที่ทำงานต่อเนื่อง

## เคล็ดลับระดับมืออาชีพสำหรับ OCR ที่เชื่อถือได้

- **ภาพที่คมชัดชนะ:** ทำการพรี‑โปรเซสภาพ (deskew, denoise) ด้วยไลบรารีเช่น **ImageSharp** ก่อน OCR  
- **ขนาดฟอนต์สำคัญ:** ข้อความที่เล็กกว่า 10 px มักพลาด; พิจารณาขยายภาพขึ้น  
- **ตรวจสอบ `ocrResult.Confidence`:** อ็อบเจกต์ `OcrResult` ยังให้คะแนนความเชื่อมั่นต่อคำ—ใช้เพื่อทำเครื่องหมายส่วนที่ความเชื่อมั่นต่ำเพื่อรีวิวด้วยมือ  
- **ประมวลผลเป็นชุด:** สำหรับหลายสิบไฟล์, ใช้ `OcrEngine` ตัวเดียวซ้ำหลายครั้งเพื่อหลีกเลี่ยงค่าใช้จ่ายการเริ่มต้นซ้ำ

## สรุป

คุณได้เรียนรู้วิธี **สกัดข้อความจากรูปภาพ** ใน C# ด้วย Aspose OCR, ครอบคลุมตั้งแต่ **โหลดรูปภาพสำหรับ OCR** ถึง **แปลงรูปภาพเป็นข้อความ** และ **อ่านข้อความจาก PNG** ตัวอย่างที่สมบูรณ์และรันได้แสดงโค้ดที่ต้องใช้, อธิบายเหตุผลของแต่ละขั้นตอน, และเสนอรูปแบบการใช้งานจริงหลายแบบ

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองนำสตริงที่สกัดไปใส่ในดัชนีการค้นหา, แปลด้วย Azure Cognitive Services, หรือสร้าง PDF ที่ค้นหาได้ด้วยเลเยอร์ข้อความเดียวกัน ความเป็นไปได้ไม่มีที่สิ้นสุด, และคุณมีพื้นฐานที่แข็งแกร่งสำหรับโครงการ **c# image to text** ใด ๆ

ทดลองปรับแต่ง, เปลี่ยนการตั้งค่าภาษา, หรือผสานสแนปนี้เข้ากับแอปพลิเคชันที่ใหญ่ขึ้น หากเจอปัญหาใด ๆ คอมเมนต์ด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}