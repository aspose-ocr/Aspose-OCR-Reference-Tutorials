---
category: general
date: 2026-10-18
description: ทำ OCR บนภาพด้วย C# อย่างรวดเร็ว เรียนรู้การดึงข้อความจาก JPG แปลงภาพเป็นข้อความและอ่านข้อความจากภาพโดยใช้
  Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: th
lastmod: 2026-10-18
og_description: ทำ OCR บนภาพใน C# ด้วย Aspose.OCR บทเรียนนี้แสดงวิธีดึงข้อความจาก
  JPG แปลงภาพเป็นข้อความและอ่านข้อความจากภาพภายในไม่กี่นาที
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: ทำ OCR บนภาพด้วย C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: วิธีทำ OCR บนภาพใน C# ด้วย Aspose.OCR
url: /th/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนภาพใน C# ด้วย Aspose.OCR

หากคุณต้องการ **ทำ OCR บนภาพ** ในแอปพลิเคชัน .NET คู่มือนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และพร้อมใช้งาน คุณจะได้เห็นวิธี **โหลดภาพสำหรับ OCR**, การจดจำอักขระ Cyrillic, และ **ดึงข้อความจากไฟล์ JPG** โดยไม่ต้องเขียนโค้ดการประมวลผลภาพระดับต่ำใด ๆ

ในบทเรียนนี้คุณจะได้ทำสิ่งต่อไปนี้:

* ติดตั้งแพ็กเกจ NuGet ของ Aspose.OCR  
* โหลดไฟล์ภาพ (JPG, PNG, BMP ฯลฯ)  
* เรียกใช้เครื่องมือ OCR เพื่อ **แปลงภาพเป็นข้อความ**  
* **อ่านข้อความจากภาพ** แล้วแสดงผลในคอนโซล  

ขั้นตอนเหล่านี้ทำงานกับภาพที่เข้ากันได้กับ .NET ใด ๆ ดังนั้นคุณจึงสามารถปรับใช้กับ PDF, ใบเสร็จสแกน, หรือภาพหน้าจอได้เช่นกัน

## ข้อกำหนดเบื้องต้น

* .NET 6.0 SDK หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)  
* Visual Studio 2022 หรือโปรแกรมแก้ไข C# ที่คุณชื่นชอบ  
* การเชื่อมต่ออินเทอร์เน็ตสำหรับการรันครั้งแรก – Aspose.OCR จะดาวน์โหลดโมดูลภาษาซีริลิกโดยอัตโนมัติ  

> **เคล็ดลับ:** ควรอัปเดตแพ็กเกจ NuGet อย่างสม่ำเสมอ; เวอร์ชันใหม่ ๆ จะช่วยปรับปรุงความแม่นยำของการจดจำและเพิ่มชุดภาษาต่าง ๆ

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR

เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

แพ็กเกจนี้ประกอบด้วยคลาส `OcrEngine` ที่ใช้เพื่อ **ทำ OCR บนไฟล์ภาพ** หลังจากคำสั่งทำงานเสร็จแล้ว การอ้างอิงแพ็กเกจจะปรากฏในไฟล์ *.csproj* ของคุณ

## ขั้นตอนที่ 2: สร้างโครงสร้างโปรแกรมคอนโซล

สร้างโปรเจกต์คอนโซลใหม่หากคุณยังไม่มี:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

แทนที่ไฟล์ *Program.cs* ที่สร้างขึ้นอัตโนมัติด้วยโค้ดที่แสดงในส่วนต่อไป โครงสร้างนี้รวม `using` ที่จำเป็นและเมธอด `Main` ที่เป็นจุดเริ่มต้นของกระบวนการ OCR

## ขั้นตอนที่ 3: โหลดภาพสำหรับ OCR

บรรทัดโค้ดแรกที่ทำงาน **โหลดภาพ** ที่คุณต้องการวิเคราะห์ Aspose.OCR รองรับสตรีมใด ๆ ดังนั้นคุณจึงสามารถโหลดไฟล์จากดิสก์, URL เว็บ, หรือทรัพยากรฝังตัวได้

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*ทำไมจึงสำคัญ*: การใช้ `ImageStream.FromFile` จะทำให้การจัดการฟอร์แมตเป็นเรื่องอัตโนมัติ ทำให้เครื่องมือ OCR ได้รับบิตแมพที่สอดคล้องกันไม่ว่าประเภทไฟล์ต้นฉบับจะเป็นอะไร และสตรีมจะถูกปล่อยโดยอัตโนมัติด้วยคำสั่ง `using`

## ขั้นตอนที่ 4: เริ่มต้นเครื่องมือ OCR และกำหนดภาษา (ไม่บังคับ)

โดยค่าเริ่มต้น Aspose.OCR จะพยายามตรวจจับภาษาอัตโนมัติ สำหรับข้อความซีริลิกคุณสามารถระบุโมดูล `Language.Cyrillic` อย่างชัดเจน ซึ่งจะทำให้การดาวน์โหลดครั้งแรกเร็วขึ้น

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

หากคุณไม่กำหนดภาษาด้วยตนเอง เครื่องมือจะดาวน์โหลดโมดูลที่จำเป็นในครั้งแรกที่เรียก `Recognize` การดาวน์โหลดทำผ่าน HTTPS และจะถูกแคชไว้ในเครื่องสำหรับการรันครั้งต่อไป

