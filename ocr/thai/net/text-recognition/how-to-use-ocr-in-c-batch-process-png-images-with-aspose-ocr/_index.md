---
category: general
date: 2026-02-14
description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากไฟล์ PNG อย่างรวดเร็ว เรียนรู้การทำ
  OCR แบบแบชของรูปภาพ, ประมวลผลหลายรูปภาพ, และใช้ Aspose OCR C# ในคู่มือเดียว
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: th
og_description: วิธีใช้ OCR ใน C# กับ Aspose OCR C# บทเรียนนี้แสดงวิธีดึงข้อความจากไฟล์
  PNG, ทำ OCR เป็นชุดบนรูปภาพหลายไฟล์, และประมวลผลหลายรูปภาพอย่างมีประสิทธิภาพ
og_title: วิธีใช้ OCR ใน C# – การดึงข้อความจาก PNG แบบเป็นชุด
tags:
- OCR
- C#
- Aspose
- Image Processing
title: วิธีใช้ OCR ใน C# – ประมวลผลภาพ PNG แบบชุดด้วย Aspose OCR
url: /th/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ประมวลผลภาพ PNG เป็นชุดด้วย Aspose OCR

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อความจากไฟล์ PNG จำนวนมากโดยไม่ต้องเขียนรหัสแยกสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อจำเป็นต้อง **extract text PNG** อย่างใหญ่โต โดยเฉพาะเมื่อภาพอยู่ในโฟลเดอร์และคุณต้องเรียกใช้เครื่องมือ OCR สำหรับแต่ละไฟล์  

ในคู่มือนี้เราจะพาคุณผ่านโซลูชันที่สมบูรณ์พร้อมใช้งานที่ **batch OCR images**, **process multiple images** พร้อมกัน และใช้ประโยชน์จากไลบรารี **Aspose OCR C#** ที่ทรงพลัง เมื่อเสร็จสิ้นคุณจะได้ไฟล์ executable เดียวที่อ่าน PNG ใด ๆ จำนวนเท่าใดก็ได้ ดึงข้อความออกมาและพิมพ์ผลลัพธ์ไปที่คอนโซล—ทั้งหมดด้วยเพียงไม่กี่บรรทัดของโค้ด

