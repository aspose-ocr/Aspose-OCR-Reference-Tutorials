---
category: general
date: 2026-03-28
description: เรียนรู้วิธีทำ OCR แบบกลุ่มใน C# และแปลงไฟล์ TIFF เป็นข้อความได้อย่างง่ายดาย
  คู่มือขั้นตอนต่อขั้นตอนนี้แสดงการสกัดข้อความจากไฟล์ TIFF ด้วย Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: th
og_description: วิธีทำ OCR แบบชุดใน C#? ทำตามบทแนะนำเต็มรูปแบบนี้เพื่อแปลงไฟล์ TIFF
  หลายหน้าเป็นข้อความที่สามารถค้นหาได้โดยใช้ Aspose OCR.
og_title: วิธีทำ OCR แบบกลุ่มใน C# – แปลงไฟล์ TIFF หลายหน้าเป็นข้อความ
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR แบบกลุ่มใน C# – แปลงไฟล์ TIFF หลายหน้าเป็นข้อความ
url: /th/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน C# – แปลง Multi‑Page TIFF เป็นข้อความ

เคยสงสัย **วิธีทำ batch OCR** ให้กับกองหน้าเอกสารสแกนโดยไม่ต้องเขียนลูปสำหรับแต่ละภาพหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—เช่นการประมวลผลใบแจ้งหนี้หรือการดิจิไทซ์เอกสารเก่า—ความต้องการ **แปลง TIFF เป็นข้อความ** ปรากฏขึ้นทุกวัน และการทำทีละหน้าอย่างเดียวก็เร็ว ๆ นี้จะกลายเป็นความยุ่งยาก

ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ C# และ Aspose OCR คุณสามารถใส่ไฟล์ multi‑page TIFF ทั้งไฟล์เข้าไปในเอนจินและได้พจนานุกรมที่แมปหมายเลขหน้าไปยังสตริงที่สกัดออกมา ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งแสดง **วิธีทำ batch OCR** อย่างชัดเจน, **วิธีสกัดข้อความจาก TIFF**, และเหตุผลว่าทำไมวิธีนี้ดีกว่าการทำด้วยมือ

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่าไลบรารี Aspose OCR ในโปรเจกต์ .NET  
- โหลดไฟล์ multi‑page TIFF ด้วย `Image.FromMultiPageFile`  
- เรียก `RecognizeBatch` เพื่อรับ `Dictionary<int,string>` ของผลลัพธ์ต่อหน้า  
- พิมพ์ผลลัพธ์ในรูปแบบที่สะอาดและอ่านง่าย  

เมื่อเสร็จสิ้นคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งแปลงไฟล์ multi‑page TIFF ใด ๆ ให้เป็นข้อความธรรมดา—ไม่ต้องใช้เครื่องมือเพิ่มเติม

### ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK (หรือเวอร์ชัน .NET ล่าสุด)  
- Visual Studio 2022 หรือ VS Code—IDE ที่คุณชอบก็ได้  
- ไลเซนส์ Aspose OCR ที่ใช้งานได้หรือคีย์ทดลองฟรี (API ทำงานได้โดยไม่มีไลเซนส์แต่จะมีลายน้ำ)  
- ตัวอย่างไฟล์ multi‑page TIFF ชื่อ `multipage.tif` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้  

> **เคล็ดลับ:** หากคุณใช้ Windows โฟลเดอร์โปรเจกต์เริ่มต้นเป็นที่สะดวกสำหรับวางไฟล์ TIFF; บน Linux/macOS ให้ปรับเส้นทางให้ตรงตามที่ตั้งไฟล์

## Step 1: Install Aspose  OCR NuGet Package

ก่อนที่เราจะเขียนโค้ดใด ๆ เราต้องการไลบรารี OCR เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงเวอร์ชันเสถียรล่าสุด (ณ มีนาคม 2026 v23.9) และเพิ่ม DLL ที่จำเป็นลงในโปรเจกต์ของคุณ ไม่ต้องกำหนดค่าพิเศษใด ๆ สำหรับแอปคอนโซลแบบง่าย

## Step 2: Create the Console Application Skeleton

มาสร้างโครงสร้างโปรแกรมขั้นต่ำที่อ้างอิงเอนจิน OCR คำสั่ง `using` มีความสำคัญ—หากไม่มีคอมไพเลอร์จะบอกว่าไม่พบประเภท

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **ทำไมต้องสำคัญ:** คลาส `Image` อยู่ในเนมสเปซย่อย, และหากลืม import `ImageProcessing` จะเจอข้อผิดพลาด “type or namespace not found” ที่อาจทำให้เสียเวลาดีบักเป็นชั่วโมง

ต่อไปให้เพิ่มเมธอด `Main` และคอมเมนต์สั้น ๆ ที่อธิบายวัตถุประสงค์:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Step 3: Initialise the OCR Engine