## ขั้นตอนที่ 5: ทำ OCR และแปลงภาพเป็นข้อความ

ตอนนี้คุณจะ **ทำ OCR บนภาพ** จริง ๆ และรับสตริงข้อความธรรมดา เมธอด `Recognize` จะทำงานหนักทั้งหมด: การเตรียมข้อมูล, การวิเคราะห์โครงสร้าง, และการจำแนกอักขระ

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

ค่าที่คืนกลับมาใน `recognizedText` จะมีการขึ้นบรรทัดใหม่ตรงกับเลย์เอาต์ต้นฉบับ ทำให้ง่ายต่อการประมวลผลต่อหรือบันทึกลงฐานข้อมูล

## ขั้นตอนที่ 6: แสดงผลลัพธ์ – อ่านข้อความจากภาพ

สุดท้าย, **อ่านข้อความจากภาพ** โดยเขียนผลลัพธ์ไปที่คอนโซล ขั้นตอนนี้ช่วยยืนยันว่า OCR ทำงานสำเร็จและแสดงให้คุณเห็นว่ามีอะไรถูกดึงออกมาบ้าง

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

เมื่อคุณรันโปรแกรม (`dotnet run`) คุณควรเห็นผลลัพธ์คล้ายกับ:

```
=== OCR Result ===
Пример текста на кириллице
```

> **หมายเหตุ:** ผลลัพธ์ที่ได้จะขึ้นอยู่กับคุณภาพของไฟล์ JPG ต้นฉบับ ภาพที่คมชัดและความละเอียดสูงจะให้ผลลัพธ์ที่ดีที่สุด

## โค้ดเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน *Program.cs* แล้วรันได้โดยไม่ต้องแก้ไข (ยกเว้นเส้นทางของภาพ)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

การรันโปรแกรมจะแสดงอักขระที่ดึงออกมาที่คอนโซล แสดงให้เห็นว่าคุณได้ **ดึงข้อความจาก JPG** และ **แปลงภาพเป็นข้อความ** อย่างสำเร็จ

## การจัดการกับกรณีที่พบบ่อย

| Scenario | Adjustment |
|----------|------------|
| **Different language** | ตั้งค่า `engine.Language = Language.English;` หรือค่า enum ที่สนับสนุนอื่น |
| **Multi‑page PDF** | แปลงแต่ละหน้าเป็นภาพ (เช่น ใช้ `Aspose.PDF`) แล้วเรียกลูป OCR สำหรับแต่ละภาพ |
| **Large batch** | ห่อการเรียก OCR ด้วยลูป `Parallel.ForEach`; ใช้ตัวอย่าง `OcrEngine` เพียงตัวเดียวเพื่อประหยัดหน่วยความจำ |
| **Low‑resolution image** | ทำการพรี‑โปรเซสด้วย `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` เพื่อลดสัญญาณรบกวนก่อนการจดจำ |

การปรับเปลี่ยนเหล่านี้ทำให้คุณ **ดึงข้อความจาก JPG** ได้ไม่ว่าภาษา, ขนาด หรือคุณภาพของไฟล์จะเป็นเช่นใด

## เคล็ดลับด้านประสิทธิภาพ

* **แคชโมดูลภาษา** – การดาวน์โหลดครั้งแรกอาจใช้เวลาสักสองสามวินาที; การรันครั้งต่อมาจะทำได้ทันที |
* **ใช้ตัวอย่าง `OcrEngine` ซ้ำ** สำหรับหลายภาพเพื่อหลีกเลี่ยงค่าใช้จ่ายในการเริ่มต้นซ้ำ ๆ |
* **จำกัดขนาดภาพ** – ภาพที่มีขนาดใหญ่มากจะเพิ่มการใช้หน่วยความจำ ปรับขนาดให้กว้างไม่เกิน 2000 px ก่อนส่งให้เครื่องมือ

## สรุป

คุณได้เรียนรู้วิธี **ทำ OCR บนภาพ** ใน C# ด้วย Aspose.OCR แล้ว โดยการโหลดภาพ, ตั้งค่าเครื่องมือ, และเรียก `Recognize` คุณสามารถ **ดึงข้อความจาก JPG**, **แปลงภาพเป็นข้อความ**, และ **อ่านข้อความจากภาพ** ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด  

ต่อจากนี้คุณอาจสำรวจต่อไป:

* เก็บผลลัพธ์ OCR ลงในฐานข้อมูลเพื่อทำดัชนีค้นหา  
* ผสานกระบวนการนี้เข้ากับ Web API ที่รับอัปโหลดภาพ  
* ใช้โมดูลภาษาอื่น (Arabic, Hindi ฯลฯ) เพื่อขยายขอบเขตการใช้งานของแอปพลิเคชัน

อย่ากลัวที่จะทดลองกับรูปแบบภาพ, ภาษา, และกลยุทธ์การประมวลผลแบบชุดต่าง ๆ รูปแบบหลัก — **โหลดภาพสำหรับ OCR → จดจำ → จัดการผลลัพธ์ข้อความ** — ยังคงเหมือนเดิม ให้คุณมีพื้นฐานที่มั่นคงสำหรับโครงการดึงข้อความใด ๆ

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [ดึงข้อความจากภาพด้วย C# พร้อมเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [แปลงภาพเป็นข้อความ – ทำ OCR บนภาพจาก URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [วิธีดึงข้อความจากภาพโดยใช้ Aspose.OCR สำหรับ .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}