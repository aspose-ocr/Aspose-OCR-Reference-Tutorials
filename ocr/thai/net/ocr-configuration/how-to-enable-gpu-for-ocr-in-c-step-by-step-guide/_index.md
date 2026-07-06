---
category: general
date: 2026-04-04
description: วิธีเปิดใช้งาน GPU ใน Aspose OCR อย่างรวดเร็ว เรียนรู้การดึงข้อความจากรูปภาพ
  โหลดรูปภาพสำหรับ OCR และจดจำข้อความด้วย C#
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: th
og_description: วิธีเปิดใช้งาน GPU ใน Aspose OCR อย่างรวดเร็ว ตามบทแนะนำนี้เพื่อดึงข้อความจากภาพ
  โหลดภาพสำหรับ OCR และจดจำข้อความด้วย C#
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# – คู่มือฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- GPU acceleration
title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR ใน C# – คู่มือเต็ม

เคยสงสัย **วิธีเปิดใช้งาน GPU** เมื่อใช้ Aspose OCR หรือไม่? บางทีคุณอาจเจอปัญหาประสิทธิภาพเมื่อต้องประมวลผลใบเสร็จหลายร้อยใบ และ CPU ไม่สามารถตามได้ ข่าวดีคือการเปิดใช้งานการเร่งความเร็วด้วย GPU ทำได้ง่ายมาก และเมื่อเปิดแล้วคุณจะเห็นว่าเครื่อง OCR ทำงานผ่านภาพได้อย่างรวดเร็ว

ในบทแนะนำนี้ เราจะไม่เพียงแค่เปิดสวิตช์ GPU เท่านั้น แต่ยังจะแสดงวิธี **โหลดภาพสำหรับ OCR**, **จดจำข้อความ**, และสุดท้าย **ดึงข้อความจากภาพ** ด้วยตัวอย่าง C# ที่เรียบง่าย เมื่อเสร็จคุณจะมีโปรแกรมพร้อมรันที่ดึงข้อความธรรมชาติจากรูปภาพที่รองรับใด ๆ — ไม่ต้องพึ่งบริการภายนอก

## สิ่งที่คุณต้องการ

- .NET 6+ (หรือ .NET Framework 4.7.2 ขึ้นไป)  
- Aspose.OCR for .NET เวอร์ชัน 24.2.0 หรือใหม่กว่า (ฟลัก GPU ถูกเพิ่มในรุ่นนี้)  
- เครื่องที่เปิดใช้งาน GPU พร้อมไดรเวอร์ที่เหมาะสม (NVIDIA CUDA 11+ ทำงานได้ดี)  
- ไฟล์ภาพที่คุณต้องการประมวลผล — เช่น ใบเสร็จสแกน, ใบแจ้งหนี้ที่ถ่ายภาพ, หรือบันทึกมือ

หากคุณมีทั้งหมดนี้แล้ว เยี่ยม—มาเริ่มกันเลย

## ขั้นตอนที่ 1: วิธีเปิดใช้งาน GPU – กำหนดค่า OCR Engine

สิ่งแรกที่คุณต้องทำคือบอก Aspose OCR ให้ใช้ GPU วิธีนี้ทำโดยการตั้งค่า property `UseGpu` บน instance ของ `OcrEngine` ค่าเริ่มต้นของ property นี้คือ `false` ดังนั้นเราต้องเปิดให้เป็น `true` อย่างชัดเจน

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**ทำไมเรื่องนี้ถึงสำคัญ:** เมื่อ `UseGpu` เป็น `true` ไลบรารีจะย้ายการคำนวณเมทริกซ์ที่หนักไปยัง GPU บน RTX 3060 ปานกลางคุณจะสังเกตเห็นว่าความหน่วงเวลาลดจากหลายวินาทีต่อภาพเหลือเพียงเศษวินาที

> **เคล็ดลับ:** หากคุณกำลังรันในสภาพแวดล้อม CI แบบไม่มีหน้าจอ (headless) ให้ตรวจสอบว่าได้ติดตั้งไดรเวอร์ GPU แล้วและบัญชีบริการมีสิทธิ์เข้าถึงอุปกรณ์ มิฉะนั้น engine จะกลับไปใช้โหมด CPU อย่างเงียบๆ

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR – ชี้ Engine ไปที่ไฟล์ของคุณ

ต่อไปเราต้อง **โหลดภาพสำหรับ OCR** Aspose OCR รองรับรูปแบบภาพใด ๆ ที่ System.Drawing รองรับ (PNG, JPEG, BMP, TIFF ฯลฯ) ตัวช่วย `ImageStream.FromFile` จะห่อไฟล์เป็นอ็อบเจ็กต์ stream ที่ต้องการ

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

หากคุณต้องการโหลดจาก `byte[]` (เช่นเมื่อภาพมาจากฐานข้อมูล) คุณสามารถใช้ `ImageStream.FromBytes(byteArray)` แทน — ผลลัพธ์เหมือนกัน เพียงแค่แหล่งที่มาต่างกัน

## ขั้นตอนที่ 3: วิธีจดจำข้อความ – รันกระบวนการ OCR

