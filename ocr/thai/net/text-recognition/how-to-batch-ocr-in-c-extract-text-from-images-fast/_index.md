---
category: general
date: 2026-03-21
description: วิธีทำ OCR แบบกลุ่มใน C# อย่างง่าย—เรียนรู้การดึงข้อความจากรูปภาพ, แปลงรูปภาพเป็นข้อความ,
  และบันทึกผล OCR เป็นข้อความพร้อมตั้งค่าภาษา
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: th
og_description: วิธีทำ OCR แบบกลุ่มใน C# ช่วยให้คุณดึงข้อความจากภาพ แปลงภาพเป็นข้อความ
  และบันทึกผล OCR เป็นข้อความ พร้อมตั้งค่าภาษา OCR ได้อย่างง่ายดาย.
og_title: วิธีทำ OCR แบบแบตช์ใน C# – คู่มือด่วน
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR แบบกลุ่มใน C# – ดึงข้อความจากรูปภาพอย่างรวดเร็ว
url: /th/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน C# – ดึงข้อความจากรูปภาพอย่างรวดเร็ว

เคยสงสัย **วิธีทำ batch OCR** เมื่อคุณมีรูปภาพหลายร้อยรูปอยู่ในโฟลเดอร์หรือไม่?  คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามวิธีดึงข้อความจากรูปภาพโดยไม่ต้องเขียนลูปสำหรับแต่ละไฟล์ ข่าวดีคือ Aspose.OCR ให้วิธีที่สะอาดและพร้อมทำงานแบบขนานเพื่อ **แปลงรูปภาพเป็นข้อความ** เพียงไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และพร้อมรันที่แสดงวิธี **บันทึก OCR เป็นข้อความ**, เลือกภาษาที่เหมาะสม, และเพิ่มการประมวลผลแบบขนานเพื่อความเร็ว.  เมื่อจบคุณจะมีโซลูชันที่เป็นอิสระซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้.

## สิ่งที่คุณต้องการ

- .NET 6 หรือใหม่กว่า (API ทำงานกับ .NET Core และ .NET Framework)
- Aspose.OCR สำหรับ .NET (แพคเกจ NuGet `Aspose.OCR`)
- โฟลเดอร์ของรูปภาพที่คุณต้องการประมวลผล (PNG, JPEG, TIFF, ฯลฯ)
- ความสนใจเล็กน้อยเกี่ยวกับการเขียนโปรแกรมแบบขนาน (ไม่บังคับแต่เป็นประโยชน์)

ไม่มีบริการเสริม, ไม่มีคีย์คลาวด์—เพียงโค้ด C# ธรรมดาที่ทำงานในเครื่อง.

---

![how to batch OCR workflow](placeholder.png){alt="how to batch OCR workflow diagram"}

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

เริ่มแรกให้สร้างแอปคอนโซล (หรือใช้แอปที่มีอยู่แล้ว) แล้วเพิ่มแพคเกจ Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **เคล็ดลับ:** หากคุณใช้ Visual Studio, คลิกขวาที่โปรเจกต์ → *Manage NuGet Packages* → ค้นหา *Aspose.OCR* และติดตั้งเวอร์ชันเสถียรล่าสุด.

สิ่งนี้ทำให้คุณเข้าถึง `OcrBatchProcessor`, `OcrEngineSettings`, และ enum `Language`.

## ขั้นตอนที่ 2: กำหนดโฟลเดอร์อินพุตและเอาต์พุต

Batch processor ต้องรู้ว่าภาพต้นฉบับอยู่ที่ไหนและไฟล์ข้อความที่ดึงออกมาควรเขียนไปที่ไหน. เก็บพาธเป็นแบบ absolute หรือ relative จากรากของโปรเจกต์—แค่ตรวจสอบให้แน่ใจว่าโฟลเดอร์มีอยู่ก่อนที่คุณจะรันโค้ด.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **ทำไมเรื่องนี้สำคัญ:** หากโฟลเดอร์เอาต์พุตไม่มีอยู่ processor จะโยน exception ทำให้การประมวลผลทั้งหมดหยุด. การสร้างโฟลเดอร์ล่วงหน้าช่วยให้การทำงานราบรื่น.

## ขั้นตอนที่ 3: ตั้งค่า OCR (รวมถึงภาษา)

