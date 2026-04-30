---
category: general
date: 2026-04-29
description: ทำการ OCR รูปภาพเป็นชุดอย่างรวดเร็วด้วย Aspose OCR ใน C# เรียนรู้วิธีดึงข้อความจากไฟล์
  JPG, อ่านข้อความจากการสแกน, และประมวลผลรายการรูปภาพแบบขนาน.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: th
og_description: ทำการ OCR รูปภาพเป็นชุดอย่างรวดเร็วด้วย Aspose OCR คู่มือนี้แสดงวิธีดึงข้อความจากไฟล์
  JPG, อ่านข้อความจากการสแกน, และประมวลผลรายการรูปภาพพร้อมกันแบบขนาน.
og_title: OCR รูปภาพเป็นชุดใน C# – OCR ขนานของสแกน JPG
tags:
- C#
- OCR
- Aspose
- Image Processing
title: การทำ OCR รูปภาพเป็นชุดใน C# – OCR ขนานของสแกน JPG
url: /th/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การทำ OCR รูปภาพเป็นชุดใน C# – OCR ขนานของสแกน JPG

เคยต้องการ **batch OCR images** แต่ไม่แน่ใจว่าจะขยายงานให้ครอบคลุมหลายไฟล์อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนามักเจออุปสรรคเมื่อพยายามอ่านข้อความจากสแกนหนึ่งต่อหนึ่ง ข่าวดีคือด้วย Aspose OCR คุณสามารถ **extract text from jpg** files, **read text from scans**, และ **process image list** รายการได้แบบขนานด้วยเพียงไม่กี่บรรทัดของ C#.

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบซึ่งแสดงให้เห็นอย่างชัดเจนว่าต้องทำอย่างไร. เมื่อเสร็จคุณจะมีแอปคอนโซลที่ทำงานอิสระซึ่งรับรู้โฟลเดอร์ของสแกน JPEG, พิมพ์ข้อความของแต่ละหน้า, และบอกระยะเวลาที่แต่ละการดำเนินการใช้ไป. ไม่มีเอกสารภายนอกให้ตามหา, ไม่มีโค้ดสแนปเพียงบางส่วน—เพียงโซลูชันเต็มที่คุณสามารถลากลง Visual Studio แล้วรันได้.

## สิ่งที่คุณต้องมี

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์บน .NET Framework 4.6+ ด้วย)
- **Aspose.OCR** NuGet package (`Install-Package Aspose.OCR`)
- ไฟล์ JPG หรือภาพสแกนจำนวนหนึ่งที่คุณต้องการประมวลผล
- IDE ใดก็ได้ที่คุณชอบ; ฉันใช้ Visual Studio 2022, แต่ VS Code ก็ทำงานได้ดีเช่นกัน

เท่านี้เอง. ถ้าคุณมี NuGet package อยู่แล้ว, ก็พร้อมเริ่มต้น.

## ขั้นตอนที่ 1 – เริ่มต้น OCR Engine (Batch OCR Images Setup)

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ `OcrEngine` และบอกให้มันรู้ว่าจะมองหาภาษาอะไร. ในกรณีส่วนใหญ่ภาษาอังกฤษก็เพียงพอ, แต่คุณสามารถสลับ `OcrLanguage.English` เป็นภาษาอื่นที่รองรับได้.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*ทำไมเรื่องนี้ถึงสำคัญ:* การเริ่มต้น engine ครั้งเดียวแล้วใช้ซ้ำกับทุกภาพนั้นมีประสิทธิภาพมากกว่าการสร้างอินสแตนซ์ใหม่สำหรับแต่ละไฟล์. มันยังทำให้ Aspose สามารถแชร์ทรัพยากรภายใน, ซึ่งจำเป็นสำหรับ **parallel OCR processing**.

## ขั้นตอนที่ 2 – สร้างรายการภาพ (Process Image List)

ต่อไปเรากำหนดคอลเลกชันของเส้นทางไฟล์ที่ต้องการส่งเข้า batch recogniser. คุณสามารถสร้างรายการนี้แบบไดนามิกด้วย `Directory.GetFiles`, แต่เพื่อความชัดเจนเราจะ hard‑code รายการไม่กี่รายการ.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*เคล็ดลับ:* หากคุณมีสแกนหลายพันไฟล์, พิจารณาใช้ `Directory.EnumerateFiles` พร้อมฟิลเตอร์เช่น `*.jpg` เพื่อหลีกเลี่ยงการโหลดรายการทั้งหมดเข้าสู่หน่วยความจำพร้อมกัน.

## ขั้นตอนที่ 3 – รัน Batch Recognition (Parallel OCR Processing)