เมื่อ engine ถูกกำหนดค่าและโหลดภาพแล้ว ถึงเวลาที่จะ **จดจำข้อความ** เมธอด `Recognize` จะทำงานหนักทั้งหมดและคืนค่าอ็อบเจ็กต์ `OcrResult` ซึ่งบรรจุข้อความธรรมดา, คะแนนความมั่นใจ, และแม้กระทั่ง bounding box หากคุณต้องการใช้ในภายหลัง

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

คุณยังสามารถเปลี่ยนภาษาได้โดยตั้งค่า `ocrEngine.Language = OcrLanguage.French;` ก่อนเรียก `Recognize()` การเร่งความเร็วด้วย GPU ทำงานไม่ว่าจะใช้ language pack ใดก็ตาม

## ขั้นตอนที่ 4: วิธีดึงข้อความจากภาพ – แสดงผลลัพธ์

สุดท้ายเราจะ **ดึงข้อความจากภาพ** โดยอ่าน property `Text` ของอ็อบเจ็กต์ผลลัพธ์ สำหรับการสาธิตเราจะพิมพ์ออกที่ console เท่านั้น แต่คุณก็สามารถเขียนลงไฟล์, ฐานข้อมูล, หรือส่งต่อไปยังบริการอื่นได้

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**ผลลัพธ์ที่คาดหวัง** (ข้อความจริงของคุณจะต่างกันตามภาพ):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

หากคุณต้องการค่าความมั่นใจดิบ คุณสามารถวนลูป `ocrResult.Regions` และตรวจสอบ `Region.Confidence` ของแต่ละรายการ

## ตัวอย่างทำงานเต็มรูปแบบ – ไฟล์เดียวพร้อมรัน

ด้านล่างเป็นโปรแกรมเต็มรูปแบบ คัดลอกและวางลงในโปรเจกต์คอนโซลใหม่, รีสโตร์แพคเกจ NuGet ของ Aspose.OCR, แล้วกด **F5**

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **หมายเหตุ:** แทนที่ `YOUR_DIRECTORY/receipt.jpg` ด้วยพาธจริงของภาพของคุณ หากโปรแกรมโยน `FileNotFoundException` ให้ตรวจสอบพาธและสิทธิ์ไฟล์อีกครั้ง

## คำถามทั่วไป & กรณีขอบ

### ถ้า GPU ไม่ถูกตรวจพบจะทำอย่างไร?

Aspose OCR จะกลับไปใช้โหมด CPU โดยอัตโนมัติและบันทึกคำเตือน เพื่อยืนยันว่าโหมดใดกำลังทำงาน ให้ตรวจสอบ `ocrEngine.IsGpuEnabled` หลังจากสร้าง — มันจะคืนค่า `true` ก็ต่อเมื่อไดรเวอร์ GPU โหลดสำเร็จ

### ฉันสามารถประมวลผลหลายภาพในลูปได้หรือไม่?

ได้เลย เพียงย้ายบรรทัด `ocrEngine.Image = …` เข้าไปในลูป `foreach (var file in files)` ใช้ instance ของ `OcrEngine` เดียวกัน; การใช้ซ้ำจะลดภาระการจัดสรรทรัพยากร GPU ซ้ำ ๆ

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### ฉันจะจัดการกับภาษาที่ไม่ใช่ภาษาอังกฤษอย่างไร?

ตั้งค่าภาษาก่อนเรียก `Recognize()` :

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

การเร่งความเร็วด้วย GPU ทำงานเช่นเดียวกัน; เพียงแต่โมเดลภาษาเปลี่ยนไป

### จะทำอย่างไรกับภาพถ่ายขนาดใหญ่และความละเอียดสูง?

หากเจอข้อผิดพลาด out‑of‑memory ให้ลดขนาดภาพก่อน Aspose OCR มี `ImageHelper.Resize` — วิธีเร็ว ๆ ที่ลดขนาดโดยไม่สูญเสียรายละเอียดมาก

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## สรุป

เราได้อธิบาย **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR, แสดงวิธี **โหลดภาพสำหรับ OCR**, สาธิต **วิธีจดจำข้อความ**, และแสดง **วิธีดึงข้อความจากภาพ** ด้วยโปรแกรม C# ที่กระชับและพร้อมใช้งานในผลิตภัณฑ์ การสลับ flag `UseGpu` จะให้ความเร็วที่เห็นได้ชัด โดยเฉพาะเมื่อประมวลผลชุดของใบเสร็จ, ใบแจ้งหนี้, หรือสตรีมเอกสารปริมาณมาก

พร้อมก้าวต่อไปหรือยัง? ลองเชื่อมต่อ pipeline OCR นี้กับฐานข้อมูลเพื่อเก็บใบเสร็จที่ดึงออก, หรือส่งข้อความธรรมชาติไปยังโมเดลประมวลผลภาษาธรรมชาติสำหรับการจัดประเภทค่าใช้จ่าย คุณยังสามารถสำรวจคอลเลกชัน `OcrResult.Regions` เพื่อรับพิกัด bounding‑box และสร้าง UI ที่ไฮไลท์แต่ละคำบนรูปต้นฉบับ

ขอให้สนุกกับการเขียนโค้ด, และเพลิดเพลินกับพลังเพิ่มจากการเร่งความเร็วด้วย GPU ที่ช่วยงาน OCR ของคุณ!

---

![ภาพอธิบายการเปิดใช้งาน GPU](gpu-ocr-diagram.png "ภาพอธิบายการเปิดใช้งาน GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}