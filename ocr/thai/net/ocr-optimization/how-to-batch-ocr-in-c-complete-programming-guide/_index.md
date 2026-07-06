---
category: general
date: 2026-03-13
description: วิธีทำ OCR เป็นชุดอย่างรวดเร็วและเชื่อถือได้พร้อมเรียนรู้การดึงข้อความจากไฟล์
  TIFF ด้วย Aspose.OCR ทำตามบทเรียนขั้นตอนต่อขั้นตอนนี้.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: th
og_description: เรียนรู้วิธีทำ OCR แบบชุดใน C# และดึงข้อความจากไฟล์ TIFF ด้วย Aspose.OCR
  คู่มือนี้ครอบคลุมการตั้งค่า โค้ด และเคล็ดลับการปฏิบัติที่ดีที่สุด
og_title: วิธีทำ OCR แบบแบตช์ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
tags:
- OCR
- C#
- Aspose
- Batch processing
title: วิธีทำ OCR แบบแบตช์ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR แบบกลุ่มใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยสงสัย **how to batch OCR** กองใบแจ้งหนี้ที่สแกนเป็นจำนวนมหาศาลโดยไม่ต้องเขียนสคริปต์แยกสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ ปัญหาที่เจอไม่ได้อยู่ที่ความแม่นยำของ OCR แต่เป็นปริมาณภาพที่ต้องจัดการ—มักเป็นไฟล์ TIFF—ที่ต้องแปลงเป็นข้อความที่สามารถค้นหาได้  

บทแนะนำนี้จะแสดงให้คุณเห็น **how to batch OCR** ด้วยการใช้ `BatchProcessor` ของ Aspose.OCR พร้อมสอนวิธี **extract text from tiff** ไฟล์ในหนึ่งการทำงานที่เรียบง่าย เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งจะประมวลผลโฟลเดอร์ทั้งหมด ใช้การเร่งความเร็วด้วย GPU (ถ้ามี) และบันทึกผลลัพธ์เป็นข้อความธรรมดาตามที่คุณต้องการ  

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือ .NET Framework 4.7.2 หากคุณต้องการใช้ runtime แบบคลาสสิก)  
- **Aspose.OCR for .NET** – คุณสามารถดาวน์โหลดแพ็กเกจ NuGet ด้วยคำสั่ง `dotnet add package Aspose.OCR`.  
- โฟลเดอร์ที่มีภาพ **TIFF** ที่คุณต้องการอ่าน (บทแนะนำใช้ `Invoices` เป็นตัวอย่าง).  
- ตัวเลือก: GPU ที่รองรับ DirectX 11 หรือ CUDA หากคุณต้องการเร่งความเร็ว.  

ไม่มีบริการเพิ่มเติม ไม่มีคีย์คลาวด์—แค่โครงการ C# ในเครื่องและไลบรารี Aspose.  

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** หากคุณใช้ Windows และวางแผนใช้การเร่งด้วย GPU อย่าลืมติดตั้งไดรเวอร์กราฟิกล่าสุด มิฉะนั้นแฟล็ก `UseGpu = true` จะกลับไปใช้ CPU โดยอัตโนมัติ.  

## ขั้นตอนที่ 2: สร้างการกำหนดค่า BatchProcessor

ต่อไปเราจะกำหนดค่า `BatchProcessor` นี่คือหัวใจของ **how to batch OCR**—คุณบอก Aspose ว่าต้องการภาษาอะไร, ตัวกรองการเตรียมล่วงหน้าใดที่ต้องใช้, และว่าจะใช้ GPU หรือไม่.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**ทำไมต้องตั้งค่าเหล่านี้?**  

- `Language = Language.English` บอกให้เอนจินใช้โมเดลภาษาอังกฤษ ซึ่งแม่นยำกว่ารุ่นทั่วไปมาก.  
- `UseGpu` สามารถลดเวลาในการประมวลผลได้ครึ่งหนึ่งบน GPU ที่ดีพอ, แต่หากคุณใช้แล็ปท็อปที่ไม่มี GPU ก็สามารถตั้งเป็น `false` ได้อย่างปลอดภัย.  
- กระบวนการกรองจำลองสิ่งที่มนุษย์ทำ: ทำให้หน้ากระดาษตรงและทำความสะอาดจุดรอยก่อนส่งให้เอนจิน OCR.  

## ขั้นตอนที่ 3: ชี้ตัวประมวลผลไปยังโฟลเดอร์ TIFF ของคุณ

ส่วนต่อไปของ **how to batch OCR** คือการบอกไลบรารีว่าที่ใดที่ไฟล์ต้นทางอยู่ รองรับไวล์การ์ด ทำให้คุณสามารถดึงไฟล์ `.tif` ทั้งหมดได้ในครั้งเดียว.  

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Edge case:** หากภาพของคุณมีส่วนขยายหลากหลาย (`.tiff`, `.tif`, `.png`) ให้เรียก `AddFolder` หลายครั้งหรือใช้ `*.*` แล้วกรองในโค้ดต่อไป.  

## ขั้นตอนที่ 4: เลือกตำแหน่งที่ผลลัพธ์ OCR จะถูกบันทึก

