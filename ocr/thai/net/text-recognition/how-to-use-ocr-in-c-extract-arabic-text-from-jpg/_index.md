---
category: general
date: 2026-03-21
description: วิธีใช้ OCR ใน C# เพื่อจดจำข้อความจากไฟล์รูปภาพ เรียนรู้การดึงข้อความภาษาอาหรับจากไฟล์
  JPG และแปลงเป็นข้อความธรรมดา
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อจดจำข้อความจากไฟล์รูปภาพ คู่มือนี้แสดงวิธีดึงข้อความภาษาอาหรับจากไฟล์
  JPG และแปลงเป็นข้อความที่แก้ไขได้
og_title: วิธีใช้ OCR ใน C# – ดึงข้อความอาหรับจากไฟล์ JPG
tags:
- OCR
- C#
- Aspose
- Arabic
title: วิธีใช้ OCR ใน C# – แยกข้อความภาษาอาหรับจากไฟล์ JPG
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – แยกข้อความอาหรับจาก JPG

เคยสงสัย **วิธีใช้ OCR** เมื่อคุณมีรูปภาพของข้อความอาหรับอยู่บนฮาร์ดไดรฟ์ของคุณหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอเรื่องนี้ นักพัฒนาหลายคนเจออุปสรรคเดียวกัน: พวกเขามีไฟล์ JPEG, ต้องการดึงคำภายใน, และไม่ต้องการเขียนโค้ดเครือข่ายประสาทเทียมตั้งแต่ต้น  

ข่าวดีคืออะไร? ด้วยไม่กี่บรรทัดของ C# คุณสามารถ **recognize text from image** ได้, ดึงอักขระอาหรับทุกตัวออกมา, และได้สตริงที่สะอาดพร้อมเก็บ, ค้นหา หรือแสดงผล ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด—การติดตั้งไลบรารี, การกำหนดค่ารุ่นภาษา, การสแกน, และสุดท้ายการพิมพ์ผลลัพธ์ เมื่อจบคุณจะสามารถ **convert JPG to text** ได้ในไม่กี่วินาที

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งแพคเกจ NuGet Aspose.OCR สำหรับ .NET
- เริ่มต้น OCR engine ในโหมด CPU (เหมาะสำหรับงานขนาดเล็ก)
- โหลดโมเดลภาษาภาษาอาหรับโดยอัตโนมัติ
- รัน OCR บนไฟล์ JPEG และดึงข้อความที่ได้รับการจดจำ
- จัดการกับปัญหาทั่วไปเช่นไฟล์ขนาดใหญ่หรือข้อมูลภาษาไม่ครบ

ไม่จำเป็นต้องมีประสบการณ์กับ OCR มาก่อน; เพียงความเข้าใจพื้นฐานของ C# และ Visual Studio ก็พอ พร้อมหรือยัง? ไปเริ่มกันเลย

## ติดตั้ง Aspose OCR สำหรับ .NET

ก่อนที่โค้ดใดจะทำงาน คุณต้องมีไลบรารี Aspose.OCR มันมาพร้อมเป็นแพคเกจ NuGet ดังนั้นการติดตั้งจึงเป็นคำสั่งเดียวเท่านั้น

```bash
dotnet add package Aspose.OCR
```

หรือถ้าคุณชอบใช้ UI ของ Visual Studio ให้เปิด **Tools → NuGet Package Manager → Manage NuGet Packages for Solution**, ค้นหา **Aspose.OCR**, แล้วคลิก **Install** แพคเกจจะดึงทุกอย่างที่คุณต้องการรวมถึงไฟล์ข้อมูลภาษา ที่ engine จะดาวน์โหลดเมื่อใช้ครั้งแรก

> **Pro tip:** ตั้งค่าโปรเจกต์ให้เป้าหมายเป็น .NET 6 หรือใหม่กว่า; เฟรมเวิร์กเก่าก็ยังทำงานได้แต่คุณจะพลาดการปรับปรุงประสิทธิภาพ

## Initialise the OCR Engine

ตอนนี้ไลบรารีพร้อมแล้ว เราสามารถสร้างอินสแตนซ์ของ `OcrEngine` ได้ สำหรับงานขนาดเล็กส่วนใหญ่โหมด CPU เริ่มต้นก็เพียงพอ—มันใช้โปรเซสเซอร์ของเครื่องและหลีกเลี่ยงการตั้งค่าเพิ่มเติมสำหรับการเร่งความเร็วด้วย GPU

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

ทำไมต้องสร้าง engine ใหม่ทุกครั้ง? วัตถุ `OcrEngine` เก็บการตั้งค่าเช่นภาษา, DPI, และรูปแบบผลลัพธ์ การจำกัดขอบเขตไว้เพียงการดำเนินการเดียวทำให้สถานะสะอาดและหลีกเลี่ยงการสับสนระหว่างโมเดลภาษาต่าง ๆ

## Load the Arabic Language Model

Aspose มีแพ็คภาษาที่ดาวน์โหลดตามความต้องการ ครั้งแรกที่คุณกำหนด `Language.Arabic` ไลบรารีจะดาวน์โหลดข้อมูลประมาณ 30 MB ไปยังโฟลเดอร์แคชบนเครื่องของคุณ การดาวน์โหลดครั้งเดียวนี้ทำให้การรันครั้งต่อไปเร็วเป็นแสง

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