ตอนนี้มาถึงหัวใจของเรื่อง: เรียก `BatchRecognize`. เมธอดนี้รับอาร์กิวเมนต์ `maxDegreeOfParallelism`, ซึ่งควบคุมจำนวนเธรดที่ Aspose จะสร้าง. โดยค่าเริ่มต้นมันใช้สี่เธรด, แต่คุณสามารถเพิ่มได้หาก CPU ของคุณมีคอร์มากกว่า.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*อะไรที่เกิดขึ้นเบื้องหลัง?* Aspose แบ่งคอลเลกชัน `imagePaths` เป็นชิ้นย่อย, ส่งแต่ละชิ้นให้กับเธรดแยกต่างหาก, แล้วรวมผลลัพธ์. นี่เป็นวิธีที่มีประสิทธิภาพที่สุดในการ **extract text from jpg** files เมื่อคุณมี **process image list** ที่สามารถทำงานพร้อมกันได้.

## ขั้นตอนที่ 4 – แสดงผลลัพธ์ (Read Text from Scans)

สุดท้ายเราวนลูปผ่านคอลเลกชัน `recognitionResults` และพิมพ์ข้อความของแต่ละไฟล์พร้อมเวลาการประมวลผล. อ็อบเจ็กต์ `OcrResult` ยังให้ชื่อไฟล์ต้นทาง, ซึ่งช่วยเมื่อคุณต้องบันทึกหรือเก็บผลลัพธ์.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

สังเกตว่าแต่ละบล็อกบอกชื่อไฟล์, ระยะเวลา OCR, และข้อความที่สกัดออกมา. นั่นคือข้อมูลที่คุณต้องการเมื่อ **reading text from scans** ในไพรไลน์การผลิต.

## การจัดการกับกรณีขอบทั่วไป

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` ถูกโยนภายใน `BatchRecognize` | ตรวจสอบเส้นทางด้วย `File.Exists` ก่อนเพิ่มลงใน `imagePaths`. |
| **Unsupported format** | Aspose รองรับเฉพาะภาพเรสเตอร์ (JPG, PNG, BMP, TIFF). | แปลง PDF เป็นภาพก่อน (ใช้ Aspose.PDF) หรือข้ามไฟล์เหล่านั้น. |
| **Memory pressure** | ภาพขนาดใหญ่มากอาจทำให้ RAM ระเบิดเมื่อหลายเธรดทำงานพร้อมกัน. | ลดค่า `maxDegreeOfParallelism` หรือปรับขนาดภาพก่อน OCR. |
| **Non‑English text** | ตั้งค่าภาษาเป็น English จะพลาดสคริปต์อื่น. | เปลี่ยน `Language = OcrLanguage.French` (หรือคอมโบหลายภาษา). |

เคล็ดลับเหล่านี้ช่วยให้งาน batch ของคุณแข็งแรง, โดยเฉพาะเมื่อคุณ **processing an image list** ที่มาจากการอัปโหลดของผู้ใช้หรือคลังสแกน.

## Pro Tip – ปรับแต่ง Parallelism

หากคุณรันบนเครื่อง 8‑core, เพิ่ม parallelism เป็น 6 หรือ 8 แล้วสังเกตความเร็วที่เพิ่มขึ้น. อย่างไรก็ตาม, จำไว้ว่าทุกเธรดก็ใช้หน่วยความจำสำหรับบิตแมปด้วย. กฎง่าย ๆ คือ:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

ใส่ค่า `maxThreads` ลงใน `BatchRecognize` เพื่อการกำหนดค่าที่ปรับตามเครื่องอัตโนมัติ.

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมคอมไพล์. เพียงแทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางที่เก็บสแกน JPG ของคุณ.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Note:** บรรทัด `using System.IO;` จำเป็นสำหรับตัวช่วย `Directory`. โค้ดจะพิมพ์ข้อความเป็นมิตรหากไม่พบ JPG ใด ๆ, ป้องกันการล้มเหลวแบบเงียบ.

## สรุป

เราได้สาธิต workflow **batch OCR images** ที่ **extracts text from jpg** files, **reads text from scans**, และประมวลผล **process image list** อย่างมีประสิทธิภาพด้วย **parallel OCR processing**. ตัวอย่างเต็มที่สามารถรันได้แสดงให้เห็นวิธีตั้งค่า engine, ป้อนคอลเลกชันไฟล์, และจัดการผลลัพธ์—ทั้งหมดนี้โดยควบคุมการใช้หน่วยความจำและจำนวนเธรด.

พร้อมก้าวต่อไปหรือยัง? ลองสลับภาษาเป็น French, เพิ่มการแปลง PDF‑to‑image, หรือเก็บข้อความ OCR ลงฐานข้อมูล. แพทเทิร์นยังคงเหมือนเดิม: เริ่มต้นครั้งเดียว, ป้อนรายการ, แล้วให้ Aspose ทำงานหนักแบบขนาน.

มีคำถามหรืออยากแชร์การปรับแต่งของคุณ? แสดงความคิดเห็นด้านล่าง, แล้วขอให้สนุกกับการเขียนโค้ด!

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}