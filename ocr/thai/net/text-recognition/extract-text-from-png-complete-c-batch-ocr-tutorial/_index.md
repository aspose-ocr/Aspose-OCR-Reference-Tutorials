---
category: general
date: 2026-04-26
description: ดึงข้อความจากไฟล์ PNG อย่างรวดเร็วด้วย C# เรียนรู้วิธีแปลงภาพเป็นข้อความ
  อ่านไฟล์ PNG วนลูปผ่านภาพ และทำ OCR เป็นชุดในไม่กี่นาที.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: th
og_description: ดึงข้อความจากไฟล์ PNG อย่างรวดเร็วด้วย C# คู่มือนี้แสดงวิธีแปลงภาพเป็นข้อความ,
  อ่านไฟล์ PNG, วนลูปผ่านภาพและทำ OCR แบบกลุ่ม
og_title: ดึงข้อความจาก PNG – บทเรียน OCR แบบแบตช์เต็มสำหรับ C#
tags:
- C#
- OCR
- Aspose
title: สกัดข้อความจาก PNG – การสอน OCR แบบแบตช์เต็มรูปแบบด้วย C#
url: /th/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก PNG – การสอน OCR แบบ Batch ด้วย C# อย่างสมบูรณ์

เคยต้อง **ดึงข้อความจากไฟล์ PNG** แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—หลายคนเจออุปสรรคเมื่อลอง OCR กับโฟลเดอร์ของภาพหน้าจอครั้งแรก ข่าวดีคือด้วยเพียงไม่กี่บรรทัดของ C# และ Aspose OCR คุณก็สามารถแปลงภาพเป็นข้อความ อ่านไฟล์ PNG, วนลูปผ่านภาพ, และประมวลผลแบบ batch ได้ในครั้งเดียว  

ในบทเรียนนี้เราจะเดินผ่านแอปคอนโซลที่พร้อมรันซึ่งทำสิ่งนั้นโดยตรง เมื่อเสร็จคุณจะมีโซลูชันที่ทำงานอิสระซึ่งดึงข้อความจากทุก PNG ในไดเรกทอรีและสร้างไฟล์ `.txt` ที่สอดคล้องกันข้าง ๆ แต่ละภาพ ไม่ต้องสคริปต์เพิ่มเติม ไม่ต้องคัดลอก‑วางด้วยมือ—เพียงโค้ดเท่านั้น

## สิ่งที่คุณต้องมี

- **.NET 6 SDK** (หรือเวอร์ชัน .NET ใด ๆ ที่ใหม่กว่า) ฟรี, เร็ว, ทำงานได้ทุกที่
- **Aspose.OCR for .NET** (แพคเกจ NuGet) ไลบรารีนี้มีการเร่งความเร็วด้วย GPU หากคุณมี GPU ที่รองรับ, แต่ก็จะกลับไปใช้ CPU โดยอัตโนมัติหากไม่มี
- โฟลเดอร์ที่มี **ภาพ PNG** จำนวนหนึ่งที่คุณต้องการประมวลผล  
- โปรแกรมแก้ไขข้อความหรือ IDE—Visual Studio, VS Code, Rider—ตามที่คุณถนัด

เท่านี้เอง หากคุณมีทั้งหมดนี้แล้ว คุณก็พร้อมเริ่มต้น

![extract text from png example](image.png "extract text from png demo screenshot")

*Image alt text: “extract text from png using C# batch OCR”*

## ขั้นตอนที่ 1 – ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

แรกเริ่ม สร้างโปรเจกต์คอนโซลใหม่และดึงแพคเกจ Aspose OCR เข้ามา

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

ทำไมต้องใช้แอปคอนโซล? เพราะเป็นโฮสต์ที่ง่ายที่สุดสำหรับงาน batch, สามารถรันจาก command line หรือกำหนดเวลาให้ทำงานด้วย task runner หากภายหลังต้องการ UI คุณก็แค่ย้ายโลจิกหลักไปยัง class library

## ขั้นตอนที่ 2 – เริ่มต้น OCR Engine ที่เร่งด้วย GPU (หรือ fallback ไปยัง CPU)

Aspose มี `GpuOcrEngine` ที่ตรวจจับ GPU ที่รองรับโดยอัตโนมัติ หากไม่พบ จะสลับไปใช้ engine ปกติบน CPU—ไม่ต้องเขียนโค้ดเพิ่ม

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**เคล็ดลับ:** หากคุณรันบนเซิร์ฟเวอร์ headless ที่ไม่มี GPU, สามารถแทนที่ `GpuOcrEngine` ด้วย `OcrEngine` ได้โดยโค้ดจะทำงานเหมือนเดิม

