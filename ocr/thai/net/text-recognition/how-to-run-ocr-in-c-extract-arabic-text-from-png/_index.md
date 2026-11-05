---
category: general
date: 2026-01-10
description: วิธีรัน OCR อย่างรวดเร็วและดึงข้อความภาษาอาหรับจากภาพ เรียนรู้การแปลงภาพเป็นข้อความ
  อ่านข้อความจาก PNG และดูวิธีดึงข้อความด้วย Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: th
og_description: วิธีรัน OCR ใน C# และดึงข้อความภาษาอาหรับจากภาพ PNG คู่มือนี้จะแสดงวิธีแปลงภาพเป็นข้อความและอ่านข้อความจาก
  PNG ทีละขั้นตอน
og_title: วิธีรัน OCR ใน C# – แยกข้อความอารบิกจากไฟล์ PNG
tags:
- OCR
- C#
- Aspose
title: วิธีใช้ OCR ใน C# – แยกข้อความภาษาอาหรับจากไฟล์ PNG
url: /th/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการรัน OCR ใน C# – ดึงข้อความภาษาอาหรับจาก PNG

เคยสงสัยไหมว่า **how to run OCR** บนรูปภาพที่มีอักขระภาษาอาหรับ? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาจำนวนมากเจออุปสรรคเมื่อพวกเขาต้อง **extract Arabic text** จาก PNG แต่ไม่รู้ว่าคลังไหนจะจัดการสคริปต์จากขวาไปซ้ายได้โดยไม่มีปัญหา.  

ในบทแนะนำนี้ เราจะพาคุณผ่านทุกอย่างที่คุณต้องรู้เพื่อ **convert image to text**, **read text from PNG**, และสุดท้าย **how to extract text** ด้วย Aspose.OCR ในแอปคอนโซล C# ที่สะอาดตา เมื่อเสร็จคุณจะมีโปรแกรมพร้อมรันที่พิมพ์สตริงภาษาอาหรับตรงไปยังเทอร์มินัลของคุณ.

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งและอ้างอิงแพคเกจ NuGet ของ Aspose.OCR.  
- กำหนดค่า OCR engine เพื่อรองรับภาษาอาหรับ.  
- โหลดภาพ PNG และรันกระบวนการจดจำ.  
- ดึงและแสดงข้อความที่ถูกดึงออกมา.  
- ปรับแต่งการตั้งค่าเพื่อความแม่นยำที่ดียิ่งขึ้นและจัดการกับข้อผิดพลาดทั่วไป.

ไม่จำเป็นต้องมีประสบการณ์กับ OCR มาก่อน เพียงแค่ความเข้าใจพื้นฐานของ C# และสภาพแวดล้อมการพัฒนา .NET (Visual Studio, Rider หรือ `dotnet` CLI ก็เพียงพอ).

---

## วิธีการรัน OCR – การตั้งค่า Aspose OCR

### ขั้นตอนที่ 1: เพิ่มแพคเกจ NuGet ของ Aspose.OCR

สิ่งแรกที่เราต้องการคือไลบรารี OCR เอง Aspose.OCR เป็นผลิตภัณฑ์เชิงพาณิชย์ แต่มีรุ่นทดลองฟรีที่ทำงานได้อย่างสมบูรณ์สำหรับการเรียนรู้.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

หรืออีกวิธีหนึ่ง เปิด **NuGet Package Manager** ใน Visual Studio ค้นหา **Aspose.OCR** แล้วคลิก **Install**.

> **Pro tip:** หากคุณวางแผนใช้ไลบรารีใน CI pipeline ให้เพิ่มแฟล็ก `-v` เพื่อล็อกเวอร์ชัน เช่น `dotnet add package Aspose.OCR -v 23.10`.

### ขั้นตอนที่ 2: สร้างโปรเจกต์คอนโซลใหม่ (หากคุณยังไม่มี)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

ตอนนี้คุณมีไฟล์ `Program.cs` ใหม่พร้อมสำหรับโค้ดของเรา.

---

## ดึงข้อความภาษาอาหรับ – เขียนโค้ด OCR

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรัน บันทึกเป็น `Program.cs` (หรือแทนที่ไฟล์ที่สร้างอัตโนมัติ).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### ทำไมแต่ละบรรทัดถึงสำคัญ

- **`OcrEngine`**: คลาสหลักที่ประสานการโหลดภาพ, การเลือกภาษา, และการจดจำ.  
- **`Language = OcrLanguage.Arabic`**: ภาษาอาหรับใช้สคริปต์จากขวาไปซ้ายและมี glyph เฉพาะ; การตั้งค่าภาษาแจ้งให้ engine ใช้โมเดลอักขระที่ถูกต้อง.  
- **`ImageStream.FromFile`**: รองรับ PNG, JPEG, BMP, และรูปแบบอื่น ๆ มากมาย หากคุณต้องการอ่านจาก `MemoryStream` (เช่นไฟล์ที่อัปโหลด) ให้แทนที่การเรียกนี้ตามความต้องการ.  
- **`Recognize()`**: ทำงานหนัก—วิเคราะห์พิกเซล, แบ่งส่วน, และจำแนกอักขระ.  
- **`ocrEngine.Text`**: สตริง Unicode สุดท้าย พร้อมสำหรับการประมวลผลต่อ, การจัดเก็บ, หรือการแสดงผล.