คุณอาจสงสัยว่า “ข้อความที่สกัดออกมาจะไปอยู่ที่ไหน?” นี่คือหัวข้อที่สามของ **how to batch OCR**—การกำหนดตำแหน่งและรูปแบบของผลลัพธ์ เราจะเก็บไฟล์ข้อความธรรมดาไว้ข้างๆ ไฟล์ต้นฉบับ.  

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

หากคุณต้องการ JSON หรือ XML แทนข้อความธรรมดา เพียงเปลี่ยน `OutputFormat.PlainText` เป็น `OutputFormat.Json` หรือ `OutputFormat.Xml` ไลบรารีจะจัดการการแปลงให้คุณ.  

## ขั้นตอนที่ 5: รันงานแบบกลุ่มและรายงานผล

สุดท้ายให้เริ่มงาน `Execute` จะบล็อกจนกว่าทุกไฟล์จะประมวลผลเสร็จ จากนั้นคุณสามารถตรวจสอบ `ProcessedCount` เพื่อยืนยันความสำเร็จ.  

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรม คอนโซลจะพิมพ์ข้อความประมาณนี้:  

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

ในโฟลเดอร์ `Output` คุณจะพบไฟล์ `.txt` หนึ่งไฟล์ต่อ TIFF ต้นฉบับ โดยชื่อไฟล์จะตรงกับชื่อรูปภาพต้นฉบับ (เช่น `Invoice_001.txt`). เปิดไฟล์ใดก็จะเห็นข้อความ OCR ดิบ—เหมาะสำหรับส่งต่อไปยังดัชนีการค้นหา หรือไปยัง pipeline การสกัดข้อมูลต่อไป.  

## การจัดการกับข้อผิดพลาดทั่วไป

### 1. GPU ไม่พร้อมใช้งาน

หาก `UseGpu = true` แต่ไม่พบอุปกรณ์ที่เข้ากันได้ Aspose จะกลับไปใช้ CPU อย่างเงียบ ๆ หากต้องการระบุอย่างชัดเจน คุณสามารถจับ `DeviceNotFoundException` ได้:  

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. ไฟล์ที่ไม่ใช่ TIFF ในโฟลเดอร์เดียวกัน

เมื่อคุณมีโฟลเดอร์ที่มีไฟล์หลากหลาย ให้กรองโดยโปรแกรม:  

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. ไฟล์ขนาดใหญ่เกินความจำ

สำหรับ TIFF หลายหน้าขนาดมหึมา ให้เปิดการสตรีม:  

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## เคล็ดลับสำหรับความแม่นยำที่ดียิ่งขึ้นเมื่อคุณ **extract text from tiff**

- **Resolution matters** – ตั้งค่าให้เป็น 300 dpi หรือสูงกว่า หากต่ำกว่า OCR engine อาจพลาดอักขระ.  
- **Color vs. Grayscale** – แปลงสแกนสีเป็นระดับสีเทาก่อน OCR; `DeskewFilter` ทำเช่นนี้โดยอัตโนมัติแล้ว แต่คุณสามารถเพิ่ม `ColorDepthReductionFilter` เพื่อความเร็วเพิ่ม.  
- **Post‑processing** – หลังจากได้ข้อความธรรมดาแล้ว ให้รันการตรวจสอบการสะกดหรือทำความสะอาดด้วย regex เพื่อแก้ไขข้อผิดพลาดทั่วไปของ OCR (เช่น “0” กับ “O”).  

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคอมไพล์และรันได้ เพียงเปลี่ยนเส้นทาง placeholder ให้เป็นไดเรกทอรีของคุณเอง.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

คอมไพล์และรัน:  

```bash
dotnet run
```

ตอนนี้คุณควรมีชุดไฟล์ `.txt` ที่เรียบร้อย—แต่ละไฟล์เป็นผลลัพธ์ของ **extracting text from tiff** ผ่านกระบวนการแบตช์อัตโนมัติเต็มรูปแบบ.  

## สรุป

เราได้อธิบาย **how to batch OCR** ใน C# ตั้งแต่ต้นจนจบ ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **extract text from tiff** อย่างมีประสิทธิภาพ จุดสำคัญที่ควรจำคือ:

1. ใช้ `BatchProcessor` ของ Aspose.OCR เพื่อหลีกเลี่ยงการเขียนลูปซ้ำ ๆ.  
2. ใช้ตัวกรองการเตรียมล่วงหน้า (deskew, despeckle) เพื่อความแม่นยำที่สูงขึ้น.  
3. เปิดการเร่งด้วย GPU เมื่อเป็นไปได้ แต่ต้องมีการสำรองด้วย CPU เสมอ.  
4. เก็บผลลัพธ์ในโครงสร้างโฟลเดอร์ที่คาดเดาได้ เพื่อให้งานต่อไปสามารถดึงข้อมูลได้โดยอัตโนมัติ.  

จากนี้คุณอาจสำรวจต่อ:

- ส่งข้อความธรรมดาไปยัง **search index** (เช่น Elasticsearch) เพื่อทำให้ใบแจ้งหนี้สามารถค้นหาได้.  
- แปลงผลลัพธ์เป็น **JSON** แล้วส่งให้โมเดล machine‑learning ที่สกัดรายการสินค้า.  
- เพิ่ม **error handling** สำหรับ TIFF ที่เสียหายหรือปัญหาการอนุญาต.  

ลองใช้งานดู,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}