## ขั้นตอนที่ 3 – วนลูปผ่านภาพในไดเรกทอรีเป้าหมาย

เราต้อง **วนลูปผ่านภาพ** และเลือกเฉพาะไฟล์ PNG เท่านั้น เมธอด `Directory.GetFiles` จะทำงานหนักส่วนนี้ และเราจะตรวจสอบกรณีโฟลเดอร์ว่าง

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

สังเกตการใช้ `SearchOption.TopDirectoryOnly` หากต้องการให้ค้นหาในโฟลเดอร์ย่อยต่อไป ให้เปลี่ยนเป็น `AllDirectories` การเปลี่ยนแปลงเล็ก ๆ นี้ทำให้คุณ **แปลงภาพเป็นข้อความ** ในโครงสร้างต้นไม้ทั้งหมดด้วยบรรทัดเดียว

## ขั้นตอนที่ 4 – ทำ OCR และบันทึกผลลัพธ์

นี่คือส่วนหลักของ workflow **batch OCR images** เราโหลดแต่ละ PNG, เรียก `Recognize()`, แล้วเขียนสตริงที่ดึงได้ลงไฟล์ `.txt` ที่มีชื่อฐานเดียวกัน

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**ทำไมต้องห่อด้วย try/catch?** แบตช์ภาพในโลกจริงมักมีไฟล์เสียหรือ PNG ที่ใช้โปรไฟล์สีแปลก ๆ การจับข้อยกเว้นจะป้องกันไม่ให้การรันทั้งหมดล่มและให้คุณดำเนินการต่อกับไฟล์ที่เหลือได้

## ขั้นตอนที่ 5 – รันแอปและตรวจสอบผลลัพธ์

คอมไพล์และเปิดแอป:

```bash
dotnet run
```

คุณควรเห็นข้อความในคอนโซลคล้ายกับ:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

เปิดไฟล์ `.txt` ใดไฟล์หนึ่งที่สร้างขึ้น—นี่คือข้อความที่ดึงมาได้ หากไฟล์ว่างเปล่า ให้ตรวจสอบคุณภาพของภาพ; OCR ทำงานดีที่สุดกับข้อความที่คมชัดและคอนทราสต์สูง

### สคริปต์ตรวจสอบอย่างรวดเร็ว (optional)

หากต้องการยืนยันว่าแต่ละ PNG มีไฟล์ข้อความที่สอดคล้องกัน ให้รัน PowerShell one‑liner เล็ก ๆ นี้:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## ความแตกต่างทั่วไป & กรณีขอบ

| Situation | What to Change |
|-----------|----------------|
| **Non‑Latin languages** (เช่น Cyrillic) | ตั้งค่า `ocrEngine.Language = Language.Cyrillic;` |
| **Large image set (>10 000 files)** | ใช้ `Parallel.ForEach` เพื่อเร่งความเร็ว, แต่ต้องระวังการใช้หน่วยความจำของ GPU |
| **Need to keep original image order** | เรียง `pngFiles` ก่อน `foreach` (`Array.Sort(pngFiles);`) |
| **Running on a CI server without a GPU** | แทนที่ `GpuOcrEngine` ด้วย `OcrEngine` เพื่อหลีกเลี่ยงข้อผิดพลาดการเริ่มต้น GPU |
| **You only want to process files that contain a specific keyword** | หลังจากได้ `result.Text` แล้ว ตรวจสอบ `result.Text.Contains("Invoice")` ก่อนเขียนไฟล์ |

การปรับแต่งเหล่านี้ทำให้คุณสามารถปรับ **pipeline แปลงภาพเป็นข้อความ** ให้เข้ากับสถานการณ์เกือบทุกอย่างที่อาจเจอ

## โค้ดเต็ม (พร้อมคัดลอก‑วาง)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

บันทึกเป็น `Program.cs`, รัน `dotnet run`, แล้วชมผลลัพธ์อันมหัศจรรย์

## สรุป

ตอนนี้คุณมี **วิธีที่สมบูรณ์และพร้อมใช้งานในระดับ production** เพื่อดึงข้อความจากไฟล์ PNG ด้วย C# บทเรียนได้ครอบคลุมทุกอย่าง—from การตั้งค่าโปรเจกต์, การเริ่มต้น OCR Engine ที่เร่งด้วย GPU, **การวนลูปผ่านภาพ**, ไปจนถึง **batch OCR images** และการบันทึกผลเป็นข้อความธรรมดา  

หากคุณอยากสำรวจขั้นต่อไป, ลอง:

- **แปลงภาพเป็นข้อความ** สำหรับฟอร์แมตอื่น ๆ (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}