### ผลลัพธ์ที่คาดหวัง

หาก `arabic_sample.png` มีวลี “مرحبا بالعالم” (Hello World) คอนโซลจะพิมพ์:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ตรวจสอบให้แน่ใจว่าภาพชัดเจน, ภาษาได้ตั้งเป็น Arabic, และเวอร์ชันของ OCR engine ตรงกับเอกสาร.

---

## แปลงภาพเป็นข้อความ – ปรับความแม่นยำ

แม้การตั้งค่าเริ่มต้นจะทำงานได้กับการสแกนที่สะอาดส่วนใหญ่ แต่ภาพในโลกจริงมักต้องการการปรับแต่งเพิ่มเติม.

| การตั้งค่า | ทำอะไร | เมื่อใช้ |
|-----------|--------|----------|
| `ocrEngine.Config.Preprocess = true` | เปิดใช้งานการทำไบนารีอัตโนมัติและการกำจัดสัญญาณรบกวน. | เอกสารสแกนที่มีเงา. |
| `ocrEngine.Config.Deskew = true` | หมุนภาพเพื่อแก้ไขการเอียงเล็กน้อย. | ภาพถ่ายที่ถ่ายมุมเอียง. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | ถือภาพทั้งหมดเป็นบล็อกข้อความหนึ่งบล็อก. | คำบรรยายง่ายหรือป้ายข้อความบรรทัดเดียว. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | จำกัดการจดจำเฉพาะอักขระภาษาอาหรับเท่านั้น. | ลดผลบวกเท็จในหน้าที่มีหลายภาษา. |

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## อ่านข้อความจาก PNG – จัดการแหล่งภาพที่แตกต่าง

บางครั้ง PNG อยู่ในฐานข้อมูลหรือมาจากคำขอเว็บ นี่คือตัวอย่างย่อยที่อ่านจาก `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

ส่วนที่เหลือของกระบวนการยังคงเหมือนเดิม ซึ่งหมายความว่า **how to extract text** จะสอดคล้องกันไม่ว่าที่มาของภาพจะเป็นอะไร.

---

## วิธีการดึงข้อความ – ตัวเลือกขั้นสูงและกรณีขอบ

### 1. PDF หรือ TIFF หลายหน้า

หากคุณต้องการ OCR เอกสารหลายหน้า ให้วนลูปผ่านแต่ละหน้า:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Note:** คุณจะต้องใช้แพคเกจ `Aspose.PDF` สำหรับโค้ดส่วนนั้น.

### 2. ตรวจจับภาษาอัตโนมัติ

Aspose.OCR ยังมีฟีเจอร์ตรวจจับอัตโนมัติ แต่ช้ากว่า หากคุณไม่แน่ใจว่าภาพมีภาษาอาหรับหรือสคริปต์อื่น ให้เปิดใช้งาน:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. เคล็ดลับด้านประสิทธิภาพ

- **Reuse the `OcrEngine`** object สำหรับหลายภาพ; การสร้างอินสแตนซ์ใหม่ทุกครั้งเพิ่มภาระ.  
- **Run in parallel** เฉพาะเมื่อคุณมีอินสแตนซ์ engine แยกตามเธรด—การแชร์อินสแตนซ์เดียวทำให้เกิด race conditions.

---

## สรุป

เราได้ครอบคลุม **how to run OCR** ใน C# ตั้งแต่ต้นจนจบ แสดงให้คุณเห็นวิธี **extract Arabic text**, **convert image to text**, **read text from PNG**, และตอบ **how to extract text** ในหลายสถานการณ์ โค้ดตัวอย่างสมบูรณ์ มีความเป็นอิสระ และพร้อมให้คุณวางลงในโปรเจกต์คอนโซล .NET ใดก็ได้.

ขั้นตอนต่อไป? ลองเปลี่ยน `OcrLanguage.Arabic` เป็น Korean หรือ Serbian Cyrillic เพื่อดูพลังหลายภาษาของไลบรารี ทดลองใช้แฟล็ก preprocessing เพื่อเพิ่มความแม่นยำบนสแกนที่มีสัญญาณรบกวน หรือรวมฟังก์ชัน OCR เข้าไปในเว็บ API เพื่อให้ผู้ใช้อัปโหลดภาพและรับผลลัพธ์ข้อความทันที.

ขอให้เขียนโค้ดอย่างสนุกสนาน และผลลัพธ์ OCR ของคุณเป็นใสเหมือนคริสตัลเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}