นี่คือที่คุณ **ตั้งค่าภาษา OCR** สำหรับ batch ทั้งหมด. Aspose.OCR รองรับหลายสิบภาษา; English เป็นค่าเริ่มต้น, แต่คุณสามารถเปลี่ยนเป็น French, Spanish, ฯลฯ โดยการเปลี่ยนค่า enum `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

หากคุณต้องการประมวลผลหลายภาษาต่อภาพ, คุณสามารถเขียนทับการตั้งค่านี้ต่อไฟล์ได้ในภายหลัง—รายละเอียดต่อไป.

## ขั้นตอนที่ 4: สร้างอ็อบเจ็กต์ `OcrBatchProcessor`

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน. `OcrBatchProcessor` ให้คุณระบุโฟลเดอร์อินพุต, โฟลเดอร์เอาต์พุต, รูปแบบเอาต์พุต, ตัวเลือกการทำงานแบบขนาน, และการตั้งค่าที่ใช้ร่วมกันที่เราสร้างไว้.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **ทำไมต้องทำงานแบบขนาน?** เมื่อคุณมีหลายสิบหรือหลายร้อยรูป, การประมวลผลทีละรูปอาจช้ามาก. การตั้งค่า `MaxDegreeOfParallelism` เป็น 4 ทำให้ runtime ใช้ 4 คอร์ของ CPU พร้อมกัน, ลดเวลารวมอย่างมากบนเครื่องทำงานทั่วไป.

## ขั้นตอนที่ 5: รันการทำงานแบบ Batch

เมื่อกำหนดค่า processor แล้ว, การทำงานเป็นการเรียกเมธอดเดียว. ไลบรารีจัดการการนับไฟล์, OCR, และการเขียนผลลัพธ์โดยอัตโนมัติ.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

เมื่อคอนโซลพิมพ์ *“Batch OCR completed.”* คุณจะพบไฟล์ `.txt` ข้างๆ รูปต้นฉบับแต่ละไฟล์ในโฟลเดอร์ `BatchResults`. ไฟล์ข้อความแต่ละไฟล์จะมีอักขระดิบที่ดึงจากภาพต้นฉบับ—ตรงกับสิ่งที่คุณต้องการ **ดึงข้อความจากรูปภาพ** เพื่อการประมวลผลต่อไป.

### ผลลัพธ์ที่คาดหวัง

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

เปิดไฟล์ใดก็ได้แล้วคุณจะเห็นการแสดงผลเป็นข้อความธรรมดาของเนื้อหาภาพ.

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์ (ไม่บังคับ)

เป็นนิสัยที่ดีที่จะตรวจสอบไฟล์บางไฟล์เพื่อให้แน่ใจว่า OCR ทำงานตามที่คาด. วิธีง่ายคืออ่านบรรทัดแรกของแต่ละไฟล์ที่สร้างและพิมพ์ออกที่คอนโซล:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

หากพบอักขระแปลกๆ ให้ลองเปลี่ยนการตั้งค่า `Language` หรือปรับคุณภาพภาพ (เช่น เพิ่ม DPI, แปลงเป็น grayscale).

## การปรับแต่งขั้นสูงและกรณีขอบ

### 1. การกำหนดภาษาตามไฟล์

บางครั้ง batch มีเอกสารหลายภาษา. คุณสามารถตรวจสอบชื่อภาพแต่ละไฟล์และกำหนดภาษาทันที:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. รูปแบบเอาต์พุตที่ต่างกัน

หากต้องการ PDF ที่ค้นหาได้แทนข้อความธรรมดา, เปลี่ยน `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

สิ่งนี้จะ **แปลงรูปภาพเป็นข้อความ** ภายในคอนเทนเนอร์ PDF, รักษาเลย์เอาต์ต้นฉบับ.

### 3. การจัดการภาพขนาดใหญ่

ภาพความละเอียดสูงมากอาจทำให้หน่วยความจำเต็ม. เพื่อให้กระบวนการเบา, เปิดการลดขนาดภาพ:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. การบันทึกข้อผิดพลาด

Processor จะโยน exception สำหรับไฟล์ที่อ่านไม่ออก. ห่อ `Execute` ด้วย try/catch และบันทึกชื่อไฟล์ที่มีปัญหา:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## ตัวอย่างทำงานเต็ม

รวมทุกอย่างเข้าด้วยกัน, นี่คือตัวอย่างโปรแกรมที่สมบูรณ์พร้อมคัดลอกและวาง:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

บันทึกไฟล์นี้เป็น `Program.cs`, สร้างโปรเจกต์, และรัน `dotnet run`. คุณจะเห็นผลลัพธ์ในคอนโซลยืนยันการเสร็จสิ้น, ตามด้วยตัวอย่างสั้นของข้อความที่ดึงออก.

---

## สรุป

เราเพิ่งอธิบาย **วิธีทำ batch OCR** ใน C# ด้วย Aspose.OCR, แสดงวิธี **ดึงข้อความจากรูปภาพ**, **แปลงรูปภาพเป็นข้อความ**, และ **บันทึก OCR เป็นข้อความ** พร้อมกับ **ตั้งค่าภาษา OCR** ให้ตรงกับเนื้อหาของคุณ. ตัวอย่างทำงานเต็มรูปแบบ, มีการประมวลผลแบบขนานเพื่อความเร็ว, และมีจุดเชื่อมต่อสำหรับสถานการณ์ขั้นสูงเช่นการกำหนดภาษาตามไฟล์หรือเอาต์พุตเป็น PDF.

พร้อมขั้นตอนต่อไปหรือยัง? ลองเปลี่ยน `OcrOutputFormat.PlainText` เป็น `SearchablePdf` แล้วดูว่าการสร้าง PDF ที่ค้นหาได้ง่ายแค่ไหน. หรือทดลองค่า `MaxDegreeOfParallelism` ต่างๆ เพื่อดึงประสิทธิภาพสูงสุดจากเครื่องหลายคอร์.

หากเจอปัญหา, ตรวจสอบพาธของโฟลเดอร์อีกครั้ง, ให้แน่ใจว่าภาพอ่านได้, และตรวจสอบว่า enum ภาษาแมตช์กับข้อความในรูปของคุณ. โค้ดสนุกนะ, ขอให้ batch OCR ของคุณเร็วและแม่นยำ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}