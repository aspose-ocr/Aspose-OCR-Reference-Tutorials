---
category: general
date: 2026-03-23
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# และเรียนรู้วิธีเพิ่ม console
  logger เพื่อรับข้อเสนอแนะแบบเรียลไทม์
draft: false
keywords:
- extract text from image
- add console logger
language: th
og_description: ดึงข้อความจากภาพด้วย Aspose OCR และเพิ่มตัวบันทึกคอนโซลเพื่อติดตามกระบวนการ
  ขั้นตอนโดยละเอียดสำหรับ C#
og_title: ดึงข้อความจากรูปภาพใน C# – คู่มือการเขียนโปรแกรมครบถ้วน
tags:
- OCR
- C#
- logging
title: สกัดข้อความจากภาพใน C# – คู่มือเต็ม
url: /th/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพใน C# – คู่มือเต็ม

ต้องการ **สกัดข้อความจากรูปภาพ** อย่างรวดเร็วและเชื่อถือได้หรือไม่? ด้วย Aspose OCR คุณทำได้เช่นนั้นในไม่กี่บรรทัดของ C#  
เราจะสาธิตวิธี **เพิ่ม console logger** เพื่อให้คุณสามารถดูการทำงานของเครื่อง OCR ที่บอกความคืบหน้าโดยตรงไปยังเทอร์มินัลของคุณ

ลองนึกภาพว่าคุณมีใบเสร็จสแกน, โน้ตมือเขียน, หรือหน้า PDF ที่บันทึกเป็น PNG คุณต้องการตัวอักษรดิบโดยไม่ต้องเปิด UI ที่ใหญ่โต บทเรียนนี้จะพาคุณผ่านโซลูชันที่คัดลอก‑และ‑วางได้ครบถ้วน ซึ่งทำงานได้กับ .NET 6+ และไลบรารี Aspose OCR ล่าสุด

เมื่อจบคู่มือนี้คุณจะสามารถ:

* โหลดไฟล์ภาพและรัน OCR เพื่อ **สกัดข้อความจากรูปภาพ** ได้  
* เชื่อมต่อ console logger เข้ากับ Aspose AI เพื่อให้คุณเห็นว่าห้องสมุดกำลังทำอะไรเบื้องหลัง  
* ใช้ post‑processor ตรวจสอบการสะกดในตัวเพื่อทำความสะอาดข้อผิดพลาดของ OCR  

> **Prerequisites** – สภาพแวดล้อมการพัฒนา .NET ที่ทำงานได้ (Visual Studio 2022, VS Code หรือ Rider), .NET 6 SDK หรือใหม่กว่า, และใบอนุญาต Aspose OCR (หรือทดลองใช้ฟรี) ไม่จำเป็นต้องใช้แพ็กเกจของบุคคลที่สามอื่นใด

## สิ่งที่คุณต้องการ

| รายการ | ทำไมจึงสำคัญ |
|------|----------------|
| **Aspose.OCR** NuGet package | ให้คลาส `OcrEngine` ที่อ่านภาพจริง |
| **Aspose.OCR.AI** NuGet package | ให้กรอบงาน post‑processor `AsposeAI` รวมถึงการตรวจสอบการสะกด |
| **Microsoft.Extensions.Logging** (optional) | ให้ interface `ILogger` สำหรับขั้นตอน **add console logger** |
| **ภาพต้นฉบับ** (`input.png`) | ไฟล์ต้นทางที่เราจะ **สกัดข้อความจากรูปภาพ** |

คุณสามารถติดตั้งแพ็กเกจเหล่านี้ผ่านเทอร์มินัลได้:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

## ขั้นตอนที่ 1 – สกัดข้อความจากรูปภาพด้วย Aspose OCR

สิ่งแรกที่เราทำคือส่งภาพให้กับ OCR engine บล็อกนี้ทำงานหนักและคืนสตริงดิบที่อาจยังมีการสะกดผิดอยู่

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**ทำไมวิธีนี้ถึงได้ผล:** `OcrEngine` จัดการการเตรียมภาพระดับต่ำทั้งหมด (การทำไบนารี, การแก้ไขการเอียง ฯลฯ) เมื่อ `Recognize()` คืนค่า `true` คุณสมบัติ `Text` จะมีตัวอักษรที่คาดการณ์ดีที่สุดแล้ว  

