---
category: general
date: 2026-04-26
description: วิธีทำ OCR รูป PNG เป็นชุดอย่างรวดเร็ว เรียนรู้การสกัดข้อความจาก PNG
  แปลงรูปเป็นข้อความ เขียนข้อความที่จดจำได้ และอ่านไดเรกทอรี PNG ด้วย Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: th
og_description: วิธีทำ OCR รูปภาพ PNG แบบเป็นชุดใน C# ด้วย Aspose OCR คู่มือนี้แสดงวิธีดึงข้อความจาก
  PNG, แปลงรูปภาพเป็นข้อความ, และบันทึกข้อความที่จดจำได้อย่างมีประสิทธิภาพ
og_title: วิธีทำ OCR รูป PNG แบบเป็นชุดใน C# – ทีละขั้นตอน
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR รูป PNG แบบเป็นชุดใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR รูป PNG ด้วย C# – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีทำ batch OCR** โฟลเดอร์เต็มของไฟล์ PNG โดยไม่ต้องเขียนโปรแกรมแยกสำหรับแต่ละภาพหรือไม่? คุณไม่ได้เป็นคนเดียวที่ต้องจัดการกับภาพหน้าจอหลายสิบภาพ, ใบเสร็จสแกน, หรือกราฟิกที่ต้องแปลงเป็นข้อความที่ค้นหาได้ ในบทเรียนนี้เราจะพาคุณผ่านโซลูชันแบบทำมือที่ **ดึงข้อความจาก PNG**, **แปลงภาพเป็นข้อความ**, และ **เขียนข้อความที่รู้จำได้** ลงไฟล์แยกแต่ละไฟล์ — ทั้งหมดนี้ทำงานโดยอ่านไดเรกทอรี PNG อัตโนมัติ

เมื่อจบคู่มือคุณจะมีแอปคอนโซล C# ที่พร้อมรันและประมวลผลภาพจำนวนใดก็ได้ในครั้งเดียว ไม่ต้องสคริปต์เพิ่มเติม ไม่ต้องคัดลอก‑วางด้วยตนเอง — เพียงโค้ดเดียวที่ทำงานหนักให้คุณ

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0** หรือใหม่กว่า (โค้ดยังทำงานได้บน .NET Framework ด้วย)  
- **Aspose.OCR for .NET** NuGet package (ทดลองใช้ฟรีสำหรับการทดสอบ)  
- โฟลเดอร์ที่มีไฟล์ *.png* จำนวนหนึ่งที่ต้องการ OCR  
- Visual Studio 2022 หรือ IDE C# ใดก็ได้ที่คุณชอบ

ถ้าคุณมีทั้งหมดนี้แล้ว เราก็พร้อมจะเริ่มลงมือทำ

## Step 1 – เตรียมโฟลเดอร์ Input และ Output *(Read PNG Directory)*

สิ่งแรกที่เราทำคือชี้โปรแกรมไปยังโฟลเดอร์ที่เก็บรูปภาพและกำหนดตำแหน่งที่ไฟล์ *.txt* ที่ได้จะถูกบันทึก การใช้ `Directory.GetFiles` จะให้คอลเลกชันของไฟล์ PNG ทุกไฟล์ในไดเรกทอรีอย่างสะอาด

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
- การใช้ไวลด์การ์ด (`*.png`) รับประกันว่าเราจะประมวลผลเฉพาะไฟล์ภาพเท่านั้น ไม่รวมไฟล์เอกสารอื่นที่อาจอยู่ในโฟลเดอร์  
- การสร้างโฟลเดอร์ output แบบอัตโนมัติช่วยป้องกัน `DirectoryNotFoundException` ที่อาจเกิดขึ้นในภายหลัง

> **เคล็ดลับ:** หากต้องการรองรับรูปแบบอื่น (JPEG, BMP) เพียงขยาย pattern การค้นหา หรือเรียก `Directory.EnumerateFiles` พร้อมระบุหลายส่วนขยาย

## Step 2 – เริ่มต้น OCR Engine *(Convert Images to Text)*

Aspose.OCR มี engine สองประเภท: `OcrEngine` ที่ทำงานบน CPU และ `GpuOcrEngine` ที่เร่งด้วย GPU สำหรับงาน batch ส่วนใหญ่ engine บน CPU เพียงพอแล้ว แต่คุณสามารถสลับชื่อคลาสได้หากมี GPU ที่รองรับ

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
- การระบุภาษาอย่างชัดเจนช่วยเพิ่มความแม่นยำอย่างมาก เพราะ engine จะรู้ว่าต้องคาดหวังชุดอักขระแบบใด  
- การเปลี่ยนเป็น `GpuOcrEngine` เพียงบรรทัดเดียว หากคุณเจอคอขวดด้านประสิทธิภาพเมื่อทำ batch ขนาดใหญ่

## Step 3 – สร้าง Batch Recogniser

