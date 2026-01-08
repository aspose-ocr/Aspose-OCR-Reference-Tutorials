---
category: general
date: 2026-01-07
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีจดจำข้อความจากรูปถ่าย
  ปรับปรุงความแม่นยำของ OCR โหลดภาพสำหรับ OCR และตั้งค่าภาษา OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR. คู่มือนี้แสดงวิธีการจดจำข้อความจากรูปภาพ,
  ปรับปรุงความแม่นยำของ OCR, โหลดภาพสำหรับ OCR และตั้งค่าภาษาของ OCR.
og_title: สกัดข้อความจากภาพด้วย Aspose OCR – คู่มือ C#
tags:
- Aspose OCR
- C#
- Image Processing
title: ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากภาพ – การทำงานเต็มรูปแบบด้วย C# และ Aspose OCR

เคยต้อง **ดึงข้อความจากภาพ** แต่ไม่แน่ใจว่าคลังใดจะให้ผลลัพธ์ที่เชื่อถือได้หรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายแอปพลิเคชันจริง—เช่น เครื่องสแกนใบเสร็จ, ตัวตรวจสอบบัตรประจำตัว, หรือแค่เครื่องมือจดบันทึกอย่างรวดเร็ว—การ **จดจำข้อความจากรูปถ่าย** เป็นฟีเจอร์ที่ต้องมี

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบที่แสดงให้คุณเห็นวิธี **โหลดภาพสำหรับ OCR**, ตั้งค่าเอนจินเพื่อ **กำหนดภาษาของ OCR**, และใช้เทคนิคการเตรียมข้อมูลล่วงหน้าเพื่อ **ปรับปรุงความแม่นยำของ OCR**. เมื่อเสร็จสิ้นคุณจะมีไฟล์ C# เดียวที่พิมพ์ข้อความที่ดึงออกมาในคอนโซล, และคุณจะเข้าใจว่าการตั้งค่าแต่ละอย่างสำคัญอย่างไร

> **เคล็ดลับ:** โค้ดนี้ทำงานกับ Aspose.OCR ≥ 23.5, .NET 6+ และสภาพแวดล้อม Windows, Linux หรือ macOS ใด ๆ ที่สามารถรัน .NET Core ได้

## สิ่งที่ต้องเตรียม

- .NET 6 SDK (หรือใหม่กว่า) ที่ติดตั้งไว้  
- Visual Studio 2022, VS Code, หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ  
- แพ็คเกจ NuGet `Aspose.OCR` (ติดตั้งด้วย `dotnet add package Aspose.OCR`)  
- ไฟล์ภาพ (JPEG/PNG) ที่มีข้อความพิมพ์หรือพิมพ์ด้วยเครื่องชัดเจน  

ถ้าคุณมีทั้งหมดนี้แล้ว, ไปต่อกันเลย

![extract text from image example](/images/ocr-example.png "extract text from image – Aspose OCR output")

## ขั้นตอนที่ 1: สร้างและทำลาย OCR Engine – “Extract Text from Image” Core

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของ `OcrEngine`. การห่อหุ้มด้วยบล็อก `using` จะรับประกันว่าทรัพยากรเนทีฟจะถูกทำลายอย่างถูกต้อง

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**ทำไมต้องทำเช่นนี้:** `OcrEngine` เก็บหน่วยความจำที่ไม่ได้จัดการสำหรับ DLL OCR เนทีฟ การทำลายมันทันทีช่วยป้องกันการรั่วของหน่วยความจำ, โดยเฉพาะเมื่อคุณประมวลผลภาพจำนวนมากเป็นชุด

## ขั้นตอนที่ 2: กำหนดการตั้งค่าการจดจำ – ปรับปรุงความแม่นยำของ OCR

ต่อไปเราจะสร้างอ็อบเจ็กต์ `RecognitionSettings`. ที่นี่เราจะ **กำหนดภาษาของ OCR** และเพิ่มฟิลเตอร์การเตรียมข้อมูลล่วงหน้าที่มักทำให้ผลลัพธ์จากข้อความที่บิดเบี้ยวกลายเป็นข้อความที่สะอาด

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**ทำไมต้องใช้ฟิลเตอร์เหล่านี้?**  
- **Deskew** แก้ปัญหาภาพที่ถ่ายด้วยโทรศัพท์แล้วเอียงไม่ตรงแกนหลายองศา  
- **Denoise** ลบจุดรบกวนที่อาจถูกตีความเป็นอักขระ  
- **ContrastEnhance** ทำให้หมึกอ่อนเด่นขึ้น, ซึ่งจำเป็นสำหรับ **การปรับปรุงความแม่นยำของ OCR**

## ขั้นตอนที่ 3: โหลดภาพ – โหลดภาพสำหรับ OCR อย่างมีประสิทธิภาพ