หากคุณต้องการสนับสนุนสคริปต์เพิ่มเติม (เช่นอังกฤษหรือฮินดี) เพียงเปลี่ยนค่า enum—ไม่ต้องเขียนโค้ดเพิ่ม Engine จะเก็บแคชแต่ละภาษาแยกกัน

## Run OCR on a JPG Image

เมื่อ engine พร้อมและโหลดโมเดลอาหรับแล้ว ให้ชี้ไปที่ภาพที่ต้องการประมวลผล เส้นทางไฟล์สามารถเป็นแบบ absolute หรือ relative; เพียงตรวจสอบให้ไฟล์มีอยู่และอ่านได้

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**Edge case:** หาก JPEG ของคุณใหญ่ (เกิน 5 MB) คุณอาจต้องลดขนาดก่อน ภาพขนาดใหญ่เพิ่มการใช้หน่วยความจำและอาจทำให้การจดจำช้าลง การปรับขนาดล่วงหน้าด้วย `System.Drawing` หรือ `ImageSharp` สามารถลดเวลาประมวลผลได้อย่างมาก

## Retrieve and Display the Recognised Text

เมธอด `Recognize` จะคืนค่าอ็อบเจกต์ `OcrResult` คุณสมบัติ `Text` ของมันจะมีข้อความแบบ plain‑text ของทุกอย่างที่ engine สามารถอ่านได้

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

เมื่อคุณรันโปรแกรมควรเห็นอักขระอาหรับพิมพ์ออกที่คอนโซล โดยคงลำดับและการขึ้นบรรทัดเดิม หากต้องการบันทึกเป็นไฟล์ให้ใช้ `File.WriteAllText` แทน

### ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือตัวอย่างแอปคอนโซลที่พร้อมรัน

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่าภาพชัดเจนและตั้งค่าภาษาเป็น `Arabic` หรือไม่ การสแกนเบลอหรือหน้าที่หมุนเป็นสาเหตุทั่วไปที่ทำให้ OCR ผิดพลาด

## Common Questions & Tips

- **ถ้าภาพมีทั้งภาษาอาหรับและอังกฤษ?**  
  ตั้งค่า `ocrEngine.Settings.Language = Language.Multilingual;` เพื่อให้ Aspose ตรวจจับหลายสคริปต์โดยอัตโนมัติ

- **ฉันสามารถเร่งความเร็วด้วย GPU ได้หรือไม่?**  
  ได้—เปลี่ยน engine เริ่มต้นเป็น `new OcrEngine(OcrEngineMode.Gpu)` หากคุณมีกราฟิกการ์ดที่รองรับและได้ติดตั้ง CUDA runtime ไว้แล้ว

- **จะจัดการการแสดงผลจากขวาไปซ้ายใน UI อย่างไร?**  
  สตริงดิบเป็น Unicode; เฟรมเวิร์ก UI สมัยใหม่ส่วนใหญ่ (WinForms, WPF, ASP.NET) รองรับการจัดวาง RTL โดยอัตโนมัติเมื่อคุณตั้งค่า `FlowDirection` ที่เหมาะสม

- **มีขีดจำกัดขนาดภาพหรือไม่?**  
  โดยเทคนิคไม่มี แต่การใช้หน่วยความจำจะเพิ่มตามความละเอียด สำหรับสแกนขนาดมหาศาล (เช่นหนังสือสแกน) ควรประมวลผลทีละหน้า

## Visual Overview

ด้านล่างเป็นแผนภาพง่าย ๆ ที่แสดงกระบวนการจากไฟล์ภาพไปยังข้อความที่สกัดออกมา  

![How to use OCR flow diagram – image to text conversion](/images/ocr-flow.png)

*Alt text:* *แผนภาพการไหลของการใช้ OCR แสดงการแปลงภาพเป็นข้อความใน C#.*

## Next Steps

ตอนนี้คุณได้เชี่ยวชาญ **วิธีใช้ OCR** สำหรับ JPEG ภาษาอาหรับแล้ว คุณสามารถขยายโซลูชันได้:

- **การประมวลผลเป็นชุด:** วนลูปโฟลเดอร์ของภาพและบันทึกผลลัพธ์แต่ละไฟล์เป็น `.txt` แยกกัน
- **หลังการประมวลผล:** ใช้ regular expressions ทำความสะอาดเครื่องหมายวรรคตอนหรือการขึ้นบรรทัดที่ไม่ต้องการ
- **การบูรณาการ:** ส่งสตริงที่สกัดออกไปยังดัชนีการค้นหา (เช่น Azure Cognitive Search) เพื่อทำการค้นหาเต็มข้อความในเอกสารที่สแกน

หากคุณสนใจภาษาอื่น ๆ เพียงสลับค่า enum `Language` อยากสกัดตารางหรือโน้ตมือเขียน? Aspose.OCR ยังมีฟีเจอร์ `LayoutAnalysis` ที่สามารถแยกบล็อกก่อนการจดจำได้อีกด้วย

---

### TL;DR

คุณได้เรียนรู้ **วิธีใช้ OCR** ใน C# เพื่อ **แยกข้อความอาหรับ** จาก JPEG อย่างมีประสิทธิภาพ **recognize text from image** และ **convert JPG to text** ตัวอย่างที่ทำงานได้เต็มรูปแบบด้านบนแสดงทุกขั้นตอน ตั้งแต่การติดตั้ง NuGet ไปจนถึงการพิมพ์สตริงสุดท้าย เพียงนำภาพตัวอย่างมาวางโค้ดแล้วรัน คุณจะเห็นผลลัพธ์โดยไม่ต้องพึ่งบริการภายนอก ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}