Aspose มี `BatchRecognizer` ที่สะดวกซึ่งรับคอลเลกชันของเส้นทางไฟล์และส่งผลลัพธ์กลับมาทีละรายการ วิธีนี้ช่วยหลีกเลี่ยงการโหลดภาพทั้งหมดเข้าสู่หน่วยความจำพร้อมกัน — เป็นรายละเอียดสำคัญสำหรับโฟลเดอร์ขนาดใหญ่

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
- Batch recogniser จัดการลูปให้เราได้โดยไม่ต้องกังวลเรื่องการวนซ้ำอย่างปลอดภัย ทำให้เรามุ่งเน้นที่การประมวลผลผลลัพธ์แต่ละรายการได้ง่ายขึ้น

## Step 4 – รัน OCR บนรูปทั้งหมดและเขียนผลลัพธ์ *(Write Recognized Text)*

ตอนนี้เราจะทำ OCR จริง ๆ เมธอด `Recognize` จะคืนค่า `IEnumerable<RecognitionResult>` ซึ่งแต่ละผลลัพธ์จะมีข้อความที่ดึงออกมาและเมตาดาต้าอื่น ๆ

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
- การใช้ `File.WriteAllText` ทำให้ข้อความถูกบันทึกด้วยการเข้ารหัส UTF‑8 โดยค่าเริ่มต้น ซึ่งรักษาอักขระพิเศษไว้ได้ครบถ้วน  
- การตั้งชื่อแบบเพิ่มลำดับ (`out_0.txt`, `out_1.txt`) ตรงกับลำดับการประมวลผล ช่วยในการดีบัก

> **กรณีขอบ:** หากภาพใดภาพหนึ่งไม่สามารถ OCR ได้ (เช่นไฟล์เสีย) `RecognitionResult.Text` จะเป็นค่าว่าง คุณสามารถเพิ่มการตรวจสอบง่าย ๆ ภายในลูปเพื่อบันทึกข้อผิดพลาดได้ดังนี้:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Step 5 – รวมทุกอย่างเข้าด้วยกัน – ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้ รวมถึง `using` directives, การตรวจสอบโฟลเดอร์, และ UI คอนโซลเล็ก ๆ เพื่อให้คุณทราบเมื่อ batch เสร็จสิ้น

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อรันโปรแกรมจะพิมพ์ข้อความประมาณนี้:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

และคุณจะเห็นไฟล์ `out_0.txt` … `out_11.txt` อยู่ในโฟลเดอร์ output, แต่ละไฟล์จะมีข้อความแบบ plain‑text ของภาพที่สอดคล้องกัน

## คำถามที่พบบ่อย & เคล็ดลับ

| Question | Answer |
|----------|--------|
| *Can I OCR sub‑folders as well?* | ใช่ — แทนที่ `Directory.GetFiles` ด้วย `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)` |
| *What if I need a different language?* | ตั้งค่า `ocrEngine.Language = Language.Spanish;` (หรือ enum ภาษาอื่นที่รองรับ) |
| *How do I handle huge batches (thousands of files)?* | พิจารณาแบ่งเป็นชิ้นย่อยหรือใช้ `Parallel.ForEach` พร้อมกำหนด degree of parallelism เพื่อหลีกเลี่ยงการใช้หน่วยความจำจนเต็ม |
| *Is the output always UTF‑8?* | `File.WriteAllText` มีค่าเริ่มต้นเป็น UTF‑8 โดยไม่มี BOM ซึ่งทำงานได้กับหลายภาษาแบบละติน หากเป็นสคริปต์เอเชียอาจต้องกำหนด `Encoding.UTF8` อย่างชัดเจน |
| *Can I get confidence scores?* | `RecognitionResult` มี property `Confidence` — คุณสามารถบันทึกค่าความเชื่อมั่นพร้อมข้อความเพื่อควบคุมคุณภาพได้ |

## ภาพรวมเชิงภาพ *(How to Batch OCR – Diagram)*

![วิธีทำ batch OCR workflow diagram แสดง input folder → OCR engine → batch recogniser → output txt files](https://example.com/diagram-how-to-batch-ocr.png "How to batch OCR")

*ข้อความ alt มีคีย์เวิร์ดหลักเพื่อให้สอดคล้องกับข้อกำหนด SEO ของรูปภาพ*

## สรุป

เราได้อธิบาย **วิธีทำ batch OCR** โฟลเดอร์ PNG ด้วย Aspose.OCR ตั้งแต่การอ่านไดเรกทอรี PNG จนถึงการเขียนไฟล์ข้อความที่รู้จำได้ โซลูชันนี้เป็นอิสระเต็มรูปแบบ ทำงานบน .NET runtime สมัยใหม่ใดก็ได้ และสามารถขยายต่อเพื่อใช้ GPU, รองรับหลายภาษา, หรือประมวลผลแบบขนานได้

พร้อมก้าวต่อไปหรือยัง? ลองเปลี่ยน `Language.Latin` เป็นภาษาต่าง ๆ หรือผสานผลลัพธ์เข้ากับดัชนีการค้นหา เพื่อให้เอกสารของคุณค้นหาได้ทันที ความเป็นไปได้ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญ batch OCR

ขอให้สนุกกับการเขียนโค้ด และอย่าลืมแสดงความคิดเห็นหากเจออุปสรรคใด ๆ นะครับ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}