Aspose มีเมธอด `ImageStream.FromFile` สำหรับการโหลดอย่างรวดเร็ว คุณยังสามารถส่ง `MemoryStream` หากภาพมาจากคำขอเว็บหรือฐานข้อมูล

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**ข้อผิดพลาดทั่วไป:** การระบุพาธด้วยเครื่องหมายทับหน้า (`/`) บน Windows ทำงานได้, แต่การใช้ `Path.Combine` จะปลอดภัยกว่าในโครงการข้ามแพลตฟอร์ม

## ขั้นตอนที่ 4: ทำการจดจำ – Recognize Text from Photo

ต่อไปเราจะเรียก `Recognize`, ส่งสตรีมภาพและการตั้งค่าของเรา เมธอดจะคืนสตริงธรรมดาที่มีข้อความที่ดึงออกมา

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

หากภาพมีหลายบล็อกของข้อความ, Aspose จะต่อข้อความเหล่านั้นด้วยการขึ้นบรรทัดใหม่, พยายามรักษาเลย์เอาต์เดิมให้มากที่สุดเท่าที่ทำได้

## ขั้นตอนที่ 5: แสดงผลลัพธ์ – ตรวจสอบการดึงข้อมูล

สุดท้ายให้เขียนผลลัพธ์ไปยังคอนโซล ในแอปพลิเคชันจริงคุณอาจเก็บไว้ในฐานข้อมูล, ส่งไปยังบริการอื่น, หรือแสดงบน UI

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

หากคุณเห็นอักขระบิดเบี้ยว, ตรวจสอบว่าภาพชัดเจน, ภาษาตรงกับข้อความ, และฟิลเตอร์การเตรียมข้อมูลล่วงหน้าเหมาะสมหรือไม่

## ขั้นตอนที่ 6: ปรับแต่งเพิ่มเติม – ปรับให้เหมาะกับกรณีขอบ

### a. สลับภาษา

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. เพิ่มฟิลเตอร์กำหนดเอง

Aspose ยังมี `PreprocessFilter.Sharpen` หรือ `PreprocessFilter.Binarize`. ทดลองใช้เมื่อชุดฟิลเตอร์พื้นฐานสามตัวไม่พอ

### c. จัดการกับภาพขนาดใหญ่

สำหรับภาพความละเอียดสูงมาก, ควรลดขนาดก่อนเพื่อประหยัดหน่วยความจำ:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## คำถามที่พบบ่อย

**ถาม: สามารถใช้กับโน้ตที่เขียนด้วยมือได้หรือไม่?**  
ตอบ: Aspose OCR ถูกปรับให้ทำงานกับข้อความพิมพ์. การจดจำข้อความมือเขียนต้องใช้เอนจินอื่น (เช่น Aspose.OCR for Handwriting หรือโมเดลแมชชีนเลิร์นนิง)

**ถาม: สามารถประมวลผลหลายภาพในลูปได้หรือไม่?**  
ตอบ: ทำได้แน่นอน. เพียงย้ายบล็อก `using (var ocrEngine = new OcrEngine())` ไปอยู่นอกลูปและใช้เอนจินเดียวกันหลายครั้งเพื่อประสิทธิภาพที่ดีกว่า

**ถาม: ถ้าภาพเป็นหน้า PDF จะทำอย่างไร?**  
ตอบ: แปลงหน้า PDF เป็นภาพก่อน (Aspose.PDF สามารถเรนเดอร์หน้าเป็น PNG/JPEG), แล้วจึงส่งให้ OCR engine

## สรุป – สิ่งที่เราได้ทำ

- **ดึงข้อความจากภาพ** ด้วยโปรแกรม C# เดียวที่รวมทุกอย่างไว้  
- แสดงวิธี **จดจำข้อความจากรูปถ่าย** พร้อมการเตรียมข้อมูลล่วงหน้าที่ **ปรับปรุงความแม่นยำของ OCR**  
- แสดงวิธีที่ถูกต้องในการ **โหลดภาพสำหรับ OCR** และ **กำหนดภาษาของ OCR** สำหรับสถานการณ์หลายภาษา  

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

- **การประมวลผลเป็นชุด:** ผสานสคริปต์นี้กับ `Directory.GetFiles` เพื่อ OCR ทั้งโฟลเดอร์  
- **การประมวลผลหลังจากดึงข้อมูล:** ใช้ regular expressions ทำความสะอาดวันที่, จำนวนเงิน, หรือรหัสหลังการดึงข้อมูล  
- **การเชื่อมต่อ:** ส่งข้อความที่ดึงออกไปยัง Azure Cognitive Search หรือ Elastic เพื่อทำเอกสารให้ค้นหาได้  

ลองทดลองผสมฟิลเตอร์, ภาษา, และแหล่งภาพต่าง ๆ ได้ตามใจ. รูปแบบหลักยังคงเหมือนเดิม: สร้างเอนจิน, ตั้งค่าการจดจำ, โหลดภาพ, ทำการจดจำ, และแสดงผล. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}