## สิ่งจำเป็น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานได้กับ .NET Core และ .NET Framework ด้วย)  
- ใบอนุญาต Aspose.OCR for .NET ที่ถูกต้อง (หรือเวอร์ชันทดลองฟรี) – คุณสามารถดาวน์โหลดได้จากเว็บไซต์ Aspose  
- โฟลเดอร์ที่บรรจุไฟล์ PNG ที่ต้องการอ่าน  
- Visual Studio 2022 (หรือ IDE ที่รองรับ C# ใดก็ได้)  

- ไม่ต้องการแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.OCR`

## ขั้นตอนที่ 1: วิธีใช้ OCR – เริ่มต้น Aspose OCR Engine

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของคลาส `Engine` วัตถุนี้ทำหน้าที่เป็นตัวกลางของเทคโนโลยี OCR พื้นฐานและสามารถทำงานบน CPU หรือ GPU ขึ้นอยู่กับฮาร์ดแวร์และใบอนุญาตของคุณ

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*ทำไมเรื่องนี้ถึงสำคัญ:* การเริ่มต้น engine เพียงครั้งเดียวแล้วนำไปใช้ซ้ำในหลายเธรดจะช่วยประหยัดหน่วยความจำและหลีกเลี่ยงค่าใช้จ่ายจากการโหลดโมเดล OCR ซ้ำหลายครั้ง อีกทั้งยังทำให้การตั้งค่าคงที่สำหรับภาพทั้งหมด

## ขั้นตอนที่ 2: Extract Text PNG – รวบรวมเส้นทางไฟล์ภาพ

ต่อไปเราต้องการคอลเลกชันของเส้นทางไฟล์ ในโครงการจริงคุณอาจอ่านโฟลเดอร์แบบไดนามิก แต่เพื่อความชัดเจนเราจะระบุไฟล์ตัวอย่างไม่กี่ไฟล์

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*เคล็ดลับ:* แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางแบบ absolute หรือ relative ไปยังโฟลเดอร์ภาพของคุณ หากมีไฟล์หลายสิบไฟล์ คุณสามารถแทนที่รายการแบบแมนนวลด้วย `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`

## ขั้นตอนที่ 3: Batch OCR Images – รันการจดจำแบบขนาน

การประมวลผลภาพทีละภาพเป็นวิธีง่ายแต่ช้า โดยใช้ `Parallel.ForEach` เราสามารถ **process multiple images** พร้อมกันได้ โดยใช้ประโยชน์จาก CPU แบบหลายคอร์

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*ทำไมต้องขนาน?* การเรียก OCR แต่ละครั้งใช้ CPU มากแต่ทำงานอิสระกัน การรันพร้อมกันจึงสามารถลดเวลาการทำงานโดยรวมได้อย่างมาก โดยเฉพาะบนเครื่องที่มี 4‑core หรือมากกว่า

## ขั้นตอนที่ 4: Process Multiple Images – แสดงข้อความที่ดึงออกมา

ตอนนี้เรามีคอลเลกชันของอ็อบเจ็กต์ `OcrResult` แล้ว เราสามารถวนลูปผ่านและพิมพ์ข้อความที่จดจำได้ นี่คือจุดที่คุณอาจเก็บผลลัพธ์ลงฐานข้อมูลหรือเขียนไฟล์ แต่การแสดงผลบนคอนโซลทำให้ตัวอย่างสั้นและกระชับ

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**ผลลัพธ์คอนโซลที่คาดหวัง (ตัวอย่าง):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

หากภาพใดโหลดไม่สำเร็จ Aspose จะโยน exception; คุณสามารถห่อการเรียก `engine.Recognize` ด้วยบล็อก try/catch เพื่อบันทึกข้อผิดพลาดโดยไม่ทำให้แบตช์ทั้งหมดหยุดทำงาน

## ขั้นตอนที่ 5: Full Working Example – รวมทุกส่วนไว้ด้วยกัน

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซล C# ใหม่ได้ รวมทุกอย่างตั้งแต่คำสั่ง `using` จนถึงลูปแสดงผลสุดท้าย

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### การรันตัวอย่าง

1. สร้างโปรเจกต์ **Console App** ใหม่ใน Visual Studio  
2. เพิ่มแพ็กเกจ **Aspose.OCR** ผ่าน NuGet (`Install-Package Aspose.OCR`)  
3. แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางที่เก็บไฟล์ PNG ของคุณ  
4. คอมไพล์และรัน – คุณควรเห็นข้อความที่ดึงออกมาปรากฏบนคอนโซล

## เคล็ดลับระดับมืออาชีพ & กรณีขอบ

- **GPU acceleration:** หากคุณมี GPU ที่รองรับและมีใบอนุญาต Aspose OCR ให้เปิดใช้งานผ่าน `EngineSettings` ก่อนสร้าง engine ซึ่งจะช่วยลดเวลาประมวลผลต่อภาพได้หลายวินาที  
- **Large files:** สำหรับภาพที่ใหญ่กว่า 10 MB ควรทำการลดขนาดลงก่อนเพื่อบรรเทาแรงกดดันของหน่วยความจำ  
- **Language support:** โดยค่าเริ่มต้น engine จะถือว่าเป็นภาษาอังกฤษ ตั้งค่า `engine.Language = Language.French;` (หรือภาษาอื่นที่รองรับ) เพื่อเพิ่มความแม่นยำกับข้อความที่ไม่ใช่ภาษาอังกฤษ  
- **Error handling:** `try/catch` ภายในลูปขนานทำให้ไฟล์เสียหายไม่ทำให้แบตช์ทั้งหมดหยุดทำงาน คุณยังสามารถบันทึกข้อผิดพลาดลงไฟล์เพื่อการตรวจสอบภายหลังได้  
- **Result storage:** แทนการพิมพ์ คุณอาจเขียน `result.Text` ลงไฟล์ `.txt` ด้วย `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีใช้ OCR** ใน C# เพื่อ **extract text PNG** ไฟล์, **batch OCR images**, และ **process multiple images** อย่างมีประสิทธิภาพด้วย Aspose OCR C# โซลูชันนี้เป็นอิสระเต็มรูปแบบ ทำงานแบบขนาน และสามารถขยายเพื่อจัดการกับไฟล์หลายร้อยหรือหลายพันไฟล์ได้ด้วยการเปลี่ยนแปลงเล็กน้อย  

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเปลี่ยนการแสดงผลบนคอนโซลเป็นรายงาน CSV, ทดลองใช้ GPU acceleration, หรือป้อนข้อความ OCR ไปยังดัชนีการค้นหา ความเป็นไปได้ไม่มีที่สิ้นสุด และรูปแบบหลัก—เริ่มต้นครั้งเดียว, รันแบบขนาน, จัดการข้อผิดพลาดอย่างสุภาพ—จะช่วยคุณในทุก ๆ pipeline การประมวลผลภาพ  

ขอให้เขียนโค้ดสนุกและ OCR ของคุณทำงานเร็วและปราศจากข้อผิดพลาด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}