`OcrEngine` คือหัวใจหลัก การสร้างอินสแตนซ์หนึ่งครั้งแล้วใช้ซ้ำสำหรับทุกหน้าเป็นวิธีที่ประหยัดหน่วยความจำและเร็ว

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **กำลังเกิดอะไรขึ้นเบื้องหลัง?** เอนจินจะโหลดโมเดลภาษาและตั้งค่าพื้นฐานโดยอัตโนมัติ (เช่น English, auto‑rotate) คุณสามารถปรับเปลี่ยนได้ภายหลัง แต่ค่าพื้นฐานนั้นเพียงพอสำหรับเอกสารส่วนใหญ่

## Step 4: Load the Multi‑Page TIFF

Aspose ทำให้การโหลดภาพหลายเฟรมเป็นเรื่องง่าย เพียงระบุพาธเต็มหรือพาธสัมพันธ์จากไดเรกทอรีทำงานของไฟล์ executable

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

หากไฟล์ไม่พบ `FromMultiPageFile` จะโยน `FileNotFoundException` ให้ห่อไว้ใน `try/catch` หากต้องการจัดการข้อผิดพลาดอย่างสุภาพ—ซึ่งเราจะสาธิตในขั้นตอนต่อไป

## Step 5: Perform Batch OCR

นี่คือจุดสำคัญของบทเรียน: `RecognizeBatch` จะคืนค่า `Dictionary<int,string>` ที่คีย์คือดัชนีหน้า (เริ่มจาก 0) และค่าคือข้อความที่สกัดได้

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **กรณีขอบ:** บางไฟล์ TIFF มีหน้าว่าง Aspose จะคืนสตริงว่างสำหรับหน้าดังกล่าว คุณสามารถกรองออกได้ในภายหลังหากไม่ต้องการให้ผลลัพธ์รก

## Step 6: Display the Results

สุดท้ายให้วนลูปผ่านพจนานุกรมและพิมพ์ข้อความของแต่ละหน้า การใช้สตริงแบบอินเทอร์โพลเทชันทำให้โค้ดดูสะอาด

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

เมื่อรันโปรแกรมควรได้ผลลัพธ์ประมาณนี้:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

หากคุณเห็นข้อความแปลก ๆ ให้ตรวจสอบว่าไฟล์ TIFF ต้นฉบับไม่เสียหายและภาษาของข้อความตรงกับค่าตั้งต้นของเอนจิน (English) คุณสามารถตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish;` สำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษได้

## Full Working Example

รวมทุกส่วนเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs` แล้วรันได้:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

บันทึก, คอมไพล์, แล้วรัน:

```bash
dotnet run
```

คุณจะเห็นเนื้อหาที่สกัดจากแต่ละหน้าถูกพิมพ์ออกที่คอนโซล นั่นคือ **c# ocr tutorial** ทั้งหมดที่คุณต้องการ

## Frequently Asked Questions & Edge Cases

### ถ้า TIFF ของฉันมีหลายสิบหน้า จะทำอย่างไร?

`RecognizeBatch` ประมวลผลทุกเฟรมในคำสั่งเดียว แต่การใช้หน่วยความจำจะเพิ่มตามจำนวนหน้า หากเอกสารใหญ่มาก (หลายร้อยหน้า) ควรประมวลผลเป็นชิ้น ๆ:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### ฉันสามารถบันทึกข้อความที่สกัดเป็นไฟล์แทนการพิมพ์ได้หรือไม่?

ได้เลย แทนที่บล็อก `Console.WriteLine` ด้วยการทำ I/O ไปยังไฟล์:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

ตอนนี้แต่ละหน้าจะได้ไฟล์ `.txt` ของตัวเอง—เหมาะสำหรับการทำดัชนีต่อไป

### จะเปลี่ยนภาษาผลลัพธ์หรือเปิดการหมุนอัตโนมัติอย่างไร?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

ต้องตั้งค่าต่าง ๆ **ก่อน** เรียก `RecognizeBatch`

## Conclusion

เราได้อธิบาย **วิธีทำ batch OCR** สำหรับไฟล์ multi‑page TIFF ด้วย Aspose OCR ใน C# โดยโหลดภาพครั้งเดียว, เรียก `RecognizeBatch`, แล้ววนลูปผ่านพจนานุกรมที่ได้ คุณสามารถ **แปลง TIFF เป็นข้อความ** ได้ในไม่กี่วินาที ตัวอย่างยังแสดงวิธี **สกัดข้อความจาก TIFF**, จัดการข้อผิดพลาด, และบันทึกผลลัพธ์เป็นไฟล์—ทั้งหมดในแอปคอนโซลที่เรียบง่ายและครบวงจร

พร้อมก้าวต่อไปหรือยัง? ลองผสานวิธีนี้กับไลบรารีสร้าง PDF เพื่อผลิต PDF ที่ค้นหาได้, หรือเชื่อมต่อผลลัพธ์กับฐานข้อมูลเพื่อสร้างคลังข้อมูลที่ค้นหาได้ คุณยังสามารถทดลองกับรูปแบบภาพอื่น (PNG, JPEG) เพียงเปลี่ยน `Image.FromMultiPageFile` เป็น `Image.FromFile`

มีคำถามเพิ่มเติมเกี่ยวกับ OCR, ไลเซนส์, หรือการปรับประสิทธิภาพ? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุกสนาน!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}