> **Tip:** หากภาพของคุณมีขนาดใหญ่ ให้พิจารณาปรับขนาดให้ ≤ 2000 px ที่ด้านยาวที่สุดก่อนส่งให้ engine จะช่วยเร่งการประมวลผลโดยไม่ทำให้ความแม่นยำลดลง

## ขั้นตอนที่ 2 – เพิ่ม Console Logger เพื่อรับข้อมูลแบบเรียลไทม์

ตอนนี้เรานำ **add console logger** เข้ามา Logging ไม่ได้มีไว้แค่การดีบักเท่านั้น; มันให้คุณมองเห็นการดาวน์โหลดโมเดล, ขั้นตอน AI‑processor, และคำเตือนใด ๆ ที่ไลบรารีอาจส่งออก

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

คุณสามารถต่อ logger นี้เข้ากับ Aspose AI ได้ดังนี้

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**สิ่งที่คุณจะเห็น:** เมื่อโมเดลตรวจสอบการสะกดถูกดาวน์โหลดอัตโนมัติ คอนโซลจะพิมพ์บรรทัดแบบนี้

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

นั่นคือข้อได้เปรียบของ **add console logger** – คุณจะไม่ต้องสงสัยว่าการดำเนินการเบื้องหลังสำเร็จหรือไม่

## ขั้นตอนที่ 3 – ตั้งค่าและลงทะเบียน Spell‑Check Post‑Processor

Aspose AI มาพร้อมกับ post‑processor ตรวจสอบการสะกดที่สะดวกซึ่งทำความสะอาดข้อผิดพลาด OCR ทั่วไป (เช่น “rec0gn1ze” → “recognize”) เราจะตั้งค่า, เลือกตำแหน่งเก็บโมเดล (ถ้าต้องการ) แล้วลงทะเบียนมัน

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**ทำไมคุณอาจต้องการเส้นทางกำหนดเอง:** ใน pipeline CI/CD คุณมักต้องการแคชโมเดลในโฟลเดอร์ที่รู้จักเพื่อหลีกเลี่ยงการดาวน์โหลดซ้ำ Flag `AllowAutoDownload` ทำให้โมเดลถูกดึงเมื่อรันโค้ดครั้งแรก

## ขั้นตอนที่ 4 – รัน Post‑Processor กับผลลัพธ์ OCR

เมื่อมีข้อความ OCR อยู่ในมือและตัวประมวลผลตรวจสอบการสะกดพร้อม เราจะส่งสตริงดิบให้ `AsposeAI` เอนจินจะรันโมเดลและตัวประมวลผลจะเก็บข้อความที่แก้ไขไว้ภายใน

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

หลังจากเรียกนี้ `spellProcessor` จะมีคอลเลกชันของอ็อบเจกต์ `RecognitionResult` แต่ละอันมีคุณสมบัติ `RecognitionText` ที่บรรจุเวอร์ชันที่ทำความสะอาดแล้ว

## ขั้นตอนที่ 5 – ดึงและแสดงข้อความที่แก้ไขแล้ว

สุดท้ายเราดึงสตริงที่แก้ไขจากตัวประมวลผลและพิมพ์ออก นี่คือช่วงที่คุณเห็นประโยชน์ของ OCR ร่วมกับ workflow **add console logger** อย่างแท้จริง

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Expected output** (สมมติว่าภาพมีวลี “Aspose OCR demo” พร้อมข้อบกพร่อง OCR บางส่วน):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

สังเกตว่า logger บอกเราว่าโมเดลพร้อมแล้ว และบรรทัดที่แก้ไขอ่านได้อย่างสะอาด

## ขั้นตอนที่ 6 – ทำความสะอาดทรัพยากร

ทั้ง `AsposeAI` และ `OcrEngine` ทำตาม `IDisposable` การทำ Dispose จะปล่อยหน่วยความจำเนทีฟและไฟล์แฮนด์เดิล ซึ่งสำคัญมากในบริการที่ทำงานต่อเนื่องเป็นเวลานาน

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แทนที่ `"YOUR_DIRECTORY"` ด้วยโฟลเดอร์จริงบนเครื่องของคุณ

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}